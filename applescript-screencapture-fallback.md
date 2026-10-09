# AppleScript + screencapture fallback

> Lets Claude see the Mac's screen and drive Mac apps from the shell when computer-use control is unavailable or its access request keeps failing.

**Applies to:** any macOS app, Xcode in particular · **Needs:** macOS, `osascript`, `screencapture`; Screen Recording (for capture) and Accessibility (for System Events keystrokes) granted to the app that runs the shell

## Why it exists

In some Claude desktop builds (here, ad-hoc re-signed copies of the app), computer-use's access request
kept failing with "Accessibility and Screen Recording not granted" even though both switches were on
and the app had been removed, re-added and restarted. The leading theory is that an ad-hoc app's
permissions are pinned to one build's signature, so a switch can look on and not match. Retrying the
request just shows the human the same dialog again. Meanwhile the same permissions did reach child
processes of the shell, so `screencapture` and `osascript` worked. Built for Quake3-iOS (Xcode canvas
previews, Mac app captures).

## What it does

1. Drive the app through its AppleScript dictionary (open files, pick scheme, build, run) or System Events keystrokes.
2. Wait on a real signal (a file, a log line, a window appearing), not a guess.
3. Capture the screen, one window or a region with `screencapture -x`.
4. Read the PNG and decide pass/fail from what is on it.

## Recipe

**1. Check what an app can script.**

```bash
sdef /Applications/<App>.app | grep -oE '<(command|property|class) name="[^"]+"' | sort -u
```

Xcode, for example, exposes `open`, `build`, `clean`, `run`, `stop`, `test`, `active scheme`,
`active run destination`, and `last scheme action result` on a workspace document.

**2. Run AppleScript from a file**, not an inline `-e` string with shell variables (quoting and
expansion prompts get in the way). Pass values as arguments:

```applescript
-- open-preview.applescript   (osascript open-preview.applescript <folder> <file>)
on run argv
  tell application "Xcode"
    activate
    open (item 1 of argv)          -- a package folder or .xcodeproj
    open (item 2 of argv)          -- the source file to show
  end tell
  delay 2
  tell application "System Events" to keystroke "p" using {option down, command down}  -- refresh canvas
end run
```

```bash
osascript open-preview.applescript "<project dir>" "<project dir>/Sources/<Feature>Preview.swift"
```

`System Events` keystrokes go to the frontmost app, so `activate` the target first. Menu items are a
more stable target than coordinates:

```applescript
tell application "System Events" to tell process "<App>"
  click menu item "Run" of menu "Product" of menu bar 1
end tell
```

**3. Capture.**

```bash
screencapture -x "$OUT/screen.png"                    # whole screen, no shutter sound
screencapture -x -R 0,0,1280,800 "$OUT/region.png"    # a region, in points
screencapture -x -o -l <window id> "$OUT/win.png"      # one window, no shadow; works when it is behind others
```

Get a window id with a CoreGraphics window list (match on owner name, take the largest):

```swift
import CoreGraphics
let l = CGWindowListCopyWindowInfo(.optionAll, kCGNullWindowID) as! [[String: Any]]
var best = (0, 0.0)
for w in l where (w[kCGWindowOwnerName as String] as? String ?? "").hasPrefix("<App>") {
  let b = w[kCGWindowBounds as String] as! [String: Double]
  if b["Height"]! > 400, b["Width"]! * b["Height"]! > best.1 { best = (w[kCGWindowNumber as String] as! Int, b["Width"]! * b["Height"]!) }
}
print(best.0)
```

Then read the PNG. Downscale large captures first (`sips -Z 1600 in.png`) to save context.

**4. Prefer non-visual evidence where it exists.** A build result, a log line, or a file on disk is a
stronger check than a picture of a label. Use the screenshot for what only a picture shows.

## Traps

- **Do not call computer-use's access request more than once** when it fails like this. Each call puts the same dialog in front of the human. Switch to this fallback.
- **The grants belong to the app running the shell**, not to `osascript` itself. If `screencapture` returns a black or wallpaper-only image, Screen Recording is missing for that app; if keystrokes do nothing, Accessibility is. The human grants them.
- **Keystrokes land in whatever is frontmost.** The Claude app's own window can take focus back between commands, so keys silently go to it. `activate` in the same script as the keystroke, and check with a capture.
- **Xcode previews: if the canvas says "Failed to build"**, the real error is in the `*.preview-thunk.dia` files in that package's DerivedData (`strings` them); previews write no `xcactivitylog`.
- **AppleScript cannot set a Swift package's run destination**; it can set scheme and destination on an `.xcodeproj` workspace document.
- **`xed <file>` or opening a lone file** can give a "Files" window with no project context that builds for the wrong platform. Open the project or package folder first, then the file.
- **After a restart, the Claude session's permission mode can reset** (for example to "Accept edits"), so every command prompts again. Put it back to the mode the human uses.
- **A picture of a stale state looks like a pass.** Check something in the capture that only the new build would show (a version string, a compile stamp, the changed element).

## What it does not cover

- Granting Screen Recording or Accessibility, or fixing why computer-use's own grant does not take. The human does that in System Settings.
- Fine pointer work: drags, hovers, gestures inside game or canvas views. Prefer app-level test hooks.
- Apps with no scripting dictionary and no menu path to the action needed.

## Loading this into Claude

> If computer-use access fails, do not request it again. See the screen with `screencapture -x`
> (`-l <window id>` for one window) and read the PNG; drive apps with `osascript` scripts saved to a
> file, using the app's own AppleScript dictionary first (`sdef` lists it), then System Events menu
> clicks, then keystrokes after `activate`. Prefer a log line or file as proof; use the capture for what
> only a picture shows, and check it shows the new build.
