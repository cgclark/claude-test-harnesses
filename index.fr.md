# Bancs de test automatisés pour Claude

<details class="langs" data-current="fr">
<summary>Langue</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · **Français** · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Des moyens pour Claude Code de vérifier son propre travail : lancer l'app, capturer quelque chose qu'il peut lire et décider si c'est réussi ou échoué avant qu'une personne doive regarder. Chaque nom ouvre une page avec la recette complète. Les pages des bancs de test sont elles-mêmes en anglais.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Recommandé par Claude" title="Recommandé par Claude" width="16" height="16"></td><td><b>Recommandé par Claude</b>: un outil standard utilisé tel quel</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Recommandé par Claude, étendu" title="Recommandé par Claude, étendu" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recommandé par Claude, étendu" title="Recommandé par Claude, étendu" width="16" height="16"></td><td><b>Recommandé par Claude, étendu</b>: un outil standard que nous avons dû compléter pour qu'il fonctionne</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td><td><b>Conçu par nous</b>: une méthode que nous avons dû mettre au point</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"> fonctionne sur cette version · <img class="o t" src="icons/square.png" alt="pas encore confirmé" title="pas encore confirmé" width="16" height="16"> pas encore confirmé · <img class="o t" src="icons/xmark.square.png" alt="ne fonctionne pas encore là" title="ne fonctionne pas encore là" width="16" height="16"> ne fonctionne pas encore là

Les bancs de test qui ne dépendent pas de la version du système sont considérés comme fonctionnels sur les deux. Les autres sont cochés d'après leur dernière utilisation ; ce Mac est passé à 27 le 2 octobre 2026, et une vérification un par un selon l'architecture de 27 reste à faire.

**Source**: l'app dans laquelle chaque banc de test a d'abord été créé

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Apps sur simulateurs, Mac & appareils

<table class="wide">
<thead><tr><th width="190">Banc de test</th><th>Capacité</th><th width="60">Source</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Simulateur en arrière-plan</a></td><td>Claude compile une app iPhone, la lance dans le simulateur en arrière-plan et prend lui-même captures et journaux, pour vérifier un écran sans prendre le contrôle du vôtre.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recommandé par Claude, étendu" title="Recommandé par Claude, étendu" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recommandé par Claude, étendu" title="Recommandé par Claude, étendu" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Sonde de mise en page</a></td><td>Claude mesure ce que l&#x27;écran a réellement disposé, comme la hauteur des barres et les positions de défilement, instant par instant pendant que vous passez d&#x27;un écran à l&#x27;autre, pour trouver pourquoi quelque chose s&#x27;affiche mal au lieu de deviner.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Crochets par argument de lancement</a></td><td>Des commutateurs cachés dans les versions de test qui ouvrent une app directement sur un écran choisi avec des données d&#x27;exemple, pour que Claude atteigne n&#x27;importe quel écran sans parcourir l&#x27;app à coups de touchers.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">App iPad sur le Mac</a></td><td>Lance la version iPad d&#x27;une app comme une app Mac ordinaire, pour que Claude la teste sur le Mac avec ses journaux et des captures de sa fenêtre.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Recommandé par Claude, étendu" title="Recommandé par Claude, étendu" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recommandé par Claude, étendu" title="Recommandé par Claude, étendu" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript et capture d&#x27;écran</a></td><td>Quand Claude ne peut pas contrôler l&#x27;écran directement, il pilote les apps Mac avec AppleScript et photographie uniquement leur fenêtre pour voir le résultat.</td></tr>
<tr><td><a href="unit-test-suites.md">Tests unitaires</a></td><td>Des tests automatiques de la logique interne d&#x27;une app, comme le calcul des scores, les itinéraires et les files d&#x27;attente, qui s&#x27;exécutent en quelques secondes sans ouvrir l&#x27;app.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recommandé par Claude" title="Recommandé par Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Liste réservée aux humains</a></td><td>Une liste tenue à jour des vérifications que seule une personne peut faire, comme porter le casque ou utiliser un vrai téléphone, pour que le reste du travail n&#x27;ait pas à les attendre.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Compiler toutes les cibles</a></td><td>Recompile ensemble les versions iPhone, Mac et Vision Pro après une modification, et vérifie que les réglages de test ne sont jamais enregistrés dans les réglages propres d&#x27;un joueur.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Aperçu en direct SwiftUI</a></td><td>Affiche un écran dans l&#x27;aperçu en direct de Xcode et le photographie, pour que Claude vérifie une modification de mise en page sans compiler ni lancer tout le jeu.</td><td class="m"><img class="o t" src="icons/square.png" alt="pas encore confirmé" title="pas encore confirmé" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Toucher via l&#x27;accessibilité</a></td><td>Touche les boutons dans le simulateur aux positions que l&#x27;app indique elle-même, au lieu de deviner où ils sont d&#x27;après une capture.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recommandé par Claude" title="Recommandé par Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Deux simulateurs, deux personnes</a></td><td>Lance l&#x27;app sur deux iPhone simulés comme deux personnes différentes, pour tester invitations, défis et synchronisation sans deux vrais téléphones.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="pas encore confirmé" title="pas encore confirmé" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Chaque écran dans chaque langue</a></td><td>Photographie chaque écran principal dans chaque langue, plus une langue inventée aux mots très longs, sur une seule planche, pour repérer facilement le texte qui ne tient pas.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Rapports de plantage</a></td><td>Récupère le rapport de plantage d&#x27;un vrai iPhone et le lit, pour qu&#x27;un plantage qui n&#x27;arrive que sur le téléphone ait une cause identifiée.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="pas encore confirmé" title="pas encore confirmé" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Recommandé par Claude" title="Recommandé par Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Petite suite de tests</a></td><td>Un petit ensemble autonome de vérifications automatiques pour un outil Python, qui s&#x27;exécute partout sans rien installer.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td></tr>
</tbody>
</table>

