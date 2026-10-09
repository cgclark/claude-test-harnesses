# Real-time ray tracing on the Mac

> Lets Claude check ray-traced rendering (AO, shadows, reflections, motion vectors, temporal accumulation) on a Mac GPU by itself: debug views that show one pipeline stage at a time, plus GPU self-checks that print PASS/FAIL. The iOS and visionOS simulators can't run ray tracing at all.

**Applies to:** Metal renderers that use ray tracing from render or compute, with temporal or denoise passes (built for a Quake 3 Metal port that runs as an iPad app on macOS) · **Needs:** an Apple silicon Mac whose GPU supports ray tracing (M3 or later for hardware-RT cost figures), Xcode command-line tools, the app runnable on the Mac (native, Catalyst, or Designed for iPad), a scriptable console or command hook. Optional: `gpucapture` / `gpudebug` (Xcode 27 command-line GPU tools)

## Why it exists

The simulator GPU has no ray tracing, so RT code never runs there. Claude's default is to test in the simulator, see a clean image and report the bug fixed. A bug that only happens with RT on comes back clean in every simulator repro, and that proves nothing. Worse, a runtime-compiled RT shader library is never compiled in the simulator. A syntax error in it doesn't break the build. It only prints a warning on real hardware and quietly falls back to raster.

On the Mac, the default failure is different: one screenshot of the final image, and a guess about what went wrong. Final pixels mix every stage. In the project this was built for:

- A sky pass rebuilt the shared view-projection after the world drew. Every post-scene pass then reconstructed world positions about 2,400 units off, so 100% of AO rays missed. The motion vectors were wrong too, and nobody had ever looked at them.
- Deferred AO went solid black after a renderer restart. The cause was NaN in reallocated history textures.
- Five "fixed" claims were false. Each was based on numbers, without a matched visible before/after under the user's own saved settings.

## What it does

1. Build and install the Mac app, then confirm the running binary by a compile stamp.
2. Launch it with a scripted command list (see `game-console-driving.md`), and read a per-map status line that proves RT is actually tracing.
3. Turn on one debug view at a time, each showing a single stage (raw AO, temporal output, normals/depth, motion, one shading term). Grab the window (see `renderer-ab-on-demos.md`) and read the image.
4. Run GPU self-check commands. They run the shipping RT code over known geometry and print counts and PASS/FAIL to the console log.
5. Measure cost: GPU ms per frame including acceleration-structure builds, a CPU `sample` profile, and a per-draw GPU profile.
6. Pass = the status line shows tracing on, each stage's view is correct, the self-checks pass, and there are no GPU errors in the log, all under the user's real saved settings.

## Recipe

1. **Run on the Mac, never the simulator, for anything RT.** For an iPad app on Apple silicon, see `designed-for-ipad-on-mac.md` for building, installing and launching from the shell. Log a compile stamp (`__DATE__ " " __TIME__`) at startup and check it on every run. A reinstalled stale copy looks fresh by file date.

2. **Print a status line on every map load** that says what is really running, for example:
   ```text
   RTR: [built <date> <time>] requested=1 tracing=1 tlas=scene instances=29 ...
   ```
   `requested=1 tracing=0` means the RT library failed to build and you are looking at raster. In the project this was built for, one shader variant missing a parameter caused exactly that.

3. **Compile the RT shaders offline.** If the engine builds RT shaders from string literals at runtime, a script can pull those literals out in the same order the engine joins them, and run the real compiler:
   ```bash
   xcrun -sdk macosx metal -std=metal3.0 -c <assembled>.metal -o /dev/null
   ```
   Exit status gates a commit. RT-from-render pipelines can also fail at pipeline creation rather than at compile, so a small harness that calls `newRenderPipelineStateWithDescriptor:` for each RT fragment shader catches the rest.

4. **Build a debug view for each stage, and split the pipeline with them.** The switches used in the project this was built for:

   | Switch | Shows | Splits |
   |---|---|---|
   | AO debug overlay (cheat-gated) | the AO term alone, full screen | AO from everything else |
   | "show raw" (`r_rtAOShowRaw`-style) | the AO before the temporal pass | reconstruction/tracing from temporal |
   | normal/depth viz | reconstructed normals, or depth | the inputs the AO rays start from |
   | temporal feedback = 0 | current frame only, history ignored | history from the current frame |
   | single shading term 1..5 | AO, lightmap, sun, dynamic light, albedo alone | which term goes dark or bright |
   | motion viz | motion vectors as red/green | camera motion from per-object motion |

   Method: find the first stage whose output is wrong while its input is right. The NaN bug fell to two switches. Raw AO was correct after the restart while the temporal output was black, so the fault was in the temporal pass. With feedback 0 the output was still black. That should be impossible if the blend really dropped history, and it pointed straight at `NaN * 0 == NaN`. When a single shading term is available, reach for it first: it answers "which term" directly instead of by elimination.

5. **Use one-shot CPU prints for matrix bugs.** Print `VP * inverse(VP)` (should be identity), the eye position, and `unproject(screen centre, near depth)`. The unprojected point should sit about one near-clip distance from the eye. Before the sky fix it sat near the world origin. This beat a long series of visual debug views.

6. **Write exact GPU self-checks** that run the shipping RT helper source as a compute kernel and compare against ground truth with atomic counters. Example (`rtcuttest`, for alpha-tested cut-outs): for each alpha-tested world triangle, fire 64 rays across its plane on a barycentric grid. "Hit this triangle" must equal "the texel here is solid". Ignore rays stopped by another triangle, since a coplanar twin says nothing about the alpha test. Print the counts and PASS when fewer than 1% of eligible rays disagree:
   ```text
   rtcuttest: <n> tris (cut-out geometry), <r> rays: hit the cut-out .., solid texels .., agree .. | unobstructed .., disagree .. -> PASS
   ```
   With cut-outs off (geometry built opaque), agreement drops to the solid fraction. That is the "before" picture, and it proves the check can fail. Other checks of the same kind: a toy BLAS/TLAS with a floor under an occluder (AO about 0.25 and sun 0.5 under it, 1.0 and 1.0 in the open), and a command that draws the same batches through two encoder models and pixel-diffs them.

