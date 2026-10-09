# Shader-math verifiers

> Lets Claude prove that a raymarch shader integrates what the bake intended (the source sprite, step-size independent, overlapping volumes combined correctly) by running the shader's arithmetic on the CPU against an answer known in advance.

**Applies to:** volume raymarching, accumulation and compositing shaders, and any GPU loop whose correct output can be computed exactly on the CPU (built for turning 2-D effect sprites into raymarched 3-D volumes for a Quake 3 Metal port) · **Needs:** Python 3 with NumPy (plus SciPy and Pillow for the preview), the baked volumes, the shader source to mirror

## Why it exists

A raymarch shader can be wrong in ways that still look like a plausible explosion. Claude's default is to tune the shader until the screenshot looks right, then move on. Two of the bugs this caught would have passed that:

1. **Wrong integral.** Compositing emissive art with Beer-Lambert extinction saturates where the art doesn't, and darkens every core. On a test blob it was 34% of peak wrong, and the brightest pixel came out at 0.59 instead of 0.90.
2. **Missing step weight.** Without a per-voxel step weight, brightness depends on the step size, so tuning the step for speed dims or blows out the effect.

A third came from the engine: the core blew out to flat white, and lowering the exposure barely moved it. Reasoning about it overstated the overshoot about 90×, because exposure was modelled as a raw multiplier when the engine divides it by the bake's normalisation. Measuring the integral replaced the guess with a number.

## What it does

1. **Mirror the shader in NumPy:** the same trilinear sampling with clamp-to-edge, start jitter, step sizing, per-voxel weight and normalisation.
2. **Compare against a known answer.** Along the bake axis, the integral must equal the source sprite pixel, because that is what the bake was constrained to. Print the max and mean error as a percentage of peak.
3. **Check invariants:** results that must not change when the step size, draw order or empty-space skipping changes.
4. **Show the bug next to the fix.** Run the wrong arithmetic too and print how far off it is, so the check is seen to fail when it should.
5. **Measure from the angles the engine actually uses,** and render orbit previews for a look outside the engine.

## Recipe

1. **The single-volume check** (bake output and the sprite it came from):
   ```bash
   python3 tools/verify_shader_math.py <volume>.npy <sprite>.png [--mode additive|alpha]
   ```
   It prints an error table at steps of 1, 0.5, 2 and 0.25 voxels, the step-size invariance against 1 voxel, and the extinction-applied-to-emissive error for contrast. On a 64³ synthetic blob: 0.06% max error at a 1-voxel step, and deviation under 0.06% across step sizes, against 34% for the wrong integral. This script always exits 0, so read the numbers (or add a threshold) before using it as a gate.
2. **The multi-volume invariants**, in 1-D where the answers are analytic:
   ```bash
   python3 tools/verify_multi_march.py      # prints A/B/C with PASS/FAIL, "ALL PASS", exit 1 on failure
   ```
   - A: overlapping emissive volumes sum, in either order. This is why the march needs no sorting.
   - B: emission behind an extinction volume is attenuated by exactly `exp(-tau)`.
   - C: skipping empty space keeps the sampling lattice and the jitter. Jumping straight to the next volume's entry lost phase (0.05 of a step) and changed the integral. Skipping whole steps didn't.
3. **The integral the engine will see:**
   ```bash
   python3 tools/measure_integral.py <effect>.qvol --gain <exposure> --steps 96 --frame 4
   ```
   This prints the 99th-percentile integral and the fraction of clipped pixels along the bake axis, at 30° and 45° off it, face-on, and along the box diagonal. Target: the 99th percentile of the exposed value near 1.0. Re-run after every re-bake, because bake settings move the normalisation.
4. **Orbit preview:**
   ```bash
   python3 tools/preview_orbit.py <volume>.npy --ramp <ramp>.png -o orbit.png --views 8 [--gif orbit.gif]
   ```
   A strip of views around the vertical axis, using the same additive integral the shader does. Read the image: the numbers can't tell you whether a cloud looks connected or cellular.
5. **Keep the mirror honest.** When the shader changes, change its NumPy mirror in the same commit, and keep each mirror's docstring naming the shader mode it copies.

## Traps

- **Axis order.** The baked volume was indexed `[y, x, z]`, so the ray origin's first component had to be the row, not the column. Get this wrong and the error table looks like a bake bug.
- **Model the engine's parameters as the engine uses them.** Exposure was a gain divided by the bake's normalisation, not a raw multiplier. Read the engine code before writing the mirror.
- **Off-axis chords are longer.** The bake identity only holds along the bake axis. A real effect is seen from any angle, so measure several directions before calling the core clipped or fine.
- **Numbers can miss what the eye sees.** Mean deviation couldn't tell connected billows from isolated cells at equal amplitude. Use the numbers to find the mechanism, and the preview to decide whether there is a problem.
- **A mirror only checks what it mirrors.** If the shader gains a mode or a weight the mirror doesn't have, the check keeps passing. Keep them in step (see Recipe step 5).
- **Re-baking changes the exposure.** Normalisation depends on bake settings such as turbulence, so a fixed gain dims or clips a new bake. Measure again; don't re-use the old gain.

## What it does not cover

The GPU itself: precision, texture filtering differences, and the engine's draw setup (depth clip, blend state, sorting against other geometry). Those need captures in the engine (see `renderer-ab-on-demos.md` and `side-by-side-reference-engine.md`). Whether the effect looks good, and whether a hollow-looking centre is physically right or an artefact of the inversion, stay with the human.

## Loading this into Claude

> Raymarch shader changes are checked on the CPU first. Run `verify_shader_math.py <volume> <sprite>` and read the error table: under 0.1% of peak at every step size. Run `verify_multi_march.py`, which must print ALL PASS. After any re-bake, run `measure_integral.py --gain <exposure>` and aim for a 99th percentile near 1.0. Look at a `preview_orbit.py` strip before calling the volume good. When the shader's arithmetic changes, update its NumPy mirror in the same commit. A screenshot that looks right isn't evidence that the integral is right.
