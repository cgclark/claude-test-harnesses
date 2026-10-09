# Automatiske testrigger for Claude

<details class="langs" data-current="nb">
<summary>Språk</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · **Norsk bokmål** · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Måter Claude Code kan sjekke sitt eget arbeid på: kjøre appen, fange noe den kan lese, og avgjøre bestått eller ikke bestått før et menneske må se på det. Hvert navn åpner en side med hele oppskriften. Selve sidene om testriggene er på engelsk.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Anbefalt av Claude" title="Anbefalt av Claude" width="16" height="16"></td><td><b>Anbefalt av Claude</b>: et standardverktøy brukt som det er</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Anbefalt av Claude, utvidet" title="Anbefalt av Claude, utvidet" width="16" height="16"><img class="o" src="icons/plus.png" alt="Anbefalt av Claude, utvidet" title="Anbefalt av Claude, utvidet" width="16" height="16"></td><td><b>Anbefalt av Claude, utvidet</b>: et standardverktøy vi måtte bygge videre på før det virket</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td><td><b>Laget av oss</b>: en metode vi måtte finne ut av selv</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"> virker på den versjonen · <img class="o t" src="icons/square.png" alt="ikke bekreftet ennå" title="ikke bekreftet ennå" width="16" height="16"> ikke bekreftet ennå · <img class="o t" src="icons/xmark.square.png" alt="virker ikke der ennå" title="virker ikke der ennå" width="16" height="16"> virker ikke der ennå

Testrigger som ikke avhenger av OS-versjonen, regnes som virkende på begge. Resten er krysset av ut fra når hver av dem sist ble brukt; denne Mac-en gikk over til 27 den 2. oktober 2026, og en gjennomgang én for én mot 27-arkitekturen gjenstår.

**Fra**: appen hver testrigg først ble laget i

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Apper på simulatorer, Mac-er & enheter

<table class="wide">
<thead><tr><th width="190">Testrigg</th><th>Funksjon</th><th width="60">Fra</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Opprinnelse</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Simulator i bakgrunnen</a></td><td>Claude bygger en iPhone-app, kjører den i simulatoren i bakgrunnen og tar egne skjermbilder og logger, slik at den kan sjekke en skjerm uten å ta over din.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Anbefalt av Claude, utvidet" title="Anbefalt av Claude, utvidet" width="16" height="16"><img class="o" src="icons/plus.png" alt="Anbefalt av Claude, utvidet" title="Anbefalt av Claude, utvidet" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Layoutsonde</a></td><td>Claude måler hva skjermen faktisk la ut, som høyden på linjer og rulleposisjoner, øyeblikk for øyeblikk mens du går mellom skjermer, slik at den kan finne ut hvorfor noe ser feil ut i stedet for å gjette.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Startargument-kroker</a></td><td>Skjulte brytere i testbygg som åpner en app rett på en valgt skjerm med eksempeldata, slik at Claude kan nå hvilken som helst skjerm uten å trykke seg gjennom appen.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">iPad-app på Mac-en</a></td><td>Kjører iPad-versjonen av en app som en vanlig Mac-app, slik at Claude kan teste den på Mac-en med loggene og skjermbilder av vinduet.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Anbefalt av Claude, utvidet" title="Anbefalt av Claude, utvidet" width="16" height="16"><img class="o" src="icons/plus.png" alt="Anbefalt av Claude, utvidet" title="Anbefalt av Claude, utvidet" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript og skjermopptak</a></td><td>Når Claude ikke kan styre skjermen direkte, styrer den Mac-apper med AppleScript og fotograferer bare vinduet deres for å se resultatet.</td></tr>
<tr><td><a href="unit-test-suites.md">Enhetstester</a></td><td>Automatiske tester av en apps interne logikk, som poengberegning, ruter og køer, som kjører på sekunder uten å åpne appen.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Anbefalt av Claude" title="Anbefalt av Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Sjekkliste bare for mennesker</a></td><td>Én løpende liste over sjekkene bare et menneske kan gjøre, som å ha på headsettet eller bruke en ekte telefon, slik at resten av arbeidet ikke venter på dem.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Bygg alle targets</a></td><td>Bygger iPhone-, Mac- og Vision Pro-versjonene på nytt samlet etter en endring, og sjekker at testinnstillinger aldri blir lagret i en spillers egne innstillinger.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Live-forhåndsvisning i SwiftUI</a></td><td>Viser én skjerm i Xcodes live-forhåndsvisning og fotograferer den, slik at Claude kan sjekke en layoutendring uten å bygge og kjøre hele spillet.</td><td class="m"><img class="o t" src="icons/square.png" alt="ikke bekreftet ennå" title="ikke bekreftet ennå" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Trykk via tilgjengelighet</a></td><td>Trykker på knapper i simulatoren der appen selv oppgir at de er, i stedet for å gjette hvor de er ut fra et skjermbilde.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Anbefalt av Claude" title="Anbefalt av Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">To simulatorer som to personer</a></td><td>Kjører appen på to simulerte iPhoner som to forskjellige personer, slik at invitasjoner, utfordringer og synkronisering kan testes uten to ekte telefoner.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="ikke bekreftet ennå" title="ikke bekreftet ennå" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Alle skjermer på alle språk</a></td><td>Fotograferer alle hovedskjermer på alle språk, pluss et oppdiktet språk med ekstra lange ord, på ett ark, slik at tekst som ikke får plass, er lett å oppdage.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Krasjrapporter</a></td><td>Henter krasjrapporten fra en ekte iPhone og leser den, slik at et krasj som bare skjer på telefonen, får en navngitt årsak.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ikke bekreftet ennå" title="ikke bekreftet ennå" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Anbefalt av Claude" title="Anbefalt av Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Liten testsuite</a></td><td>Et lite, selvstendig sett med automatiske sjekker for et Python-verktøy, som kjører hvor som helst uten at noe må installeres.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td></tr>
</tbody>
</table>

