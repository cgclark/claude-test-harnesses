# Automaattiset testikehykset Claudelle

<details class="langs" data-current="fi">
<summary>Kieli</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · **Suomi** · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Tapoja, joilla Claude Code voi tarkistaa oman työnsä: ajaa sovelluksen, tallentaa jotain, mitä se pystyy lukemaan, ja ratkaista, meneekö testi läpi vai ei, ennen kuin ihmisen tarvitsee katsoa. Jokainen nimi avaa sivun, jolla on koko ohje. Itse testikehysten sivut ovat englanniksi.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Clauden suosittelema" title="Clauden suosittelema" width="16" height="16"></td><td><b>Clauden suosittelema</b>: vakiotyökalu sellaisenaan</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Clauden suosittelema, laajennettu" title="Clauden suosittelema, laajennettu" width="16" height="16"><img class="o" src="icons/plus.png" alt="Clauden suosittelema, laajennettu" title="Clauden suosittelema, laajennettu" width="16" height="16"></td><td><b>Clauden suosittelema, laajennettu</b>: vakiotyökalu, jota meidän piti täydentää ennen kuin se toimi</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td><td><b>Meidän tekemämme</b>: menetelmä, joka meidän piti kehittää itse</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"> toimii kyseisessä versiossa · <img class="o t" src="icons/square.png" alt="ei vielä vahvistettu" title="ei vielä vahvistettu" width="16" height="16"> ei vielä vahvistettu · <img class="o t" src="icons/xmark.square.png" alt="ei vielä toimi siinä" title="ei vielä toimi siinä" width="16" height="16"> ei vielä toimi siinä

Testikehykset, jotka eivät riipu käyttöjärjestelmän versiosta, lasketaan toimiviksi molemmissa. Muut on merkitty sen mukaan, milloin kutakin viimeksi käytettiin; tämä Mac siirtyi versioon 27 2. lokakuuta 2026, ja kunkin tarkistus yksi kerrallaan 27:n arkkitehtuuria vasten on vielä tekemättä.

**Lähtöisin**: sovellus, jossa kukin testikehys alun perin rakennettiin

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Sovellukset simulaattoreissa, Maceissa & laitteissa