7. **Measure cost with a GPU stat command.** Average over displayed frames, not command buffers: a stereo frame commits two. Count acceleration-structure builds separately, because they run on their own command buffers and the frame time never sees them:
   ```text
   gpustat: <n> frames, GPU <ms>/frame (frame <ms> + side passes <ms>) [<k> command buffers]
   gpustat TLAS instances: <avg>
   gpustat AS: TLAS <n> builds <ms>/frame (... refit, ... rebuilt) | BLAS <n> blocking builds <ms>/frame
   ```
   Call it twice around a timed window. Then cut the cost down by switching features off one at a time. In the project this was built for: raster 85 fps, RT with AO and reflections off 62, AO on 44, both on 13. Reflections were the biggest single cost.

8. **Profile CPU and GPU from the shell.** Measure a Release build. For the CPU side:
   ```bash
   sample <pid> 8 -file <out>.txt      # then list the heaviest callees under the render entry point
   ```
   That found a per-entity linear name scan costing 20% of scene rendering, which no GPU feature would fix. For a per-draw GPU profile, launch with `MTL_CAPTURE_ENABLED=1`, then:
   ```bash
   gpucapture list
   gpucapture start -p <pid> -o <out>.gputrace -c 1
   printf 'profile run --exec serial --embed\nwait\n' | gpudebug -t <out>.gputrace --oneshot -q
   printf 'profile load\nwait\ngo performance\ninfo timeline\ngo commands\nlist 0-24\n' | gpudebug -t <out>.gputrace --oneshot -q
   ```
   The per-draw table only fills in the second session, which loads the embedded profile.

9. **Report GPU faults.** Create command buffers with encoder execution status error options, label every encoder with its file:line, and print command-buffer errors from the completion handler on the next main-thread tick. Without this, a faulted frame just comes back black and stays black.

10. **Gate debug views before shipping.** Make every debug view cheat-gated or unsaved, reset it at launch from one central list, and enforce both with a build-time check script (the same rule as in `renderer-ab-on-demos.md`). Strip test-only launch hooks before distribution.

## Traps

- **A clean simulator run proves nothing for RT.** RT code does not run there. The simulator SDK also lacks Metal 4 types and some argument-buffer tiers, so guard that code with `#if !TARGET_OS_SIMULATOR` and test it on the Mac.
- **Headless runs load the user's saved settings.** A fix verified under other settings is not verified. Read the live values back, and give the before/after the same settings.
- **A debug view can show a different buffer from the one applied.** The AO overlay showed the pre-blur buffer while lighting used the spatially blurred one. It looked clean while the applied AO was not. Make each view show exactly what the next stage consumes.
- **A debug view routed through the stage under test blames the wrong stage.** A depth view that passed through the temporal pass made depth look broken when it was fine.
- **Same-frame sub-renders overwrite globals that post-scene passes read.** Sky, portals, mirrors, HUD 3-D icons and model previews all rebuild view matrices or entity lists. In one case the motion pass ran after the HUD icons and saw 1 entity instead of 42. Snapshot the main view's state when it draws, and don't let sub-renders publish over it.
- **Reallocated history textures can hold NaN.** `mix(cur, hist, 0)` is still NaN when `hist` is NaN, and the bad value then persists frame to frame. Sanitise history (`isfinite` → fall back to current, clamp to the valid range). A "history valid" flag alone did not fix it.
- **RT lighting multiplied into self-lit surfaces turns them black.** AO × sun on environment-mapped or emissive surfaces (pickups inside a dark room) hid their colour. Carry the material type to the shader, and skip AO and sun for those surfaces.
- **The obvious reflection savings did nothing.** Skipping low-fresnel pixels and shortening rays both gained about 0 fps. The cost was the closest-hit intersector plus hit shading. Measure before assuming; the fix is structural (half-res trace, or only reflective-flagged surfaces).
- **GPU use-after-free.** A command buffer keeps alive what it binds, not what a TLAS reaches by address. Freeing entity BLASes or world buffers while frames were in flight page-faulted, and every later frame was black. Wait for the last frame before freeing.
- **fps pinned at the refresh rate** means the window sits on a 60 Hz display. Compare GPU ms instead.
- **GPU traces are large** (about 1 GB for one RT frame). Simulators are never capturable. Delete traces when done.

## What it does not cover

The target device's GPU, thermals and frame pacing: the Mac's RT hardware is not the headset's or the phone's, and costs only transfer roughly. Whether a visible change is better or worse stays the human's call, as do stereo comfort and anything seen through a headset (see `vision-pro-screenshots.md`).

## Loading this into Claude

> Ray-traced rendering is tested on the Mac build, never in the simulator: the simulator can't ray trace and every RT repro comes back clean there. Before judging an image, check the status line says tracing=1 and the compile stamp matches the build. Debug by stage: turn on one debug view at a time (raw, temporal, normals/depth, single shading term, motion) and find the first stage whose output is wrong. Use one-shot CPU prints for matrix bugs. Run the GPU self-check commands and read their PASS/FAIL lines. Measure cost with the GPU stat command (acceleration-structure builds included) on a Release build, and switch features off one at a time to see where the time goes. No "fixed" without a matched visible before/after under the user's saved settings. Debug switches are cheat-gated or unsaved and reset at launch.
