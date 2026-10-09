# Banchi di prova automatici per Claude

<details class="langs" data-current="it">
<summary>Lingua</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · **Italiano** · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Modi in cui Claude Code può controllare il proprio lavoro: avviare l'app, catturare qualcosa che sa leggere e decidere se il test è superato o fallito prima che una persona debba guardare. Ogni nome apre una pagina con la procedura completa. Le pagine dei singoli banchi di prova sono in inglese.

<img class="c" src="icons/claude-code.svg" alt="Consigliato da Claude" title="Consigliato da Claude" width="16" height="16"> **Consigliato da Claude**: uno strumento standard usato così com'è (8)<br>
<img class="c" src="icons/claude-code.svg" alt="Consigliato da Claude, esteso" title="Consigliato da Claude, esteso" width="16" height="16"><img class="o" src="icons/plus.png" alt="Consigliato da Claude, esteso" title="Consigliato da Claude, esteso" width="16" height="16"> **Consigliato da Claude, esteso**: uno strumento standard che abbiamo dovuto integrare perché funzionasse (4)<br>
<img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"> **Creato da noi**: un metodo che abbiamo dovuto ideare (30)

<img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"> funziona su quella versione · <img class="o t" src="icons/square.png" alt="non ancora confermato" title="non ancora confermato" width="16" height="16"> non ancora confermato · <img class="o t" src="icons/xmark.square.png" alt="lì non funziona ancora" title="lì non funziona ancora" width="16" height="16"> lì non funziona ancora

I banchi di prova che non dipendono dalla versione del sistema operativo contano come funzionanti su entrambe. Gli altri sono spuntati in base all'ultimo utilizzo; questo Mac è passato a 27 il 2 ottobre 2026, e manca ancora una verifica uno per uno sull'architettura di 27.

**Da**: l'app in cui ogni banco di prova è stato creato per la prima volta

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/big-top.png" alt="" width="20" height="20"> Big Top</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## App su simulatori, Mac & dispositivi

<table class="wide">
<thead><tr><th width="190">Banco di prova</th><th>Funzione</th><th width="60">Da</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Simulatore in background</a></td><td>Claude compila un&#x27;app per iPhone, la esegue nel simulatore in background e fa da sé screenshot e log, così può controllare una schermata senza occupare la tua.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Consigliato da Claude, esteso" title="Consigliato da Claude, esteso" width="16" height="16"><img class="o" src="icons/plus.png" alt="Consigliato da Claude, esteso" title="Consigliato da Claude, esteso" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Sonda di layout</a></td><td>Claude misura ciò che la schermata ha davvero disposto, come l&#x27;altezza delle barre e le posizioni di scorrimento, istante per istante mentre passi da una schermata all&#x27;altra, così trova perché qualcosa appare sbagliato invece di tirare a indovinare.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Hook da argomenti di avvio</a></td><td>Interruttori nascosti nelle build di test che aprono un&#x27;app direttamente su una schermata scelta con dati di esempio, così Claude raggiunge qualsiasi schermata senza attraversare l&#x27;app a forza di tocchi.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">App per iPad sul Mac</a></td><td>Esegue la versione per iPad di un&#x27;app come una normale app per Mac, così Claude può testarla sul Mac con i suoi log e gli screenshot della finestra.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Consigliato da Claude, esteso" title="Consigliato da Claude, esteso" width="16" height="16"><img class="o" src="icons/plus.png" alt="Consigliato da Claude, esteso" title="Consigliato da Claude, esteso" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript e cattura dello schermo</a></td><td>Quando Claude non può controllare direttamente lo schermo, guida le app del Mac con AppleScript e fotografa solo la loro finestra per vedere il risultato.</td></tr>
<tr><td><a href="unit-test-suites.md">Test unitari</a></td><td>Test automatici della logica interna di un&#x27;app, come punteggi, percorsi e code, che girano in pochi secondi senza aprire l&#x27;app.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Consigliato da Claude" title="Consigliato da Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Lista solo per persone</a></td><td>Un elenco aggiornato dei controlli che solo una persona può fare, come indossare il visore o usare un telefono vero, così il resto del lavoro non deve aspettarli.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Compilare ogni target</a></td><td>Ricompila insieme le versioni per iPhone, Mac e Vision Pro dopo una modifica, e verifica che le impostazioni di test non finiscano mai salvate nelle impostazioni di un giocatore.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Anteprima dal vivo SwiftUI</a></td><td>Mostra una schermata nell&#x27;anteprima dal vivo di Xcode e la fotografa, così Claude può controllare una modifica al layout senza compilare ed eseguire l&#x27;intero gioco.</td><td class="m"><img class="o t" src="icons/square.png" alt="non ancora confermato" title="non ancora confermato" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Tocchi tramite accessibilità</a></td><td>Tocca i pulsanti nel simulatore nelle posizioni indicate dall&#x27;app stessa, invece di indovinare dove sono da uno screenshot.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Consigliato da Claude" title="Consigliato da Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Due simulatori come due persone</a></td><td>Esegue l&#x27;app su due iPhone simulati come due persone diverse, così inviti, sfide e sincronizzazione si possono testare senza due telefoni veri.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="non ancora confermato" title="non ancora confermato" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Ogni schermata in ogni lingua</a></td><td>Fotografa ogni schermata principale in ogni lingua, più una lingua inventata con parole lunghissime, su un unico foglio, così il testo che non ci sta salta all&#x27;occhio.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Report di arresto anomalo</a></td><td>Scarica il report di arresto anomalo da un iPhone vero e lo legge, così un crash che avviene solo sul telefono ha una causa precisa.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="non ancora confermato" title="non ancora confermato" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Consigliato da Claude" title="Consigliato da Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Piccola suite di test</a></td><td>Un piccolo insieme autonomo di controlli automatici per uno strumento Python, che gira ovunque senza installare nulla.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td></tr>
</tbody>
</table>

