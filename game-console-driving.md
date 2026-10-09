# Game console driving

> Lets Claude run commands in a game engine's in-game console and read the results back as text, without typing into the game window.

**Applies to:** game engines with a developer console and a command buffer (built for Quake 3 ports on iOS, iPadOS-on-Mac and visionOS) · **Needs:** the engine source (to add a launch hook and a log mirror), a simulator or a launcher that passes environment variables (`xcrun simctl`, `open --env`, `xcrun devicectl`), Bash

## Why it exists

A game's console is often the best test surface it has: one line sets a debug switch, loads a map, takes a screenshot, prints internal state. By default Claude drives it the way a person does. It focuses the window, opens the console with the backtick key, and types through computer-use, then reads the result off a screenshot. That failed in every way we tried:

- Synthetic keystrokes are lossy. About 10 characters sent, about 5 arrived, and not as a clean prefix. The loss was in the OS and simulator key path, not in console code.
- The Claude window took keyboard focus back, so keystrokes went to the wrong app. A stray keystroke once landed in an open Xcode editor and broke a source file.
- Paste doesn't work. `cmd+V` arrives as a bare `v`, and the engine's own paste key (Shift+Insert) can't be sent.
- A phantom key event put a leading `a` on the first command after every launch (`/devmap` became `/adevmap`).
- The simulator only forwards host keys when its `ConnectHardwareKeyboard` default is true. It was unset, so every keyboard test in the simulator had silently tested nothing.
- With a map running, bare console text went to chat instead of the command parser (see Traps). The setting didn't change and nothing reported an error.

We worked this out from scratch at least three times, losing hours each time. The fix was to stop typing: give the engine a scripted command channel and a log Claude can read.

## What it does

1. Claude writes a `;`-separated command script, for example `devmap <map>;wait;screenshot;quit`.
2. The launcher passes it to the app in an environment variable. The app feeds each command into the engine's command buffer on a timer, the same path a typed command takes after Return.
3. The engine's console output goes somewhere Claude can read from Bash: captured stdout, a log file, or the system log.
4. Claude greps the log for the lines the commands print, and reads any screenshot the script took.
5. The run ends with `quit`, so the log is complete and no test state is left on screen.

## Recipe

1. **Add a launch-time command hook.** In the app, after the engine has booted, read an env var and queue each command on a timer:
   ```swift
   // Fires only when <APP>_AUTODELAY is set, so a normal launch never runs it.
   if let s = env["<APP>_AUTODELAY"], let delay = Double(s) {
       let script = env["<APP>_AUTOCMD"] ?? ""
       for (i, cmd) in script.split(separator: ";").enumerated() {
           DispatchQueue.main.asyncAfter(deadline: .now() + delay + Double(i) * 1.5) {
               Cbuf_AddText("\(cmd)\n")   // the engine's command buffer
           }
       }
   }
   ```
   The command buffer can't drop characters and doesn't need window focus. Launch arguments (`+devmap <map>`) and `autoexec.cfg` both failed here, because the UI layer took over the boot and the command was lost. The env-var hook worked.

2. **Launch with the script, scoped to that one launch.**
   ```bash
   # Simulator: env vars need the SIMCTL_CHILD_ prefix; --console-pty captures engine stdout
   SIMCTL_CHILD_<APP>_AUTODELAY=4 SIMCTL_CHILD_<APP>_AUTOCMD="$CMDS" \
     xcrun simctl launch --console-pty <udid> <bundle-id> > run.log 2>&1 &

   # macOS: --env scopes variables to this launch (launchctl setenv leaks into every later app)
   open -g "<installed .app path>" --env "<APP>_AUTODELAY=4" --env "<APP>_AUTOCMD=$CMDS" \
     --args -ApplePersistenceIgnoreState YES

   # Device: --terminate-existing, or the env vars are ignored
   xcrun devicectl device process launch --device <device-id> --terminate-existing \
     --environment-variables '{"<APP>_AUTODELAY":"4","<APP>_AUTOCMD":"..."}' <bundle-id>
   ```
   Wrap it in one script that builds, installs, launches with `CMDS`, sleeps long enough for the boot plus each command, then screenshots and prints the log tail. The call becomes `CMDS="toggleconsole;quit" ./run-sim.sh`.

3. **Make the console readable.** Use whichever of these the platform allows:
   - **stdout:** `simctl launch --console-pty` captures the engine's print output. The engine's own prints don't reach the unified log, so `log stream` misses them.
   - **log file:** `seta logfile "2"` writes `qconsole.log` in the game's home directory. `1` buffers and `2` flushes after each print. Read the file with Bash after the run.
   - **system log:** if the app container is sealed (macOS 27 seals it from every other process), mirror the engine's print function to `os_log` behind an env var, and pull the run's lines afterwards:
     ```bash
     /usr/bin/log show --start "$START" --predicate 'subsystem == "<your.subsystem>"' --style compact \
       | sed -E 's/^.*<your.subsystem>:console\] //' > console.log
     ```
   Have the engine print what you need to check, such as matrices, counters or a build stamp, rather than reading it off a screenshot. One CPU log line of a matrix settled a bug faster than a visual debug view.

