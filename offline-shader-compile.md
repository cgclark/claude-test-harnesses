# Offline shader compile

> Lets Claude prove that a runtime-compiled Metal shader compiles, on any Mac, before it ships, even though the simulator never compiles it and a failure on hardware only prints a warning.

**Applies to:** Metal renderers that build shader libraries from source strings at runtime (`newLibraryWithSource:`), especially paths gated on GPU features the simulator lacks (built for the ray-tracing world shader of a Quake 3 Metal port) · **Needs:** macOS, Xcode with the Metal Toolchain component installed, Python 3

## Why it exists

The ray-tracing library is compiled only when the GPU reports ray tracing from render. The simulator never reports it, so it never compiles that source. A syntax error in it doesn't break the build and doesn't show in the simulator. On real hardware it prints one line, `shadow shader compile failed`, and the renderer quietly falls back to raster. Claude's default is to build, run the simulator, see a clean image, and call the change done. That proves nothing about this shader. `realtime-raytracing-on-mac.md` (recipe step 3) covers the wider RT test loop. This file is the compile step on its own.

## What it does

1. Read the engine source file that holds the shader as C string literals.
2. Pull out the named literals in the order the engine joins them, skipping `//` comments between the pieces and unescaping `\n`, `\t`, `\"`, `\\`.
3. Join them with the same separators the engine's `stringWithFormat:` uses, and write one `.metal` file.
4. Run the real Metal compiler over it. Exit status is the compiler's, so the check can gate a commit.

## Recipe

1. Write a small script for your engine (ours is about 70 lines). It needs the source path, the literal names in order, and the separator:
   ```python
   SRC   = '<renderer>/<file>.m'
   NAMES = ['<baseShaderSrc>', '<helpersSrc>', '<rtSuffix>']    # same order as the engine
   shader = parts[0] + '\n' + parts[1] + '\n' + parts[2]         # same separators as the engine
   ```
2. Compile:
   ```bash
   xcrun -sdk macosx metal -std=metal3.0 -c <assembled>.metal -o /dev/null
   ```
3. Run it after every edit to the shader strings, and before a commit:
   ```bash
   python3 tools/<shader-check>.py          # prints "RT shader OK (<n> lines)" or the compiler errors
   python3 tools/<shader-check>.py --emit   # also says where the assembled .metal was written
   ```
   On failure, the script prints the assembled file's path. Compiler line numbers refer to that file, not to the `.m`.

## Traps

- **The Metal compiler may not be installed.** Recent Xcode releases ship it as a separate download. Without it, the check fails with `cannot execute tool 'metal' due to missing Metal Toolchain; use: xcodebuild -downloadComponent MetalToolchain`. Read that as a missing tool, not a broken shader. It happened on the machine these notes were written on: the extraction ran, the compile didn't.
- **Each Xcode needs its own Metal compiler.** The download is tied to one Xcode build: after the Xcode 27 upgrade, the Xcode 26 compiler was still on disk but unused, and the same error came back. Check with `xcodebuild -showComponent MetalToolchain` after every Xcode update.
- **Pieces spliced in by macro.** A shader string can begin with a C macro that is itself string literals (`kRTHelpersSrc` starts with `MTL_FOV_HELPERS_SRC` from `tr_metal.h`). An extractor that collects only quoted strings drops it silently, and the offline compile then fails on an undeclared function the engine has no trouble with. The script expands `#define` string macros from the renderer's sources.
- **The order has to match the engine.** If the engine adds a piece, renames a literal, or changes the separator, the script compiles something else and passes. Keep the literal names and the join next to each other in the engine, and update the script in the same commit.
- **Language version.** The engine passes `options:nil`, so the device's default language version applies. The script pins `-std=metal3.0`. Pin the same version on both sides, or a shader that uses newer features passes one check and fails the other.
- **Runtime macros.** If the engine passes preprocessor macros in its compile options, the offline run has to define the same ones (`-D NAME=value`). Ours passes none.
- **Compiling isn't linking.** A clean compile doesn't catch a binding or argument mismatch, which only shows when the pipeline is created. On hardware, a missing compile warning together with a passing offline check pointed at a binding mismatch, not a syntax error. Call `newRenderPipelineStateWithDescriptor:` for each RT shader in a small harness to catch those (see `realtime-raytracing-on-mac.md`).
- **One library checked, others not.** The renderer this was built for has about 20 `newLibraryWithSource:` calls across 7 files. The script covers the one the simulator can never reach. The others run in the simulator, but they are only checked when the code path that uses them actually runs.

## What it does not cover

Whether the shader is right: only that it compiles. Pipeline creation, GPU faults and the image itself need the Mac or the device (`realtime-raytracing-on-mac.md`). Shaders the engine generates at runtime from data, rather than from fixed literals, need the engine to dump the final source.

## Loading this into Claude

> Any edit to a runtime-compiled shader string runs `python3 <shader-check script>` before the change is called done. A clean simulator run doesn't count, because the simulator never compiles that library. If the check fails with "missing Metal Toolchain", tell the user to install it (`xcodebuild -downloadComponent MetalToolchain`) rather than reporting a shader error. When you add or reorder a shader piece in the engine, update the script's list in the same commit.
