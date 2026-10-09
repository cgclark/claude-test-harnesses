# Automatiska testriggar för Claude

<details class="langs" data-current="sv">
<summary>Språk</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · **Svenska** · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Sätt för Claude Code att kontrollera sitt eget arbete: köra appen, fånga något den kan läsa och avgöra godkänt eller underkänt innan en människa behöver titta. Varje namn öppnar en sida med hela receptet. Själva sidorna om testriggarna är på engelska.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Rekommenderat av Claude" title="Rekommenderat av Claude" width="16" height="16"></td><td><b>Rekommenderat av Claude</b>: ett standardverktyg som används som det är</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Rekommenderat av Claude, utökat" title="Rekommenderat av Claude, utökat" width="16" height="16"><img class="o" src="icons/plus.png" alt="Rekommenderat av Claude, utökat" title="Rekommenderat av Claude, utökat" width="16" height="16"></td><td><b>Rekommenderat av Claude, utökat</b>: ett standardverktyg som vi fick bygga på innan det fungerade</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td><td><b>Byggt av oss</b>: en metod som vi fick ta fram själva</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"> fungerar på den versionen · <img class="o t" src="icons/square.png" alt="inte bekräftat än" title="inte bekräftat än" width="16" height="16"> inte bekräftat än · <img class="o t" src="icons/xmark.square.png" alt="fungerar inte där än" title="fungerar inte där än" width="16" height="16"> fungerar inte där än

Testriggar som inte beror på OS-versionen räknas som fungerande på båda. Resten är markerade utifrån när var och en senast användes; den här Macen gick över till 27 den 2 oktober 2026, och en kontroll av var och en mot 27-arkitekturen återstår.

**Från**: appen som varje testrigg först byggdes i

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Appar på simulatorer, Macar & enheter

<table class="wide">
<thead><tr><th width="190">Testrigg</th><th>Funktion</th><th width="60">Från</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Ursprung</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Simulator i bakgrunden</a></td><td>Claude bygger en iPhone-app, kör den i simulatorn i bakgrunden och tar egna skärmbilder och loggar, så att den kan kontrollera en skärm utan att ta över din.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Rekommenderat av Claude, utökat" title="Rekommenderat av Claude, utökat" width="16" height="16"><img class="o" src="icons/plus.png" alt="Rekommenderat av Claude, utökat" title="Rekommenderat av Claude, utökat" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Layoutsond</a></td><td>Claude mäter vad skärmen faktiskt lade ut, som höjder på fält och rullningspositioner, ögonblick för ögonblick medan du går mellan skärmar, så att den kan hitta varför något ser fel ut i stället för att gissa.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Startargumentkrokar</a></td><td>Dolda växlar i testbyggen som öppnar en app direkt på en vald skärm med exempeldata, så att Claude kan nå vilken skärm som helst utan att trycka sig igenom appen.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">iPad-app på Macen</a></td><td>Kör iPad-versionen av en app som en vanlig Mac-app, så att Claude kan testa den på Macen med dess loggar och skärmbilder av fönstret.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Rekommenderat av Claude, utökat" title="Rekommenderat av Claude, utökat" width="16" height="16"><img class="o" src="icons/plus.png" alt="Rekommenderat av Claude, utökat" title="Rekommenderat av Claude, utökat" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript och skärmbilder</a></td><td>När Claude inte kan styra skärmen direkt styr den Mac-appar med AppleScript och fotograferar bara deras fönster för att se resultatet.</td></tr>
<tr><td><a href="unit-test-suites.md">Enhetstester</a></td><td>Automatiska tester av en apps interna logik, som poängräkning, rutter och köer, som körs på några sekunder utan att appen öppnas.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Rekommenderat av Claude" title="Rekommenderat av Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Checklista endast för människor</a></td><td>En löpande lista över de kontroller som bara en människa kan göra, som att bära headsetet eller använda en riktig telefon, så att resten av arbetet inte behöver vänta på dem.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Bygg alla targets</a></td><td>Bygger om iPhone-, Mac- och Vision Pro-versionerna tillsammans efter en ändring och kontrollerar att testinställningar aldrig sparas i en spelares egna inställningar.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Live-förhandsvisning i SwiftUI</a></td><td>Visar en skärm i Xcodes live-förhandsvisning och fotograferar den, så att Claude kan kontrollera en layoutändring utan att bygga och köra hela spelet.</td><td class="m"><img class="o t" src="icons/square.png" alt="inte bekräftat än" title="inte bekräftat än" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Tryck via tillgänglighet</a></td><td>Trycker på knappar i simulatorn på de positioner som appen själv rapporterar, i stället för att gissa var de finns utifrån en skärmbild.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Rekommenderat av Claude" title="Rekommenderat av Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Två simulatorer som två personer</a></td><td>Kör appen på två simulerade iPhones som två olika personer, så att inbjudningar, utmaningar och synkronisering kan testas utan två riktiga telefoner.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="inte bekräftat än" title="inte bekräftat än" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Varje skärm på varje språk</a></td><td>Fotograferar varje huvudskärm på varje språk, plus ett påhittat språk med extra långa ord, på ett ark, så att text som inte får plats är lätt att upptäcka.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Kraschrapporter</a></td><td>Hämtar kraschrapporten från en riktig iPhone och läser den, så att en krasch som bara händer på telefonen får en namngiven orsak.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="inte bekräftat än" title="inte bekräftat än" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Rekommenderat av Claude" title="Rekommenderat av Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Liten testsvit</a></td><td>En liten, fristående uppsättning automatiska kontroller för ett Python-verktyg, som körs var som helst utan att något behöver installeras.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td></tr>
</tbody>
</table>

