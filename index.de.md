# Automatisierte Testumgebungen für Claude

<details class="langs" data-current="de">
<summary>Sprache</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · **Deutsch** · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Wege, wie Claude Code die eigene Arbeit prüft: die App starten, etwas erfassen, das es lesen kann, und über bestanden oder nicht bestanden entscheiden, bevor ein Mensch nachsehen muss. Jeder Name öffnet eine Seite mit der vollständigen Anleitung. Die Seiten zu den Testumgebungen selbst sind auf Englisch.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Von Claude empfohlen" title="Von Claude empfohlen" width="16" height="16"></td><td><b>Von Claude empfohlen</b>: ein Standardwerkzeug, unverändert genutzt</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Von Claude empfohlen, erweitert" title="Von Claude empfohlen, erweitert" width="16" height="16"><img class="o" src="icons/plus.png" alt="Von Claude empfohlen, erweitert" title="Von Claude empfohlen, erweitert" width="16" height="16"></td><td><b>Von Claude empfohlen, erweitert</b>: ein Standardwerkzeug, das wir ergänzen mussten, bevor es funktionierte</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td><td><b>Von uns gebaut</b>: eine Methode, die wir selbst entwickeln mussten</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"> funktioniert mit dieser Version · <img class="o t" src="icons/square.png" alt="noch nicht bestätigt" title="noch nicht bestätigt" width="16" height="16"> noch nicht bestätigt · <img class="o t" src="icons/xmark.square.png" alt="funktioniert dort noch nicht" title="funktioniert dort noch nicht" width="16" height="16"> funktioniert dort noch nicht

Testumgebungen, die nicht von der Betriebssystemversion abhängen, gelten für beide als funktionsfähig. Die übrigen sind nach ihrer letzten Nutzung abgehakt; dieser Mac wurde am 2. Oktober 2026 auf 27 umgestellt, und eine Prüfung jeder einzelnen gegen die Architektur von 27 steht noch aus.

**Aus**: die App, in der jede Testumgebung zuerst gebaut wurde

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Apps auf Simulatoren, Macs & Geräten

<table class="wide">
<thead><tr><th width="190">Testumgebung</th><th>Fähigkeit</th><th width="60">Aus</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Herkunft</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Simulator im Hintergrund</a></td><td>Claude baut eine iPhone-App, startet sie im Hintergrund im Simulator und erstellt selbst Screenshots und Logs, damit es einen Bildschirm prüfen kann, ohne Ihren zu übernehmen.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Von Claude empfohlen, erweitert" title="Von Claude empfohlen, erweitert" width="16" height="16"><img class="o" src="icons/plus.png" alt="Von Claude empfohlen, erweitert" title="Von Claude empfohlen, erweitert" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Layout-Sonde</a></td><td>Claude misst, was der Bildschirm tatsächlich angeordnet hat, etwa Leistenhöhen und Scrollpositionen, Moment für Moment, während Sie zwischen Bildschirmen wechseln, damit es die Ursache findet, wenn etwas falsch aussieht, statt zu raten.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Startargument-Hooks</a></td><td>Versteckte Schalter in Test-Builds, die eine App direkt auf einem gewählten Bildschirm mit Beispieldaten öffnen, damit Claude jeden Bildschirm erreicht, ohne sich durch die App zu tippen.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">iPad-App auf dem Mac</a></td><td>Führt die iPad-Version einer App als normale Mac-App aus, damit Claude sie auf dem Mac mit ihren Logs und Fenster-Screenshots testen kann.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Von Claude empfohlen, erweitert" title="Von Claude empfohlen, erweitert" width="16" height="16"><img class="o" src="icons/plus.png" alt="Von Claude empfohlen, erweitert" title="Von Claude empfohlen, erweitert" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript und Bildschirmaufnahme</a></td><td>Wenn Claude den Bildschirm nicht direkt steuern kann, bedient es Mac-Apps mit AppleScript und fotografiert nur ihr Fenster, um das Ergebnis zu sehen.</td></tr>
<tr><td><a href="unit-test-suites.md">Unit-Tests</a></td><td>Automatische Tests der internen Logik einer App, etwa Punktewertung, Routen und Warteschlangen, die in Sekunden laufen, ohne die App zu öffnen.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Von Claude empfohlen" title="Von Claude empfohlen" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Checkliste nur für Menschen</a></td><td>Eine fortlaufende Liste der Prüfungen, die nur ein Mensch machen kann, etwa das Headset aufsetzen oder ein echtes Telefon benutzen, damit die übrige Arbeit nicht darauf warten muss.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Jedes Ziel bauen</a></td><td>Baut nach einer Änderung die Versionen für iPhone, Mac und Vision Pro gemeinsam neu und prüft, dass Testeinstellungen nie in die eigenen Einstellungen eines Spielers gespeichert werden.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">SwiftUI-Live-Vorschau</a></td><td>Zeigt einen Bildschirm in der Live-Vorschau von Xcode und fotografiert ihn, damit Claude eine Layoutänderung prüfen kann, ohne das ganze Spiel zu bauen und zu starten.</td><td class="m"><img class="o t" src="icons/square.png" alt="noch nicht bestätigt" title="noch nicht bestätigt" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Tippen per Bedienungshilfen</a></td><td>Tippt im Simulator auf Tasten an den Positionen, die die App selbst meldet, statt anhand eines Screenshots zu raten, wo sie sind.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Von Claude empfohlen" title="Von Claude empfohlen" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Zwei Simulatoren als zwei Personen</a></td><td>Führt die App auf zwei simulierten iPhones als zwei verschiedene Personen aus, damit Einladungen, Herausforderungen und Synchronisierung ohne zwei echte Telefone getestet werden können.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="noch nicht bestätigt" title="noch nicht bestätigt" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Jeder Bildschirm in jeder Sprache</a></td><td>Fotografiert jeden Hauptbildschirm in jeder Sprache, dazu in einer erfundenen Sprache mit extralangen Wörtern, auf einem Blatt, damit Text, der nicht passt, leicht auffällt.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Absturzberichte</a></td><td>Holt den Absturzbericht von einem echten iPhone und liest ihn, damit ein Absturz, der nur auf dem Telefon passiert, eine benannte Ursache bekommt.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="noch nicht bestätigt" title="noch nicht bestätigt" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Von Claude empfohlen" title="Von Claude empfohlen" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Kleine Testsuite</a></td><td>Ein kleiner, eigenständiger Satz automatischer Prüfungen für ein Python-Werkzeug, der überall läuft, ohne etwas zu installieren.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td></tr>
</tbody>
</table>