## Graphismes & jeux

<table class="wide">
<thead><tr><th width="190">Banc de test</th><th>Capacité</th><th width="60">Source</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Pilotage de la console du jeu</a></td><td>Envoie des commandes à la console intégrée du jeu depuis un script et lit ensuite son journal, au lieu de taper dans la fenêtre du jeu.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Images avant et après</a></td><td>Rejoue la même séquence de jeu enregistrée avant et après une modification graphique et compare les images pixel par pixel.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Lancer de rayons sur le Mac</a></td><td>Des vues de test qui montrent séparément chaque étape de l&#x27;éclairage par lancer de rayons (ombres, reflets, lumière ambiante), plus des autovérifications qui affichent réussi ou échoué.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Captures Vision Pro</a></td><td>Capture ce qu&#x27;affiche l&#x27;app Vision Pro, y compris la vue de chaque œil en 3D, dans le simulateur et sur le casque.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="pas encore confirmé" title="pas encore confirmé" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recommandé par Claude, étendu" title="Recommandé par Claude, étendu" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recommandé par Claude, étendu" title="Recommandé par Claude, étendu" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Compilation des shaders hors ligne</a></td><td>Compile le code graphique de lancer de rayons sur le Mac, car le simulateur l&#x27;ignore et les erreurs n&#x27;apparaîtraient sinon que sur un appareil.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">Capture d&#x27;image GPU</a></td><td>Capture une image sur la puce graphique et liste le coût de chaque étape de dessin, pour trouver ce qui est lent.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="pas encore confirmé" title="pas encore confirmé" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recommandé par Claude" title="Recommandé par Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Calculs des shaders</a></td><td>Recalcule lentement et exactement les effets de fumée et de feu de Quake 3, et vérifie que la version graphique rapide dessine la même image.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
</tbody>
</table>

## Voix, langues & données

<table class="wide">
<thead><tr><th width="190">Banc de test</th><th>Capacité</th><th width="60">Source</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Des captures au texte</a></td><td>Convertit captures et numérisations en texte sur le Mac avant que Claude les lise, ce qui garde les images privées et utilise bien moins de mémoire de Claude.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Le Mac prononce des phrases de test avec des voix de synthèse dans la reconnaissance vocale de l&#x27;app, pour tester les commandes vocales sans que personne ne parle.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="pas encore confirmé" title="pas encore confirmé" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Lecture audio sur un appareil</a></td><td>Le Mac transforme chaque conversation de test en fichier audio, que l&#x27;app du téléphone écoute à la place du micro, pour tester les fonctions vocales sur le vrai téléphone sans que personne ne parle.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Formulations Siri</a></td><td>Vérifie que les phrases intégrées à l&#x27;app pour Siri, comme « order my usual », correspondent à ce que disent les gens ; savoir si Siri les achemine correctement demande toujours le téléphone.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Instantané de référence</a></td><td>Enregistre la sortie complète de l&#x27;app avant une réécriture, puis vérifie que la version réécrite produit exactement la même sortie.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="pas encore confirmé" title="pas encore confirmé" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Précision de la transcription</a></td><td>Passe la reconnaissance vocale de l&#x27;app sur des enregistrements publics accompagnés de transcriptions exactes, et compte le nombre de caractères erronés.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Contrôle des traductions</a></td><td>Vérifie que chaque traduction conserve ses noms, nombres et termes convenus, et qu&#x27;aucun texte à l&#x27;écran n&#x27;est resté non traduit. Sert aussi pour Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Données réelles</a></td><td>Teste la correspondance des itinéraires sur un ensemble de sorties réellement enregistrées plutôt qu&#x27;inventées, ce qui a révélé des bugs que les tests inventés avaient manqués.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="pas encore confirmé" title="pas encore confirmé" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Identique à l&#x27;app d&#x27;origine</a></td><td>Compare la base de données de notre version iPad avec celle de l&#x27;app Windows d&#x27;origine, table par table et ligne par ligne.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td></tr>
</tbody>
</table>