## Grafikk & spill

<table class="wide">
<thead><tr><th width="190">Testrigg</th><th>Funksjon</th><th width="60">Fra</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Opprinnelse</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Styring av spillkonsollen</a></td><td>Sender kommandoer til spillets innebygde konsoll fra et skript og leser loggen etterpå, i stedet for å skrive i spillvinduet.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Før- og etterbilder</a></td><td>Spiller av det samme innspilte spillklippet før og etter en grafikkendring og sammenligner bildene piksel for piksel.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Strålesporing på Mac-en</a></td><td>Testvisninger som viser hvert trinn i den strålesporede belysningen (skygger, refleksjoner, omgivelseslys) hver for seg, pluss selvsjekker som skriver ut bestått eller ikke bestått.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Pro-skjermbilder</a></td><td>Fanger det Vision Pro-appen viser, inkludert hvert øyes bilde i 3D, i simulatoren og på headsettet.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ikke bekreftet ennå" title="ikke bekreftet ennå" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Anbefalt av Claude, utvidet" title="Anbefalt av Claude, utvidet" width="16" height="16"><img class="o" src="icons/plus.png" alt="Anbefalt av Claude, utvidet" title="Anbefalt av Claude, utvidet" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Shaderkompilering offline</a></td><td>Kompilerer grafikkoden for strålesporing på Mac-en, fordi simulatoren hopper over den og feil ellers bare ville vist seg på en enhet.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPU-bildeopptak</a></td><td>Fanger ett bilde på grafikkbrikken og lister opp hva hvert tegnetrinn kostet, for å finne det som er tregt.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="ikke bekreftet ennå" title="ikke bekreftet ennå" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Anbefalt av Claude" title="Anbefalt av Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Shadermatematikk</a></td><td>Regner ut Quake 3s røyk- og ildeffekter på nytt, sakte og nøyaktig, og sjekker at den raske grafikkversjonen tegner det samme bildet.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
</tbody>
</table>

## Stemme, språk & data

<table class="wide">
<thead><tr><th width="190">Testrigg</th><th>Funksjon</th><th width="60">Fra</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Opprinnelse</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Skjermbilder til tekst</a></td><td>Gjør skjermbilder og skanninger om til tekst på Mac-en før Claude leser dem, noe som holder bildene private og bruker langt mindre av Claudes minne.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac-en sier testfraser med syntetiske stemmer inn i appens talegjenkjenning, slik at talekommandoer kan testes uten at noen snakker.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ikke bekreftet ennå" title="ikke bekreftet ennå" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Lydavspilling på en enhet</a></td><td>Mac-en gjør hver testsamtale om til en lydfil, og appen på telefonen lytter til den i stedet for mikrofonen, slik at talefunksjoner kan testes på den ekte telefonen uten at noen snakker.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Siri-formuleringer</a></td><td>Sjekker at frasene som er bygget inn i appen for Siri, som &quot;order my usual&quot;, stemmer med det folk sier; om Siri sender dem riktig vei, krever fortsatt telefonen.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Referanseøyeblikksbilde</a></td><td>Lagrer appens fullstendige utdata før en omskriving, og sjekker deretter at den omskrevne versjonen gir nøyaktig samme utdata.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ikke bekreftet ennå" title="ikke bekreftet ennå" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Transkripsjonsnøyaktighet</a></td><td>Kjører appens tale-til-tekst på offentlige opptak som har korrekte transkripsjoner, og måler hvor mange tegn den får feil.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Oversettelsessjekker</a></td><td>Sjekker at hver oversettelse beholder navn, tall og avtalte termer, og at ingen tekst på skjermen er latt være uoversatt. Brukes også for Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Ekte data</a></td><td>Tester rutematching på et sett ekte innspilte turer i stedet for oppdiktede, noe som fant feil de oppdiktede testene hadde oversett.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ikke bekreftet ennå" title="ikke bekreftet ennå" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Samsvar med originalappen</a></td><td>Sammenligner databasen i vår iPad-versjon med den fra den opprinnelige Windows-appen, tabell for tabell og rad for rad.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td></tr>
</tbody>
</table>

