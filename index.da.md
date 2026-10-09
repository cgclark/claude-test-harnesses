# Automatiske testopstillinger til Claude

<details class="langs" data-current="da">
<summary>Sprog</summary>

[English](index.md) · [العربية](index.ar.md) · **Dansk** · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Måder, hvorpå Claude Code kan tjekke sit eget arbejde: køre appen, optage noget, den kan læse, og afgøre bestået eller ikke bestået, før et menneske behøver at se på det. Hvert navn åbner en side med hele opskriften. Selve siderne om testopstillingerne er på engelsk.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Anbefalet af Claude" title="Anbefalet af Claude" width="16" height="16"></td><td><b>Anbefalet af Claude</b>: et standardværktøj brugt, som det er</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Anbefalet af Claude, udvidet" title="Anbefalet af Claude, udvidet" width="16" height="16"><img class="o" src="icons/plus.png" alt="Anbefalet af Claude, udvidet" title="Anbefalet af Claude, udvidet" width="16" height="16"></td><td><b>Anbefalet af Claude, udvidet</b>: et standardværktøj, vi måtte bygge videre på, før det virkede</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td><td><b>Bygget af os</b>: en metode, vi selv måtte finde frem til</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"> virker på den version · <img class="o t" src="icons/square.png" alt="endnu ikke bekræftet" title="endnu ikke bekræftet" width="16" height="16"> endnu ikke bekræftet · <img class="o t" src="icons/xmark.square.png" alt="virker ikke der endnu" title="virker ikke der endnu" width="16" height="16"> virker ikke der endnu

Testopstillinger, der ikke afhænger af OS-versionen, tæller som virkende på begge. Resten er markeret ud fra, hvornår hver enkelt sidst blev brugt; denne Mac skiftede til 27 den 2. oktober 2026, og en gennemgang én for én mod 27-arkitekturen mangler stadig.

**Fra**: den app, hver testopstilling først blev bygget i

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Apps på simulatorer, Mac'er & enheder

<table class="wide">
<thead><tr><th width="190">Testopstilling</th><th>Funktion</th><th width="60">Fra</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oprindelse</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Simulator i baggrunden</a></td><td>Claude bygger en iPhone-app, kører den i simulatoren i baggrunden og tager selv skærmbilleder og logs, så den kan tjekke en skærm uden at overtage din.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Anbefalet af Claude, udvidet" title="Anbefalet af Claude, udvidet" width="16" height="16"><img class="o" src="icons/plus.png" alt="Anbefalet af Claude, udvidet" title="Anbefalet af Claude, udvidet" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Layoutsonde</a></td><td>Claude måler, hvad skærmen faktisk lagde ud, såsom bjælkehøjder og rullepositioner, øjeblik for øjeblik, mens du skifter mellem skærme, så den kan finde ud af, hvorfor noget ser forkert ud, i stedet for at gætte.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Startargument-hooks</a></td><td>Skjulte kontakter i testbuilds, der åbner en app direkte på en valgt skærm med eksempeldata, så Claude kan nå enhver skærm uden at trykke sig gennem appen.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">iPad-app på Mac&#x27;en</a></td><td>Kører iPad-versionen af en app som en almindelig Mac-app, så Claude kan teste den på Mac&#x27;en med dens logs og skærmbilleder af vinduet.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Anbefalet af Claude, udvidet" title="Anbefalet af Claude, udvidet" width="16" height="16"><img class="o" src="icons/plus.png" alt="Anbefalet af Claude, udvidet" title="Anbefalet af Claude, udvidet" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript og skærmoptagelse</a></td><td>Når Claude ikke kan styre skærmen direkte, styrer den Mac-apps med AppleScript og fotograferer kun deres vindue for at se resultatet.</td></tr>
<tr><td><a href="unit-test-suites.md">Enhedstest</a></td><td>Automatiske test af en apps interne logik, såsom pointberegning, ruter og køer, der kører på få sekunder uden at åbne appen.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Anbefalet af Claude" title="Anbefalet af Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Tjekliste kun for mennesker</a></td><td>Én løbende liste over de tjek, kun et menneske kan udføre, såsom at have headsettet på eller bruge en rigtig telefon, så resten af arbejdet ikke venter på dem.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Byg alle targets</a></td><td>Genbygger iPhone-, Mac- og Vision Pro-versionerne samlet efter en ændring og tjekker, at testindstillinger aldrig bliver gemt i en spillers egne indstillinger.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Live-forhåndsvisning i SwiftUI</a></td><td>Viser én skærm i Xcodes live-forhåndsvisning og fotograferer den, så Claude kan tjekke en layoutændring uden at bygge og køre hele spillet.</td><td class="m"><img class="o t" src="icons/square.png" alt="endnu ikke bekræftet" title="endnu ikke bekræftet" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Tryk via tilgængelighed</a></td><td>Trykker på knapper i simulatoren på de positioner, appen selv oplyser, i stedet for at gætte, hvor de er, ud fra et skærmbillede.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Anbefalet af Claude" title="Anbefalet af Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">To simulatorer som to personer</a></td><td>Kører appen på to simulerede iPhones som to forskellige personer, så invitationer, udfordringer og synkronisering kan testes uden to rigtige telefoner.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="endnu ikke bekræftet" title="endnu ikke bekræftet" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Alle skærme på alle sprog</a></td><td>Fotograferer alle hovedskærme på alle sprog, plus et opdigtet sprog med ekstra lange ord, på ét ark, så tekst, der ikke passer, er let at få øje på.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Nedbrudsrapporter</a></td><td>Henter nedbrudsrapporten fra en rigtig iPhone og læser den, så et nedbrud, der kun sker på telefonen, får en navngivet årsag.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="endnu ikke bekræftet" title="endnu ikke bekræftet" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Anbefalet af Claude" title="Anbefalet af Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Lille testsuite</a></td><td>Et lille, selvstændigt sæt automatiske tjek til et Python-værktøj, der kører overalt uden at installere noget.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td></tr>
</tbody>
</table>

