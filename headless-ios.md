# Headless iOS Simulator

> Lets Claude build, install, launch, drive and screenshot an iOS app in the Simulator from the shell, so it can see the running app itself instead of asking a human to press Run and look.

**Applies to:** iOS / iPadOS / watchOS apps built with Xcode · **Needs:** macOS with Xcode command-line tools (`xcrun simctl`, `xcodebuild`), an existing simulator device for the project

## Why it exists

Without a harness Claude stops at "BUILD SUCCEEDED" and asks the human to check the screen. A green
build is not what is on the simulator: the user kept reporting strings "still not localized" that were
fixed in source, because the sim held a build that was compiled but never reinstalled. Other failures
that shaped this recipe: picking a stock device type created a new multi-GB simulator and a new
permission prompt each time; a test run left a debug state on screen and the human reported it as a
regression; and fixed `sleep`s before screenshots caught the boot screen again and again.

Built for Quake3-iOS, AutoBarista and Throwdown; nothing below is specific to them.

## What it does

1. Resolve the project's own simulator **by name** and boot it with no viewer window.
2. Build the simulator slice, terminate the old process, `simctl install` the fresh `.app` (always overwrites).
3. Launch with test hooks passed as `SIMCTL_CHILD_*` environment variables.
4. Wait on evidence (a log line, a file) rather than a fixed sleep, then `simctl io screenshot` and read the PNG and the log.
5. Pass/fail from the log line or screenshot; then terminate the app, undo any test-only state, and shut the sim down.

## Recipe

**1. Pick the device the project already uses.** Never create one, and never borrow a stock device
because it exists. UDIDs change when Xcode or macOS is upgraded, so resolve by name in a sourced
helper instead of pasting a UDID:

```bash
# sim-ids.sh — source it: . tools/sim-ids.sh
sim_udid() {   # $1 = regex on the device name; prefers a booted match
  xcrun simctl list devices available -j | python3 -c "
import json,re,sys
want=re.compile(sys.argv[1])
devs=[d for ds in json.load(sys.stdin)['devices'].values() for d in ds if want.search(d['name'])]
devs.sort(key=lambda d: d['state']!='Booted')
print(devs[0]['udid'] if devs else '')" "$1"
}
UDID=${UDID:-$(sim_udid '^<App> <device>$')}
[ -n "$UDID" ] || { echo "no '<App> <device>' simulator — recreate it by that name" >&2; exit 1; }
```

Giving the project dedicated, named devices (`<App> A`, `<App> B`) keeps tests off the human's own sim
and means any viewer-panel permission is granted once per device, not once per run.

**2. Boot headless.** `simctl boot` starts the device with no window. Do not open the Simulator /
Device Hub app for an unattended run. Strip `SIMCTL_CHILD_*` from the boot's environment (see Traps).

```bash
# bash (compgen is not in zsh)
( for v in $(compgen -e | grep '^SIMCTL_CHILD_'); do unset "$v"; done
  xcrun simctl boot "$UDID" 2>/dev/null ) || true
xcrun simctl bootstatus "$UDID" -b >/dev/null
```

**3. Build, then install over the old copy.**

```bash
xcodebuild -project <App>.xcodeproj -scheme <scheme> -sdk iphonesimulator \
  -configuration Debug -destination "platform=iOS Simulator,id=$UDID" \
  -derivedDataPath build/sim build 2>&1 | grep -E "error:|BUILD (SUCCEEDED|FAILED)"
APP=build/sim/Build/Products/Debug-iphonesimulator/<App>.app
xcrun simctl terminate "$UDID" <bundle-id> 2>/dev/null || true
xcrun simctl install "$UDID" "$APP"
```

**4. Launch with test hooks.** Arguments are often eaten by the app's UI layer; environment survives.
Add DEBUG-only, env-gated hooks to the app (`AUTOSTART=1`, `OPEN_SCREEN=settings`, a command script)
so a launch can reach any screen without taps.

```bash
SIMCTL_CHILD_<HOOK>=1 xcrun simctl launch --terminate-running-process \
  --stdout="$OUT/stdout.log" --stderr="$OUT/stderr.log" "$UDID" <bundle-id>
```

To read `NSLog`/`os_log` from an app that is already running, without relaunching or bringing a window
forward:

```bash
xcrun simctl spawn "$UDID" log stream --level debug --style compact \
  --predicate 'eventMessage CONTAINS "<log tag>"' > "$OUT/app.log" 2>&1 &
```

**5. Wait on evidence, then capture.**

