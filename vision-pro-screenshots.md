# Vision Pro screenshots

> Lets Claude see what a visionOS app actually shows, including immersive spaces and each eye of a stereo render, instead of reasoning from code and marking the result "unverified".

**Applies to:** visionOS apps with windows, RealityKit immersive spaces, or CompositorServices (Metal) immersive spaces (built for a Quake 3 port's visionOS target) · **Needs:** macOS with Xcode and a visionOS simulator runtime, `xcrun simctl`; for a headset, a Vision Pro paired for development and `xcrun devicectl`

## Why it exists

Run while the Simulator is the frontmost app, `xcrun simctl io <udid> screenshot` returns a solid black image for immersive content, byte-identical every time. Claude concluded immersive views could not be captured. It shipped changes as "code-reasoned, unverified", guessed blind for hours, and asked the human to look.

Two more gaps sit behind that one. The simulator presents **one view**, so even a good screenshot says nothing about the second eye: disparity, swapped eyes, and HUD depth conflicts are all invisible. And synthetic host input mostly does not reach a visionOS guest, so Claude could not get the app into the state worth capturing.

## What it does

1. Launch the app straight into the space under test with environment flags. Steer it with a command file the app polls, not with synthetic input.
2. Wait for a log line proving the content has rendered.
3. Bring another macOS app to the front, then `simctl io … screenshot`. Check the PNG is not black, then read it.
4. For stereo, an in-app command writes each eye's finished frame to its own file. Compare the two images region by region.
5. On a headset, use the same in-app capture and pull the files with `devicectl`. Anything only seen through the lenses stays with the human.

**What works where:**

| Capture | visionOS simulator | Vision Pro |
|---|---|---|
| Window / Shared Space screenshot | `simctl io screenshot` | Human-driven system capture (not scripted here) |
| Immersive space (RealityKit or Metal) | `simctl io screenshot` after backgrounding the Simulator; shows the last frame drawn | Human-driven system capture |
| Both eyes as the compositor shows them | Not possible: one view, no disparity | Only by wearing it |
| Each eye as the app rendered it | In-app per-eye capture, files read from the data container | Same capture, pulled with `devicectl device copy from` (*) |
| Motion | The app's own fixed-timestep video capture (see `renderer-ab-on-demos.md`) | Same (*) |
| Logs | `simctl spawn … log stream` | `devicectl device process launch --console` (*) |

(*) Syntax checked against `devicectl` help; not yet run against a headset in the project this was built for.

## Recipe

1. **Resolve the simulator by name, never a hard-coded UDID** (devices get recreated):
   ```bash
   xcrun simctl list devices | grep "<sim name>"
   ```
2. **Build and install.** `simctl install` upgrades in place. Never `simctl uninstall`: it deletes the data container, along with any test data placed there.
   ```bash
   xcodebuild -project <App>.xcodeproj -scheme <scheme> -destination 'platform=visionOS Simulator,name=<sim name>' build
   xcrun simctl install <udid> <path to built .app>
   ```
3. **Launch into the space under test.** Give the app environment flags that open the immersive space, select the mode, and auto-open any screen you want to capture. Gaze-driven menus can't be scripted, so skip them. Simulator env vars need the `SIMCTL_CHILD_` prefix:
   ```bash
   SIMCTL_CHILD_<APP>_<SPACE_FLAG>=1 xcrun simctl launch <udid> <bundle-id>
   ```
4. **Drive state from a file, not from input.** The app polls `<data container>/Documents/<drive file>` a few times a second, runs each line (key taps, menu navigation, console commands), then truncates the file and logs that it ran. See `game-console-driving.md` for the command side.
   ```bash
   C=$(xcrun simctl get_app_container <udid> <bundle-id> data)
   printf '<command>\n' > "$C/Documents/<drive file>"
   ```
5. **Read logs without stealing focus.** Attach a log stream to the running app. Filter on the message text: filtering on the sender image path doesn't match Foundation-routed `NSLog` and returns nothing.
   ```bash
   xcrun simctl spawn <udid> log stream --level debug --style compact \
     --predicate 'eventMessage CONTAINS "<log tag>"' > sim.log 2>&1 &
   ```
6. **Wait for a render marker, then capture from the background.** Poll the log for a line the app prints only once the content is up (a mesh built, N frames drawn). Don't sleep a guessed interval. Then:
   ```bash
   open -a Finder        # any app other than Simulator; not your IDE
   sleep 2
   xcrun simctl io <udid> screenshot --type=png shot.png
   ```
   Check for real content before reading the image: a black capture is about 150 KB, a real one several MB, or check a histogram.
7. **Capture each eye in the app.** The renderer must actually be drawing two eyes: if the app's stereo path is a latched engine switch, set it at launch and restart the renderer before loading content (for example `set <stereo switch> 1; vid_restart; <load map>; <wait>; <capture command>`), using `set`, never the archiving form. With it off, the capture command runs and writes nothing. Add a command that, on the frame each eye finishes, copies that eye's colour texture (or array slice, when amplified) to the CPU and writes `<tag>_L` / `<tag>_R` into the app's data directory. In the simulator, read the files from `get_app_container … data`. Then compare the eyes per region by the horizontal shift that best maps left onto right:
   - near geometry: large shift, in the right direction (near objects sit further left in the right eye);
   - far geometry and reflections: small shift;
   - HUD: a small shift if the app places it at a depth; zero shift means it is still screen-space, a depth conflict worth flagging;
   - a sign flip: swapped eyes.

   In the project this was built for: about 84 px at near pillars and 10–14 px in a mirror's reflection, at 3840×2160 per eye. The HUD measured 0 before it was given a depth; once it was, zero became the warning sign. A HUD region that overlaps a view weapon measures badly (the weapon dominates), so pick a HUD area clear of it. A debug flag that paints the depth sent to the compositor as grey (near white, far black, sky black) checks depth orientation the same way.
8. **On a headset** (marked (*) above):
   ```bash
   xcrun devicectl device install app --device <device> <path to device .app>
   xcrun devicectl device process launch --device <device> --terminate-existing --console \
     -e '{"<APP>_<SPACE_FLAG>":"1"}' <bundle-id>
   xcrun devicectl device copy from --device <device> --domain-type appDataContainer \
     --domain-identifier <bundle-id> --source Documents/<capture dir>/<tag>_L.tga --destination ./out/
   ```
   When a recording is running on the device, the compositor can hand the app a second drawable (visionOS 26). Render every drawable it returns, or the recording won't match what the wearer sees.

## Traps

- **A black immersive screenshot.** The Simulator was frontmost. Background it first. Don't bring an app forward by a name that could launch a second copy of something.
- **The captured frame is stale.** Immersive rendering freezes once the Simulator loses focus, so you capture the last frame it drew. Relaunch, wait for the render marker, then background and capture.
- **Env vars passed as argv.** `simctl launch <udid> <bundle> KEY=VAL` hands `KEY=VAL` to the app as an argument, not an environment variable. Without the `SIMCTL_CHILD_` prefix, the app quietly opened the flat view instead of the stereo space for a long time.
- **A good simulator screenshot is not a stereo check.** The simulator has one view: no disparity, no Metal 4, no framebuffer fetch. Per-eye files prove what the engine rendered for each eye, not the compositor's reprojection, foveation or lens view.
- **Synthetic input doesn't reach the guest.** Host key events mostly don't survive. In one measurement arrow keys arrived and Return did not. Clicks need pointer capture (⌃⌘K, *Send Pointer to Device*), and the gaze highlight only exists while the mouse is moving, so click mid-motion. ⇧⌘K (*Connect Hardware Keyboard*) is one key away and silently disconnects the keyboard.
- **A wedged Simulator lies.** With several devices booted, `simctl list` reported "Booted" while shutdown said "Shutdown", and input stopped arriving. Shut down every device, quit Simulator, and boot only the Vision Pro. Rebooting just the one device didn't help.
- **An orphaned `simctl launch --console-pty` wedges CoreSimulator.** Every later `simctl` call hangs. Kill leftovers before starting. If you must use it, detach with `nohup … < /dev/null &`. It also brings the Simulator to the front.
- **`simctl launch` is not an icon tap.** A bug that needed a real icon launch never reproduced under `simctl`. When the user reports something the tooling can't reproduce, change the tooling.
- **`.full` immersion stopped hardware-keyboard events in the simulator** while the keyboard still showed as attached. An A/B where both arms fail is not a null result: at least one arm must show the behaviour.
- **The simulator's game controller lacks some buttons.** Thumbstick clicks and the centre buttons never arrive, so test those on hardware.
- **`screencapture` needs Screen Recording permission; `simctl io` doesn't.** Use `simctl io` for the simulator.
- **Saved test switches come back.** Reset debug flags at launch, and change live settings through the drive file rather than the saved config, which the app rewrites on exit.

## What it does not cover

Wearing the headset: depth and comfort, lens distortion, reprojection and judder, head and hand tracking, real refresh rate and frame pacing, and how bright or washed-out the image looks through the optics. On-device system screenshots and recordings are human-driven, and this harness doesn't script them. The per-eye files show what the app rendered; whether it looks right in the headset is the human's call.

## Loading this into Claude

> visionOS output is checked from captures, not from code. Launch into the space under test with `SIMCTL_CHILD_` flags. Drive state through the app's drive file, never synthetic input. Wait for the render marker in `simctl spawn … log stream`. Then bring another app forward and run `xcrun simctl io <udid> screenshot`, and check the PNG isn't black before reading it. A simulator screenshot shows one view only: for stereo, use the in-app per-eye capture and compare left/right disparity per region (a HUD at zero shift when it should sit at a depth is a finding, a sign flip means swapped eyes). On a headset, pull the same captures with `devicectl device copy from`. Comfort, tracking and anything seen through the lenses is reported as needing the human in the headset.