## Grafik & spel

<table class="wide">
<thead><tr><th width="190">Testrigg</th><th>Funktion</th><th width="60">Från</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Ursprung</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Styrning av spelkonsolen</a></td><td>Skickar kommandon till spelets inbyggda konsol från ett skript och läser dess logg efteråt, i stället för att skriva i spelfönstret.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Före- och efterbilder</a></td><td>Spelar upp samma inspelade spelklipp före och efter en grafikändring och jämför bildrutorna pixel för pixel.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Ray tracing på Macen</a></td><td>Testvyer som visar varje steg i den strålspårade belysningen (skuggor, reflexer, omgivningsljus) för sig, plus självkontroller som skriver ut godkänt eller underkänt.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Pro-skärmbilder</a></td><td>Fångar vad Vision Pro-appen visar, inklusive varje ögas vy i 3D, i simulatorn och i headsetet.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="inte bekräftat än" title="inte bekräftat än" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Rekommenderat av Claude, utökat" title="Rekommenderat av Claude, utökat" width="16" height="16"><img class="o" src="icons/plus.png" alt="Rekommenderat av Claude, utökat" title="Rekommenderat av Claude, utökat" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Offlinekompilering av shaders</a></td><td>Kompilerar grafikkoden för ray tracing på Macen, eftersom simulatorn hoppar över den och fel annars bara skulle synas på en enhet.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPU-bildrutefångst</a></td><td>Fångar en bildruta på grafikkretsen och listar vad varje ritsteg kostade, för att hitta det som är långsamt.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="inte bekräftat än" title="inte bekräftat än" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Rekommenderat av Claude" title="Rekommenderat av Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Shadermatematik</a></td><td>Räknar om Quake 3:s rök- och eldeffekter långsamt och exakt och kontrollerar att den snabba grafikversionen ritar samma bild.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
</tbody>
</table>

## Röst, språk & data

<table class="wide">
<thead><tr><th width="190">Testrigg</th><th>Funktion</th><th width="60">Från</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Ursprung</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Skärmbilder till text</a></td><td>Omvandlar skärmbilder och skanningar till text på Macen innan Claude läser dem, vilket håller bilderna privata och använder mycket mindre av Claudes minne.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Macen talar testfraser med syntetiska röster in i appens taligenkänning, så att röstkommandon kan testas utan att någon pratar.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="inte bekräftat än" title="inte bekräftat än" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Ljuduppspelning på en enhet</a></td><td>Macen gör om varje testsamtal till en ljudfil som appen på telefonen lyssnar på i stället för mikrofonen, så att röstfunktioner kan testas på den riktiga telefonen utan att någon pratar.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Siri-fraser</a></td><td>Kontrollerar att fraserna som är inbyggda i appen för Siri, som &quot;order my usual&quot;, stämmer med vad folk säger; om Siri dirigerar dem rätt kräver fortfarande telefonen.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Referensögonblicksbild</a></td><td>Sparar appens fullständiga utdata före en omskrivning och kontrollerar sedan att den omskrivna versionen ger exakt samma utdata.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="inte bekräftat än" title="inte bekräftat än" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Transkriberingsnoggrannhet</a></td><td>Kör appens tal-till-text på offentliga inspelningar som har korrekta transkriptioner och mäter hur många tecken den får fel.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Översättningskontroller</a></td><td>Kontrollerar att varje översättning behåller sina namn, siffror och överenskomna termer, och att ingen text på skärmen har lämnats oöversatt. Används även för Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Riktiga data</a></td><td>Testar ruttmatchning på en uppsättning riktiga inspelade turer i stället för påhittade, vilket hittade buggar som de påhittade testerna hade missat.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="inte bekräftat än" title="inte bekräftat än" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Matcha originalappen</a></td><td>Jämför databasen i vår iPad-version med den från den ursprungliga Windows-appen, tabell för tabell och rad för rad.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td></tr>
</tbody>
</table>

