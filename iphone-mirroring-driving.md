# Drive a real iPhone through iPhone Mirroring

> Lets Claude tap, scroll, type on and screenshot a real iPhone from the Mac through the iPhone Mirroring window, when computer-use control is unavailable, and capture only that window.

**Applies to:** any app on a real iPhone, including system apps (Safari, Shortcuts, Settings) a simulator can't stand in for · **Needs:** macOS with iPhone Mirroring set up for the phone, Swift (`swiftc`, from the Xcode command-line tools), `screencapture`, `xcrun devicectl` with the phone paired; Screen Recording and Accessibility granted to the app that runs the shell

## Why it exists

Some steps only happen on the real phone: adding a downloaded file in Safari, answering a system
permission question, checking what a Shortcut or the Watch actually did. Without a way to reach the
phone, Claude writes "now tap X on your phone" and waits for a description back. Computer-use would let
it drive the mirroring window, but it is not always available (see
[AppleScript + screencapture fallback](applescript-screencapture-fallback.md)), and the obvious
substitute fails: System Events clicks land on the Mac window but never reach the mirrored phone. Real
mouse events posted with CoreGraphics do. Built for Circus, to install and run a generated Shortcut on a
phone.

## What it does

1. Find the iPhone Mirroring window's ID and bounds with `CGWindowListCopyWindowInfo`.
2. Capture that window alone with `screencapture -o -l <window id>` and read the PNG.
3. Convert a point on the capture to a screen point, and post real mouse or keyboard events there with small Swift CGEvent tools: tap, long-press, drag, type.
4. Launch apps directly with `xcrun devicectl device process launch` instead of hunting for icons.
5. Capture again and check the screen changed the way the action should have changed it.

## Recipe

Read [AppleScript + screencapture fallback](applescript-screencapture-fallback.md) first: it covers the
grants, running scripts from files, and `screencapture` in general. This page adds only what the
mirrored phone needs.

**1. Build the tools once**, into a scratch folder, each from its own file:

```swift
// tap.swift: tap <x> <y> [hold seconds]   screen points; a 1.2 s hold is a long-press
import CoreGraphics
import Foundation
let a = CommandLine.arguments
let p = CGPoint(x: Double(a[1])!, y: Double(a[2])!)
let hold = a.count > 3 ? Double(a[3])! : 0.08
func post(_ t: CGEventType) {
    CGEvent(mouseEventSource: nil, mouseType: t, mouseCursorPosition: p, mouseButton: .left)?.post(tap: .cghidEventTap)
}
post(.mouseMoved); usleep(80_000)
post(.leftMouseDown); usleep(useconds_t(hold * 1_000_000))
post(.leftMouseUp)
```

```swift
// drag.swift: drag <x1> <y1> <x2> <y2>   the way to scroll; drag up to scroll down
import CoreGraphics
import Foundation
let a = CommandLine.arguments.dropFirst().map { Double($0)! }
let from = CGPoint(x: a[0], y: a[1]), to = CGPoint(x: a[2], y: a[3])
func post(_ t: CGEventType, _ p: CGPoint) {
    CGEvent(mouseEventSource: nil, mouseType: t, mouseCursorPosition: p, mouseButton: .left)?.post(tap: .cghidEventTap)
}
post(.mouseMoved, from); usleep(80_000); post(.leftMouseDown, from); usleep(80_000)
for i in 1...20 {
    let f = Double(i) / 20
    post(.leftMouseDragged, CGPoint(x: from.x + (to.x - from.x) * f, y: from.y + (to.y - from.y) * f))
    usleep(15_000)
}
usleep(150_000); post(.leftMouseUp, to)
```

```swift
// typeit.swift: typeit "<text>"   types into the focused field, one character at a time
import CoreGraphics
import Foundation
for ch in CommandLine.arguments[1].utf16 {
    var c = ch
    for down in [true, false] {
        let e = CGEvent(keyboardEventSource: nil, virtualKey: 0, keyDown: down)
        e?.keyboardSetUnicodeString(stringLength: 1, unicodeString: &c)
        e?.post(tap: .cghidEventTap)
        usleep(25_000)
    }
}
```

```swift
// winid.swift: winid "<owner name>"   prints: window id, x, y, width, height (screen points)
import CoreGraphics
import Foundation
let list = CGWindowListCopyWindowInfo([.optionAll], kCGNullWindowID) as! [[String: Any]]
for w in list where (w[kCGWindowOwnerName as String] as? String) == CommandLine.arguments[1]
                 && (w[kCGWindowLayer as String] as? Int) == 0 {
    let b = w[kCGWindowBounds as String] as! [String: Any]
    print(w[kCGWindowNumber as String]!, b["X"]!, b["Y"]!, b["Width"]!, b["Height"]!)
}
```

```bash
swiftc -O tap.swift -o tap
swiftc -O drag.swift -o drag
swiftc -O typeit.swift -o typeit
swiftc -O winid.swift -o winid
```

