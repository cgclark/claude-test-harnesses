# Unit test suites (XCTest, Swift Testing, node:test)

> Lets Claude check an app's domain logic (route matching, scoring, identity rules, relay rules, queues, phrase matching) on every change, headlessly, in seconds to minutes, without a device or a person.

**Applies to:** Swift apps and packages, Node services · **Needs:** Xcode command-line tools and the project's own simulator for app-hosted tests; `swift test` for packages; Node 18+ for `node --test`

## Why it exists

This is standard practice, and Claude recommended it. Our sizes: about 990 XCTest cases in a fitness app,
about 50 in a coffee-machine app, 77 Swift Testing tests in a voice-routing package, and 35 `node:test`
cases for a relay server. Built for Throwdown, Frictionless Coffee and Big Top. The useful part is where
they fell short, below.

## What it does

1. Pure logic is pulled out of views and hardware code so a test can call it (a recipe's step segmentation, queue reordering, wake-phrase matching, standings after an exchange).
2. Claude runs the suite after each edit batch, from the shell.
3. Pass = exit code 0 and the summary line. A failure names the test and the assertion.

## Recipe

```bash
# App-hosted XCTest / Swift Testing, on the project's own simulator (resolve it by name: headless-ios.md)
xcodebuild test -project <App>.xcodeproj -scheme <scheme> \
  -destination "platform=iOS Simulator,id=$UDID" -derivedDataPath build 2>&1 | tail -30
#   one class while iterating:  -only-testing:<TestTarget>/<TestClass>

# Swift package
swift test                   # or: swift test --filter <Suite>

# Node service
node --test <dir>/           # picks up *.test.js
```

For a server, have the test start it in-process on a free port with its data in a temp directory, and turn
off every outbound call with env vars, so the suite can't reach a real service:

```js
process.env.<APP>_DATA = fs.mkdtempSync(path.join(os.tmpdir(), '<app>-'));
process.env.PORT = '0';
process.env.<APP>_PUSH = '0';          // no real push, no store lookups
const { start } = require('./server.js');
```

## Traps

- **Testing with yourself as the other person hides identity bugs.** "The host travels as me" passed every test and every human check for three weeks, because both ends had the same id. Give each side its own key and store. See `two-simulator-peer-test.md`.
- **Synthetic fixtures pass where real data fails.** Generated loops kept passing while the same real loop, ridden four times, came out as four routes. The fixtures are now real tracks. See `real-data-fixtures.md`.
- **The test host is the app, with the simulator's saved data.** App-hosted tests loaded the simulator's saved people list and in-app language, so results depended on what the simulator held. Reset that state in `setUp`, or inject stores.
- **Tests must not write to real stores.** A test wrote two invented workouts into the system health store on every run. Inject the store or recorder and assert on what would have been written.
- **Don't share a simulator between a unit run and a UI-test run.** One kills the other's test host. Two Claude sessions on one simulator hang each other too; give each its own named device.
- **`swift test` prints "Executed 0 tests" for XCTest even when Swift Testing ran everything.** Read the `Test run with N tests … passed` line.
- **Unit tests stop at the framework edge.** Siri voice routing can't be invoked from a test, and the simulator has no Bluetooth. An App Intents test framework announced for Xcode 27 wasn't in the shipping Xcode when we checked; verify before planning around a new test API.
- **Incremental builds can skip files edited outside Xcode**, so a green run may be the old code. See `build-check-all-targets.md`.

## What it does not cover

What the user sees (`headless-ios.md`, `localized-screens-contact-sheets.md`), two people at once
(`two-simulator-peer-test.md`), hardware, voice, real accounts and push. A green suite is "the logic agrees
with itself", not "it works".

## Loading this into Claude

> After every edit batch, run the unit suites before reporting: `xcodebuild test -scheme <scheme>
> -destination "platform=iOS Simulator,id=$UDID"` on `<App> <device>` (never a simulator a UI test is
> using), `swift test` in `<package>`, `node --test <dir>/`. New logic goes in a pure function with a test.
> Peer logic is tested with two distinct identities, routes with the real fixtures, and stores are injected,
> never real. Report the summary line, and say what the suites can't cover.
