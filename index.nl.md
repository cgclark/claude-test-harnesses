# Geautomatiseerde testharnassen voor Claude

<details class="langs" data-current="nl">
<summary>Taal</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · **Nederlands** · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Manieren waarop Claude Code zijn eigen werk kan controleren: de app draaien, iets vastleggen dat het kan lezen en bepalen of het slaagt of faalt voordat iemand ernaar hoeft te kijken. Elke naam opent een pagina met het volledige recept. De harnaspagina's zelf zijn in het Engels.

<img class="c" src="icons/claude-code.svg" alt="Aanbevolen door Claude" title="Aanbevolen door Claude" width="16" height="16"> **Aanbevolen door Claude**: een standaardtool, ongewijzigd gebruikt (8)<br>
<img class="c" src="icons/claude-code.svg" alt="Aanbevolen door Claude, uitgebreid" title="Aanbevolen door Claude, uitgebreid" width="16" height="16"><img class="o" src="icons/plus.png" alt="Aanbevolen door Claude, uitgebreid" title="Aanbevolen door Claude, uitgebreid" width="16" height="16"> **Aanbevolen door Claude, uitgebreid**: een standaardtool die we moesten aanvullen voordat hij werkte (4)<br>
<img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"> **Door ons gebouwd**: een methode die we zelf moesten uitzoeken (30)

<img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"> werkt op die versie · <img class="o t" src="icons/square.png" alt="nog niet bevestigd" title="nog niet bevestigd" width="16" height="16"> nog niet bevestigd · <img class="o t" src="icons/xmark.square.png" alt="werkt daar nog niet" title="werkt daar nog niet" width="16" height="16"> werkt daar nog niet

Testharnassen die niet van de OS-versie afhangen, tellen als werkend op beide. De rest is afgevinkt op basis van het laatste gebruik; deze Mac is op 2 oktober 2026 overgestapt op 27, en een controle per testharnas tegen de architectuur van 27 moet nog komen.

**Uit**: de app waarin elk testharnas het eerst is gebouwd

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/big-top.png" alt="" width="20" height="20"> Big Top</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Apps op simulators, Macs & apparaten

<table class="wide">
<thead><tr><th width="190">Testharnas</th><th>Functie</th><th width="60">Uit</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oorsprong</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Simulator op de achtergrond</a></td><td>Claude bouwt een iPhone-app, draait die op de achtergrond in de simulator en maakt zelf screenshots en logs, zodat het een scherm kan controleren zonder het jouwe over te nemen.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Aanbevolen door Claude, uitgebreid" title="Aanbevolen door Claude, uitgebreid" width="16" height="16"><img class="o" src="icons/plus.png" alt="Aanbevolen door Claude, uitgebreid" title="Aanbevolen door Claude, uitgebreid" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Layoutmeting</a></td><td>Claude meet wat er werkelijk op het scherm is opgebouwd, zoals balkhoogtes en scrollposities, moment voor moment terwijl je tussen schermen wisselt, zodat het kan vinden waarom iets er verkeerd uitziet in plaats van te gokken.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Opstartschakelaars</a></td><td>Verborgen schakelaars in testbuilds die een app direct op een gekozen scherm met voorbeeldgegevens openen, zodat Claude elk scherm kan bereiken zonder door de app te tikken.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">iPad-app op de Mac</a></td><td>Draait de iPad-versie van een app als gewone Mac-app, zodat Claude die op de Mac kan testen met de logs en screenshots van het venster.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Aanbevolen door Claude, uitgebreid" title="Aanbevolen door Claude, uitgebreid" width="16" height="16"><img class="o" src="icons/plus.png" alt="Aanbevolen door Claude, uitgebreid" title="Aanbevolen door Claude, uitgebreid" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript en schermopname</a></td><td>Als Claude het scherm niet rechtstreeks kan bedienen, stuurt het Mac-apps aan met AppleScript en fotografeert het alleen hun venster om het resultaat te zien.</td></tr>
<tr><td><a href="unit-test-suites.md">Unittests</a></td><td>Automatische tests van de interne logica van een app, zoals scores, routes en wachtrijen, die in enkele seconden draaien zonder de app te openen.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Aanbevolen door Claude" title="Aanbevolen door Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Checklist voor mensen</a></td><td>Eén doorlopende lijst van de controles die alleen een mens kan doen, zoals de headset opzetten of een echte telefoon gebruiken, zodat de rest van het werk daar niet op hoeft te wachten.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Elk doel bouwen</a></td><td>Bouwt na een wijziging de iPhone-, Mac- en Vision Pro-versie samen opnieuw, en controleert dat testinstellingen nooit in de eigen instellingen van een speler worden opgeslagen.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">SwiftUI-livevoorvertoning</a></td><td>Toont één scherm in de livevoorvertoning van Xcode en fotografeert het, zodat Claude een layoutwijziging kan controleren zonder de hele game te bouwen en te starten.</td><td class="m"><img class="o t" src="icons/square.png" alt="nog niet bevestigd" title="nog niet bevestigd" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Tikken via toegankelijkheid</a></td><td>Tikt in de simulator op knoppen op de posities die de app zelf doorgeeft, in plaats van aan de hand van een screenshot te raden waar ze zitten.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Aanbevolen door Claude" title="Aanbevolen door Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Twee simulators als twee mensen</a></td><td>Draait de app op twee gesimuleerde iPhones als twee verschillende mensen, zodat uitnodigingen, uitdagingen en synchronisatie getest kunnen worden zonder twee echte telefoons.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="nog niet bevestigd" title="nog niet bevestigd" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Elk scherm in elke taal</a></td><td>Fotografeert elk hoofdscherm in elke taal, plus een verzonnen taal met extra lange woorden, op één vel, zodat tekst die niet past makkelijk opvalt.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Crashrapporten</a></td><td>Haalt het crashrapport van een echte iPhone en leest het, zodat een crash die alleen op de telefoon gebeurt een benoemde oorzaak krijgt.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="nog niet bevestigd" title="nog niet bevestigd" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Aanbevolen door Claude" title="Aanbevolen door Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Kleine testsuite</a></td><td>Een kleine, zelfstandige set automatische controles voor een Python-tool, die overal draait zonder iets te installeren.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td></tr>
</tbody>
</table>

