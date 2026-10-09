# Launch-argument test hooks

> Lets Claude open any screen, seed data, replay a demo, take on a test identity or dump internal state by setting environment variables at launch, so it can reach and check states that no tap, gesture or simulator feature can reach.

**Applies to:** iOS, iPadOS, watchOS, visionOS and Designed-for-iPad-on-Mac apps whose source you control · **Needs:** the app's source, a DEBUG build configuration, a launcher that passes environment variables (`xcrun simctl launch`, `open --env`, `xcrun devicectl`, an Xcode scheme)

## Why it exists

Without hooks, Claude tries to reach a screen by tapping at guessed coordinates. When that fails it asks
the human to go there and look. Each app had a screen that couldn't be reached that way:

- A game's menus are drawn by the engine and have no accessibility tree. Coordinate taps against them were
  "unreliable enough that it has blocked most verification runs" (source comment). One env var that opens
  Settings at launch removed the biggest time sink in that project.
- In a fitness app, the simulator's injected taps never reached the bottom fifth of the screen. The demo-ride
  button sat there, so the one screen that can only be checked indoors couldn't be opened indoors.
- The simulator has no workouts, no Bluetooth, no Memoji, and it can't type an emoji into a name field.
  A biometric lock stops every unattended launch.
- Checking a two-person feature needs a second identity (see `two-simulator-peer-test.md`).

Built for Throwdown, Frictionless Coffee, a Quake 3 port (about 150 `Q3_*` hooks) and Claude
Watch. The pattern is the same in each.

## What it does

1. The app reads a named env var (or a `-flag` launch argument) once, early, inside `#if DEBUG`.
2. The hook does one thing: opens a screen, seeds a store, starts a replay, sets an identity, or writes a dump.
3. It logs one line when it fires, so the harness can wait on that line instead of sleeping.
4. Claude launches with the variable set, waits for the line, then screenshots, reads the log, or pulls the dump file.
5. Pass/fail comes from the screenshot, the log or the file. The next launch without the variable is a normal launch.

Hook kinds that earned their place:

| Kind | Examples (names as used) | What it replaces |
|---|---|---|
| Open a screen | `RACEME_SHOW=races\|rivals\|history\|trends\|settings`, `Q3_OPEN_SETTINGS=1`, `Q3_OPEN_RTR=1`, `STARTORDERS=1`, `<APP>_OPEN=<screen>` | Tapping through menus, or screens taps can't reach |
| Seed data | `SEEDTEST=1` (two people, several drinks), `SEEDQUEUE=1` (a 5-order queue), `<APP>_SEED=1` (one sample record), `CIRCUIT_SEED=<mode>`, a debug health-data seeder | An empty simulator |
| Replay / demo | `RACEME_DEMO=<n>`, `RACEME_DEMO_RATE=2`, `RACEME_DEMO_END=back\|detour`, `WATCH_DEMO=choose\|ready\|count\|done\|song\|rest`, `DEMOMODE=1` + `DEMOSTEP=<s>` (simulated machine), `Q3_AUTOCMD="<cmds>"` | Riding, exercising or brewing for real |
| Identity | `RACEME_RIDER=<alias>`, `THROWDOWN_TEST_RIDER="Name\|IN\|🦊"`, `-resetIdentityVault` | A second person, typing an emoji |
| Round trip | `SHARETEST=1` (export → parse → stage a shared profile), `QRTEST=1` | A second device |
| Dump state | `DUMPI18N=1` (English base strings to a file), `DUMPVOICES=1`, `Q3_DUMPENG=1`, `Q3_TEXDUMP` | Reading internals by guesswork |
| Extra logging | `Q3_FOCUSLOG`, `Q3_KEYLOG`, `Q3_PADLOG`, `TRACESCAN=1` | Attaching a debugger |
| Test fixture | `Q3_STEREOTEST=<ipd>`, `Q3_JUMPTEST=1`, `APPROVAL_PREVIEW=1\|ql`, `PAGER_PREVIEW=1` | Hardware or live data the sim lacks |
| Skip a gate | `CW_SIM_UNLOCK=1` (biometric lock, simulator builds only) | A face or finger |

## Recipe

**1. Read hooks in one place, compiled out of release.** Keep them in a file or block the release build never sees:

```swift
#if DEBUG
enum TestHooks {
    static let env = ProcessInfo.processInfo.environment
    static var openScreen: String? { env["<APP>_SHOW"] }          // <APP>_SHOW=settings
    static var seed: Bool { env["<APP>_SEED"] == "1" }
    static var resetIdentity: Bool { ProcessInfo.processInfo.arguments.contains("-reset<Thing>") }
}
#endif
```

Use one prefix per app (`<APP>_`), so a grep finds every hook and a leaked variable is easy to trace.
Anything that skips authentication goes under `#if targetEnvironment(simulator)` as well, so a device
debug build can't skip it either.

**2. Make each hook one-shot and ready-aware.** Fire once per launch (a static flag), and only once the UI
can take it (a window exists, nothing else is presented). Log a line:

```swift
if !Self.didOpen, TestHooks.openScreen == "settings", view.window != nil, presentedViewController == nil {
    Self.didOpen = true
    NSLog("<APP>: <APP>_SHOW=settings → presenting Settings")
    present(SettingsViewController(), animated: false)
}
```

**3. Launch with the hook.**

