# Designed for iPad on the Mac

> Lets Claude build, install, launch and screenshot an iOS app running natively on an Apple silicon Mac ("Designed for iPad"), so it can test on real Mac hardware (GPU features the Simulator lacks) without anyone pressing Run.

**Applies to:** iOS / iPadOS apps whose target supports "Mac (Designed for iPad)" · **Needs:** Apple silicon Mac, Xcode command-line tools, Screen Recording permission for the process that takes screenshots

## Why it exists

The Simulator cannot do hardware ray tracing and some Metal paths, so those changes went untested
unless a human pressed Xcode's Run and looked. From the shell, everything obvious fails: `open` on the
built `.app` is refused, `xcodebuild` reports success without updating the copy macOS runs, and a whole
test session was once spent judging a five-hour-old binary because LaunchServices picked a stale
install. Built for Quake3-iOS (ray-traced renderer) and an on-device transcription app.

## What it does

1. Build with the Designed-for-iPad destination.
2. Package the product as `Payload/<App>.app` in an `.ipa` and `open` it; macOS's installer installs it.
3. Find the installed copy whose binary matches the build, and launch that copy by path with `--env` test hooks, in the background.
4. Read the unified log (and a startup compile stamp) and screenshot the app's window from outside.
5. Pass/fail from the log line or image; the run ends with the app quitting itself.

## Recipe

**0. Check the target supports it.**

```bash
xcodebuild -showdestinations -scheme <scheme> | grep 'variant:Designed for'
# needs SUPPORTS_MAC_DESIGNED_FOR_IPHONE_IPAD = YES
```

**1. Build.** The product lands in `Debug-iphoneos` and is `platform IOS` (`vtool -show-build`).

```bash
xcodebuild -project <App>.xcodeproj -scheme <scheme> \
  -destination 'platform=macOS,variant=Designed for iPad' build
DD=$(ls -d ~/Library/Developer/Xcode/DerivedData/<App>-*/Build/Products | head -1)
APP="$DD/Debug-iphoneos/<App>.app"
```

**2. Install via `.ipa`.** Quit the app first; the installer is asynchronous, so poll.

```bash
pkill -f "Wrapper/<App>.app/<App>" 2>/dev/null; sleep 2
STAGE="${TMPDIR:-/tmp}/<app>-ipa"; rm -rf "$STAGE"; mkdir -p "$STAGE/Payload"
cp -R "$APP" "$STAGE/Payload/"
( cd "$STAGE" && zip -qr <App>.ipa Payload )
open -g "$STAGE/<App>.ipa"
```

**3. Resolve the copy that matches this build** (the installer adds copies, it does not replace them):

```bash
WANT=$(shasum "$APP/<App>" | cut -d' ' -f1)
for a in /Applications/<App>*.app; do
  [ "$(shasum "$a/Wrapper/<App>.app/<App>" 2>/dev/null | cut -d' ' -f1)" = "$WANT" ] && { TARGET=$a; break; }
done
[ -n "${TARGET:-}" ] || echo "install did not take yet: retry for ~30 s, then fail"
```

**4. Launch by path, in the background, with env hooks.**

```bash
START=$(date '+%Y-%m-%d %H:%M:%S')
open -g "$TARGET" --env "<HOOK>=1" --env "<SCRIPT>=step1;step2;quit" \
  --args -ApplePersistenceIgnoreState YES
```

`-g` keeps focus with whatever the human is doing. `--env` scopes variables to this launch
(`launchctl setenv` leaks into the whole GUI session). Have the hook script end with the app quitting.

**5. Read results.** Make the app log through `os_log` with its own subsystem, and print a compile
stamp at startup (`"built " __DATE__ " " __TIME__`):

```bash
/usr/bin/log show --start "$START" --predicate 'subsystem == "<subsystem>"' --style compact
/usr/bin/log stream --predicate 'process == "<App>"' --level debug --style compact   # live
```

