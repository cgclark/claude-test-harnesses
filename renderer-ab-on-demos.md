# Renderer A/B on a frozen demo

> Lets Claude prove that a renderer change does (or does not) change the picture, by diffing window grabs of the same frozen demo frame under each setting, with a same-setting control to separate real differences from noise.

**Applies to:** game engines and renderers with demo/replay playback and a scriptable console (built for a Quake 3 Metal port running as an iPad app on macOS) · **Needs:** macOS, `screencapture` with Screen Recording granted to the terminal/agent, `swiftc` (for a window-id helper and an image differ), `cwebp` optional, a recorded demo, a way to feed console commands at launch

## Why it exists

Without it, Claude tests a renderer change by loading an empty map, taking one screenshot, and saying it looks right. An empty map has no players, projectiles, effects or HUD changes, which is exactly where pass-ordering and barrier bugs show. A HUD flicker in a barrier-less mode was invisible on an empty map and obvious on a demo. Separately, "before" and "after" screenshots from two runs always differ (animation, effect randomness, console text), so a raw diff can't tell a regression from noise, and Claude would either call everything a change or wave everything through.

## What it does

1. Launch the installed build with a scripted command list: set a fixed aspect ratio, play a demo, freeze it at a chosen moment.
2. For each config (`name:console commands`), reset all test switches, apply the config, let it settle, and grab the game window 3 times from outside the app.
3. Diff consecutive grabs within one config: a frozen frame must not change, so any difference is flicker.
4. Diff each config against the first config: that is the A/B result.
5. Pull the engine console from the system log and grep it for GPU errors and config markers.
6. Pass = A/B diff no larger than the control diff (or the expected change only), zero flicker, no GPU errors in the log.

## Recipe

1. **Make the console reachable.** Mirror the engine's print function to `os_log` under a subsystem you own (behind an env var such as `<APP>_OSLOG=1`), so the console survives a sealed app container. Read it with:
   ```bash
   /usr/bin/log show --start "$START" --predicate 'subsystem == "<your.subsystem>"' --style compact \
     | sed -E 's/^.*<your.subsystem>:console\] //' > console.log
   ```
2. **Feed commands at launch.** An env var holding a `;`-separated command list that the app runs on a timer (one command per tick) is the most reliable path; launch arguments and autoexec files were lost to the UI boot. On macOS, scope env vars to one launch:
   ```bash
   open -g "<installed .app path>" --env "<APP>_AUTOCMD=$CMDS" --env "<APP>_OSLOG=1" \
     --args -ApplePersistenceIgnoreState YES
   ```
3. **Freeze deterministically.** Add two engine switches: freeze demo time at an exact millisecond, and step the demo at a fixed frame time (16 ms). Then the frozen frame, random effects included, is pixel-identical across launches and across builds. Without the fixed step, a freeze is only comparable within one launch.
4. **Fix the aspect ratio** to the shipping target (16:9 here, set via a latched cvar and a `vid_restart` at the start), not whatever the dev window happens to be.
5. **Build the command list** (pseudocode of the real script):
   ```text
   pushcvar <every saved setting that would change the measurement> ; pushcvar r_widescreen 1 ; vid_restart ; wait x4
   fixedStep 16 ; freezeDemoAt <ms> ; demo <name> ; wait xN
   for each config:  testreset ; echo CFG_<name> ; <config cmds> ; wait x8
   unfreeze ; popcvar ; quit
   ```
6. **Grab from outside the app.** Find the game's largest on-screen window id with a small Swift tool over `CGWindowListCopyWindowInfo` (filter by owner name, height > 400), then:
   ```bash
   screencapture -x -o -l "$(<winid-tool>)" "$OUT/<config>-<n>.png"
   cwebp -quiet -q 85 in.png -o out.webp      # optional: WebP for sharing
   ```
   Wait for each config's `CFG_<name>` marker to appear in the log, sleep ~7 s for temporal effects to settle, then take 3 grabs 0.3 s apart.