<table class="wide">
<thead><tr><th width="190">Testikehys</th><th>Toiminto</th><th width="60">Lähtöisin</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Alkuperä</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Taustasimulaattori</a></td><td>Claude rakentaa iPhone-sovelluksen, ajaa sitä simulaattorissa taustalla ja ottaa itse kuvakaappaukset ja lokit, joten se voi tarkistaa näkymän ottamatta sinun näyttöäsi haltuunsa.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Clauden suosittelema, laajennettu" title="Clauden suosittelema, laajennettu" width="16" height="16"><img class="o" src="icons/plus.png" alt="Clauden suosittelema, laajennettu" title="Clauden suosittelema, laajennettu" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Asettelun mittaus</a></td><td>Claude mittaa, mitä näytölle todella aseteltiin, kuten palkkien korkeudet ja vierityskohdat, hetki hetkeltä, kun siirryt näkymästä toiseen, jotta se voi selvittää arvaamatta, miksi jokin näyttää väärältä.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Käynnistysargumenttikoukut</a></td><td>Testiversioiden piilotetut kytkimet, jotka avaavat sovelluksen suoraan valittuun näkymään esimerkkidatalla, joten Claude pääsee mihin tahansa näkymään napauttelematta koko sovelluksen läpi.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">iPad-sovellus Macilla</a></td><td>Ajaa sovelluksen iPad-version tavallisena Mac-sovelluksena, joten Claude voi testata sitä Macilla sen lokien ja ikkunan kuvakaappausten avulla.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Clauden suosittelema, laajennettu" title="Clauden suosittelema, laajennettu" width="16" height="16"><img class="o" src="icons/plus.png" alt="Clauden suosittelema, laajennettu" title="Clauden suosittelema, laajennettu" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript ja näytönkaappaus</a></td><td>Kun Claude ei voi ohjata näyttöä suoraan, se ohjaa Mac-sovelluksia AppleScriptillä ja kuvaa vain niiden ikkunan nähdäkseen tuloksen.</td></tr>
<tr><td><a href="unit-test-suites.md">Yksikkötestit</a></td><td>Automaattiset testit sovelluksen sisäiselle logiikalle, kuten pisteytykselle, reiteille ja jonoille; ne ajetaan sekunneissa avaamatta sovellusta.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Clauden suosittelema" title="Clauden suosittelema" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Tarkistuslista vain ihmiselle</a></td><td>Yksi jatkuvasti päivittyvä lista tarkistuksista, jotka vain ihminen voi tehdä, kuten lasien pitäminen päässä tai oikean puhelimen käyttö, jotta muu työ ei jää odottamaan niitä.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Käännä kaikki kohteet</a></td><td>Kääntää iPhone-, Mac- ja Vision Pro -versiot uudelleen yhdessä muutoksen jälkeen ja tarkistaa, ettei testiasetuksia koskaan tallenneta pelaajan omiin asetuksiin.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">SwiftUI:n live-esikatselu</a></td><td>Näyttää yhden näkymän Xcoden live-esikatselussa ja kuvaa sen, joten Claude voi tarkistaa asettelumuutoksen kääntämättä ja ajamatta koko peliä.</td><td class="m"><img class="o t" src="icons/square.png" alt="ei vielä vahvistettu" title="ei vielä vahvistettu" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Napautus saavutettavuustietojen avulla</a></td><td>Napauttaa simulaattorin painikkeita kohdista, jotka sovellus itse ilmoittaa, sen sijaan että arvaisi niiden paikan kuvakaappauksesta.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Clauden suosittelema" title="Clauden suosittelema" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Kaksi simulaattoria kahtena ihmisenä</a></td><td>Ajaa sovellusta kahdella simuloidulla iPhonella kahtena eri ihmisenä, joten kutsuja, haasteita ja synkronointia voi testata ilman kahta oikeaa puhelinta.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="ei vielä vahvistettu" title="ei vielä vahvistettu" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Jokainen näkymä joka kielellä</a></td><td>Kuvaa jokaisen päänäkymän jokaisella kielellä sekä keksityllä kielellä, jossa on erityisen pitkiä sanoja, yhdelle arkille, joten tekstin, joka ei mahdu, huomaa helposti.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Kaatumisraportit</a></td><td>Hakee kaatumisraportin oikeasta iPhonesta ja lukee sen, joten vain puhelimessa tapahtuvalle kaatumiselle löytyy nimetty syy.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ei vielä vahvistettu" title="ei vielä vahvistettu" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Clauden suosittelema" title="Clauden suosittelema" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Pieni testisarja</a></td><td>Pieni, itsenäinen joukko automaattisia tarkistuksia Python-työkalulle; se toimii missä tahansa asentamatta mitään.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td></tr>
</tbody>
</table>

## Grafiikka & pelit

<table class="wide">
<thead><tr><th width="190">Testikehys</th><th>Toiminto</th><th width="60">Lähtöisin</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Alkuperä</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Pelikonsolin ohjaus</a></td><td>Lähettää skriptistä komentoja pelin sisäänrakennettuun konsoliin ja lukee sen lokin jälkikäteen sen sijaan, että kirjoittaisi peli-ikkunaan.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="5"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Ennen ja jälkeen -kuvat</a></td><td>Toistaa saman tallennetun pelipätkän ennen grafiikkamuutosta ja sen jälkeen ja vertaa kuvia pikseli pikseliltä.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Säteenseuranta Macilla</a></td><td>Testinäkymät, jotka näyttävät säteenseurantavalaistuksen jokaisen vaiheen (varjot, heijastukset, ympäristövalo) erikseen, sekä itsetarkistukset, jotka tulostavat hyväksytty tai hylätty.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Pro -kuvakaappaukset</a></td><td>Tallentaa, mitä Vision Pro -sovellus näyttää, myös kummankin silmän näkymän 3D:nä, simulaattorissa ja laitteessa.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Clauden suosittelema, laajennettu" title="Clauden suosittelema, laajennettu" width="16" height="16"><img class="o" src="icons/plus.png" alt="Clauden suosittelema, laajennettu" title="Clauden suosittelema, laajennettu" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Shaderien offline-käännös</a></td><td>Kääntää säteenseurannan grafiikkakoodin Macilla, koska simulaattori ohittaa sen ja virheet näkyisivät muuten vasta laitteessa.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPU-kuvan kaappaus</a></td><td>Kaappaa yhden kuvan grafiikkapiiriltä ja listaa, mitä kukin piirtovaihe maksoi, jotta hitaat kohdat löytyvät.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="ei vielä vahvistettu" title="ei vielä vahvistettu" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Clauden suosittelema" title="Clauden suosittelema" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Shaderien matematiikka</a></td><td>Laskee Quake 3:n savu- ja tulitehosteet uudelleen hitaasti ja tarkasti ja tarkistaa, että nopea grafiikkaversio piirtää saman kuvan.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
</tbody>
</table>

