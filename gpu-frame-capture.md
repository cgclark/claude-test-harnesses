# GPU frame capture

> Lets Claude capture one frame of a running Metal app from the shell and read the GPU cost of each draw call, instead of guessing which pass is slow from the total frame time.

**Applies to:** Metal apps that run natively on the Mac (including iPad apps running on a Mac) (built for a Quake 3 Metal port with ray tracing) · **Needs:** macOS 27 / Xcode 27 command-line GPU tools (`gpucapture`, `gpudebug`), an Apple silicon Mac, a few GB of free disk space

## Why it exists

Frame totals (a GPU stat command, `metalperftrace`) say how slow a frame is, not where the time goes. Without a per-draw view, Claude switches features off one at a time and infers. That works for big switches but can't see a single expensive draw. Xcode's GPU capture shows the breakdown, but it needs a person at the Xcode UI. The command-line tools do the same thing headless. Origin: a standard tool Claude recommended. We wrapped it in one script.

## What it does

1. Launch the app with `MTL_CAPTURE_ENABLED=1`, driven to the view under test by a command script (see `game-console-driving.md`).
2. After a fixed delay, find the app's process id in `gpucapture list`, and capture exactly one frame to a `.gputrace` outside the app's container.
3. Replay it once to collect an embedded profile, then again in a fresh session to print the timeline and the most expensive draws.

## Recipe

The commands are in `realtime-raytracing-on-mac.md`, recipe step 8. The wrapper adds a delay and a process lookup:

```bash
EXTRA_ENV="MTL_CAPTURE_ENABLED=1" CMDS="<map load>;wait;...;<setviewpos ...>" <run script> &
sleep <AT>                                    # long enough for the load and the view to settle
pid=$(gpucapture list | awk '$3 == "<process name>" { print $1; exit }')
gpucapture start -p "$pid" -o <out>.gputrace -c 1
printf 'profile run --exec serial --embed\nwait\n' | gpudebug -t <out>.gputrace --oneshot -q
printf 'profile load\nwait\nstatus\ngo performance\ninfo timeline\ngo commands\nlist 0-24\n' \
  | gpudebug -t <out>.gputrace --oneshot -q | grep -E '^Summary:|^draw[0-9]|Name  *Shaders'
```

Label every encoder and pipeline in the app (file and pass name), or the draw list is anonymous.

## Traps

- **No `MTL_CAPTURE_ENABLED=1`, no process.** `gpucapture list` shows nothing capturable without it.
- **Simulators are never capturable.** The device list is this Mac only. Run the Mac build.
- **The per-draw table is empty in the session that collects the profile.** Load the embedded profile in a second session.
- **Traces are big.** One ray-traced frame was about 1.1 GB. Delete traces when done.
- **A sealed container doesn't matter**, because `-o` writes the trace on the host. Still check that the installed app matches the build you just made (see `renderer-ab-on-demos.md`, "Stale binary").
- **Capture a Release build** for cost figures. Debug builds move the hot spots.

## What it does not cover

The target device's GPU: Mac draw costs only roughly transfer to a phone or headset. A capture is one frame, so stutter and frame pacing need a timed run. The `grep` patterns match the output of `gpudebug` 1.0. The `gpucapture` flags above were checked against its help text, but the capture wasn't rerun when this note was written, so recheck the patterns if the tools change.

## Loading this into Claude

> To find which pass or draw is slow, capture one frame with `<gpu-profile script> <out>.gputrace` (launches with `MTL_CAPTURE_ENABLED=1`, captures one frame, prints the most expensive draws). Use a Release build on the Mac, never the simulator. Delete the trace afterwards.