7. **Diff.** A ~20-line Swift tool with ImageIO/CoreGraphics that prints differing-pixel count, count over a threshold (>8), max channel delta, and writes an amplified diff PNG. Read the numbers, then Read the diff image.
   ```bash
   <imgdiff> a.png b.png diff.png
   # pixels 10223616 differing 0 (0.0000%) >8: 0 maxDelta 0
   ```
8. **Cross-build A/B.** Check out the old commit in a separate worktree, build it into its own derived-data path, install it, and run the same script with a different `OUTDIR`; compare frame for frame. Only overlay digits (an fps counter) should differ.
9. **Timing mode.** The same configs can run a timedemo each with vsync off; grep the log for the fps lines. Run on the internal high-refresh display.
10. **Motion.** For effects that must be judged moving, record one demo of the event and replay it once per render mode with the engine's own video capture, then split the AVI into frames with `ffmpeg`. Identical gameplay per clip, so clips differ only by the renderer.

## Traps

- **No control, no conclusion.** Compare "off vs on" to "on vs on" (same setting, a few seconds later), never to zero. Animation and console text always differ.
- **Plain timed freezes are not comparable across launches.** Only the exact-millisecond freeze with a fixed step is. Without it, compare within one launch only.
- **Test switches that get saved come back every launch** and look like new bugs (a saved anaglyph mode doubled every frame for later runs). Never register a test switch as archived; reset every test switch at launch from a central list; enforce both with a build-time check script. A harness that touches a saved setting must `pushcvar`/`popcvar` it, or snapshot and restore the config file.
- **Stale binary.** Reinstalling an iOS-on-Mac app adds `App 2.app`, `App 3.app`; launching by bundle id let LaunchServices pick a five-hour-old copy and a whole session judged code that wasn't running. Launch by path, after checking that the installed binary's hash matches the build output.
- **A hidden window renders nothing.** Screensaver, display sleep, or another app taking focus pauses rendering and yields empty or stale grabs. Wrap the run in `caffeinate -d -i -u -t 1800`, launch with `open -g`, and make the engine keep rendering when unfocused.
- **"Reopen windows?" modal after a crash** hangs the launch at 0% CPU with no log. Always pass `--args -ApplePersistenceIgnoreState YES`.
- **The app container is sealed** (macOS 27): no other process can read the engine's own screenshots or config. Grab the window and read `os_log` instead.
- **Command pacing.** Each `;`-separated command fires one tick (1.5 s here) after the last, so `wait` is a delay unit, and the console log may only flush on `quit`. Count the waits.
- **fps pinned at a refresh interval** (59.8 fps) means the window was on a 60 Hz external display: the result measures the display, not the renderer.
- **Video coverage.** Recorded video advances a fixed 1/framerate of game time per frame, multiplied by `timescale`. Work out how many game seconds a capture covers before saying an event isn't in the demo. One was at frame 549 of 685 and was reported missing twice.
- **Reused frames.** A video script that converts "the newest" files silently reused the previous run's frames, producing an A/B whose two panels showed different weapons. Stamp each run and convert only newer files; check that both panels show the same event.
- **zsh's `log` is a builtin.** Ad-hoc commands must call `/usr/bin/log show`.
- **Multiple build targets.** If the renderer also ships to other platforms, the A/B passing on the Mac doesn't mean the other targets compile. Build all of them before calling it done.

## What it does not cover

The headset or device itself: real display, refresh pacing, thermal behaviour, two-eye stereo comfort, and anything only the real GPU does (the simulator and the Mac differ in feature tiers). Whether a visible difference is better or worse is still the human's call; the harness only proves where and how much the image changed.

## Loading this into Claude

> Renderer changes are tested with the demo A/B harness (`<path to demo-ab script>`), never on an empty map and never by eye from one screenshot. Run at the shipping aspect ratio on a frozen demo; read the flicker lines (must be 0) and the A/B diff next to a same-setting control before calling a difference real; read the amplified diff image. Use the exact-millisecond freeze for cross-build comparisons. Debug and test switches are never archived and are reset at launch; any saved setting a run touches is pushed and popped. Launch the installed copy by path after checking its hash matches the build.