```bash
for i in $(seq 1 60); do grep -q "<ready line>" "$OUT/app.log" && break; sleep 1; done
xcrun simctl io "$UDID" screenshot "$OUT/shot.png"      # needs no window, never takes focus
```

Batch several checks per launch (drive to screen A, shoot, screen B, shoot); the launch-and-settle cycle
is the expensive part, not the build.

**6. Files and preferences.** Resolve the container each time; its UUID rotates on every install.
Write preferences through the daemon, never by editing the plist.

```bash
DATA=$(xcrun simctl get_app_container "$UDID" <bundle-id> data)
xcrun simctl spawn "$UDID" defaults write <bundle-id> <key> <value>
```

**7. End clean.** Every run ends here, pass or fail:

```bash
xcrun simctl terminate "$UDID" <bundle-id> 2>/dev/null || true
# reset anything the run changed that persists (archived settings, debug prefs) before quitting
xcrun simctl shutdown "$UDID"      # unless the human is watching it
```

## Traps

- **Built but not installed.** `xcodebuild` never touches the sim. End every edit batch with build → `simctl install` → launch.
- **Xcode's incremental build can skip files edited outside Xcode** and still print BUILD SUCCEEDED. `touch` the edited sources before building, or log a compile stamp (`__DATE__ " " __TIME__`) at startup and check it.
- **`SIMCTL_CHILD_*` set during `boot` leak.** The boot hands them to the sim's launchd and every later launch inherits them; one test variable kept opening Settings on every launch for a day. Pass them only on the `launch` line.
- **`--console-pty` holds the caller until the app exits**, and brings the viewer window forward if one is open. If you need it, detach fully: `nohup xcrun simctl launch --console-pty ... > log 2>&1 < /dev/null &`. Prefer `--stdout=/--stderr=` or `simctl spawn ... log stream`.
- **An orphaned `--console-pty` launch wedges CoreSimulator**: every later `simctl` call hangs with no output. Before a run, `pkill -f "simctl launch --console-pty $UDID"`, and wrap calls in `timeout`.
- **Several booted sims can degrade the service**: `simctl list` says Booted while `shutdown` says "already Shutdown", and launches hang. Shut down every device, quit the viewer app, boot only the one you need. Rebooting one device does not fix it.
- **Two Claude sessions on one sim hang each other** (1–3 min timeouts on boot/install/launch). Give each session its own named device.
- **Do not edit the sim's preferences plist with `plutil`.** It fights `cfprefsd`'s cache and silently wipes user settings. Use `simctl spawn defaults write` or launch env.
- **Do not edit an on-disk config the app rewrites on exit.** A `terminate` after your edit restores the old value. Set the value through the app (hook or command) and read it back from the app's log.
- **Log lines may carry colour or prefix codes**; anchor a grep on the message, not `^`.
- **Clicking a rotated or game view from outside is skewed.** Add env-gated test hooks instead of synthesising taps.
- **Simulator.app is gone in the Xcode 27 era**, replaced by **Device Hub** (`open -a "Device Hub"`). `simctl` is unchanged.
- **watchOS:** install the watch app only after the paired watch sim has fully booted, or the install is silently lost. Queued WatchConnectivity transfers (`transferUserInfo`, files) never deliver between sims; direct messages do.
- **Leftover test state reads as a regression.** A run that ended without quitting left a debug render mode on screen and the human reported a bug. Check the sim is back to normal (or the app closed) before reporting.

## What it does not cover

- Real-device behaviour: the device main-thread stack is smaller, so some launch crashes never reproduce on the sim (see `device-crashlog-pull.md`). Anything touching the launch path needs a device run.
- Hardware the sim lacks: Bluetooth LE, hardware ray tracing, some Metal features, real sensors, cameras, HealthKit data.
- Sign-in, payments, push, TestFlight distribution, and how it feels in the hand. Those stay with the human.

## Loading this into Claude

> Test iOS changes in the Simulator headlessly, never by asking me to press Run. Resolve the device by
> name from `tools/sim-ids.sh` (only `<App> <device>`; never create or borrow another device). After
> every edit batch: build the simulator slice, `simctl terminate`, `simctl install`, launch with
> `SIMCTL_CHILD_*` test hooks, wait on a log line rather than a sleep, `simctl io screenshot`, and read
> the PNG and log before saying it works. Boot with `simctl`, not the viewer app. End every run with
> `simctl terminate`, test-only state undone, and `simctl shutdown` unless I am watching.