## Puhe, kieli & data

<table class="wide">
<thead><tr><th width="190">Testikehys</th><th>Toiminto</th><th width="60">Lähtöisin</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Alkuperä</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Kuvakaappauksista tekstiä</a></td><td>Muuttaa kuvakaappaukset ja skannaukset tekstiksi Macilla ennen kuin Claude lukee ne, mikä pitää kuvat yksityisinä ja kuluttaa paljon vähemmän Clauden muistia.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac puhuu testilauseita synteettisillä äänillä sovelluksen puheentunnistimeen, joten äänikomentoja voi testata ilman, että kenenkään tarvitsee puhua.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ei vielä vahvistettu" title="ei vielä vahvistettu" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Äänen toisto laitteella</a></td><td>Mac muuntaa jokaisen testikeskustelun äänitiedostoksi, ja puhelimen sovellus kuuntelee sitä mikrofonin sijaan, joten äänitoimintoja voi testata oikealla puhelimella ilman, että kenenkään tarvitsee puhua.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Siri-lauseet</a></td><td>Tarkistaa, että sovellukseen Siriä varten rakennetut lauseet, kuten &quot;order my usual&quot;, vastaavat sitä, mitä ihmiset sanovat; se, ohjaako Siri ne oikein, vaatii yhä puhelimen.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Referenssitilannekuva</a></td><td>Tallentaa sovelluksen koko tulosteen ennen uudelleenkirjoitusta ja tarkistaa sitten, että uudelleenkirjoitettu versio tuottaa täsmälleen saman tulosteen.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ei vielä vahvistettu" title="ei vielä vahvistettu" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Litteroinnin tarkkuus</a></td><td>Ajaa sovelluksen puheentunnistuksen julkisilla äänitteillä, joiden mukana on oikeat litteroinnit, ja laskee, kuinka monta merkkiä menee väärin.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Käännöstarkistukset</a></td><td>Tarkistaa, että jokainen käännös säilyttää nimet, numerot ja sovitut termit ja ettei mitään näytön tekstiä ole jäänyt kääntämättä. Käytössä myös Quake 3:ssa.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Oikeat tiedot</a></td><td>Testaa reittien tunnistusta joukolla oikeita tallennettuja ajoja keksittyjen sijaan, ja näin löytyi virheitä, jotka keksityt testit olivat ohittaneet.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ei vielä vahvistettu" title="ei vielä vahvistettu" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Vastaavuus alkuperäiseen sovellukseen</a></td><td>Vertaa iPad-versiomme tietokantaa alkuperäisen Windows-sovelluksen tietokantaan taulu taululta ja rivi riviltä.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td></tr>
</tbody>
</table>

## Laitteisto, verkot & palvelut

