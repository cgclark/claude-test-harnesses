# Accessibility-tree tapping

> Lets Claude tap a simulator control at the frame the accessibility tree reports for it, and confirm the tap from the tree, instead of guessing coordinates from a screenshot.

**Applies to:** iOS / iPadOS simulator apps with standard UIKit or SwiftUI controls · **Needs:** `idb` (`idb-companion` from Homebrew plus the `fb-idb` Python client), a booted simulator

## Why it exists

Claude's default is to read a screenshot, estimate where a button is, and tap there. A miss usually lands
on something plausible and reads as "the button does nothing". Once, a backwards rotation sent the tap to
the character preview, which rotated the model, and Claude produced eight identical frames and a wrong
conclusion that the jump never fires.

Built for the Quake 3 port's native Settings screens. It's a standard tool (Claude recommended it); what
follows is what we learned using it.

## What it does

1. `idb ui describe-all` dumps the on-screen accessibility tree as JSON: label, identifier and frame for each element.
2. Claude picks the element by label or identifier and taps the centre of its frame.
3. It re-reads the tree: the new screen's labels appearing is the pass. No screenshot needed.

## Recipe

```bash
# Is it installed? The CLI from pip often lands in a Python env that isn't on PATH.
command -v idb idb_companion || python3 -m pip show fb-idb
# Install if missing
brew tap facebook/fb && brew install idb-companion
python3 -m pip install fb-idb
idb list-targets          # must list the project's simulator as Booted
```

```bash
idb ui describe-all --udid "$UDID" > tree.json
# center.py: print the centre of the first element whose label or identifier matches
#   import json, sys
#   for e in json.load(open(sys.argv[1])):
#       if sys.argv[2] in (e.get("AXLabel"), e.get("AXUniqueId")):
#           f = e["frame"]; print(round(f["x"] + f["width"]/2), round(f["y"] + f["height"]/2)); break
read X Y < <(python3 center.py tree.json "Done")
idb ui tap --udid "$UDID" "$X" "$Y"
idb ui describe-all --udid "$UDID" | grep -q '"<label on the next screen>"' && echo PASS
```

Long press: `idb ui tap --duration 1.1 X Y` (not a zero-length swipe). Text: `idb ui text "…"`.

## Traps

- **Taps are in points, not screenshot pixels.** `simctl io screenshot` returns the full-resolution framebuffer. Divide by the device scale (2 on iPads, 3 on recent iPhones) before tapping, or the tap lands on nothing.
- **A landscape app reports landscape frames, but `idb ui tap` takes portrait points.** The rotation direction differed between two iPad models (`tap = (W - y, x)` on one, `(y, H - x)` on the other). Calibrate once per device: find one element whose position you know from a screenshot, and check which formula puts the tap on it.
- **Engine-drawn UI has no tree.** An SDL or Metal menu exposes nothing, and its relative-mouse cursor ignores taps. A visionOS app has no tree that `idb` or `simctl` can tap. Use a launch hook to open the screen (`launch-argument-test-hooks.md`), then tap the native controls.
- **Some screen regions never received taps.** In one app, injected taps didn't reach the bottom fifth of the screen. A launch hook was the only way to open the screens behind those buttons.
- **Read state from the tree, not from `defaults read`.** Once `simctl spawn … defaults read` returned one character while the screen plainly showed another. The button label in `describe-all` was right.
- **Key injection reaches some input paths and not others.** In a game, `idb ui key` reached one keyboard path but not the controller poll or the engine's own key handling. Check each path with a log line before relying on it.
- **Target state can be stale.** `list-targets` showed a simulator as Booted seconds after another session had shut it down; `describe-all` then refused. Check `simctl list` and boot if needed.
- **`idb` can lag a new Xcode.** It worked with Xcode 27 and iOS 27 simulators when this was written. After an Xcode upgrade, if `idb-companion` won't load the new CoreSimulator, say so rather than falling back to guessed coordinates.
- **When you own the app, XCUITest does this better.** It taps by `accessibilityIdentifier`, waits for existence, and asserts (see `localized-screens-contact-sheets.md`). `idb` is for a quick tap in a running app without a test target.

## What it does not cover

Anything the tree can't see: games, custom-drawn views, visionOS spatial input, system sheets in another
process. Also reach and gesture feel on a real device, which stays with a person.

## Loading this into Claude

> Tap simulator controls by their accessibility frames, never by coordinates guessed from a screenshot. Run
> `idb ui describe-all --udid <UDID>`, take the centre of the element's frame (points, not pixels; convert
> landscape frames with this device's formula: `<formula>`), `idb ui tap`, then re-read the tree to confirm the
> next screen. If `idb` isn't on PATH, check `python3 -m pip show fb-idb` before saying it's missing. For screens
> with no tree, use a launch hook.
