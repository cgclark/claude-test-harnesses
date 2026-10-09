# Layout probe

> Lets Claude measure what UIKit actually laid out — bar heights, scroll offsets and insets, the frame and text attributes of a label inside a system view — frame by frame through a transition, so it finds the cause of a layout bug instead of guessing at fixes.

**Applies to:** iOS / iPadOS apps, SwiftUI or UIKit · **Needs:** Xcode with an iOS runtime, `simctl`, `ffmpeg` (for the frame sheet)

## Why it exists

A screenshot shows the end state of a layout bug, not how it got there. By default Claude reasons from the
screenshot to a likely cause, edits the code, rebuilds and looks again. When the cause is inside UIKit, every
guess looks plausible and none of them tests anything.

Built for Throwdown. In Arabic only, the first screen pushed after launch opened with its large title
collapsed into the bar. Five guessed fixes in a row did nothing: warming the title font, warming a separate
navigation controller, the digit locale, the typesetting language, and the bar's appearance attributes. A
probe found the cause in two runs. The bar gives some large titles a taller label (46.3 pt for Arabic, and
also for Polish "Własny" and Vietnamese "Tuỳ chỉnh"; 42.7 pt for English; 40.7 pt for the brand name in
Polish), and keeps the tallest it has laid out. So the first push between heights was the first time the bar
had to grow, and that left the pushed screen collapsed, in Polish and Vietnamese as well as Arabic. The fix:
one shared large-title modifier adds the invisible Arabic letter mark (U+061C) to every title in every
language, so they all share the tall line.

## What it does

1. A temporary timer in the app walks the window's view hierarchy every 0.1 s and `NSLog`s the numbers in
   question, with a fixed prefix.
2. Claude drives the app to the failing moment (tap, push, pop), then the passing one for comparison.
3. Claude reads the lines back from the simulator's unified log, keeping only the ones that changed.
4. For a transition, a screen recording is cut into a tiled frame sheet, one image showing every frame.
5. The failing and passing numbers are compared. Each hypothesis then gets one experiment that changes one
   thing, checked against the same numbers. Afterwards the probe and experiments are removed, and the diff
   confirms nothing is left.

## Recipe

**1. The probe.** Add it to a file the target already compiles (a new file may need the project
regenerated). Mark every line so removal is a single search:

```swift
enum LayoutProbe { // PROBE — remove
    static func start() {
        var n = 0
        Timer.scheduledTimer(withTimeInterval: 0.1, repeats: true) { t in
            n += 1; if n > 300 { t.invalidate() }                       // 30 s, then stops
            guard let window = UIApplication.shared.connectedScenes
                .compactMap({ $0 as? UIWindowScene }).first?.windows.first else { return }
            var out: [String] = []
            func walk(_ v: UIView) {
                if let b = v as? UINavigationBar { out.append(String(format: "bar h%.1f", b.bounds.height)) }
                if let s = v as? UIScrollView, s.bounds.height > 500, abs(s.convert(s.bounds, to: nil).minX) < 10 {
                    out.append(String(format: "scroll off%.1f inset%.1f", s.contentOffset.y, s.adjustedContentInset.top))
                }
                if let l = v as? UILabel, (l.font?.pointSize ?? 0) > 30, n % 10 == 0 {   // e.g. a large title
                    out.append("label \(l.text ?? "") \(l.frame) in \(type(of: l.superview!))")
                }
                v.subviews.forEach(walk)
            }
            walk(window)
            NSLog("PROBE %d %@", n, out.joined(separator: " | "))
        }
    }
}
```

Start it from the app's `init` with `DispatchQueue.main.async { LayoutProbe.start() } // PROBE`.

**2. Drive the failing case, then the passing one,** with the simulator tools (tap, swipe). Note roughly when
each happened, because the tick count gives the time.

**3. Read the log, changes only:**

```bash
xcrun simctl spawn <udid> log show --last 2m --style compact \
  --predicate 'eventMessage BEGINSWITH "PROBE"' | sed -E 's/.*PROBE/PROBE/' \
  | awk '{k=$0; sub(/PROBE [0-9]+ /,"",k); if (k!=p) print; p=k}'
```

**4. A transition as one image:**

```bash
xcrun simctl io <udid> recordVideo --codec h264 --force push.mov &   # start, then tap
kill -INT %1                                                         # stop a few seconds later
ffprobe -v error -select_streams v -show_entries frame=pts_time -of csv=p=0 push.mov   # when frames change
ffmpeg -ss <first change> -i push.mov -vf "fps=30,scale=250:-1,crop=250:180:0:0,tile=8x3" -frames:v 1 sheet.png
```

The crop keeps only the top of each frame (the bar), so 24 frames fit on one readable sheet.

**5. Bisect with launch arguments before editing code.** Phone language against app language
(`-AppleLanguages (en)` with the app's own language key set to the failing one, and the reverse), first push
against second, one screen against another. Each run separates causes without a rebuild.

**6. One experiment per hypothesis.** Change one thing, mark it, rebuild, compare the same probe lines.
Revert it before the next experiment. When the numbers match the passing case, write the real fix, then
remove the probe. `git diff` must show only the fix.

## Traps

- **A label measured on its own isn't the label in the bar.** A plain `UILabel`, `sizeThatFits`, and the font's
  `lineHeight` all gave 42.7 pt for Arabic and Latin alike. Only the label inside the bar's own view measured
  46.3 pt. Probe the live hierarchy, not a copy.
- **Warm-ups are per object.** Laying out a separate navigation controller warmed nothing, because the height
  was state in the app's own bar. If an experiment primes a cache, prime the one actually in use.
- **Bar appearance attributes can be ignored.** A paragraph style in `largeTitleTextAttributes` changed nothing.
  Exaggerate a test value (70 pt) so "no effect" is unambiguous.
- **Screen recordings only store frames that change.** `fps=10` from time 0 repeated the idle home screen.
  Find the first changed frame with `ffprobe`, and start the sheet there.
- **The first tap after a relaunch can land before the app has drawn.** Take a screenshot before trusting a tap.
- **zsh has no `PIPESTATUS`.** `xcodebuild … | grep` reports grep's status, so a failed build looks fine.
  Write the build to a log and check `$?` and the log's `error:` count.
- **Don't leave the probe in.** It logs ten lines a second. Search for the marker and check the diff before
  committing.

## What it does not cover

It measures layout, not whether the result looks right. The screenshot and the human still judge that. Private
UIKit views can change between iOS releases, so a probe keyed on a private class name needs checking on each
new OS.

## Loading this into Claude

> For a layout bug whose cause isn't visible in the code, measure before fixing. Add the `LayoutProbe` timer
> (every line marked `// PROBE`), reproduce the failing case and a passing one, read
> `log show --predicate 'eventMessage BEGINSWITH "PROBE"'`, and tile any transition with `ffmpeg … tile=8x3`.
> Bisect with launch arguments first. Run one marked experiment per hypothesis and revert it before the next.
> When the numbers match the passing case, write the fix and remove every probe line.