## Grafica & giochi

<table class="wide">
<thead><tr><th width="190">Banco di prova</th><th>Funzione</th><th width="60">Da</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Guida della console di gioco</a></td><td>Invia comandi alla console integrata del gioco da uno script e poi ne legge il log, invece di scrivere nella finestra del gioco.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Fotogrammi prima e dopo</a></td><td>Riproduce la stessa clip di gioco registrata prima e dopo una modifica grafica e confronta i fotogrammi pixel per pixel.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Ray tracing sul Mac</a></td><td>Viste di test che mostrano separatamente ogni passaggio dell&#x27;illuminazione in ray tracing (ombre, riflessi, luce ambientale), più autoverifiche che stampano superato o fallito.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Screenshot di Vision Pro</a></td><td>Cattura ciò che mostra l&#x27;app per Vision Pro, compresa la vista di ciascun occhio in 3D, nel simulatore e sul visore.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="non ancora confermato" title="non ancora confermato" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Consigliato da Claude, esteso" title="Consigliato da Claude, esteso" width="16" height="16"><img class="o" src="icons/plus.png" alt="Consigliato da Claude, esteso" title="Consigliato da Claude, esteso" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Compilazione shader offline</a></td><td>Compila sul Mac il codice grafico del ray tracing, perché il simulatore lo salta e gli errori altrimenti emergerebbero solo su un dispositivo.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">Cattura di frame GPU</a></td><td>Cattura un fotogramma sul chip grafico ed elenca quanto è costato ogni passaggio di disegno, per trovare cosa è lento.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="non ancora confermato" title="non ancora confermato" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Consigliato da Claude" title="Consigliato da Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Calcoli degli shader</a></td><td>Ricalcola in modo lento ed esatto gli effetti di fumo e fuoco di Quake 3, e verifica che la versione grafica veloce disegni la stessa immagine.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
</tbody>
</table>

## Voce, lingue & dati

<table class="wide">
<thead><tr><th width="190">Banco di prova</th><th>Funzione</th><th width="60">Da</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Da screenshot a testo</a></td><td>Trasforma screenshot e scansioni in testo sul Mac prima che Claude li legga, il che mantiene private le immagini e usa molta meno memoria di Claude.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m" rowspan="8"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Il Mac pronuncia frasi di prova con voci sintetiche nel riconoscimento vocale dell&#x27;app, così i comandi vocali si possono testare senza che nessuno parli.</td><td class="app-c"><img class="app-sm" src="icons/apps/big-top.png" alt="Big Top" title="Big Top" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="non ancora confermato" title="non ancora confermato" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td></tr>
<tr><td><a href="siri-phrasing-check.md">Frasi per Siri</a></td><td>Verifica che le frasi integrate nell&#x27;app per Siri, come «order my usual», corrispondano a ciò che dice la gente; se Siri le instrada correttamente richiede ancora il telefono.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Snapshot di riferimento</a></td><td>Salva l&#x27;output completo dell&#x27;app prima di una riscrittura, poi verifica che la versione riscritta produca esattamente lo stesso output.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="non ancora confermato" title="non ancora confermato" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Precisione della trascrizione</a></td><td>Fa girare la trascrizione vocale dell&#x27;app su registrazioni pubbliche corredate di trascrizioni corrette, e conta quanti caratteri sbaglia.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Controlli sulle traduzioni</a></td><td>Verifica che ogni traduzione mantenga nomi, numeri e termini concordati, e che nessun testo sullo schermo sia rimasto non tradotto. Usato anche per Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Dati reali</a></td><td>Testa il riconoscimento dei percorsi su una serie di uscite reali registrate invece che inventate, e ha trovato bug sfuggiti ai test inventati.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="non ancora confermato" title="non ancora confermato" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Come l&#x27;app originale</a></td><td>Confronta il database della nostra versione per iPad con quello dell&#x27;app Windows originale, tabella per tabella e riga per riga.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td></tr>
</tbody>
</table>

