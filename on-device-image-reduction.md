# On-device image reduction

> Lets Claude read screenshots, scans and screen captures of test results as text, with line positions, reduced on the Mac before anything reaches its context, so it can check many captures without spending image tokens on each.

**Applies to:** any harness that ends in a picture: simulator and device screenshots, game frames with on-screen
text, scanned or exported reports, live Mac windows · **Needs:** macOS with Apple Vision (macOS 26 for the newest
requests), Xcode command-line tools to compile two small Swift tools; optional Screen Recording and Accessibility
permissions for live capture; optional Python 3.10+ and MLX for the local vision-model tier

## Why it exists

By default Claude reads each screenshot as an image. One full page or screen costs roughly 1,500–2,500 context
tokens, against 500–700 for the same content as text, and the image stays in the context for the rest of the
session. A harness that captures twenty screens, or one per language, fills the context with pixels, so Claude
checks a few and asks the user to look at the rest. Compaction is lossy and global; the only way to keep an image out
is not to load it.

Built first for batches of scanned documents, then reused as the capture step for screenshot-based test harnesses.

## What it does

1. The harness writes its capture to disk (a `simctl` screenshot, a frame grab, a PDF).
2. A local reducer turns it into text: `ocr` for documents (plain text, page markers), `screenreduce ocr` for screens
   (JSON lines with pixel boxes and confidence), `screenreduce ax` for a live Mac app's accessibility tree.
3. Claude, or a subagent, reads only the text or JSON and checks for the expected strings, their order, or their
   position.
4. When text is not enough (colour, layout, an icon), escalate one frame to Claude's own vision inside a subagent, so
   the image is gone when the subagent returns.

## Recipe

**1. Build the reducers** from source (prebuilt binaries do not travel well across Macs):

```bash
swiftc -O scripts/ocr.swift -o scripts/ocr
swiftc -O scripts/screenreduce.swift -o scripts/screenreduce
```

**2. Reduce a screenshot** and check it:

```bash
xcrun simctl io <device> screenshot <out>/home.png
screenreduce ocr <out>/home.png
# {"w":1600,"h":600,"lines":[{"t":"Tests: 42 passed, 1 failed","box":[58,128,844,81],"conf":1}, ...],
#  "text":"Tests: 42 passed, 1 failed\nFAIL testCheckoutTotal"}
screenreduce ocr <out>/home.png | python3 -c "import json,sys; t=json.load(sys.stdin)['text']; sys.exit(0 if '<expected label>' in t else 1)"
```

Boxes are `[x, y, w, h]` in image pixels, origin top-left. On Retina captures that is twice the point size, so convert
before comparing with layout code or tap coordinates.

**3. Reduce documents and reports:**

```bash
ocr <report>.pdf -o <out>/report.txt --page-sep --quiet   # text layer used when present; scans go to Vision
ocr <scan>.png --lang de-DE,en-US                          # language hints for non-English text
ocr <scan>.pdf --force-vision --pages 2-3                  # ignore a bad text layer, OCR only these pages
scripts/ocr-batch.sh <dir> <out-dir>                       # a folder to sidecar .txt, skipping up-to-date ones
```

**4. Live screen, when there is no file:**

```bash
screenreduce capture -R <x>,<y>,<w>,<h>    # screencapture + OCR in one step; needs Screen Recording
screenreduce ax                            # frontmost app's accessibility tree as JSON; needs Accessibility
```

For native Mac apps try `ax` first: roles, titles, values and frames are exact, and cheaper than OCR. It stops at 500
nodes or depth 14.

**5. Batches go through subagents.** For many captures, spawn one subagent per file (or per few files). Each runs
the reducer, reads only the output, and returns a small record such as `{"file": ..., "expected": [...],
"missing": [...], "pass": true}`. The main thread never opens an image. The `ocr-index` skill packages this for
document folders.

**6. Local vision model, for non-text content only.** When a capture has no text to check (a chart, a photo, a
rendered scene) and the description is enough:

```bash
scripts/vlm-probe.sh <image> "<question>" [mlx-community/<model>]   # first run creates a venv and downloads weights
```

## Traps

- **Vision returns nothing, with no error.** Some colour profiles and bit depths (a profiled PNG from `sips`) give 0
  observations. Redraw every image into a plain device-RGB bitmap before OCR; the tools do this. If a reducer
  returns empty, suspect the image format before concluding the screen is blank.
- **Small local vision models cannot transcribe.** On a clean invoice that Vision OCR read exactly, a 2B 4-bit model
  hedged that the text was "not fully visible" and a 3B 4-bit model collapsed into repeating one word 42 times.
  Use OCR for text; keep the VLM for describing non-text content, and downscale images first (a 1700×2200 image
  was about 4,850 of the model's own tokens).
- **On-device output is lossy and decided in advance.** OCR drops styling, colour and anything it misreads. Keep the
  originals on disk and escalate a single frame when a result depends on what text cannot carry.
- **"Ignore the images" does not work.** Opening a scan or screenshot loads the raster whatever the intent. Reduce
  first, then read the text.
- **Confidence is not correctness.** A `conf` of 1 means Vision is sure of what it read, not that the screen is right.
  Compare against expected strings.
- **Search on reduced images.** When images go through an index, confirm a word you know is on a captured screen is
  found before trusting a no-hit (see [Document value verification](document-value-verification.md)).
- **Permissions belong to the host app.** `capture` and `ax` need Screen Recording and Accessibility granted to the
  terminal or app running them, not to the tool. Without them `capture` writes no file and `ax` exits with a message.
- **Batch script file types.** `ocr-batch.sh` globs PDF, PNG, JPEG and TIFF only; convert WebP or HEIC first.

## What it does not cover

Visual quality: colour, alignment, clipping, animation, and anything with no text. Those need Claude's own vision on
the specific frame, or a pixel diff (see [Renderer A/B on demos](renderer-ab-on-demos.md)). It also does not replace
reading app state directly: a launch-argument state dump or an accessibility tree is more exact than OCR of a
screenshot.

## Loading this into Claude

> Screenshots and scans are reduced on device before reading: `screenreduce ocr <png>` for screens (JSON with pixel
> boxes), `ocr <file> --page-sep --quiet` for documents, `screenreduce ax` for a live Mac app. Check expected text
> against the JSON; do not open the image. For more than a few captures, use one subagent per file and return only
> pass/fail records. Escalate a single frame to vision, in a subagent, only when the check depends on colour or
> layout. Never use a small local VLM to read text.
