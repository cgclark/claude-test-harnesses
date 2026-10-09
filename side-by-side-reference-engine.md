# Side-by-side against a reference engine

> Lets Claude show the same scene in its port and in a stock or reference build, frame for frame, so "matches the original" is a picture and a number instead of a claim.

**Applies to:** engine ports, renderer rewrites, and asset pipelines that have a working reference build (an upstream engine, another platform's port, or the original technique inside your own build). Built for a Quake 3 Metal port compared against an open-source Vulkan/GL engine, and for volumetric effects compared against the sprites they replace · **Needs:** both builds runnable on the same machine (simulator, Mac, or a desktop binary), a way to send console commands to each (see `game-console-driving.md`), `ffmpeg`, `sips` (macOS) or any image converter, `cwebp` optional, Python 3 for the numbers

## Why it exists

Without a reference, Claude judges a port against its memory of what the original looks like, and says it matches. When it does compare, it records two clips separately and puts them next to each other. Those clips are never in sync. In the project this was built for:

- Unsynchronised weapon videos wasted a session. The two engines are driven by different mechanisms on different clocks, so the panels showed different moments, and every difference was mostly timing.
- A "grenade" comparison shipped with a grenade in one panel and a different weapon in the other. A reference window had taken focus, our app paused rendering and wrote no frames, and the script reused the previous run's frames without saying so.
- Portal and mirror rendering was slow in the simulator. Benchmarking the reference on the same simulator first showed it ran at 60 fps where ours ran at 2. That turned "optimise this" into "copy what the reference does", and ours went to 57.
- Our relit maps had to load in a stock engine. Several of the ways a map file breaks in a stock engine fail silently, so "it loads" had to be checked there, not in our renderer.

## What it does

1. Pick fixed viewpoints by coordinates (a `setviewpos`-style command), not by walking or by where the player happened to spawn.
2. Drive each build to the same viewpoints through its own command channel. In each build, the command script takes the screenshot itself, straight after it sets the view.
3. Capture both the same way when you can. Where you can't, normalise rotation and scale per side, explicitly.
4. Assemble one artifact: an `hstack` per view into a short video or a contact sheet, each side marked, plus a number per view (mean luminance, fps, or a diff count).
5. Pass = both panels show the same view and the same event, and the number is inside the tolerance you set before the run. Whether the look is right is still the human's call.

Variants we used:

| Variant | Our side | Reference side | Output |
|---|---|---|---|
| Stills walk | our build in a simulator, launch-time command hook, engine screenshot after each view | reference iOS build in the same simulator, driven over its loopback console bridge, `simctl io screenshot` | 2 fps side-by-side mp4 |
| Asset A/B in a stock engine | not used: the original asset against our modified asset | stock desktop binary run twice in the background, a generated `.cfg`, the modified asset in a mod directory | `sheet.webp` (rows = views) + luminance per view |
| Effect A/B | our renderer, new technique on | the same build with the original technique (sprites) | frame bursts, or video from one replayed demo |
| Animated texture | setting 0 against setting 1 | the same | 16 frames across one full animation cycle per setting |

## Recipe

1. **Fix the viewpoints.** Read each position once in-game (`viewpos` or similar) and keep it in the script as `x y z yaw [pitch]`. Hard-coding beats "wherever the player spawned".
2. **Drive our build** with a command script (see `game-console-driving.md` for the launch hook):
   ```bash
   cmds="devmap <map>;wait 250"
   for y in <y1> <y2> <y3>; do cmds="$cmds;setviewpos <x> $y <z> <yaw>;wait 40;screenshot"; done
   SIMCTL_CHILD_<APP>_AUTODELAY=4 SIMCTL_CHILD_<APP>_AUTOCMD="$cmds" xcrun simctl launch <udid> <our-bundle-id>
   ```
   Poll the screenshots folder until the expected count has arrived, then convert (`sips -s format png in.tga --out out.png`).
3. **Drive the reference.** Use whatever it already has. A console bridge on loopback:
   ```bash
   send() { printf '%s\n' "$1" | nc -w 1 127.0.0.1 <bridge-port>; }
   send "setviewpos <x> <y> <z> <yaw>"; sleep 1.5; xcrun simctl io <udid> screenshot ref_00.png
   ```
   Or, for a stock desktop binary, write a `.cfg` and exec it at launch, in the background, with separate base and home paths:
   ```bash
   SDL_MAC_BACKGROUND_APP=1 ./<engine-binary> +set fs_basepath <base> +set fs_homepath <home> \
     +set fs_game <moddir> +set r_mode -1 +set r_customwidth 1280 +set r_customheight 720 \
     +set com_maxfpsUnfocused 0 +exec ab.cfg
   ```
   with `ab.cfg` = `devmap <map>`, `wait 900`, `cg_draw2D 0`, `cg_drawGun 0`, then per view `setviewpos <v>`, `wait 60`, `setviewpos <v>`, `wait 120`, `screenshot ab_<tag>_<n>`, and finally `quit`. Put the base data in a throwaway base path made of symlinks, and the modified asset in a mod directory, so neither original file is touched.
4. **Assemble.** Mark each side with a coloured border. This needs no font support in `ffmpeg`:
   ```bash
   ffmpeg -framerate 2 -i ours_%02d.png -framerate 2 -i ref_%02d.png -filter_complex \
     "[0:v]pad=iw+16:ih+16:8:8:0x18A558[a];[1:v]pad=iw+16:ih+16:8:8:0xE08A2B[b];[a][b]hstack=inputs=2,format=yuv420p" \
     -r 12 side_by_side.mp4
   ```
   For stills, `hstack` each pair and `vstack` the rows into one sheet, then `cwebp -q 85`.
5. **Add a number.** Mean grey level of each view below the sky line (the lower two thirds), printed as `original A  ours B  (+N%)`. For performance, fps from the same viewpoint in both builds on the same simulator or machine.
6. **Motion.** For an effect that has to be judged moving, record one demo of the event and replay it once per mode with the engine's own fixed-timestep video capture (see `renderer-ab-on-demos.md`, step 10). Before saying an event is missing, work out how many game seconds the capture covered.
7. **Check before reporting.** Open the assembled image and confirm that both panels show the same view and the same event. Then report the numbers.

## Traps

- **Unsynchronised clips compare nothing.** Two engines on two clocks never line up. Step both through identical viewpoints instead, and let the engine's own script take each shot.
- **Externally timed captures drift.** In our engine a `.cfg` `wait N` expired about 3× early, because the command buffer runs about 3 times per frame. Screenshots timed from outside ended up at different positions on the two sides.
- **Focus theft empties a run.** When another window takes focus, our app pauses rendering and writes zero frames. Stamp each run (`touch` a file), convert only screenshots newer than the stamp, and fail loudly on zero frames. Run the reference in the background, and sample the frontmost app during the run (`lsappinfo front`) so the report says whether focus was taken.
- **Different capture paths disagree.** Engine screenshots came out landscape at one size. `simctl io` came out portrait with the game rotated inside it. Rotate only the side that needs it (`transpose=1`), then scale both to the same width. Better still, capture both sides the same way.
- **`timescale` doesn't decouple the command tick.** The launch hook's tick was game time too, so slowing the game slowed the commands by the same factor, and a blast still got about 5 frames. Fire a burst of screenshots and pick frames by eye, or use demo replay plus video.
- **Turn rate is game time.** Set `timescale` before any `+lookdown`, or one tick spins the view to the floor. `setviewpos` without a pitch argument keeps the last run's pitch: send `centerview` first.
- **Saved settings carry between runs.** Latched cvars need a `vid_restart` before the frame counts. Archived ones come back from the config every launch, so set them explicitly in every run (see `game-console-driving.md`).
- **Command-line binaries can't follow links into a sealed app container.** Point a stock binary at its own symlinked base path, not at the app's data folder.
- **HUD on or off is a decision.** Keep the HUD and gun when they are part of what you are comparing (portals). Turn them off for lighting or asset A/Bs.
- **Benchmark the reference first.** Before optimising a slow path, run the reference at the same viewpoint on the same simulator. If it is fast, copy its approach rather than inventing one.

## What it does not cover

The reference is not ground truth for anything it doesn't implement: a different graphics API gives small shading differences that are expected, not bugs. Which side looks better is the human's call. Device-only behaviour (ray tracing, real refresh rates, the headset) needs the target hardware (see `realtime-raytracing-on-mac.md` and `vision-pro-screenshots.md`). Redistributing the reference's assets in the comparison output is a licensing question, not a testing one.

## Loading this into Claude

> Claims that our build "matches the original" are backed by a side-by-side against `<reference build>`, never by memory. Step both builds through the same fixed viewpoints (`setviewpos <x y z yaw pitch>`), and let each build's own command script take the shot right after setting the view. Never sync two separately timed recordings. Capture both sides the same way, or normalise rotation and scale explicitly. Stamp each run, convert only new frames, and fail on zero frames. Run the reference in the background and report whether it took focus. Mark the sides with coloured borders, and add a number per view (luminance below the sky line, or fps). Open the assembled image and check both panels show the same view and event before reporting. Before optimising a slow path, benchmark the reference at the same viewpoint first.