## Matériel, réseaux & services

<table class="wide">
<thead><tr><th width="190">Banc de test</th><th>Capacité</th><th width="60">Source</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Comparer à un appareil fiable</a></td><td>Enregistre le comportement d&#x27;une configuration qui fonctionne (l&#x27;iPhone relié directement aux écouteurs) et y compare un enregistrement de notre pont.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Captures Bluetooth</a></td><td>Enregistre le trafic Bluetooth lui-même, pour voir ce que les appareils ont réellement envoyé plutôt que ce qu&#x27;ils ont signalé.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Recommandé par Claude" title="Recommandé par Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Contrôles d&#x27;état</a></td><td>Vérifie que chaque service web répond depuis internet, et que la route qui doit être bloquée est refusée.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Banc de test</th><th>Capacité</th><th width="60">Source</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Pilotage du navigateur</a></td><td>Claude ouvre des pages dans un navigateur, remplit des formulaires et lit le résultat, pour vérifier qu&#x27;un site fonctionne et s&#x27;affiche correctement.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recommandé par Claude" title="Recommandé par Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Vérification du déploiement web</a></td><td>Après une mise à jour du site, vérifie que chaque fichier est arrivé intact sur le serveur, puis contrôle la mise en page aux largeurs téléphone, tablette et ordinateur.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Propres à un projet (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Banc de test</th><th>Capacité</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Mods du jeu</a></td><td>Charge chaque mod multijoueur populaire dans notre version du jeu, lance une carte et cherche des erreurs dans le journal.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="pas encore confirmé" title="pas encore confirmé" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Côte à côte avec l&#x27;original</a></td><td>Enregistre la même scène dans notre version et dans le jeu original, côte à côte, pour montrer toute différence.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="pas encore confirmé" title="pas encore confirmé" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Captures des niveaux</a></td><td>Prend une image de chaque carte sous l&#x27;angle de caméra choisi par son auteur, et les dispose sur une seule planche.</td></tr>
</tbody>
</table>

### Projet en langue des signes

<table>
<thead><tr><th width="190">Banc de test</th><th>Capacité</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Comparaison de mouvement</a></td><td>Rejoue une main signante générée par ordinateur à côté de la vraie personne signante dont elle est issue, image par image, pour vérifier que le mouvement correspond.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Banc de test</th><th>Capacité</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Vérifier les valeurs citées</a></td><td>Avant que Claude cite une date ou un chiffre tiré d&#x27;un document, vérifie que le texte exact figure bien dans ce document.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
</tbody>
</table>

### Pont Bluetooth Ranger

<table>
<thead><tr><th width="190">Banc de test</th><th>Capacité</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Sondes et tableau de bord du pont</a></td><td>De petits programmes de test et un tableau de bord en direct pour le pont audio Bluetooth du vélo, qui montrent tampons audio, force du signal et connexions en roulant.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
</tbody>
</table>

### Portail de réservation

<table>
<thead><tr><th width="190">Banc de test</th><th>Capacité</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Réservation à blanc</a></td><td>Parcourt une réservation en ligne jusqu&#x27;à la dernière étape et s&#x27;arrête, pour tester les étapes sans faire de vraie réservation.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Banc de test</th><th>Capacité</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Origine</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Contrôle d&#x27;animation</a></td><td>Mesure un diagramme animé pendant sa lecture et vérifie, à une fraction de pixel près, que les éléments s&#x27;alignent et ne se chevauchent pas.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="fonctionne sur cette version" title="fonctionne sur cette version" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Conçu par nous" title="Conçu par nous" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Une version plus technique, écrite pour être chargée dans Claude, est le [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) sur GitHub.
