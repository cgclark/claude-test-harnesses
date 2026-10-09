# Claude automated testing harnesses

<details class="langs" data-current="en">
<summary>Language</summary>

**English** · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Ways for Claude Code to check its own work: run the app, capture something it can read, and decide pass or fail before a person has to look. Each name opens a page with the full recipe.

<img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"> **Claude recommended**: a standard tool used as is (8)<br>
<img class="c" src="icons/claude-code.svg" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"> **Claude recommended, extended**: a standard tool we had to add to before it worked (4)<br>
<img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"> **Built by us**: a method we had to work out (30)

<img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"> works on that version · <img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"> not confirmed yet · <img class="o t" src="icons/xmark.square.png" alt="doesn&#x27;t work there yet" title="doesn&#x27;t work there yet" width="16" height="16"> doesn't work there yet

Harnesses that don't depend on the OS version count as working on both. The rest are ticked from when each was last used; this Mac moved to 27 on 2 October 2026, and a one-by-one check against the 27 architecture is still to come.

**From**: the app each harness was first built in

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/big-top.png" alt="" width="20" height="20"> Big Top</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Apps on simulators, Macs & devices

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="60">From</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Headless simulator</a></td><td>Claude builds an iPhone app, runs it in the simulator in the background and takes its own screenshots and logs, so it can check a screen without taking over yours.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Layout probe</a></td><td>Claude measures what the screen actually laid out, such as bar heights and scroll positions, moment by moment as you move between screens, so it can find why something looks wrong instead of guessing.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Launch-argument hooks</a></td><td>Hidden switches in test builds that open an app straight on a chosen screen with sample data, so Claude can reach any screen without tapping through the app.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">iPad app on the Mac</a></td><td>Runs the iPad version of an app as an ordinary Mac app, so Claude can test it on the Mac with its logs and window screenshots.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript and screen capture</a></td><td>When Claude can&#x27;t control the screen directly, it drives Mac apps with AppleScript and photographs just their window to see the result.</td></tr>
<tr><td><a href="unit-test-suites.md">Unit tests</a></td><td>Automatic tests of an app&#x27;s internal logic, such as scoring, routes and queues, that run in seconds without opening the app.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Human-only checklist</a></td><td>One running list of the checks only a person can make, such as wearing the headset or using a real phone, so the rest of the work doesn&#x27;t wait for them.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Build every target</a></td><td>Rebuilds the iPhone, Mac and Vision Pro versions together after a change, and checks that test settings never get saved into a player&#x27;s own settings.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">SwiftUI live preview</a></td><td>Shows one screen in Xcode&#x27;s live preview and photographs it, so Claude can check a layout change without building and running the whole game.</td><td class="m"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Tap by accessibility</a></td><td>Taps buttons in the simulator at the positions the app itself reports, instead of guessing where they are from a screenshot.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Two simulators as two people</a></td><td>Runs the app on two simulated iPhones as two different people, so invitations, challenges and syncing can be tested without two real phones.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Every screen in every language</a></td><td>Photographs every main screen in every language, plus a made-up language with extra-long words, on one sheet, so text that doesn&#x27;t fit is easy to spot.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Crash reports</a></td><td>Pulls the crash report off a real iPhone and reads it, so a crash that only happens on the phone gets a named cause.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Small test suite</a></td><td>A small, self-contained set of automatic checks for a Python tool, which runs anywhere without installing anything.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
</tbody>
</table>

## Graphics & games

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="60">From</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Game console driving</a></td><td>Sends commands to the game&#x27;s built-in console from a script and reads its log afterwards, instead of typing into the game window.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Before-and-after frames</a></td><td>Plays the same recorded game clip before and after a graphics change and compares the frames pixel by pixel.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Ray tracing on the Mac</a></td><td>Test views that show each step of the ray-traced lighting (shadows, reflections, ambient light) on its own, plus self-checks that print pass or fail.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Pro screenshots</a></td><td>Captures what the Vision Pro app shows, including each eye&#x27;s view in 3D, in the simulator and on the headset.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude recommended, extended" title="Claude recommended, extended" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Offline shader compile</a></td><td>Compiles the ray-tracing graphics code on the Mac, because the simulator skips it and mistakes would otherwise only show up on a device.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPU frame capture</a></td><td>Captures one frame on the graphics chip and lists what each drawing step cost, to find what&#x27;s slow.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Shader maths</a></td><td>Recalculates Quake 3&#x27;s smoke and fire effects slowly and exactly, and checks the fast graphics version draws the same picture.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