## Grafik & Spiele

<table class="wide">
<thead><tr><th width="190">Testumgebung</th><th>Fähigkeit</th><th width="60">Aus</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Herkunft</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Spielkonsole steuern</a></td><td>Schickt Befehle aus einem Skript an die eingebaute Konsole des Spiels und liest danach sein Log, statt ins Spielfenster zu tippen.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="5"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Vorher-nachher-Bilder</a></td><td>Spielt denselben aufgezeichneten Spielclip vor und nach einer Grafikänderung ab und vergleicht die Bilder Pixel für Pixel.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Raytracing auf dem Mac</a></td><td>Testansichten, die jeden Schritt der Raytracing-Beleuchtung (Schatten, Spiegelungen, Umgebungslicht) einzeln zeigen, dazu Selbsttests, die bestanden oder nicht bestanden ausgeben.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Pro-Screenshots</a></td><td>Erfasst, was die Vision Pro-App zeigt, einschließlich der Ansicht jedes Auges in 3D, im Simulator und auf dem Headset.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Von Claude empfohlen, erweitert" title="Von Claude empfohlen, erweitert" width="16" height="16"><img class="o" src="icons/plus.png" alt="Von Claude empfohlen, erweitert" title="Von Claude empfohlen, erweitert" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Shader offline kompilieren</a></td><td>Kompiliert den Raytracing-Grafikcode auf dem Mac, weil der Simulator ihn überspringt und Fehler sonst erst auf einem Gerät auftauchen würden.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPU-Frame-Aufnahme</a></td><td>Nimmt ein Bild auf dem Grafikchip auf und listet auf, was jeder Zeichenschritt gekostet hat, um zu finden, was langsam ist.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="noch nicht bestätigt" title="noch nicht bestätigt" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Von Claude empfohlen" title="Von Claude empfohlen" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Shader-Mathematik</a></td><td>Berechnet die Rauch- und Feuereffekte von Quake 3 langsam und exakt nach und prüft, dass die schnelle Grafikversion dasselbe Bild zeichnet.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
</tbody>
</table>

## Stimme, Sprache & Daten

<table class="wide">
<thead><tr><th width="190">Testumgebung</th><th>Fähigkeit</th><th width="60">Aus</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Herkunft</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Screenshots zu Text</a></td><td>Wandelt Screenshots und Scans auf dem Mac in Text um, bevor Claude sie liest, was Bilder privat hält und weit weniger von Claudes Gedächtnis verbraucht.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Der Mac spricht Testsätze mit synthetischen Stimmen in die Spracherkennung der App, damit Sprachbefehle getestet werden können, ohne dass jemand spricht.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="noch nicht bestätigt" title="noch nicht bestätigt" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Audiowiedergabe auf einem Gerät</a></td><td>Der Mac macht aus jedem Testgespräch eine Audiodatei, und die App auf dem Telefon hört statt des Mikrofons diese Datei, damit Sprachfunktionen auf dem echten Telefon getestet werden können, ohne dass jemand spricht.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Siri-Formulierungen</a></td><td>Prüft, dass die in die App eingebauten Sätze für Siri, etwa „order my usual“, dem entsprechen, was Menschen sagen; ob Siri sie richtig weiterleitet, braucht weiterhin das Telefon.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Referenz-Snapshot</a></td><td>Speichert die vollständige Ausgabe der App vor einer Neufassung und prüft dann, dass die neu geschriebene Version genau dieselbe Ausgabe erzeugt.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="noch nicht bestätigt" title="noch nicht bestätigt" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Transkriptionsgenauigkeit</a></td><td>Lässt die Sprache-zu-Text-Funktion der App über öffentliche Aufnahmen laufen, zu denen korrekte Transkripte gehören, und bewertet, wie viele Zeichen sie falsch erkennt.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Übersetzungsprüfungen</a></td><td>Prüft, dass jede Übersetzung ihre Namen, Zahlen und vereinbarten Begriffe beibehält und dass kein Bildschirmtext unübersetzt geblieben ist. Wird auch für Quake 3 genutzt.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Echte Daten</a></td><td>Testet den Routenabgleich mit einer Reihe echter aufgezeichneter Fahrten statt erfundener, was Fehler fand, die die erfundenen Tests übersehen hatten.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="noch nicht bestätigt" title="noch nicht bestätigt" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Gleich wie die Original-App</a></td><td>Vergleicht die Datenbank in unserer iPad-Version mit der aus der ursprünglichen Windows-App, Tabelle für Tabelle und Zeile für Zeile.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td></tr>
</tbody>
</table>