## Hårdvara, nätverk & tjänster

<table class="wide">
<thead><tr><th width="190">Testrigg</th><th>Funktion</th><th width="60">Från</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Ursprung</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Jämför med en enhet som fungerar</a></td><td>Spelar in hur en uppsättning som man vet fungerar beter sig (iPhonen som pratar direkt med hörlurarna) och jämför en inspelning av vår brygga med den.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetooth-inspelningar</a></td><td>Spelar in själva Bluetooth-trafiken, för att se vad enheterna faktiskt skickade i stället för vad de rapporterade.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Rekommenderat av Claude" title="Rekommenderat av Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Hälsokontroller</a></td><td>Kontrollerar att varje webbtjänst svarar från internet och att den rutt som ska vara blockerad nekas.</td></tr>
</tbody>
</table>

## Webb

<table class="wide">
<thead><tr><th width="190">Testrigg</th><th>Funktion</th><th width="60">Från</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Ursprung</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Webbläsarstyrning</a></td><td>Claude öppnar sidor i en webbläsare, fyller i formulär och läser resultatet, för att kontrollera att en webbplats fungerar och ser rätt ut.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Rekommenderat av Claude" title="Rekommenderat av Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Kontroll av webbplatsdriftsättning</a></td><td>Efter en uppdatering av en webbplats kontrolleras att varje fil kom fram oskadd till servern, och sedan kontrolleras layouten i mobil-, surfplatte- och datorbredd.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Projektspecifika (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Testrigg</th><th>Funktion</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Ursprung</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Spelmoddar</a></td><td>Läser in varje populär multiplayer-modd i vår version av spelet, startar en bana och söker efter fel i loggen.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="inte bekräftat än" title="inte bekräftat än" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Sida vid sida med originalet</a></td><td>Spelar in samma scen i vår version och i originalspelet, sida vid sida, för att visa eventuella skillnader.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="inte bekräftat än" title="inte bekräftat än" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Skärmbilder av banor</a></td><td>Tar en bild av varje bana från den kameravinkel som banans skapare valde och lägger ut dem på ett ark.</td></tr>
</tbody>
</table>

### Teckenspråksarbete

<table>
<thead><tr><th width="190">Testrigg</th><th>Funktion</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Ursprung</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Rörelsejämförelse</a></td><td>Spelar upp en datorgenererad tecknande hand bredvid den riktiga teckenspråkstalare den skapades från, bildruta för bildruta, för att kontrollera att rörelsen stämmer.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Testrigg</th><th>Funktion</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Ursprung</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Kontrollera citerade värden</a></td><td>Innan Claude citerar ett datum eller en siffra ur ett dokument kontrolleras att exakt den texten verkligen finns i dokumentet.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger Bluetooth-brygga

<table>
<thead><tr><th width="190">Testrigg</th><th>Funktion</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Ursprung</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Bryggsonder och instrumentpanel</a></td><td>Små testprogram och en liveinstrumentpanel för cykelns Bluetooth-ljudbrygga, som visar ljudbuffertar, signalstyrka och anslutningar under turen.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
</tbody>
</table>

### Bokningsportal

<table>
<thead><tr><th width="190">Testrigg</th><th>Funktion</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Ursprung</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Provbokning</a></td><td>Går igenom en onlinebokning fram till sista steget och stannar, så att stegen kan testas utan att en riktig bokning görs.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Testrigg</th><th>Funktion</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Ursprung</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Animationskontroll</a></td><td>Mäter ett animerat diagram medan det spelas upp och kontrollerar att delarna linjerar och inte överlappar, ner till en bråkdel av en pixel.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fungerar på den versionen" title="fungerar på den versionen" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Byggt av oss" title="Byggt av oss" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

En mer teknisk version, skriven för att läsas in i Claude, är [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) på GitHub.
