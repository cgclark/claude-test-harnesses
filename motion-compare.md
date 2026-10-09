# Motion compare

> Lets Claude put a generated signing hand next to the source signer, aligned on the same moment of the sign, and measure where the motion differs, instead of judging an animation on its own.

**Applies to:** generated or retargeted motion checked against a reference performance: sign language, gesture, hand or body animation from capture data or a model (built for an ASL sign-generation prototype that drives a 21-joint hand figure in an iOS app) · **Needs:** Python 3 with OpenCV and NumPy, `ffmpeg`, `xcrun simctl` (to record the app), `pygltflib` for GLB files, Blender run headless for FBX files, a hand-landmark detector for the landmark overlay (MediaPipe here), a reference clip you are allowed to use

## Why it exists

Seen on its own, a generated sign looks plausible. Claude's default is to render it, see a hand that moves, and report it working. People who could read the sign kept finding what a lone render hides:

- **Lost repetition.** Signs made from monocular video had lost their repeated taps: 0 motion cycles where the capture-based signs kept 3. The 3-D hand estimator drops motion-blurred frames, and the fast taps are exactly those frames. Only a frame-aligned comparison with the source made this visible.
- **Limp motion.** Generated signs moved at a fraction of the source speed (peak joint speed median 0.72 against 1.70 for captured signs). That is the "not intentional" feeling, measured.
- **A clock-aligned compare that didn't line up.** The source clips have rest before and after the sign, while the model's trajectory is the sign only. Looping both on one clock showed the video at rest while the model signed. Windowing only the video wasn't enough either: two models with a slow lead-in (68% and 81% of frames in the sign itself) still drifted.
- **A motion file with no motion.** An animation export had hundreds of animation curves and tens of thousands of keyframes, all holding one value. Counting curves said "animated". Only checking each curve's range showed it was static.
- **A wedged simulator.** Once the compare view (3-D scene plus video player) ran, the simulator's screenshots timed out. Rendering the model offline from its joint data kept the comparison going.

## What it does

1. **Inspect the source asset.** List its nodes, skin, animations (channel count and duration) and hand bones, so its rig can be mapped onto the app's joint schema. Then check that each animation curve actually changes value.
2. **Record the generated side.** Either a `simctl io recordVideo` of the app's figure, or an offline render of the joint data in the app's look.
3. **Align on content, not on time.** Find one event in each clip (here the frame where the hands tap), take a window around it in both, resample both to the same length, and stack them side by side with labels.
4. **Optional landmark check.** Run a landmark detector on the source video, and draw the detected joints in the app's style next to each source frame. This checks the extraction step on its own, before any model is involved.
5. **Measure:** peak joint speed (limp against crisp), motion-cycle count (repetition), handshape error against the source, and the surface gap between the two hands (contact against collision).
6. Read the side-by-side, then the numbers. Correctness of the sign itself goes to a fluent signer.

## Recipe

1. **Inspect the asset:**
   ```bash
   python3 tools/glb_inspect.py <sign>.glb          # nodes, animations (channels, duration), hand bones, hierarchy
   <blender> -b --python tools/fbx_probe.py -- <sign>.fbx          # actions, curve and key counts, key extent
   <blender> -b --python tools/fbx_motion_probe.py -- <sign>.fbx   # curves whose value range > 1e-4
   ```
   A static file reports `MOVING=0`. Run the same probe on a sign you know moves, to show the probe can tell the difference.
2. **Record the app figure** (see `headless-ios.md`): launch straight into the sign under test with an environment flag, then
   ```bash
   xcrun simctl io <udid> recordVideo --codec=h264 fig.mp4    # Ctrl-C to stop
   ```
3. **Build the aligned side-by-side:**
   ```bash
   python3 tools/synced_compare.py fig.mp4 src.mp4 out.mp4 --crop <x1> <y1> <x2> <y2> \
     --src-tap <frame> [--outlen 57] [--settle 1.4]
   ```
   The figure's tap is the frame with the most skin-coloured pixels in the centre columns of the crop, searched in the 2.3 s after `--settle` (which skips the app launch). The source tap is a frame index you supply. Both windows are resampled to `--outlen` frames and written as one H.264 mp4. The skin test is a brightness threshold against the app's dark background, so retune it for another look.
4. **Landmark overlay** (checks extraction, not generation):
   ```bash
   python3 tools/side_by_side.py src.mp4 overlay.mp4
   ```
5. **Strips and windows.** For a still review, grab both clips at matching fractions of each one's active window into a two-row filmstrip. Find each active window from motion energy: frame differences on the video, joint velocity on the model, active above 30% of the range. Map active window to active window, not clip to clip.
6. **Gaps between hands.** Measure the gap between finger surfaces, not joint centres: segment-to-segment distance between bones minus both radii. Below 0 means interpenetration, about 0 is touching. With thick rendered fingers, signs that really touch sat at about -0.02 to -0.06, so set the threshold from the rendered finger radius, not a fixed distance.

## Traps

- **Clock sync is not content sync.** Trim both sides to the active part of the sign before aligning. Even then, two performers sign at different tempos, so the middle drifts. Only content-based time warping (DTW) fixes that, and it isn't built here.
- **Curve count is not motion.** Test each keyframe curve's value range, and run a known-moving control alongside.
- **Landmark coordinate conventions.** MediaPipe's world landmarks are y-down. Without negating y, the hand came out mirrored, fingertips folding to the back of the hand.
- **Estimator depth can be wrong.** The 3-D estimator's camera depth was unusable (both hands about a metre apart in depth), so placement came from the 2-D projection. Flattening both hands to one depth then made fingers pass through each other. Separate the hands in depth per sign until the surface gap is right.
- **Match the app's scale and look offline.** The figure draws joints as fixed-radius spheres, so how plump a hand looks depends on the trajectory's scale. Recorded data at the wrong scale looked skeletal next to authored signs. Offline renders must use the app's scale, finger thickness and lighting, or the comparison judges the renderer.
- **Rotation in recordings.** `simctl` records the device in portrait, so landscape content comes out rotated, and the direction can change from launch to launch. Default the compare view to portrait, or check the rotation every time.
- **Two Python environments.** The landmark detector and the 3-D hand estimator needed incompatible NumPy versions. Keep them in separate environments, and pin the detector's version.
- **Reference data licences.** The public sign-video and motion-capture sets we found are licensed for non-commercial or research use. Use reference clips for internal testing only. Don't commit them, bundle them in a release, or put them in published comparisons. Publish the generated side alone, or film your own reference.

## What it does not cover

Whether the sign is correct, understandable and natural: handshape detail, movement, facial grammar, and regional or personal variation. That needs a fluent signer reviewing in the app. These tools only make the differences easy to see and count. Two performances can legitimately differ (repetition count in the citation form, tempo), so a difference is a question for the reviewer, not automatically a bug.

## Loading this into Claude

> Generated motion is judged next to its source, never on its own. Before using an asset, run `glb_inspect.py` or the FBX motion probe, and confirm the curves actually change value. Record the app figure with `simctl io recordVideo` (or render the joints offline in the app's scale and style if the simulator wedges). Build the comparison with `synced_compare.py`, aligned on a content event, and compare active window to active window. Report peak joint speed, cycle count and the gap between hand surfaces alongside the video. Reference clips are internal-only and never published. Whether a sign is right is the fluent signer's call. Report what differs and ask.
