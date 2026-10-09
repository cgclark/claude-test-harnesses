# Animation self-check

> Lets Claude measure an animated diagram frame by frame at a given window size, so it can report every hand-over jump and every overlap to sub-pixel precision instead of eyeballing a playback.

**Applies to:** scripted SVG/HTML animations whose timeline can be set from code: diagram-to-diagram morphs, explainer animations, transitions between two charts (built for an animation that turns a capability map into a project plan) · **Needs:** a page that exposes its timeline (a time variable, a `render(t)` and a `pause()`), a browser Claude can run JavaScript in (see [browser-driving.md](browser-driving.md)), and the window sizes the user actually views at

We built this harness. How to open the page, set the viewport and run JavaScript in it is in [browser-driving.md](browser-driving.md). This page covers what to measure in an animation and how.

## Why it exists

Claude showed animation work it had only watched. The user saw each defect on a phone, one at a time:

- Words jumped in size at the hand-over from the drawing to the moving copies. Text set directly at a tiny font size rendered about 11% wider than the same text drawn at full size and scaled down.
- Everything resized partway through, because a scrollbar appeared and disappeared inside the frame.
- The layout was measured at one width and drawn at another.
- Two legends were on screen at once during a crossfade.
- A moving piece crossed other shapes in flight, or stalled at a corner of its path.
- Dashes looked solid in flight, because the two coincident edges of a flat box dashed out of step.

None of these show up in a screenshot of the first or last frame. Several are under a pixel, or last a fraction of a second.

## What it does

1. **Pause and seek.** Stop playback, then set the page's time variable to chosen instants and call `render(t)` directly, so every frame is the same on every run.
2. **Measure at hand-overs.** At the instant before and after one element replaces another, read both elements' `getBoundingClientRect()` and report the largest difference in left, top and width.
3. **Sweep for overlaps.** Step through an interval (0.01 to 0.1 s), and at each step test the boxes of moving pieces against everything visible (opacity above 0.05). Report what was crossed, by id.
4. **Check motion and style rules.** Over the same steps, sample speed for stalls, opacity for "two at once", dash gaps for solid frames and dash jumps, fill colour for see-through or darker frames.
5. **Return one line per rule.** Pass = every distance under 1 px (ours read 0.14 to 0.50), every count 0, every "crosses" / "over" reads `nothing`. The script prints numbers and leaves the judging to whoever reads it. It has no thresholds of its own.

## Recipe

### 1. Make the timeline addressable

The page must have, at script top level (so the console can reach them):

