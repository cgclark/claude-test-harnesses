# Device crash-log pull

> Lets Claude install a build on a paired iPhone, launch it with the console attached, and pull and read the device's own crash report, so a device-only crash gets a named cause instead of "it crashes on open".

**Applies to:** iOS apps on a real, paired device · **Needs:** Xcode command-line tools (`xcrun devicectl`), a device paired with this Mac (USB or network) and unlocked, development signing; optionally `libimobiledevice` (`idevicecrashreport`) for USB

## Why it exists

The Simulator gives a larger main-thread stack and skips some framework paths, so an app can pass every
sim test and unit test and still crash the instant it opens on a phone. Without this, Claude reports
"tests green", ships a TestFlight build, and the human finds the crash. That happened three times on one
app (AutoBarista): a SwiftUI type nested too deeply, a Swift 6 actor-isolation trap in an audio
callback, and an uncatchable `AVAudioEngine` exception. Each was named only by reading the device's
`.ips`.

## What it does

1. Build for the connected device with automatic development signing.
2. Install with `devicectl` and launch **with `--console`**, holding it open long enough to crash.
3. Pull the device's crash reports to a local folder.
4. Parse the `.ips` (two JSON lines): exception, termination, and the triggered thread's frames.
5. Pass = the app idles in the console and no new `.ips` appears; fail = a backtrace and a report naming the frame.

## Recipe

**1. Find the device and build for it.**

```bash
xcrun devicectl list devices            # note the device identifier
xcodebuild build -project <App>.xcodeproj -scheme <scheme> -configuration Debug \
  -destination 'id=<device>' -derivedDataPath build-dev -allowProvisioningUpdates
```

Use `-configuration Release` when the crash only shows in a release build.

**2. Install and launch with the console attached.**

```bash
xcrun devicectl device install app --device <device> \
  build-dev/Build/Products/Debug-iphoneos/<App>.app
timeout 20 xcrun devicectl device process launch --console --terminate-existing \
  --environment-variables '{"<HOOK>":"1"}' --device <device> <bundle-id>
```

A surviving app prints its startup logs and idles at "Waiting for the application to terminate...". An
instant return with a backtrace is a crash. Use a DEBUG-only env hook to drive the suspect code path
(for example, start the audio listener) so no one has to tap through the UI.

**3. Pull crash reports.**

```bash
mkdir -p crashes
xcrun devicectl device copy from --device <device> --domain-type systemCrashLogs \
  --source . --destination crashes
ls -t crashes/<App>-*.ips | head      # older ones may be under crashes/Retired/
```

Over USB, `idevicecrashreport` also works: `idevicecrashreport -k -e -f <App> crashes` (`-k` keeps the
reports on the device; `-e` also writes a readable `.crash`).

**4. Read the report.** The `.ips` is a JSON header line followed by a JSON body:

```python
# ips.py — python3 ips.py <file.ips>
import json, sys
head, body = open(sys.argv[1]).read().split("\n", 1)
h, b = json.loads(head), json.loads(body)
print(h.get("app_name"), h.get("app_version"), h.get("build_version"), h.get("os_version"))
print("exception:", b.get("exception"))
print("termination:", b.get("termination"))
imgs = b.get("usedImages", [])
t = next((t for t in b.get("threads", []) if t.get("triggered")), None)
for f in (t or {}).get("frames", [])[:25]:
    img = imgs[f["imageIndex"]].get("name", "?") if "imageIndex" in f else "?"
    print(f"  {img:28} {f.get('symbol', hex(f.get('imageOffset', 0)))}")
```

The first frame in your own module usually names the closure or view at fault.

**Known signatures:**

| Report shows | Cause | Fix |
|---|---|---|
| `EXC_BAD_ACCESS`/SIGSEGV, "Could not determine thread index for stack guard region", frames repeating `TypeDecoder::decodeMangledType` ↔ `decodeGenericArgs` in `libswiftCore` | One SwiftUI `body` builds a generic type nested too deeply (many modified pages in a `TabView`, wrappers stacked at the root); the device stack overflows at launch | `AnyView`-box the heavy children and the root content, or split them into separate `View` structs. Re-check after adding any root-level modifier or `.environmentObject` |
| `EXC_BREAKPOINT`, `swift_task_isCurrentExecutor` → `dispatch_assert_queue_fail` | Swift 6: a `@MainActor` class's closure called off-main by a framework (permission reply, audio tap, speech result) | Don't make callback owners `@MainActor`; confine state to a private serial queue and hop only published state and user callbacks to main |
| SIGABRT in `AVAudioEngineImpl::InstallTapOnNode` | Uncatchable ObjC exception: tap reinstalled per cycle, or input format 0 Hz / 0 channels after a route change | Install the tap once per session; check `sampleRate > 0 && channelCount > 0` before installing, retry otherwise |

## Traps

- **A plain `process launch` returns immediately and hides the crash.** Always use `--console` and hold it open.
- **Read the signal correctly.** `signal 11` (SIGSEGV) is a crash. `signal 15` is your `timeout` killing the console, and `signal 5` on detach is the console going away, not the app crashing.
- **`idevicecrashreport` cannot see network-paired (CoreDevice) devices**; it says "No device found". Use `devicectl ... --domain-type systemCrashLogs`, or connect USB.
- **`idevicecrashreport` without `-k` deletes the reports from the device** after copying.
- **A green Simulator does not prove the app launches.** Any change to the launch path (root view wiring, new root `@StateObject`, `TabView` structure) needs a device launch before TestFlight.
- **Patching off-main closures one at a time is whack-a-mole**: the crash moves to the next callback. Fix the isolation of the owning class.
- **A dev install over the TestFlight build can muddy App Shortcut / Siri registration.** For those tests, delete and reinstall the TestFlight build.
- **Device locked or not trusted:** install and launch fail with pairing or "locked" errors. The human unlocks it.

## What it does not cover

- Crashes that need real-world conditions (Bluetooth peers, routes changing mid-ride, low memory over hours) unless a hook can reproduce them.
- TestFlight and App Store crash reports from other users' devices (use App Store Connect / Xcode Organizer).
- Pairing the device, trusting the Mac, unlocking, and granting permission prompts on the phone. The human does those.

## Loading this into Claude

> Never treat a green Simulator as proof the app launches. For any launch-path change, and for any
> "crashes on device" report: build for the paired device (`xcrun devicectl list devices`), install with
> `devicectl device install app`, launch with `devicectl device process launch --console
> --terminate-existing` under a `timeout`, then pull `--domain-type systemCrashLogs` and read the newest
> `<App>-*.ips` (exception, termination, triggered thread). Name the faulting frame before proposing a
> fix, and confirm afterwards that a fresh launch idles and writes no new report.
