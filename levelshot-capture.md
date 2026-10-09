# Levelshot capture

> Lets Claude re-shoot every map's loading-screen image (levelshot) unattended, from the camera the map itself defines or, when it defines none, the camera that best matches the original author's own image, and refuse to ship any shot taken without the renderer state it was meant to show.

**Applies to:** games with per-level thumbnails or loading screens that need re-capturing after a renderer upgrade, where levels carry camera entities and some ship an author-made image (built for a Quake 3 Metal port: stock and add-on maps, iPad and headset targets) · **Needs:** the engine's command channel and console log (see `game-console-driving.md`), level files you can parse (here BSP entity and brush lumps inside `.pk3` zips), Python 3 with Pillow and NumPy (in a venv if the system Python refuses installs), the hardware the target renderer needs (ray tracing ran only on the Mac)

## Why it exists

Asked for new levelshots, Claude's default is to load each map, stand wherever the player spawns, and take a screenshot. Spawn points mostly face a wall. Nothing then checks what renderer state the shot was taken under, and the batch run leaves its settings in the player's config. Each of these happened at least once in the project this was built for:

- A run of force-quits shrank the app window, the render size followed it, and a whole batch came out at the wrong resolution. Nothing stopped it.
- A capture's renderer settings stayed in the player's saved config. MSAA went from 1× to 4×. Later runs also left the crosshair off, the HUD hidden and a different player model.
- Large maps came back pure black at the default waits. The world, or its ray-tracing structures, wasn't ready when the shot fired.
- One map's own camera sat inside a door's bounds. The shot was black or fine depending on where the door happened to be.
- A mouse touched during the settle wait turned the view, and the shot came from the wrong angle.
- Shots were downscaled for packing and then upscaled by the loading screen: on the headset, 1024 px back up to 3840.
- A matcher run generated one big script and `exec`'d it. It overflowed the engine's 128 KB command buffer and sat at the menu for 7 minutes, having run nothing.

## What it does

1. **Cameras from the data.** Parse each level's entities. The camera is the end-of-match intermission point aimed at its target, the same rule the game uses. With no intermission point, fall back to the first spawn point, level, and log that it did. Store the result as a table: `{map: [[x,y,z],[yaw,pitch]]}`.
2. **Match the author when the level has no camera.** Generate candidate cameras in open space, render them all in one engine session, and score each against the author's shipped image. Then build a contact sheet of the author's image and the top 11 candidates, so a human picks one.
3. **Capture.** Generate one script that pins the render size, sets and echoes the renderer state once a world is loaded, then for each map loads it, hides the HUD, poses the camera, waits, poses again, and takes the shot.
4. **Guard settings.** Snapshot every saved setting before the run and restore them after, from outside the engine, with the app closed.
5. **Gate on evidence.** Read the console log back. If the hardware line or any required setting is wrong, refuse to pack the shots.
6. **Pack.** Crop to each target's aspect without resampling, average supersampled pixels down, check sizes and orientation, keep lossless masters, and write a contact sheet of every shot.

## Recipe

1. **Extract cameras**, and keep the table in the repo:
   ```bash
   python3 extract-cameras.py <pak-or-dir> ...           # print {map: camera}
   python3 extract-cameras.py --merge <pak-or-dir> ...   # add missing maps to the table
   python3 extract-cameras.py --check <pak-or-dir> ...   # compare, change nothing
   ```
   Generate a human-readable camera list from the table, with a reproducible `setviewpos x y z yaw pitch` line per map. Make `--check` exit 1 if any level no longer agrees with the table.