## Voice, language & data

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="60">From</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Screenshots to text</a></td><td>Turns screenshots and scans into text on the Mac before Claude reads them, which keeps images private and uses far less of Claude&#x27;s memory.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m" rowspan="8"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>The Mac speaks test phrases in synthetic voices into the app&#x27;s speech recogniser, so voice commands can be tested without anyone talking.</td><td class="app-c"><img class="app-sm" src="icons/apps/big-top.png" alt="Big Top" title="Big Top" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
<tr><td><a href="siri-phrasing-check.md">Siri phrasing</a></td><td>Checks that the phrases built into the app for Siri, such as &quot;order my usual&quot;, match what people say; whether Siri routes them correctly still needs the phone.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Golden snapshot</a></td><td>Saves the app&#x27;s full output before a rewrite, then checks the rewritten version produces exactly the same output.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Transcription accuracy</a></td><td>Runs the app&#x27;s speech-to-text on public recordings that come with correct transcripts, and scores how many characters it gets wrong.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Translation checks</a></td><td>Checks that every translation keeps its names, numbers and agreed terms, and that no on-screen text was left untranslated. Used for Quake 3 too.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Real data</a></td><td>Tests route matching on a set of real recorded rides instead of made-up ones, which found bugs the made-up tests had missed.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Match the original app</a></td><td>Compares the database in our iPad version with the one from the original Windows app, table by table and row by row.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td></tr>
</tbody>
</table>

## Hardware, networks & services

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="60">From</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Compare with a known-good device</a></td><td>Records how a known-good setup behaves (the iPhone talking straight to the earbuds) and compares a recording of our bridge against it.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetooth captures</a></td><td>Records the Bluetooth traffic itself, to see what the devices actually sent rather than what they reported.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Health checks</a></td><td>Checks that each web service answers from the internet, and that the route which should be blocked is refused.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="60">From</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Browser driving</a></td><td>Claude opens pages in a browser, fills in forms and reads the result, to check a site works and looks right.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude recommended" title="Claude recommended" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Website deploy check</a></td><td>After a website update, checks every file arrived intact on the server, then checks the layout at phone, tablet and desktop widths.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Project-specific (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Game mods</a></td><td>Loads each popular multiplayer mod into our version of the game, starts a map, and checks the log for errors.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Side by side with the original</a></td><td>Records the same scene in our version and in the original game, side by side, to show any difference.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="not confirmed yet" title="not confirmed yet" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Level screenshots</a></td><td>Takes a picture of each map from the camera angle the map&#x27;s author chose, and lays them out on one sheet.</td></tr>
</tbody>
</table>

### Sign-language work

<table>
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Motion compare</a></td><td>Plays a computer-generated signing hand next to the real signer it was made from, frame by frame, to check the motion matches.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Check quoted values</a></td><td>Before Claude quotes a date or figure from a document, checks that the exact text really appears in that document.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger Bluetooth bridge

<table>
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Bridge probes and dashboard</a></td><td>Small test programs and a live dashboard for the bike&#x27;s Bluetooth audio bridge, showing sound buffers, signal strength and connections while riding.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

### Booking portal

<table>
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Booking dry run</a></td><td>Goes through an online booking up to the final step and stops, so the steps can be tested without making a real booking.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Harness</th><th>Capability</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origin</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Animation check</a></td><td>Measures an animated diagram while it plays, checking that pieces line up and don&#x27;t overlap, to a fraction of a pixel.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="works on that version" title="works on that version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Built by us" title="Built by us" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

A more technical version, written for loading into Claude, is the [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) on GitHub.
