# Claude automated testing harnesses

Test harnesses built since June 2026 so Claude Code can check its own work: run the thing, capture a
result it can read, and decide pass or fail before a person has to look. Many of these were not
something Claude included, knew how to do, or mentioned at the start; they had to be found one
project at a time. Others are standard methods Claude recommended and we used heavily.

Each linked name is a self-contained file written to be loaded into another Claude instance: why it
exists, the loop, a recipe with placeholders, the traps that cost real time, what stays with a person,
and a paragraph to paste into a project's `CLAUDE.md`. [TEMPLATE.md](TEMPLATE.md) is the shape.
[index.md](index.md) is the same list in plain language, in 27 languages, also on the web at
[gate.locii-innovations.com/ai/…/test_harnesses](https://gate.locii-innovations.com/ai/TZcyE-nc36-Fu-naDOIm2So4/test_harnesses/).

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"></td><td><b>Claude recommended</b>: a standard tool or practice Claude proposed, used as is</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"></td><td><b>Claude recommended, extended</b>: a standard tool we had to add to before it worked reliably</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td><td><b>Built by us</b>: a method we had to develop</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"> works on that version · <img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"> not confirmed yet · <img class="o t" src="icons/xmark.square.png" alt="doesn&#x27;t work there yet" title="doesn&#x27;t work there yet" width="16" height="16"> doesn't work there yet

Harnesses that don't depend on the OS version count as working on both. The rest are ticked from when each was last used; this Mac moved to 27 on 2 October 2026, and a one-by-one check against the 27 architecture is still to come.

**From**: the app each harness was first built in

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Apps on simulators, Macs & devices

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="60">From</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Headless simulator</a></td><td>Build, install, launch, screenshot and log an app with no Xcode window, on named simulators, in the background, ending clean</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Layout probe</a></td><td>Timed view-hierarchy probe read from the unified log, transitions tiled into one frame sheet, one marked experiment per hypothesis</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Launch-argument hooks</a></td><td>Boot straight into a screen, seed data, replay a demo or dump state via environment variables passed at launch</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">iPad app on the Mac</a></td><td>Run and drive the iPad build natively on the Mac, with logs and window screenshots</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript and screen capture</a></td><td>Drive and capture Mac apps when desktop control isn&#x27;t available</td></tr>
<tr><td><a href="unit-test-suites.md">Unit tests</a></td><td>Domain logic: routes, scoring, identity, relay rules, queues</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Human-only checklist</a></td><td>A running list of checks that need a person, a device or the headset, so nothing else waits on them</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Build every target</a></td><td>Forced rebuild of iOS, Mac and visionOS together; test settings never saved into a player&#x27;s config</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">SwiftUI live preview</a></td><td>A UI change in Xcode&#x27;s live canvas, captured, without running the app</td><td class="m"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Tap by accessibility</a></td><td>Tap controls by their real frames instead of guessed coordinates</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Two simulators as two people</a></td><td>Invitations, sync and challenges between two people, using two named simulators</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Every screen in every language</a></td><td>Every key screen in every language plus a doubled-length pseudo-locale, checked for overflow</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Crash reports</a></td><td>Pull and read a real device&#x27;s crash report without Xcode</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Small test suite</a></td><td>A Python toolkit&#x27;s behaviour with one check helper and an exit-code gate</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
</tbody>
</table>

## Graphics & games

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="60">From</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Game console driving</a></td><td>Run engine commands from a script and read the console log back, instead of typing into the game</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="5"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Before-and-after frames</a></td><td>Frame grabs and pixel diffs from a recorded demo at a fixed aspect ratio, before and after a change</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Ray tracing on the Mac</a></td><td>Debug views that isolate each ray-tracing stage, exact GPU self-checks, per-pass timings</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Pro screenshots</a></td><td>What a visionOS app actually shows, in the simulator and on the headset, including immersive and two-eye views</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Offline shader compile</a></td><td>Ray-tracing shaders that the simulator never compiles, compiled offline on the Mac</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPU frame capture</a></td><td>Cost per draw call from a single captured frame</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Shader maths</a></td><td>A raymarch shader reproduces the reference sprite; invariants across marches</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

## Voice, language & data

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="60">From</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Screenshots to text</a></td><td>Screenshots and scans reduced to text locally before Claude reads them</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Speech features with no one speaking: synthetic voices → on-device transcriber → the app&#x27;s own turn logic</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Audio replay on a device</a></td><td>Real phone, no one speaking: synthesised scenario audio → the app&#x27;s on-device transcriber in place of the mic (holds while the app speaks) → app log done line checked</td></tr>
<tr><td><a href="siri-phrasing-check.md">Siri phrasing</a></td><td>Compiled App Shortcut phrases match what people say; real routing stays on the device</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Golden snapshot</a></td><td>A refactor or data migration reproduces the old output exactly</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Transcription accuracy</a></td><td>Character error rate against public ground-truth speech sets</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Translation checks</a></td><td>Arguments, glossary terms and inflection markup survive translation; no text escapes localization; bot chat against a blessed baseline</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Real data</a></td><td>Algorithms against a real corpus instead of synthetic data, without seeded data leaking into real stores</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Match the original app</a></td><td>A ported database matches the original app&#x27;s baseline</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
</tbody>
</table>

## Hardware, networks & services

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="60">From</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Compare with a known-good device</a></td><td>Captures from the device under test diffed against a known-good reference device</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetooth captures</a></td><td>What is actually on the wire: links, codecs, audio channels, signal strength</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Health checks</a></td><td>Each service answers through the tunnel and proxy</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="60">From</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Browser driving</a></td><td>Pages, forms and layouts in Claude in Chrome (your real sessions) or the desktop app&#x27;s browser pane</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Website deploy check</a></td><td>Every deployed file matches by checksum; layout at five widths; computed styles across browsers</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Project-specific (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Game mods</a></td><td>Each multiplayer mod loads and hosts a map; logs checked for load and VM errors</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Side by side with the original</a></td><td>Video of the same scene in our port and a reference build</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Level screenshots</a></td><td>Map screenshots matched to the map author&#x27;s camera, with contact sheets</td></tr>
</tbody>
</table>

### Sign-language work

<table>
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Motion compare</a></td><td>A generated signing hand against the source signer, frame for frame</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Check quoted values</a></td><td>A date or value Claude quotes is checked against the source document</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger Bluetooth bridge

<table>
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Bridge probes and dashboard</a></td><td>Mic-to-Siri end to end, protocol bisects, buffer and signal plots while riding</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

### Booking portal

<table>
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Booking dry run</a></td><td>A portal booking driven to the last step and stopped before confirming</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Animation check</a></td><td>Hand-overs and overlaps in an animated map, measured at a given window size</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

</details>