Screenshot the window from outside (the app's own screenshot files may be unreadable, see Traps):

```swift
// winid.swift — print the window number of <App>'s largest on-screen window
import CoreGraphics
let l = CGWindowListCopyWindowInfo(.optionAll, kCGNullWindowID) as! [[String: Any]]
var best = (0, 0.0)
for w in l where (w[kCGWindowOwnerName as String] as? String ?? "").hasPrefix("<App>") {
  let b = w[kCGWindowBounds as String] as! [String: Double]
  if b["Height"]! > 400, b["Width"]! * b["Height"]! > best.1 { best = (w[kCGWindowNumber as String] as! Int, b["Width"]! * b["Height"]!) }
}
print(best.0)
```

```bash
swiftc -O winid.swift -o "${TMPDIR:-/tmp}/winid"
screencapture -x -o -l "$("${TMPDIR:-/tmp}/winid")" "$OUT/shot.png"
```

**Fallback: Xcode's Run.** If the `.ipa` route is unavailable, Xcode's Run installs and launches. Trigger
it from the **Product menu → Run**, not the toolbar ▶ (see Traps), then confirm the build moved:
`stat -f '%Sm' "$APP/<App>"` must be newer than your last edit.

## Traps

- **`open` on the DerivedData bundle fails** ("incorrect executable format"); `lsregister -f` does not help, the loader refuses. Only the installed copy launches.
- **`xcodebuild` compiles but does not install.** macOS runs a Wrapper copy on a read-only volume; you cannot copy a new binary in. Install through the `.ipa`, every time.
- **The installer adds `/Applications/<App> 2.app`, `3.app`, ...**, root-owned, one full bundle each, and each new path re-asks the app's permissions. `open -b <bundle-id>` then lets LaunchServices pick one, and it picked a stale one. Launch by the shasum-matched path; remove old copies (root needed, so ask the human or use a narrow sudoers rule they set up).
- **Verify by content, never mtime.** The installed copy's mtime is when the install ran, so a reinstalled stale binary looks fresh. Use the shasum match and the logged compile stamp.
- **Designed-for-iPad build caching:** from about the third build, changes compile but are not picked up until a clean. Record the product's mtime, build, and if it did not move while sources are newer, clean **with the same destination** and rebuild. A bare `xcodebuild clean` wipes other destinations' products too.
- **Every `.ipa` install opens a Finder "Applications" window.** Note Finder's window ids before, close only new ones named "Applications" after.
- **Each install can re-raise macOS's local-network prompt.** Give the app a test env flag that opens no sockets.
- **A launch can hang on "reopen windows after unexpected quit?"** (0% CPU, no log). Pass `--args -ApplePersistenceIgnoreState YES`.
- **Newer macOS seals app containers** from other processes, Terminal and Claude included, so files the app writes there (logs, screenshots) cannot be read. Log through `os_log`; screenshot from outside with `screencapture -l`.
- **In zsh, `log` is a builtin** ("too many arguments"). Call `/usr/bin/log`.
- **Fullscreen pauses rendering when focus leaves the app**, so a long run halts the first time a shell call steals focus. Run windowed, or have the app keep rendering while unfocused (a test flag).
- **Window size persists in the app's preferences** and a force-quit can leave it small; drawable resolution follows it. Restore with `defaults write` while the app is quit, or pin the render size with a test flag.
- **Xcode's Stop is SIGKILL.** A setting changed less than about a minute before Stop/Run can be lost before `cfprefsd` flushes; it looks like a persistence bug and is not. Check the plist on disk (`find ~/Library -name "<bundle-id>.plist"`; the container folder is a bare UUID).
- **The toolbar ▶ drops synthetic clicks** and sits about 10 px from Stop, at an x that moves with window width. Use the Product menu.
- **Computer-use allowlists match the bundle name, not the display name.** If the app's window is missing from screenshots, request access by its bundle name.
- **No debugger, and `devicectl` does not list the Mac.** A crash caught by an attached debugger writes no `.ips`; use `log stream`, which is also the only place Metal validation errors and GPU faults appear.
- **Compile-time checks stay iOS.** `#if os(macOS)` is never true here; branch on `ProcessInfo.processInfo.isiOSAppOnMac` at runtime.

## What it does not cover

- iPhone/iPad hardware behaviour (stack size, sensors, Bluetooth, thermals). Test on a device.
- Mac-only UI differences a human would notice (pointer feel, window chrome, keyboard focus).
- Removing root-owned old installs and granting system permissions (Screen Recording, sudoers rules). The human does those.

## Loading this into Claude

> For anything the Simulator cannot do, test the "Designed for iPad" build on this Mac headlessly:
> build with `-destination 'platform=macOS,variant=Designed for iPad'`, package it as
> `Payload/<App>.app` in an `.ipa`, `open -g` it to install, then launch the `/Applications` copy whose
> binary shasum matches the build, by path, with `open -g <path> --env ...
> --args -ApplePersistenceIgnoreState YES`. Never launch by bundle id. Confirm the compile stamp in
> `/usr/bin/log show --predicate 'subsystem == "<subsystem>"'`, screenshot with `screencapture -l
> <window id>`, and have the test script quit the app at the end.