## Graphics & games

<table class="wide">
<thead><tr><th width="190">Testharnas</th><th>Functie</th><th width="60">Uit</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oorsprong</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Gameconsole aansturen</a></td><td>Stuurt vanuit een script opdrachten naar de ingebouwde console van de game en leest daarna het log, in plaats van in het gamevenster te typen.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Frames voor en na</a></td><td>Speelt dezelfde opgenomen gameclip af voor en na een grafische wijziging en vergelijkt de frames pixel voor pixel.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Raytracing op de Mac</a></td><td>Testweergaven die elke stap van de geraytracete belichting (schaduwen, reflecties, omgevingslicht) apart tonen, plus zelftests die geslaagd of mislukt melden.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Pro-screenshots</a></td><td>Legt vast wat de Vision Pro-app laat zien, inclusief het beeld van elk oog in 3D, in de simulator en op de headset.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="nog niet bevestigd" title="nog niet bevestigd" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Aanbevolen door Claude, uitgebreid" title="Aanbevolen door Claude, uitgebreid" width="16" height="16"><img class="o" src="icons/plus.png" alt="Aanbevolen door Claude, uitgebreid" title="Aanbevolen door Claude, uitgebreid" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Shaders offline compileren</a></td><td>Compileert de grafische raytracingcode op de Mac, omdat de simulator die overslaat en fouten anders pas op een apparaat zouden opduiken.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPU-framecapture</a></td><td>Legt één frame vast op de grafische chip en toont wat elke tekenstap kostte, om te vinden wat traag is.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="nog niet bevestigd" title="nog niet bevestigd" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Aanbevolen door Claude" title="Aanbevolen door Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Shaderwiskunde</a></td><td>Herberekent de rook- en vuureffecten van Quake 3 langzaam en exact, en controleert of de snelle grafische versie hetzelfde beeld tekent.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
</tbody>
</table>

## Spraak, taal & data

<table class="wide">
<thead><tr><th width="190">Testharnas</th><th>Functie</th><th width="60">Uit</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oorsprong</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Screenshots naar tekst</a></td><td>Zet screenshots en scans op de Mac om in tekst voordat Claude ze leest, wat afbeeldingen privé houdt en veel minder van Claudes geheugen gebruikt.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m" rowspan="8"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>De Mac spreekt testzinnen met synthetische stemmen in de spraakherkenning van de app in, zodat spraakopdrachten getest kunnen worden zonder dat iemand praat.</td><td class="app-c"><img class="app-sm" src="icons/apps/big-top.png" alt="Big Top" title="Big Top" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="nog niet bevestigd" title="nog niet bevestigd" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td></tr>
<tr><td><a href="siri-phrasing-check.md">Siri-formuleringen</a></td><td>Controleert of de zinnen die voor Siri in de app zijn ingebouwd, zoals &quot;order my usual&quot;, overeenkomen met wat mensen zeggen; of Siri ze goed doorstuurt, kan nog alleen op de telefoon worden gecontroleerd.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Referentiesnapshot</a></td><td>Slaat de volledige uitvoer van de app op vóór een herschrijving en controleert daarna of de herschreven versie precies dezelfde uitvoer geeft.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="nog niet bevestigd" title="nog niet bevestigd" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Transcriptienauwkeurigheid</a></td><td>Laat de spraak-naar-tekst van de app los op openbare opnames met correcte transcripties en scoort hoeveel tekens er fout gaan.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Vertaalcontroles</a></td><td>Controleert of elke vertaling haar namen, getallen en afgesproken termen behoudt, en of er geen schermtekst onvertaald is gebleven. Ook gebruikt voor Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Echte gegevens</a></td><td>Test routeherkenning op een set echt opgenomen ritten in plaats van verzonnen ritten, wat bugs aan het licht bracht die de verzonnen tests hadden gemist.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="nog niet bevestigd" title="nog niet bevestigd" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Gelijk aan de originele app</a></td><td>Vergelijkt de database in onze iPad-versie met die van de originele Windows-app, tabel voor tabel en rij voor rij.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td></tr>
</tbody>
</table>

