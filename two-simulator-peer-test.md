# Two-simulator peer test

> Lets Claude test a peer-to-peer feature (invitations, shared challenges, sync between two people) end to end on one Mac: two named simulators act as two different people, and Claude drives both and reads each side's screen and log.

**Applies to:** iOS apps where one user sends something to another (invites, shared documents, multiplayer state)
through a relay, a link or a file · **Needs:** Xcode with an iOS runtime, two simulators reserved for the project,
a DEBUG-only way to give a device a different identity, the relay reachable from the Mac (local or staging)

## Why it exists

By default Claude unit-tests the encoder and decoder of an invitation and then asks the user to try it between two
phones. The user's two phones are usually on one account, and in an app where identity syncs across a person's
devices that makes them **one person**. So the human test is inviting yourself, and it looks right.

Built for a fitness-challenge app. Inviting yourself hid a "the host travels as *me*" bug for three weeks: same id
on both ends, so every screen read correctly. Running two simulators as two different riders also found a sync bug
no single device shows. A challenge arriving from the inbox changed the list under a pull-to-refresh, which
cancelled the rest of the sync. The cancelled requests were then read as "can't reach the server" and the red
outage banner came up.

## What it does

1. Two simulators with fixed names (here "Ari" and "Beth") are the project's only test devices. Scripts resolve them
   by name.
2. Each launches as a different person. One uses a DEBUG identity alias passed by env var, the other runs the real
   identity path, so both code paths stay exercised.
3. Claude drives the flow across both: A creates and sends, B receives (link, file or relay) and answers, A syncs.
   Each step ends in a screenshot and a log grep on the side that should have changed.
4. Pass = both sides show the same state (who's in, standings, results) and neither log has an error.
5. A pure-logic twin of the same flow runs in the unit suite: two stores, copies swapped as the relay would, with
   both asserted to agree after every exchange.

## Recipe

**1. Reserve two simulators, by name:**

```bash
xcrun simctl create "<App> A" "<iPhone model>" <iOS runtime id>
xcrun simctl create "<App> B" "<iPhone model>" <iOS runtime id>
udid() { xcrun simctl list devices available -j | python3 -c "
import json,sys; n=sys.argv[1]
print(next(d['udid'] for ds in json.load(sys.stdin)['devices'].values() for d in ds if d['name']==n))" "$1"; }
A=$(udid "<App> A"); B=$(udid "<App> B")
```

**2. Add a DEBUG identity alias** to the app: an env var for a simulator launched from the command line, or a local
default for a physical phone (which can't be handed an env var). The alias must **never sync** (keep it out of
iCloud/the server's identity store), and it must **namespace local stores**, or test data lands in the real
person's records. Optionally take a display name and face too (`<APP>_TEST_RIDER="Beth|BE|🦊"`), since the
simulator can't type an emoji.

**3. Build once, install on both, launch as two people.** Env vars reach a simulator app only through the
`SIMCTL_CHILD_` prefix:

```bash
xcodebuild -project <App>.xcodeproj -scheme <scheme> -sdk iphonesimulator \
  -destination "id=$A" -configuration Debug build
for d in $A $B; do xcrun simctl boot $d 2>/dev/null; xcrun simctl install $d <path to built .app>; done
SIMCTL_CHILD_<APP>_RIDER=ari-test xcrun simctl launch --console-pty $A <bundle id> > a.log 2>&1 &
SIMCTL_CHILD_<APP>_TEST_RIDER="Beth|BE|🦊" xcrun simctl launch --console-pty $B <bundle id> > b.log 2>&1 &
```

**4. Drive the exchange.** Send from A (UI automation, or a DEBUG launch hook that opens the sheet), then hand
the result to B:

```bash
xcrun simctl openurl $B "<invite link>"     # universal link: needs the associated domain to resolve, else Safari opens
xcrun simctl io $A screenshot a-1.png; xcrun simctl io $B screenshot b-1.png
grep -E "<sync done>|<error>" a.log b.log
```

For the receiving end on its own, generate a real invitation file **with the app's own encoder** in a test, not by
hand. A hand-rolled copy of the format tests the copy (here the payload was raw DEFLATE, the detail a copy gets
wrong silently).

**5. Test the relay on its own too**, with scripted peers that each hold their own signing key (`node --test
relay/`, or your server's equivalent). That covers the rules (who may write what, replayed signatures refused)
without simulators. Then one simulator plus one scripted peer is a quick end-to-end check.

**6. Keep the two-phone unit test** for the multi-day logic: each phone has its own store, copies swap every
"evening", and the test asserts both agree on the standings every day and on the final result.

## Traps

- **Same account = same person.** Two devices signed into one account share the synced identity, so an invite
  between them is an invite to yourself. Use the alias, and keep one simulator on the real path so it stays tested.
- **New simulators cost the user a permission grant.** Live simulator panels ask once per device. Reuse the two
  named ones. If one is missing, recreate it under the same name rather than borrowing a stock device.
- **UDIDs change on Xcode/OS upgrades.** An upgrade recreated every simulator. Resolve by name in every script;
  never paste a UDID.
- **An env var given to `xcodebuild` doesn't reach the app in the simulator.** Use `SIMCTL_CHILD_*` on launch.
  From tests, write output files to the simulator's own temporary directory, which is a real path on the Mac.
- **`simctl spawn <sim> defaults write <bundle id> ...` doesn't reach the app's preferences.** Write to the plist
  inside the container (`defaults write "<data container>/Library/Preferences/<bundle id>" ...`). Don't
  `defaults delete` a setting the app mirrors from iCloud: it gets refilled.
- **Queued WatchConnectivity transfers never deliver between simulators.** Direct messages do. Install a watch app
  only after the paired watch simulator has fully booted, or the install is silently lost.
- **Keep the simulators' data between builds.** A new non-optional field with a default value still made old saved
  data fail to decode. The list read as empty, and the next save overwrote the user's saved circuit. It surfaced
  only because one simulator had real saved data. Wiping simulators per run would have hidden it.
- **Tests and demos must not write real records.** A demo replay saved an 8 km ride that never happened, and a
  unit test wrote two invented workouts into the system health store on every run. Inject the recorder/store and
  assert on what would have been written.
- **A cancelled request is not an outage.** If refresh can be cancelled by a list change, two simulators exchanging
  will trigger it. Make the sync run to the end whoever asked, and never map cancellation to "server down".

## What it does not cover

Push notifications and their wording on a real lock screen, real accounts and the identity sync between a person's
own devices, universal links from Messages, GPS and sensors, and anything on a physical watch. Those go on the
human's device checklist.

## Loading this into Claude

> Peer features are tested between the two project simulators, "<App> A" and "<App> B" (resolve by name; never
> create or attach another). A launches with `SIMCTL_CHILD_<APP>_RIDER=<alias>`, B runs the real identity path.
> Drive send on A → receive on B → sync on A, screenshot and grep both logs at each step, and pass only when both
> sides agree. Run `node --test relay/` for relay rules and the two-phone unit test for multi-day logic. Never
> test an invitation between two devices on the same account.