**2. Find the window and capture it alone.**

```bash
open -a "iPhone Mirroring"
./winid "iPhone Mirroring"          # e.g. 4711 1200 180 336 744
screencapture -x -o -l 4711 phone.png
sips -g pixelWidth -g pixelHeight phone.png
```

`-l` captures that one window, even behind others, so nothing else on the screen is ever in the image.
Never fall back to a full-screen capture to "see the phone".

**3. Map a point on the capture to the screen.** `winid` reports points; the PNG is in pixels
(normally twice the points on a Retina display). For a point at pixel `(px, py)` on `phone.png`:

```
scale   = pixelWidth / window width
screenX = window x + px / scale
screenY = window y + py / scale
```

CGEvent and the window list both use global points from the top-left of the main display, so no flip
is needed.

**4. Act, then capture again.**

```bash
./tap <screenX> <screenY>                  # tap
./tap <screenX> <screenY> 1.2              # long-press
./drag <x> <y+200> <x> <y-200>             # scroll the content down
./tap <field x> <field y>; ./typeit "<text>"
screencapture -x -o -l <window id> phone.png
```

Re-run `winid` before acting if the window may have moved or reopened: the ID changes when mirroring
reconnects.

**5. Launch apps without tapping icons.**

```bash
xcrun devicectl list devices
xcrun devicectl device process launch --device <device> --terminate-existing <bundle id>
```

System apps launch the same way by their bundle ID. If `devicectl` refuses because the device is
locked, open the app by tapping its icon in the mirroring window instead.

**6. Tell a capture is real.** Before trusting a capture as evidence:

- the window ID came from `winid` in this step, and its owner is iPhone Mirroring;
- the PNG's size matches the window's bounds times the scale (a wrong ID gives another window's size);
- it shows the phone's screen, not a "Connecting…", "iPhone in use" or lock placeholder;
- it differs from the previous capture where the action should have changed something (compare `shasum` of the two files when in doubt), and shows something only the new state has: the typed text, the new screen title, the status-bar clock moving on.

Where the app can write a log or file, pull that too ([device crash-log pull](device-crashlog-pull.md)
shows `devicectl device copy from`); it is stronger proof than a picture.

## Traps

- **System Events clicks don't reach the phone.** `click at` and AppleScript UI clicks hit the Mac window only. Post CGEvents at `.cghidEventTap`.
- **The scroll wheel barely moves the phone.** Wheel events scroll a few points at most. Scroll with a drag, as a finger would.
- **The events move the real pointer.** Each tap takes the Mac's mouse for a moment. Tell the human before a run of actions, and keep runs short. A click posted only to the Mirroring app's process, without moving the pointer and with the window behind, has no effect: the window must be in front and the pointer must really move.
- **Drag-to-scroll doesn't work on every screen.** It scrolls most lists, but some views ignore it (a share sheet's row of apps didn't move). If a drag doesn't scroll, confirm with a capture and find another way to reach the item, such as search.
- **Mirroring connects only while the phone is locked**, and drops as soon as someone uses the phone. Ask the human to lock it and leave it; if the capture shows a placeholder, wait for them to put it down and reconnect.
- **An alarm or timer going off on the phone ends mirroring.** Reconnect, then re-run `winid`.
- **Safari in Private mode asks for the Mac's password** in the mirroring window to unlock private tabs. Claude never types it; switch to a normal tab, or ask the human.
- **Tapping a tile in Shortcuts runs that shortcut.** To inspect one, long-press the tile and choose Edit.
- **Typing goes to whatever has focus.** Tap the field, capture, check the keyboard is up, then type.
- **Coordinates from the PNG are pixels, events are points.** Forgetting the scale taps twice as far from the window's corner.

## What it does not cover

- Setting up iPhone Mirroring, pairing the phone, and granting Screen Recording and Accessibility. The human does these.
- Typing passwords or passcodes, answering Face ID, and payment sheets. The human does these on the phone.
- Multi-finger gestures (pinch, rotate) and hardware buttons; mirroring takes one pointer.
- Watch, CarPlay or anything on another screen the phone drives.
- Timing-sensitive input (games, held drags with precise speed).

## Loading this into Claude

> To act on the real iPhone when computer-use is unavailable, use iPhone Mirroring. Find its window
> with the `winid` tool (`CGWindowListCopyWindowInfo`, owner "iPhone Mirroring") and capture only that
> window with `screencapture -x -o -l <window id>`; never capture the full screen. Convert PNG pixels to
> screen points with the window's bounds and scale, then post real CGEvents with the `tap`, `drag` and
> `typeit` tools (System Events clicks don't reach the phone; scroll by dragging). Launch apps with
> `xcrun devicectl device process launch --device <device> <bundle id>`. Ask the human to lock the
> phone and leave it while mirroring runs. After every action, capture again and check the change is
> there before calling it done.