## Hardware, Netzwerke & Dienste

<table class="wide">
<thead><tr><th width="190">Testumgebung</th><th>Fähigkeit</th><th width="60">Aus</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Herkunft</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Vergleich mit einem bewährten Gerät</a></td><td>Zeichnet auf, wie sich ein bewährter Aufbau verhält (das iPhone direkt mit den Ohrhörern verbunden), und vergleicht eine Aufnahme unserer Brücke damit.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetooth-Mitschnitte</a></td><td>Zeichnet den Bluetooth-Verkehr selbst auf, um zu sehen, was die Geräte tatsächlich gesendet haben, statt was sie gemeldet haben.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Von Claude empfohlen" title="Von Claude empfohlen" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Zustandsprüfungen</a></td><td>Prüft, dass jeder Webdienst aus dem Internet antwortet und dass die Route, die gesperrt sein soll, abgewiesen wird.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Testumgebung</th><th>Fähigkeit</th><th width="60">Aus</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Herkunft</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Browser steuern</a></td><td>Claude öffnet Seiten in einem Browser, füllt Formulare aus und liest das Ergebnis, um zu prüfen, dass eine Website funktioniert und richtig aussieht.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Von Claude empfohlen" title="Von Claude empfohlen" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Website-Deploy-Prüfung</a></td><td>Prüft nach einem Website-Update, dass jede Datei unbeschädigt auf dem Server angekommen ist, und dann das Layout in Telefon-, Tablet- und Desktop-Breite.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Projektspezifisch (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Testumgebung</th><th>Fähigkeit</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Herkunft</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Spiel-Mods</a></td><td>Lädt jede beliebte Mehrspieler-Mod in unsere Version des Spiels, startet eine Karte und prüft das Log auf Fehler.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="noch nicht bestätigt" title="noch nicht bestätigt" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Neben dem Original</a></td><td>Zeichnet dieselbe Szene in unserer Version und im Originalspiel nebeneinander auf, um jeden Unterschied zu zeigen.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="noch nicht bestätigt" title="noch nicht bestätigt" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Level-Screenshots</a></td><td>Macht ein Bild jeder Karte aus dem Kamerawinkel, den der Autor der Karte gewählt hat, und ordnet sie auf einem Blatt an.</td></tr>
</tbody>
</table>

### Gebärdensprach-Projekt

<table>
<thead><tr><th width="190">Testumgebung</th><th>Fähigkeit</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Herkunft</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Bewegungsvergleich</a></td><td>Spielt eine computergenerierte gebärdende Hand neben der echten gebärdenden Person ab, aus der sie erzeugt wurde, Bild für Bild, um zu prüfen, dass die Bewegung übereinstimmt.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Testumgebung</th><th>Fähigkeit</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Herkunft</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Zitierte Werte prüfen</a></td><td>Bevor Claude ein Datum oder eine Zahl aus einem Dokument zitiert, prüft es, dass genau dieser Text wirklich in dem Dokument steht.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger-Bluetooth-Brücke

<table>
<thead><tr><th width="190">Testumgebung</th><th>Fähigkeit</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Herkunft</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Brücken-Sonden und Dashboard</a></td><td>Kleine Testprogramme und ein Live-Dashboard für die Bluetooth-Audiobrücke am Fahrrad, die Tonpuffer, Signalstärke und Verbindungen während der Fahrt zeigen.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
</tbody>
</table>

### Buchungsportal

<table>
<thead><tr><th width="190">Testumgebung</th><th>Fähigkeit</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Herkunft</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Buchungs-Probelauf</a></td><td>Geht eine Online-Buchung bis zum letzten Schritt durch und hält an, damit die Schritte getestet werden können, ohne wirklich zu buchen.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Testumgebung</th><th>Fähigkeit</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Herkunft</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Animationsprüfung</a></td><td>Vermisst ein animiertes Diagramm, während es abläuft, und prüft auf Bruchteile eines Pixels genau, dass Teile bündig sind und sich nicht überlappen.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funktioniert mit dieser Version" title="funktioniert mit dieser Version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Von uns gebaut" title="Von uns gebaut" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Eine technischere Fassung, geschrieben zum Laden in Claude, ist die [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) auf GitHub.
