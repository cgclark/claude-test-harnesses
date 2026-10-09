# Plugin test cases

> Lets Claude run each third-party plugin (mod, add-on, extension) inside the host it is porting, headlessly, and read back which of the plugin's modules loaded, which failed and with what error, instead of reasoning from forum posts about whether it "should work".

**Applies to:** hosts that load third-party code they don't control: game engines and their mods, interpreters and
bytecode VMs, apps with plugin folders · **Needs:** a scriptable host (a launch-time command hook or CLI), a log
Claude can read, the plugins themselves (downloaded with the user's go-ahead), Xcode + `simctl` if the host is an
iOS/visionOS app

## Why it exists

By default Claude answers "will plugin X work?" from public sources: compatibility tables, issue trackers, forum
posts. Those describe someone else's build. A port changes exactly the parts plugins lean on: the VM, the memory
limits, the file search order, the network stack. So the answer goes back to the user unchecked, and the user finds
out by installing the plugin.

Built for an iOS/visionOS port of a game engine, where mods can run only as interpreted bytecode (iOS forbids a JIT).
The research said one popular mod had a known interpreter bug when hosting. Running it showed the failure was real,
and in the upstream interpreter too: stock upstream fails the same way. That moved the fix from "patch our port" to
"replace the interpreter". After the replacement, all three mods that could be tested played.

## What it does

1. **One plugin = one test case.** Each case is a folder with the plugin's files, plus the action that exercises
   *all* of its modules. For game mods, hosting a map runs server, client and UI code. Joining a server runs only
   the client half.
2. The harness links the folder into the host's data directory, launches the host with a scripted command sequence
   (switch to the plugin, run the action, wait, screenshot, quit), then removes the link.
3. It greps the host log for **load lines** (which modules loaded, from where) and **known failure signatures**
   (VM errors, drops, missing dependencies).
4. Pass = every module loaded, no failure signature, and the screenshot shows the plugin's own UI.
5. **A/B on the host's switch:** when the host has two implementations of the thing plugins depend on (old and new
   interpreter, say), run the same case under both. A plugin that fails under both, and under the stock upstream
   build, is not your port's bug.

## Recipe

**1. Give the host a launch-time command hook** if it has none: an env var holding a `;`-separated script, each
command issued a fixed delay after the last. On iOS simulators an app gets env vars through the `SIMCTL_CHILD_`
prefix:

```bash
SIMCTL_CHILD_<APP>_AUTOCMD="<cmd1>;<cmd2>;quit" xcrun simctl launch --console-pty <udid> <bundle id> > run.log 2>&1
```

**2. Write the case runner**, `tools/plugin-check.sh <plugin dir> [action] [extra commands]`:

```bash
#!/bin/bash
set -uo pipefail
src=$(cd "${1:?usage: plugin-check.sh <plugin dir> [action] [extra]}" && pwd); name=$(basename "$src")
action=${2:-<default action>}; extra=${3:-}
udid=$(<resolve the simulator by NAME, not a pasted UDID>)
xcrun simctl boot "$udid" 2>/dev/null
C=$(xcrun simctl get_app_container "$udid" <bundle id> data) || { echo "app not installed"; exit 1; }
[ -e "$C/Documents/$name" ] && { echo "$C/Documents/$name exists, not touching it"; exit 1; }
ln -s "$src" "$C/Documents/$name"            # COPY=1 variant: cp -R, for plugins that list loose files
# Padding commands are the "wait": each is issued a fixed interval after the last.
W=""; for i in $(seq 1 ${WAITS:-16}); do W="$W;echo plugin-check waiting"; done
<launch with AUTOCMD="<switch to $name>${extra:+;$extra};$action$W;screenshot;quit">  > "$out.log"
C=$(xcrun simctl get_app_container "$udid" <bundle id> data)   # it moves on reinstall: look it up again
[ -L "$C/Documents/$name" ] && rm "$C/Documents/$name"
xcrun simctl shutdown "$udid"
grep -a -E "<load line>|<failure signature 1>|<failure signature 2>|ERROR|Fatal" "$out.app.log" | head -30
```

**3. Collect the failure signatures** before running anything: the host's own error strings for module loads, and
every known bug from the plugins' issue trackers (one engine's list: `could not find appropriate entry point`,
`VM program counter out of range`, `OP_JUMP`, `OP_LEAVE`, `ERR_DROP`, `bad opcode`, `stack overflow`). They go in
the grep.

**4. Keep a results table** in the repo (`docs/<plugins>.md`): plugin, version, action, result, the commit that
made it pass, and the reason for any case not run ("needs base version 1.03a, which we don't have").

**5. A/B wrapper** for the host switch. It runs the same case twice and prints one line per side:

```bash
for impl in 1 0; do
  OUT=${TMPDIR:-/tmp}/ab-$impl RUN="<benchmark action>" ./tools/plugin-check.sh "$src" "" "set <switch> $impl" >/dev/null 2>&1
  printf '<switch> %s: ' "$impl"; grep -a -E "<result line>" "${TMPDIR:-/tmp}/ab-$impl.app.log" | tail -1
done
```

**6. Rule out upstream.** Run the failing case on the stock upstream build too (a local dedicated server, a desktop
build). The same failure there means the plugin or upstream is at fault, not your port.

## Traps

- **A plugin's code is not the code you compiled.** In this engine, built-in modules were compiled in and only
  plugins ran interpreted, so the base game passing proved nothing about the interpreter. Name which code path each
  case actually exercises.
- **Joining is not hosting.** The known VM failures were in the server module, which runs only when you host.
  Choose the action that loads every module, and say which modules a case did not reach.
- **Missing dependency packs look like failures.** One mod stopped at "map pack missing" until its own map packs
  were added. Read the drop message before calling it a crash. A real client would download them from the server.
- **The app's data container moves on every reinstall.** Look up the container path after the run, not before, or
  the cleanup removes nothing and the next run finds a stale link.
- **Don't change settings by editing the config file.** The host rewrites it on exit, and the container path
  rotates. Set the value through the command script (`set <cvar> <value>`), then echo it back and read the echo in
  the log.
- **The launch hook may need a second variable.** Here the command script did nothing unless a separate
  "auto-disconnect delay" variable was also set. Make the runner set both.
- **Log lines carry colour codes.** A `^`-anchored grep returns 0 against `^1Loading ...`. Anchor on the message.
- **The host's own UI layers leak into a plugin's menus.** The port drew its own button art under stock asset names,
  and a mod may ship different art under the same names. Draw custom layers only for the base content.
- **Leave the simulator clean.** End with `quit` and `simctl shutdown`. A booted sim with a stale link breaks the
  next case.
- **A plugin you can't get is "not run", not "works".** Record why and what would settle it.

## What it does not cover

Online play against real public servers and their mix of versions, performance on real devices (the simulator is
fine for relative A/B on CPU cost, not absolute speed), touch/controller input inside a plugin's menus, and plugins
that need paid or region-locked downloads. Downloading plugins needs the user's go-ahead each time.

## Loading this into Claude

> Plugin compatibility is tested, not researched: `tools/plugin-check.sh <plugin dir> [action]` loads the plugin in
> the simulator, runs `<action>` (which must load every plugin module), screenshots, quits and greps the log for load
> lines and the failure signatures listed in the script. Record every case in `docs/<plugins>.md` with the commit
> that made it pass. When a case fails, A/B the host switch (`tools/ab.sh`) and try stock upstream before patching
> the port. Never download a plugin without asking.