2. **Match levels without a camera** to the author's image:
   ```bash
   python3 match-vantage.py search --pitches=-20,0,15 <map>   # candidates, renders, ranked sheet
   python3 match-vantage.py refine <map> <x> <y> <z> <yaw> <pitch>   # jitter around a pick
   python3 match-vantage.py accept <map> <x> <y> <z> <yaw> <pitch> "<what the view shows>"
   python3 match-vantage.py rank <map>                        # re-score without the engine
   ```
   - Candidates come from spawn and target points (raised until they're clear of solid brushes, 8 yaws, a line-of-sight check) plus a grid over the spawn-point bounds, de-duplicated.
   - Each render is shrunk to a 512 px JPEG as it lands. A full TGA was 22 MB.
   - Score = 0.5 × SSIM on a blurred 64×64 + 0.3 × edge correlation + 0.2 × colour-histogram overlap. Renders that are almost black (mean below 0.02) are dropped.
   - Author stamps (title banners, inset pictures, URLs) are masked by pasting the candidate's own pixels into those regions of the author's image.
   - Read the sheet, pick by eye, and record each override with its reason. Record a deliberate decision to keep a map's own camera too, or someone will redo it.
3. **Generate the capture script and run it:**
   ```bash
   python3 config-guard.py snapshot
   python3 make-capture-cfg.py --quit --width <W> --height <H> --ss 2 > <game data>/lscap.cfg
   CMDS="exec lscap" WAIT=1500 <run script>
   python3 config-guard.py restore
   ```
   Per map, the script runs `devmap <map>`, `wait 240`, HUD and gun off, `noclip`, `setviewpos …`, `wait 120`, `setviewpos …` again 3 frames before the shot, `screenshot LS_<map>`, `wait 60`. The preamble echoes every required setting after the first map has loaded. `--wait-scale 2.5` is for the maps that come back black.
4. **Finish:** gate, then pack.
   ```bash
   finish-capture.sh          # prints the evidence, then packs; refuses on any mismatch unless FORCE=1
   # two targets from two passes, packed directly:
   python3 pack-levelshots.py <4:3 grabs> --src-spatial <16:9 grabs> --ss 2 --contact-sheet sheet.jpg
   ```
   The gate requires the log's hardware line (here `Apple9(HW)=YES`), each required setting at its value, a "capture complete" line, and the expected number of grabs. Read the contact sheet before calling the batch done.

## Traps

- **Echo settings only after a world loads.** Some renderer settings aren't registered until a map is up. An echo before that proves nothing.
- **The log may only flush on quit.** Without `--quit`, the evidence gate has nothing to read. A missing log is a warning (the grabs still pack), and the report must say that the renderer state wasn't verified.
- **Pin the render size.** It follows the window, and the window follows whatever state force-quits left it in. Pin it in the script, unpin it at the end, and make the packer refuse grabs below the minimum height.
- **A closing `seta` doesn't restore latched settings.** They write their current value on quit. Restore from outside the engine, with the app closed, and restore every saved line, not just the ones you expected to change.
- **Re-pose right before the shot.** The run happens in a live app, and a touched mouse turns the view during the wait.
- **Black shots.** Big maps need longer waits, and a camera inside a moving brush's bounds is black some of the time. Check the mean brightness of each shot before packing. Some maps really are that dark: don't "fix" those.
- **Never resample twice.** Crop the grab to each aspect and ship its own pixels. If the field of view is horizontal and the vertical FOV is derived from the viewport, a 16:9 frame is exactly the centre band of a 4:3 frame. But cropping 16:9 out of a 4:3 grab loses height, so take a second pass at 16:9 when that height matters.
- **Texture caps can shrink bigger images.** An engine-wide maximum texture size box-halved any levelshot over the cap, so a bigger file showed up smaller. Exempt the levelshot from the cap and log the exemption.
- **Big scripts silently run nothing.** `exec` puts the whole file into a fixed-size command buffer. Split it into files under about 48 KB, each ending with `exec <next>`.
- **The scoring ranks; it doesn't decide.** Styled author images (scanlines, vignettes, logos, posterised colour) fool it. When the author's image is a logo rather than a view, keep the map's own camera.
- **Keep the masters.** The packed files are lossy. Write each grab losslessly, one file per map, named after the map, so a re-encode doesn't need a recapture.
- **Orientation.** Engine grabs have come out rotated. Detect portrait grabs and rotate them, and print that you did.

## What it does not cover

Whether a matched camera is "the author's view": the score narrows the search, a person picks. How the image looks on the target displays, especially through a headset (see `vision-pro-screenshots.md`). Licensing of third-party levels and their shipped images, which decides what can be redistributed. Platforms without the renderer feature being captured, which need their own pass.

## Loading this into Claude

> Level thumbnails are captured by the levelshot harness, never by standing at a spawn point. Cameras come from the level data (the intermission point aimed at its target). For levels without one, run `match-vantage.py search`, read the ranked sheet, and `accept` a pick with a reason. Every capture runs between `config-guard.py snapshot` and `restore`, pins the render size, re-poses right before each shot, and ends with `quit`. Run `finish-capture.sh` and treat its refusal as a failed capture. Never pass FORCE=1 without saying why. Ship the grabs' own pixels, cropped, never resampled twice. Open the contact sheet before reporting the batch done.