## Grafik & spil

<table class="wide">
<thead><tr><th width="190">Testopstilling</th><th>Funktion</th><th width="60">Fra</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oprindelse</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Styring af spilkonsollen</a></td><td>Sender kommandoer til spillets indbyggede konsol fra et script og læser bagefter dens log i stedet for at skrive i spilvinduet.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Før og efter-billeder</a></td><td>Afspiller det samme optagede spilklip før og efter en grafikændring og sammenligner billederne pixel for pixel.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Ray tracing på Mac&#x27;en</a></td><td>Testvisninger, der viser hvert trin i den ray-tracede belysning (skygger, refleksioner, omgivende lys) for sig, plus selvtjek, der udskriver bestået eller ikke bestået.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Pro-skærmbilleder</a></td><td>Optager, hvad Vision Pro-appen viser, inklusive hvert øjes billede i 3D, i simulatoren og på headsettet.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="endnu ikke bekræftet" title="endnu ikke bekræftet" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Anbefalet af Claude, udvidet" title="Anbefalet af Claude, udvidet" width="16" height="16"><img class="o" src="icons/plus.png" alt="Anbefalet af Claude, udvidet" title="Anbefalet af Claude, udvidet" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Offline shaderkompilering</a></td><td>Kompilerer ray tracing-grafikkoden på Mac&#x27;en, fordi simulatoren springer den over, og fejl ellers først ville vise sig på en enhed.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPU-billedoptagelse</a></td><td>Optager ét billede på grafikchippen og viser, hvad hvert tegnetrin kostede, for at finde det, der er langsomt.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="endnu ikke bekræftet" title="endnu ikke bekræftet" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Anbefalet af Claude" title="Anbefalet af Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Shadermatematik</a></td><td>Genberegner Quake 3&#x27;s røg- og ildeffekter langsomt og præcist og tjekker, at den hurtige grafikversion tegner det samme billede.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
</tbody>
</table>

## Stemme, sprog & data

<table class="wide">
<thead><tr><th width="190">Testopstilling</th><th>Funktion</th><th width="60">Fra</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oprindelse</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Skærmbilleder til tekst</a></td><td>Omdanner skærmbilleder og scanninger til tekst på Mac&#x27;en, før Claude læser dem, hvilket holder billederne private og bruger langt mindre af Claudes hukommelse.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac&#x27;en siger testfraser med syntetiske stemmer ind i appens talegenkendelse, så stemmekommandoer kan testes, uden at nogen taler.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="endnu ikke bekræftet" title="endnu ikke bekræftet" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Lydafspilning på en enhed</a></td><td>Mac&#x27;en laver hver testsamtale om til en lydfil, og appen på telefonen lytter til den i stedet for mikrofonen, så stemmefunktioner kan testes på den rigtige telefon, uden at nogen taler.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Siri-formuleringer</a></td><td>Tjekker, at de fraser, der er bygget ind i appen til Siri, såsom &quot;order my usual&quot;, svarer til det, folk siger; om Siri sender dem det rigtige sted hen, kræver stadig telefonen.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Referencesnapshot</a></td><td>Gemmer appens fulde output før en omskrivning og tjekker derefter, at den omskrevne version giver præcis det samme output.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="endnu ikke bekræftet" title="endnu ikke bekræftet" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Transskriptionsnøjagtighed</a></td><td>Kører appens tale-til-tekst på offentlige optagelser, der følger med korrekte transskriptioner, og måler, hvor mange tegn den tager fejl af.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Oversættelsestjek</a></td><td>Tjekker, at hver oversættelse bevarer sine navne, tal og aftalte termer, og at ingen tekst på skærmen er efterladt uoversat. Bruges også til Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Rigtige data</a></td><td>Tester rutematchning på et sæt rigtige optagede ture i stedet for opdigtede, hvilket fandt fejl, som de opdigtede test havde overset.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="endnu ikke bekræftet" title="endnu ikke bekræftet" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Match den originale app</a></td><td>Sammenligner databasen i vores iPad-version med den fra den originale Windows-app, tabel for tabel og række for række.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td></tr>
</tbody>
</table>