## Hardware, reti & servizi

<table class="wide">
<thead><tr><th width="190">Banco di prova</th><th>Funzione</th><th width="60">Da</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Confronto con un dispositivo affidabile</a></td><td>Registra il comportamento di una configurazione che funziona (l&#x27;iPhone collegato direttamente agli auricolari) e la confronta con una registrazione del nostro ponte.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Catture Bluetooth</a></td><td>Registra il traffico Bluetooth vero e proprio, per vedere cosa hanno davvero inviato i dispositivi invece di cosa hanno dichiarato.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Consigliato da Claude" title="Consigliato da Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Controlli di stato</a></td><td>Verifica che ogni servizio web risponda da internet e che il percorso che dovrebbe essere bloccato venga rifiutato.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Banco di prova</th><th>Funzione</th><th width="60">Da</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Guida del browser</a></td><td>Claude apre pagine in un browser, compila moduli e legge il risultato, per verificare che un sito funzioni e appaia correttamente.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Consigliato da Claude" title="Consigliato da Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Verifica della pubblicazione del sito</a></td><td>Dopo un aggiornamento del sito, verifica che ogni file sia arrivato integro sul server, poi controlla il layout alle larghezze di telefono, tablet e desktop.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Specifici di un progetto (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Banco di prova</th><th>Funzione</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Mod del gioco</a></td><td>Carica ogni mod multigiocatore popolare nella nostra versione del gioco, avvia una mappa e cerca errori nel log.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="non ancora confermato" title="non ancora confermato" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Fianco a fianco con l&#x27;originale</a></td><td>Registra la stessa scena nella nostra versione e nel gioco originale, fianco a fianco, per mostrare qualsiasi differenza.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="non ancora confermato" title="non ancora confermato" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Screenshot dei livelli</a></td><td>Scatta un&#x27;immagine di ogni mappa dall&#x27;angolazione scelta dal suo autore e le dispone su un unico foglio.</td></tr>
</tbody>
</table>

### Progetto sulla lingua dei segni

<table>
<thead><tr><th width="190">Banco di prova</th><th>Funzione</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Confronto del movimento</a></td><td>Riproduce una mano che segna generata al computer accanto alla persona segnante reale da cui è stata ricavata, fotogramma per fotogramma, per verificare che il movimento corrisponda.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Banco di prova</th><th>Funzione</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Verifica dei valori citati</a></td><td>Prima che Claude citi una data o una cifra da un documento, verifica che quel testo esatto compaia davvero nel documento.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
</tbody>
</table>

### Ponte Bluetooth Ranger

<table>
<thead><tr><th width="190">Banco di prova</th><th>Funzione</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Sonde e dashboard del ponte</a></td><td>Piccoli programmi di test e una dashboard dal vivo per il ponte audio Bluetooth della bici, che mostrano buffer audio, potenza del segnale e connessioni mentre si pedala.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
</tbody>
</table>

### Portale di prenotazione

<table>
<thead><tr><th width="190">Banco di prova</th><th>Funzione</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Prenotazione di prova</a></td><td>Percorre una prenotazione online fino all&#x27;ultimo passaggio e si ferma, così i passaggi si possono testare senza fare una prenotazione vera.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Banco di prova</th><th>Funzione</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Controllo dell&#x27;animazione</a></td><td>Misura un diagramma animato mentre viene riprodotto, verificando con precisione di una frazione di pixel che i pezzi siano allineati e non si sovrappongano.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funziona su quella versione" title="funziona su quella versione" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creato da noi" title="Creato da noi" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Una versione più tecnica, scritta per essere caricata in Claude, è il [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) su GitHub.