- `let t`, the current time in seconds, and `render(t)`, which draws that instant from scratch with no dependence on the previous frame
- `pause()`
- named constants for the phase boundaries (ours: `LEG0`, `LEGD` for the legend's flight, `SWAP` for the main hand-over, `LAND` for landing)
- handles to the things being checked: the moving pieces, their sources and targets, the legend, the title, the stage

If `render` depends on the previous frame, seeking gives different answers from playback, and the check measures something the user never sees.

### 2. Build-time checks first

Catch mapping errors before anything is drawn. Our builder refuses to build if a moving piece has no target, a target phase doesn't exist, or a dashed line is unmapped:

```bash
python3 <scoping-tools>/animate.py <map_data.py> <ROADMAP.md> <out.html>
# AssertionError: not on the roadmap: <phase>      ← build stops
```

### 3. The browser check

Our check is one async function (`check.js`, about 80 lines) pasted into the page's console or run through the browser tool's JavaScript action. Its skeleton:

```js
(async () => {
  await new Promise(r => setTimeout(r, 800));            // let fonts and layout settle
  pause();
  const R = el => el.getBoundingClientRect();
  const hit = (a, b) => a.left < b.right - 1 && b.left < a.right - 1 &&
                        a.top < b.bottom - 1 && b.top < a.bottom - 1;   // 1 px tolerance
  const out = [`${innerWidth}x${innerHeight}`];

  // hand-over: the source just before, the copy just after
  t = SWAP - 0.01; render(t);
  const before = Object.fromEntries(sources.map(s => [s.id, R(s.el)]));
  t = SWAP + 0.005; render(t);
  let w = 0;
  for (const p of copies) { const a = R(p.el), b = before[p.id];
    w = Math.max(w, Math.abs(a.left - b.left), Math.abs(a.top - b.top), Math.abs(a.width - b.width)); }
  out.push(`main hand-over ${w.toFixed(2)}`);

  // overlap sweep: moving boxes against everything visible
  const crossed = new Set();
  for (let tt = A; tt <= B; tt += 0.04) { t = tt; render(t);
    for (const el of visibleShapes()) for (const m of movers()) if (hit(R(m), R(el))) crossed.add(el.id); }
  out.push(`flight crosses: ${crossed.size ? [...crossed].join(', ') : 'nothing'}`);

  out.push(`page ${document.documentElement.scrollWidth}x${document.documentElement.scrollHeight}`);
  return out;
})()
```

The rules ours checks, each one a defect the user found:

| Line | Measures |
|---|---|
| `legend inside frame`, `legend clear of title` | final legend box within the stage, no overlap with any title line |
| `legend over map` | nothing visible under the legend's final place while the first diagram still shows |
| `<item>: words N, box N` | at landing, the travelling words and swatch against the target's words (a DOM `Range` after the swatch) and swatch: largest left, width or centre difference |
| `legend flight crosses` | moving pieces against visible shapes over the whole flight |
| `legend flight stalls` | speed sampled 60 times: one rise to a peak then one fall, any reversal over 0.05 px is a stall |
| `frames showing both legends` | frames where the moving copy and its target are both visible (opacity above 0) |
| `integration shading` | frames where a fill's alpha is below 1, and frames darker (by luminance) than both ends |
| `solid pieces mid-flight; largest dash step` | dash gap near zero between 30% and 85% of a piece's flight, and the largest change in gap between steps |
| `main hand-over` | the largest jump between each source shape and its moving copy |
| `segmented overlaps` | splitting pieces against landed bars and the legend |
| `page WxH` | must equal the window: anything larger means a scrollbar, which resizes the layout |

### 4. Run at every window size the user views

We ran at **844x390** (phone landscape), **375x812** (phone portrait) and **1800x1000** (desktop). With the built-in pane:

```text
resize_window   width=844 height=390
javascript_tool location.reload()               ← re-lay out at the new size
javascript_tool <check.js contents>             ← returns the lines above
resize_window   preset=desktop                  ← when finished
```

Reload after each resize. The layout is computed once, after fonts load, and a resize without a reload measures a layout drawn for the old size.

Then look at a few frames at a large size around each hand-over. The numbers cover geometry, not taste.

### 5. Keep the check next to the builder

Every time the user names a new rule, add a line to the check in the same change, so a later edit can't quietly break it. Our commit history has check lines added alongside "never fades", "dashed in flight" and "case-insensitive" fixes.

## Traps

- **Text at tiny font sizes is wider.** Text set directly at a few px rendered about 11% wider than the same text at full size scaled down. Draw moving text at the source's size and animate a scale transform.
- **Box and text widths differ.** A text element's box and the page's rendered text differed by about 1.5%. Match widths on screen by measuring both, not by computing from font size.
- **Scrollbars inside the frame.** A scrollbar appearing mid-animation narrows the layout and everything jumps. Use `overflow: hidden` on the frame, and size the stage to fit the window's height. The `page WxH` line catches this.
- **Measure before fonts load and every width is wrong.** Lay out after `document.fonts.ready`, and wait before the first probe.
- **Crossfades show two of something.** Swap the copy for its target only on the frame it lands exactly. Never fade one in while the other fades out.
- **Coincident edges dash out of step.** A flat box's top and bottom edges, dashed separately, look solid. Walk its path from the left middle and centre a dash at half its length so both edges dash together.
- **Computed colours come back in mixed formats.** `color-mix()` results read back as `color(srgb 0..1 ...)`, not `rgb()`. `fill: none` read as black once. Parse both formats, and give shapes that have no outline an explicit fill.
- **Box hits are conservative.** Circles and curves are tested by bounding box, so a near miss can count as a hit. Check a reported crossing by eye at that frame before changing the path.
- **The path in a note can be wrong.** The task named a check under one project folder, but the file is in another. Find the file on disk before running it.

## What it does not cover

Whether the motion looks good: easing, pacing, what should move at all. That is the user's call. Real devices: phone GPU frame drops, Safari's rendering, and the user's own viewport. The script measures layout in one engine at one size per run. Playback timing: it seeks frames and never measures playback frame rate. Changes nobody asked for. Change only what the user names.

What was verified for this page: we ran a trimmed copy of `check.js` (legend placement, landing distances, main hand-over, page size) against the built page at 844x390 in the built-in pane. It returned hand-over 0.14 px, word landings 0.18 and 0.22 px, swatch landings 0.50 px, and page 844x390. The sweep, stall, dash and shading sections were not re-run for this write-up.

## Loading this into Claude

> After any change to the animation builder or its data, rebuild with `<build command>`. Then open the page in the browser, and at each of `<sizes>` set the viewport, reload, and run `<path>/check.js` through the JavaScript tool. The change is done only when every distance is under 1 px, every count is 0, every "crosses" or "over" line reads `nothing`, and `page` equals the window size. Then look at frames around each hand-over at a large size. When the user states a new rule for the animation, add a line for it to `check.js` in the same change. Report the check's output lines, not "looks right".