4. **For a running instance, use remote console (rcon).** The engine's server answers an out-of-band UDP packet on loopback. Launch once with `set net_port <port>; set rconpassword <password>; devmap <map>`, then:
   ```bash
   python3 - "$@" <<'PY'
   import socket, sys
   s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM); s.settimeout(2.0)
   s.sendto(b"\xff\xff\xff\xffrcon <password> " + " ".join(sys.argv[1:]).encode(), ("127.0.0.1", <port>))
   print(s.recvfrom(16384)[0][4:].decode("latin-1").replace("print\n", "", 1).strip())
   PY
   ```
   `q3rcon <cvar>` reads a value and `q3rcon <cvar> <value>` sets it. This takes under a second and needs no relaunch. A simulator shares the host's network stack, so loopback reaches it. For long output, keep calling `recvfrom` until it goes quiet. One packet truncates.

5. **For input after boot, use a command file (debug builds only).** If the app has to be driven mid-session, for example when the scene has no accessibility tree, poll a file in the app's documents folder each frame, run each line once and delete it. Post `key <NAME>` lines to the same event queue real input uses:
   ```bash
   C=$(xcrun simctl get_app_container <udid> <bundle-id> data)
   printf 'key ENTER\nmap <map>\n' > "$C/Documents/<drive-file>.txt"
   ```
   Keep this behind `#if DEBUG`. It is a remote-control surface into the game.

6. **Clean up.** End every script with `quit` (or `simctl terminate`), and put back any saved setting the run changed (see Traps).

## Traps

- **In-game, bare console text is chat.** With a map running, `con_autochat` sends a line that doesn't start with `/` to `say`. `rconpassword <password>` turned up in chat and set nothing. At the menu there is no server, so bare commands run, which is why the same line worked in one place and not the other. Start every in-game command with `/`, including lines you give the user to type. A multi-command line needs it once: `/seta a 1; bind X "y"`.
- **The hook is gated on the delay variable.** In our port, `AUTOCMD` does nothing unless `AUTODISCONNECT` (the delay) is also set. Set both or nothing runs.
- **Commands fire one per tick (1.5 s here).** `wait` is a delay unit, not a frame wait. Add about 10 of them to cover a map load, and size the launcher's sleep from the command count.
- **The log may be stale until shutdown.** End the script with `quit` and read the log afterwards. Use `logfile 2`, not `1`.
- **rcon needs a server.** At the menu nothing answers. Playing a demo replaces the listen server, so rcon stops until a map is loaded again. A `seta rconpassword` in the config doesn't apply to an instance that is already running. Set it live once with `/rconpassword <password>`.
- **Port collisions.** A second engine build or a stale simulator instance can hold the default port, and the engine silently moves to the next one. Probe both ports, or kill the stale instance.
- **`map` sets `sv_cheats 0`, `devmap` sets it to 1.** Cheat-protected cvars silently refuse under `map`.
- **`devmap` in the config file doesn't auto-load.** Config exec runs too early in boot. Use the launch hook.
- **Test cvars that get saved come back every launch.** A saved debug switch reappeared as an apparent bug three times (a broken explosion, a stray crosshair, every frame drawn twice). Never register a test cvar as archived. Reset every test cvar at launch from one list. Enforce both with a build-time check script. A `seta` line in the config re-arms a cvar whatever flags the code gives it, so the launch reset is the real guard.
- **Harness runs that touch the user's settings must restore them.** Add `pushcvar <name> <value>` / `popcvar` to the engine, and journal pushed values to a file so a run killed before its pop is restored at the next launch. Or snapshot the config's `seta` lines before the run and restore them after.
- **Leave the screen clean.** A shader-remap test run without `quit` left odd-coloured panels on the running simulator, and the user reported it as a regression. Check the app is closed or back to normal before you report.
- **To change a cvar live, don't edit the config file.** The engine rewrites it on exit. Use rcon or the command file.
- **`SIMCTL_CHILD_` vars given to `simctl boot` stick.** They go to the simulator's launchd, and every later launch inherits them. Unset them before booting, and pass them only on the launch.
- **Typing is a last resort, for bootstrap only.** If you must type (for example, once, to set the rcon password): bring the app forward, click inside the window body (a title-bar click didn't take focus), open the console fresh with the backtick key, send one character per action about 0.25 s apart, and zoom on the prompt to check it before pressing Return. If a task seems to need typing, restructure it as a script.

## What it does not cover

The keyboard and controller input paths themselves: the command buffer skips them, so a bug in key handling won't show. Test those with real HID events (`idb ui key` / `idb ui text` on a simulator) or on hardware. Anything only a physical device does, such as ray tracing, a paired controller, or feel. Whether the picture looks right is still the human's call. The harness proves which commands ran and what the engine printed.

## Loading this into Claude

> This engine is tested through its console, never by typing into the game window. Run commands with `CMDS="<cmd>;<cmd>;quit" <run script>`, which passes them through the launch-time command hook, and read the console from `<log path or log show command>`. For a running instance use `<rcon helper> <cvar> [value]`. Every in-game console line, including ones given to the user, starts with `/`. End every run with `quit`. Debug and test cvars are never archived and are reset at launch. Any saved setting a run touches is pushed and popped.