<table class="wide">
<thead><tr><th width="190">Testikehys</th><th>Toiminto</th><th width="60">Lähtöisin</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Alkuperä</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Vertailu toimivaksi tiedettyyn laitteeseen</a></td><td>Tallentaa, miten toimivaksi tiedetty kokoonpano käyttäytyy (iPhone suoraan yhteydessä nappikuulokkeisiin), ja vertaa siltamme tallennetta siihen.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetooth-kaappaukset</a></td><td>Tallentaa itse Bluetooth-liikenteen, jotta nähdään, mitä laitteet todella lähettivät eikä vain mitä ne ilmoittivat.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Clauden suosittelema" title="Clauden suosittelema" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Toimivuustarkistukset</a></td><td>Tarkistaa, että jokainen verkkopalvelu vastaa internetistä ja että reitti, jonka pitäisi olla estetty, torjutaan.</td></tr>
</tbody>
</table>

## Verkko

<table class="wide">
<thead><tr><th width="190">Testikehys</th><th>Toiminto</th><th width="60">Lähtöisin</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Alkuperä</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Selaimen ohjaus</a></td><td>Claude avaa sivuja selaimessa, täyttää lomakkeita ja lukee tuloksen tarkistaakseen, että sivusto toimii ja näyttää oikealta.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Clauden suosittelema" title="Clauden suosittelema" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Sivustopäivityksen tarkistus</a></td><td>Sivustopäivityksen jälkeen tarkistaa, että jokainen tiedosto saapui palvelimelle ehjänä, ja sitten asettelun puhelimen, tabletin ja tietokoneen leveydellä.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Projektikohtaiset (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Testikehys</th><th>Toiminto</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Alkuperä</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Pelimodit</a></td><td>Lataa jokaisen suositun moninpelimodin meidän versioomme pelistä, käynnistää kentän ja etsii lokista virheitä.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="ei vielä vahvistettu" title="ei vielä vahvistettu" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Rinnakkain alkuperäisen kanssa</a></td><td>Tallentaa saman kohtauksen meidän versiossamme ja alkuperäisessä pelissä rinnakkain, jotta mahdolliset erot näkyvät.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ei vielä vahvistettu" title="ei vielä vahvistettu" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Kenttäkuvat</a></td><td>Ottaa kuvan jokaisesta kentästä kentän tekijän valitsemasta kamerakulmasta ja asettelee ne yhdelle arkille.</td></tr>
</tbody>
</table>

### Viittomakielityö

<table>
<thead><tr><th width="190">Testikehys</th><th>Toiminto</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Alkuperä</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Liikevertailu</a></td><td>Toistaa tietokoneella tuotettua viittovaa kättä sen oikean viittojan rinnalla, jonka pohjalta se tehtiin, kuva kuvalta, ja tarkistaa, että liike vastaa.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Testikehys</th><th>Toiminto</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Alkuperä</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Lainattujen arvojen tarkistus</a></td><td>Ennen kuin Claude lainaa päivämäärän tai luvun asiakirjasta, tarkistetaan, että täsmälleen sama teksti todella löytyy asiakirjasta.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger Bluetooth -silta

<table>
<thead><tr><th width="190">Testikehys</th><th>Toiminto</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Alkuperä</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Sillan mittausohjelmat ja kojelauta</a></td><td>Pieniä testiohjelmia ja reaaliaikainen kojelauta pyörän Bluetooth-äänisillalle; ne näyttävät äänipuskurit, signaalinvoimakkuuden ja yhteydet ajon aikana.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
</tbody>
</table>

### Varausportaali

<table>
<thead><tr><th width="190">Testikehys</th><th>Toiminto</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Alkuperä</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Varauksen kuivaharjoitus</a></td><td>Käy verkkovarauksen läpi viimeiseen vaiheeseen asti ja pysähtyy, jotta vaiheet voi testata tekemättä oikeaa varausta.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Testikehys</th><th>Toiminto</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Alkuperä</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Animaation tarkistus</a></td><td>Mittaa animoitua kaaviota sen toistuessa ja tarkistaa, että osat ovat kohdallaan eivätkä mene päällekkäin, pikselin murto-osan tarkkuudella.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="toimii kyseisessä versiossa" title="toimii kyseisessä versiossa" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Meidän tekemämme" title="Meidän tekemämme" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Teknisempi versio, joka on kirjoitettu Claudeen ladattavaksi, on [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) GitHubissa.