```bash
# Simulator: only SIMCTL_CHILD_-prefixed variables reach the app; pass them on launch, never on boot
SIMCTL_CHILD_<APP>_SHOW=settings xcrun simctl launch --terminate-running-process "$UDID" <bundle-id>

# Launch arguments go after the bundle id; -key value pairs also override UserDefaults for this launch only
xcrun simctl launch "$UDID" <bundle-id> -reset<Thing> -<defaultsKey> <value>

# Mac (Designed for iPad / native): scope to one launch
open -g "<path to .app>" --env "<APP>_SHOW=settings"

# Physical device from the Mac (flag checked in devicectl's help; not run with hooks here)
xcrun devicectl device process launch --device <device-id> \
  -e '{"<APP>_SHOW":"settings"}' <bundle-id>
```

For a phone launched from its home screen, where nothing can pass an env var, read the same hook from a
local `UserDefaults` key as a fallback (the identity alias did this). The full launch, wait and capture
loop is in `headless-ios.md`; the Mac launch is in `designed-for-ipad-on-mac.md`; engine commands through a
hook are in `game-console-driving.md`.

**4. Wait on the hook's log line, then capture.**

```bash
for i in $(seq 1 60); do grep -q "<APP>_SHOW=settings" "$OUT/app.log" && break; sleep 1; done
xcrun simctl io "$UDID" screenshot "$OUT/settings.png"
```

**5. Pull dumps from the container.** Dump hooks write to the app's Documents folder:

```bash
DATA=$(xcrun simctl get_app_container "$UDID" <bundle-id> data)
cat "$DATA/Documents/<dump>.json"
```

**6. Check nothing leaks into release.** Add a source check to the build script that fails on any hook read
outside a DEBUG block. A simple version walks `#if`/`#endif` and flags `environment["<APP>_` outside one.
`strings` on the release binary can miss names: Swift keeps short string literals (15 bytes or fewer) inline
in the code, so they never show up as strings.

## Traps

- **`KEY=VAL` after the bundle id is an argument, not an env var.** The app sees `nil`. Use `SIMCTL_CHILD_KEY=VAL` in simctl's own environment. This cost an hour on one hook.
- **`SIMCTL_CHILD_*` set during `simctl boot` sticks to every later launch.** One hook kept opening Settings for a day. See `headless-ios.md`.
- **Hooks that fire every time a view appears overwrite the tester's changes.** The seed and builder hooks re-ran each time the home list reappeared, and the seed was written back over edits. Fire once per launch.
- **Seeded data becomes real data.** A health seeder's synthetic rides were ordinary workouts once saved. They showed up as a route in the picker, added to the training load, were pushed to a server as history, and Claude spent rounds treating its own test loop as the user's route. Fix: filter out records the app wrote, and purge them on launch on devices. The platform only lets an app delete what it saved, so the purge can't reach real data. A demo replay also saved a ride that never happened. Seed into a namespaced store, or inject the store and assert on what would have been written.
- **Hooks gated on a second variable silently do nothing.** The engine's command hook ran only when its delay variable was also set (see `game-console-driving.md`). Document each hook's partner next to it.
- **A written rule doesn't keep hooks out of release.** Hook reads drift outside `#if DEBUG` as code moves, and nobody notices because debug runs still work. What fixed it for good was moving every read onto one helper that returns nothing outside DEBUG (a Swift `TestHooks` type, or a single C function for an engine), plus a source check in the build that fails on any read outside that helper. Wrapping each read in `#if DEBUG` where it's used also works, but only a build check keeps it that way.
- **A Release build that needs hooks is its own build, not a leak.** Performance scripts that drive a Release copy through a hook should turn the gate on with an explicit compiler flag in that one script, so the shipped Release build still compiles every hook out. Confirm by disassembling the shipped build's gate: it should be a plain "return nothing".
- **Scheme environment variables persist for human runs.** Leave scheme entries with `isEnabled = "NO"` and remove them after use. Xcode keeps the scheme in memory, so after editing an `.xcscheme` on disk, quit and reopen Xcode.
- **An identity alias must never sync and must namespace local stores**, or test data lands in the person's real records. See `two-simulator-peer-test.md`.
- **Remove a hook when its reason is gone.** A hook that auto-started recording was deleted once the race it chased was fixed. Left in, it would have kept a capture path alive that normal use never takes.
- **Test switches the app saves come back next launch** and look like bugs. Reset them at launch from one list; see `build-check-all-targets.md`.

## What it does not cover

A hook only proves the screen or state it opens. How someone gets there (navigation, reach, gestures, Siri,
the home screen) needs UI automation or a person. Sensors, Bluetooth, real health data, biometric prompts,
push and anything on a headset stay on the device list (`human-verify-queue.md`).

## Loading this into Claude

> Reach screens and states through the app's DEBUG launch hooks, not by tapping at coordinates or asking me.
> Hooks are env vars with the `<APP>_` prefix, read once per launch inside `#if DEBUG`, each logging a line
> when it fires. On the simulator pass them as `SIMCTL_CHILD_<APP>_<HOOK>=…` on the `launch` line only, never
> on `boot` and never after the bundle id. When a screen can't be reached, add a hook in the same commit:
> one-shot, ready-aware, logged, and added to the hook list in `<hook file>`. Seed only into namespaced or
> purgeable stores. The build check fails on any hook read outside DEBUG.
