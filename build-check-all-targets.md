# Build-check every target

> Lets Claude prove a change compiles on every platform that shares the code (iOS simulator, Mac and visionOS), that the product really was rebuilt, and that no test setting can outlive the run that set it, before it reports anything as done.

**Applies to:** apps with several targets or projects compiling shared sources (iOS + Designed for iPad / Catalyst + visionOS), engines with saved console settings · **Needs:** Xcode command-line tools, XcodeGen if a project is generated, Python 3, Bash

## Why it exists

By default Claude builds the target it's working on, sees `BUILD SUCCEEDED`, and reports done. Three ways
that turned out false in one Quake 3 port:

- **The third target.** The visionOS project compiled the same engine sources through a separate, generated
  project. During one feature it couldn't link at all, and nobody noticed until the human tried, because only
  the iOS and Mac targets were being built. This had been raised many times before.
- **Nothing compiled.** Xcode's incremental build skipped files edited outside Xcode and still printed
  `BUILD SUCCEEDED`. A stale binary reached the human twice in one session, even after a `touch`.
- **Test settings came back.** Debug switches saved to the player's config reappeared at every launch and
  were reported as bugs three times (a "broken" explosion, a stray crosshair, every frame drawn twice).
  Capture runs also left the player's MSAA at 4x, which caused a "frame rate is low" report. Writing the rule
  down didn't stop it.

## What it does

1. `build-check.sh` touches every shared source, then builds each target: simulator, Mac, visionOS.
2. For each target it compares the product's mtime with the newest source. A product that didn't move gets a
   clean of that destination only and one rebuild; still stale is a failure.
3. It regenerates the XcodeGen project before building it.
4. It runs source guards, any of which fails the build: test switches never saved and always reset at launch;
   two mirrored defaults tables agree; a generated file matches its source.
5. Around any harness run that launches the app, `config-guard.py` snapshots every saved setting first and
   restores it after the app quits.

## Recipe

**1. One script, every target, with no argument.**

```bash
./tools/build-check.sh            # all targets
./tools/build-check.sh sim|mac|vision
```

```bash
find <Shared> <Engine> -name '*.m' -o -name '*.c' -o -name '*.swift' -o -name '*.h' | xargs touch
run() {   # label, product binary, build command…
  local label=$1 product=$2; shift 2
  local before=$(stat -f %m "$product" 2>/dev/null || echo 0) src=$(newest_source_mtime)
  "$@" 2>&1 | grep -q "BUILD SUCCEEDED" || { echo "✗ $label"; rc=1; return; }
  if [ "$(stat -f %m "$product")" = "$before" ] && [ "$src" -gt "$before" ]; then
    "${@:1:$(($#-1))}" clean >/dev/null 2>&1          # same destination, action swapped to clean
    "$@" 2>&1 | grep -q "BUILD SUCCEEDED" && [ "$(stat -f %m "$product")" -ge "$src" ] \
      || { echo "✗ $label: still stale"; rc=1; return; }
  fi
  echo "✓ $label"
}
run "simulator" "<DerivedData>/Debug-iphonesimulator/<App>.app/<App>" \
  xcodebuild -project <App>.xcodeproj -scheme <scheme> -sdk iphonesimulator \
             -destination "platform=iOS Simulator,id=$UDID" build
run "mac" "<DerivedData>/Debug-iphoneos/<App>.app/<App>" \
  xcodebuild -project <App>.xcodeproj -scheme <scheme> \
             -destination 'platform=macOS,variant=Designed for iPad' build
(cd <Spatial> && xcodegen generate)
run "visionOS" "<DerivedData>/Debug-xrsimulator/<Spatial>.app/<Spatial>" \
  xcodebuild -project <Spatial>/<Spatial>.xcodeproj -scheme <Spatial> \
             -destination 'generic/platform=visionOS Simulator' build
exit $rc
```

The Mac build works from the command line; only running a Designed-for-iPad build needs Xcode (see
`designed-for-ipad-on-mac.md`).

**2. Guard test switches mechanically.** `check-test-cvars.py` finds every console variable whose name
marks it as a test switch (`debug|diag|dump|show|viz|probe|skip`, plus an explicit list), and fails if any
is registered as saved (`CVAR_ARCHIVE`) or is missing from the one function that resets test switches at
launch. A real setting that matches the pattern goes in an allow-list with its reason. The launch reset is
the real guard: an old `seta` line in a config re-arms a variable whatever flags the code gives it.

**3. Guard mirrored tables.** When two languages each hold a copy of the same defaults (here Swift's controller
bindings and the C engine's boot defaults), a script parses both and fails on any difference.
`check-binding-defaults.sh` exists because three bindings drifted with nothing failing: the Swift value
overrode the C one at runtime, so the drift only showed on first boot.

**4. Snapshot and restore the player's settings around every run.**

```bash
config-guard.py snapshot      # app closed: save every saved-setting line
<run the capture / matcher / A-B harness; let the app quit>
config-guard.py restore       # wait for the app to exit, put every value back, remove lines the run added
```

The restore has to happen from outside the engine with the app closed. Latched settings write their current
value on quit, so a closing command inside the run can't put them back.

## Traps

- **"BUILD SUCCEEDED" isn't evidence of a rebuild.** Check the product's mtime against the newest source; a `touch` alone didn't prevent stale binaries.
- **A bare `xcodebuild clean` wipes every configuration's products.** Then the other destination's binary looks stale on the next run. Clean with the same `-sdk`/`-destination` as the build.
- **Generated projects miss new files until regenerated.** Wildcard source rules in `project.yml` only pick up a new file when `xcodegen generate` runs, so the spec listed a file the project didn't have.
- **Regenerating drops files added to the project by hand** that no rule in `project.yml` covers. Diff the old and new file lists after regenerating.
- **Platform macros overlap.** The visionOS target defined both `IOS` and `VISIONOS`, so `#ifdef IOS` code compiled there. iOS-only code needs `#if defined(IOS) && !defined(VISIONOS)`.
- **Keep an existing snapshot.** If one already exists, the last restore didn't run, and the config now holds test values. Snapshotting again would save them as the player's. This happened.
- **Restore only what was there before.** At first, only the ~20 renderer settings the capture set were restored, and runs kept leaking others: crosshair off (twice), the player model changed, the HUD hidden. Save and restore every line, and remove lines the run added.
- **`pgrep -f <app path>` matches the shell that mentions the path** and waits forever. Use `pgrep -x <process name>`.
- **Don't edit a config the app rewrites on exit.** To change a setting in a running app, send it a command (see `game-console-driving.md`).

## What it does not cover

Building isn't running. Each target still needs its own launch check (`headless-ios.md`,
`designed-for-ipad-on-mac.md`, `vision-pro-screenshots.md`), and device-only and headset-only behaviour goes
to `human-verify-queue.md`. The test-switch guard covers the switches it can name; a test setting with an
ordinary name needs adding to its list by hand.

## Loading this into Claude

> A change isn't done until `./tools/build-check.sh` (no argument) passes on every target: simulator, Mac
> and visionOS. Never build just one, and never report on `BUILD SUCCEEDED` alone. The script proves each
> product was rebuilt. A new debug or test setting is never saved, and goes in the launch reset list in the
> same commit; the build fails otherwise. Every harness run that launches the app is wrapped in
> `config-guard.py snapshot` / `restore`. After `xcodegen generate`, diff the project's file list.