## Hardware, netværk & tjenester

<table class="wide">
<thead><tr><th width="190">Testopstilling</th><th>Funktion</th><th width="60">Fra</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oprindelse</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Sammenlign med en enhed, der virker</a></td><td>Optager, hvordan en opsætning, der vides at virke, opfører sig (iPhonen, der taler direkte med øretelefonerne), og sammenligner en optagelse af vores bro med den.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetooth-optagelser</a></td><td>Optager selve Bluetooth-trafikken for at se, hvad enhederne faktisk sendte, frem for hvad de rapporterede.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Anbefalet af Claude" title="Anbefalet af Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Sundhedstjek</a></td><td>Tjekker, at hver webtjeneste svarer fra internettet, og at den rute, der skal være blokeret, bliver afvist.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Testopstilling</th><th>Funktion</th><th width="60">Fra</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oprindelse</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Browserstyring</a></td><td>Claude åbner sider i en browser, udfylder formularer og læser resultatet for at tjekke, at et websted virker og ser rigtigt ud.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Anbefalet af Claude" title="Anbefalet af Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Tjek af webstedsudrulning</a></td><td>Efter en opdatering af et websted tjekkes det, at hver fil kom intakt frem til serveren, og derefter tjekkes layoutet i telefon-, tablet- og desktopbredde.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Projektspecifikke (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Testopstilling</th><th>Funktion</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oprindelse</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Spilmods</a></td><td>Indlæser hver populær multiplayer-mod i vores version af spillet, starter en bane og tjekker loggen for fejl.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="endnu ikke bekræftet" title="endnu ikke bekræftet" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Side om side med originalen</a></td><td>Optager den samme scene i vores version og i det originale spil, side om side, for at vise enhver forskel.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="endnu ikke bekræftet" title="endnu ikke bekræftet" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Skærmbilleder af baner</a></td><td>Tager et billede af hver bane fra den kameravinkel, banens skaber valgte, og lægger dem ud på ét ark.</td></tr>
</tbody>
</table>

### Tegnsprogsarbejde

<table>
<thead><tr><th width="190">Testopstilling</th><th>Funktion</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oprindelse</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Bevægelsessammenligning</a></td><td>Afspiller en computergenereret tegnende hånd ved siden af den rigtige tegnsprogsbruger, den blev lavet ud fra, billede for billede, for at tjekke, at bevægelsen stemmer overens.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Testopstilling</th><th>Funktion</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oprindelse</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Tjek citerede værdier</a></td><td>Før Claude citerer en dato eller et tal fra et dokument, tjekkes det, at den nøjagtige tekst virkelig står i dokumentet.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger Bluetooth-bro

<table>
<thead><tr><th width="190">Testopstilling</th><th>Funktion</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oprindelse</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Brosonder og dashboard</a></td><td>Små testprogrammer og et live-dashboard til cyklens Bluetooth-lydbro, der viser lydbuffere, signalstyrke og forbindelser under kørslen.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
</tbody>
</table>

### Bookingportal

<table>
<thead><tr><th width="190">Testopstilling</th><th>Funktion</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oprindelse</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Prøvebooking</a></td><td>Gennemgår en onlinebooking frem til det sidste trin og stopper, så trinene kan testes uden at lave en rigtig booking.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Testopstilling</th><th>Funktion</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oprindelse</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Animationstjek</a></td><td>Måler et animeret diagram, mens det afspilles, og tjekker, at delene flugter og ikke overlapper, ned til en brøkdel af en pixel.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den version" title="virker på den version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bygget af os" title="Bygget af os" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

En mere teknisk version, skrevet til at blive indlæst i Claude, er [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) på GitHub.