## Maskinvare, nettverk & tjenester

<table class="wide">
<thead><tr><th width="190">Testrigg</th><th>Funksjon</th><th width="60">Fra</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Opprinnelse</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Sammenlign med en enhet som virker</a></td><td>Tar opp hvordan et oppsett som er kjent for å virke, oppfører seg (iPhonen som snakker direkte med øreproppene), og sammenligner et opptak av broen vår med det.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetooth-opptak</a></td><td>Tar opp selve Bluetooth-trafikken, for å se hva enhetene faktisk sendte i stedet for hva de rapporterte.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Anbefalt av Claude" title="Anbefalt av Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Helsesjekker</a></td><td>Sjekker at hver webtjeneste svarer fra internett, og at ruten som skal være blokkert, blir avvist.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Testrigg</th><th>Funksjon</th><th width="60">Fra</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Opprinnelse</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Nettleserstyring</a></td><td>Claude åpner sider i en nettleser, fyller ut skjemaer og leser resultatet, for å sjekke at et nettsted virker og ser riktig ut.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Anbefalt av Claude" title="Anbefalt av Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Sjekk av nettstedsutrulling</a></td><td>Etter en oppdatering av et nettsted sjekkes det at hver fil kom uskadd fram til serveren, og deretter sjekkes layouten i telefon-, nettbrett- og skrivebordsbredde.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Prosjektspesifikke (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Testrigg</th><th>Funksjon</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Opprinnelse</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Spillmoder</a></td><td>Laster hver populær flerspillermod inn i vår versjon av spillet, starter et brett og sjekker loggen for feil.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="ikke bekreftet ennå" title="ikke bekreftet ennå" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Side om side med originalen</a></td><td>Tar opp den samme scenen i vår versjon og i originalspillet, side om side, for å vise eventuelle forskjeller.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ikke bekreftet ennå" title="ikke bekreftet ennå" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Skjermbilder av brett</a></td><td>Tar et bilde av hvert brett fra kameravinkelen brettets skaper valgte, og legger dem ut på ett ark.</td></tr>
</tbody>
</table>

### Tegnspråkarbeid

<table>
<thead><tr><th width="190">Testrigg</th><th>Funksjon</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Opprinnelse</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Bevegelsessammenligning</a></td><td>Spiller av en datagenerert tegnende hånd ved siden av den ekte tegnspråkbrukeren den ble laget fra, bilde for bilde, for å sjekke at bevegelsen stemmer.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Testrigg</th><th>Funksjon</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Opprinnelse</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Sjekk siterte verdier</a></td><td>Før Claude siterer en dato eller et tall fra et dokument, sjekkes det at den nøyaktige teksten virkelig står i dokumentet.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger Bluetooth-bro

<table>
<thead><tr><th width="190">Testrigg</th><th>Funksjon</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Opprinnelse</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Brosonder og dashbord</a></td><td>Små testprogrammer og et live-dashbord for sykkelens Bluetooth-lydbro, som viser lydbuffere, signalstyrke og tilkoblinger mens man sykler.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
</tbody>
</table>

### Bookingportal

<table>
<thead><tr><th width="190">Testrigg</th><th>Funksjon</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Opprinnelse</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Prøvebestilling</a></td><td>Går gjennom en nettbestilling fram til siste trinn og stopper, slik at trinnene kan testes uten å gjøre en ekte bestilling.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Testrigg</th><th>Funksjon</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Opprinnelse</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Animasjonssjekk</a></td><td>Måler et animert diagram mens det spilles av, og sjekker at delene står på linje og ikke overlapper, ned til en brøkdel av en piksel.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="virker på den versjonen" title="virker på den versjonen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Laget av oss" title="Laget av oss" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

En mer teknisk versjon, skrevet for å lastes inn i Claude, er [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) på GitHub.