## Hardware, netwerken & diensten

<table class="wide">
<thead><tr><th width="190">Testharnas</th><th>Functie</th><th width="60">Uit</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oorsprong</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Vergelijken met een bewezen apparaat</a></td><td>Legt vast hoe een bewezen goed werkende opstelling zich gedraagt (de iPhone die rechtstreeks met de oordopjes praat) en vergelijkt een opname van onze bridge daarmee.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetooth-opnames</a></td><td>Neemt het Bluetooth-verkeer zelf op, om te zien wat de apparaten echt verstuurden in plaats van wat ze meldden.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Aanbevolen door Claude" title="Aanbevolen door Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Statuscontroles</a></td><td>Controleert of elke webservice vanaf het internet antwoordt, en of de route die geblokkeerd hoort te zijn wordt geweigerd.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Testharnas</th><th>Functie</th><th width="60">Uit</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oorsprong</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Browser aansturen</a></td><td>Claude opent pagina&#x27;s in een browser, vult formulieren in en leest het resultaat, om te controleren of een site werkt en er goed uitziet.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Aanbevolen door Claude" title="Aanbevolen door Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Controle na websiterelease</a></td><td>Controleert na een website-update of elk bestand intact op de server is aangekomen, en daarna de layout op telefoon-, tablet- en desktopbreedte.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Projectspecifiek (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Testharnas</th><th>Functie</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oorsprong</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Gamemods</a></td><td>Laadt elke populaire multiplayermod in onze versie van de game, start een map en controleert het log op fouten.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="nog niet bevestigd" title="nog niet bevestigd" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Naast het origineel</a></td><td>Neemt dezelfde scène op in onze versie en in de originele game, naast elkaar, om elk verschil te laten zien.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="nog niet bevestigd" title="nog niet bevestigd" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Levelscreenshots</a></td><td>Maakt een afbeelding van elke map vanuit de camerahoek die de maker van de map koos, en zet ze samen op één vel.</td></tr>
</tbody>
</table>

### Gebarentaalwerk

<table>
<thead><tr><th width="190">Testharnas</th><th>Functie</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oorsprong</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Bewegingsvergelijking</a></td><td>Speelt een computergegenereerde gebarende hand af naast de echte gebaarder op wie die is gebaseerd, frame voor frame, om te controleren of de beweging overeenkomt.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Testharnas</th><th>Functie</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oorsprong</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Geciteerde waarden controleren</a></td><td>Controleert, voordat Claude een datum of getal uit een document citeert, of de exacte tekst echt in dat document staat.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger Bluetooth-bridge

<table>
<thead><tr><th width="190">Testharnas</th><th>Functie</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oorsprong</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Bridge-tests en dashboard</a></td><td>Kleine testprogramma&#x27;s en een live dashboard voor de Bluetooth-audiobridge van de fiets, met geluidsbuffers, signaalsterkte en verbindingen tijdens het rijden.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
</tbody>
</table>

### Boekingsportaal

<table>
<thead><tr><th width="190">Testharnas</th><th>Functie</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oorsprong</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Proefboeking</a></td><td>Doorloopt een onlineboeking tot de laatste stap en stopt dan, zodat de stappen getest kunnen worden zonder een echte boeking te maken.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Testharnas</th><th>Functie</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Oorsprong</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Animatiecontrole</a></td><td>Meet een geanimeerd diagram terwijl het afspeelt en controleert tot op een fractie van een pixel of de onderdelen aansluiten en niet overlappen.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="werkt op die versie" title="werkt op die versie" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Door ons gebouwd" title="Door ons gebouwd" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Een technischere versie, geschreven om in Claude te laden, is de [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) op GitHub.
