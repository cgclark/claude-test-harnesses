# Środowiska testów automatycznych Claude

<details class="langs" data-current="pl">
<summary>Język</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · **Polski** · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Sposoby, w jakie Claude Code może sam sprawdzić swoją pracę: uruchomić aplikację, przechwycić coś, co potrafi odczytać, i rozstrzygnąć, czy test przeszedł, zanim człowiek musi to obejrzeć. Każda nazwa otwiera stronę z pełnym opisem. Same strony środowisk testowych są po angielsku.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Polecane przez Claude" title="Polecane przez Claude" width="16" height="16"></td><td><b>Polecane przez Claude</b>: standardowe narzędzie używane bez zmian</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Polecane przez Claude, rozszerzone" title="Polecane przez Claude, rozszerzone" width="16" height="16"><img class="o" src="icons/plus.png" alt="Polecane przez Claude, rozszerzone" title="Polecane przez Claude, rozszerzone" width="16" height="16"></td><td><b>Polecane przez Claude, rozszerzone</b>: standardowe narzędzie, które musieliśmy uzupełnić, żeby działało</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td><td><b>Zbudowane przez nas</b>: metoda, którą musieliśmy opracować</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"> działa w tej wersji · <img class="o t" src="icons/square.png" alt="jeszcze niepotwierdzone" title="jeszcze niepotwierdzone" width="16" height="16"> jeszcze niepotwierdzone · <img class="o t" src="icons/xmark.square.png" alt="tam jeszcze nie działa" title="tam jeszcze nie działa" width="16" height="16"> tam jeszcze nie działa

Środowiska testowe niezależne od wersji systemu liczą się jako działające w obu. Pozostałe są zaznaczone według tego, kiedy każde było ostatnio używane; ten Mac przeszedł na 27 dnia 2 października 2026 r., a sprawdzenie każdego z osobna pod kątem architektury 27 jest jeszcze przed nami.

**Skąd**: aplikacja, w której dane środowisko testowe powstało

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Aplikacje na symulatorach, Macach i urządzeniach

<table class="wide">
<thead><tr><th width="190">Środowisko testowe</th><th>Możliwość</th><th width="60">Skąd</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Pochodzenie</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Symulator w tle</a></td><td>Claude buduje aplikację na iPhone, uruchamia ją w symulatorze w tle i sam robi zrzuty ekranu oraz zbiera logi, więc może sprawdzić ekran, nie przejmując Twojego.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Polecane przez Claude, rozszerzone" title="Polecane przez Claude, rozszerzone" width="16" height="16"><img class="o" src="icons/plus.png" alt="Polecane przez Claude, rozszerzone" title="Polecane przez Claude, rozszerzone" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Sonda układu</a></td><td>Claude mierzy, jak ekran faktycznie się ułożył, np. wysokości pasków i pozycje przewijania, chwila po chwili podczas przechodzenia między ekranami, więc może znaleźć przyczynę problemu zamiast zgadywać.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Przełączniki w argumentach uruchomienia</a></td><td>Ukryte przełączniki w wersjach testowych, które otwierają aplikację od razu na wybranym ekranie z przykładowymi danymi, więc Claude może dotrzeć do każdego ekranu bez przeklikiwania się przez aplikację.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">Aplikacja na iPad na Macu</a></td><td>Uruchamia wersję aplikacji na iPad jako zwykłą aplikację na Maca, więc Claude może ją testować na Macu, korzystając z jej logów i zrzutów okna.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Polecane przez Claude, rozszerzone" title="Polecane przez Claude, rozszerzone" width="16" height="16"><img class="o" src="icons/plus.png" alt="Polecane przez Claude, rozszerzone" title="Polecane przez Claude, rozszerzone" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript i zrzuty ekranu</a></td><td>Gdy Claude nie może bezpośrednio sterować ekranem, obsługuje aplikacje na Maca przez AppleScript i fotografuje tylko ich okno, żeby zobaczyć wynik.</td></tr>
<tr><td><a href="unit-test-suites.md">Testy jednostkowe</a></td><td>Automatyczne testy wewnętrznej logiki aplikacji, np. punktacji, tras i kolejek, które trwają kilka sekund i nie wymagają otwierania aplikacji.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Polecane przez Claude" title="Polecane przez Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Lista tylko dla człowieka</a></td><td>Jedna bieżąca lista kontroli, które może wykonać tylko człowiek, np. założenie gogli albo użycie prawdziwego telefonu, żeby reszta pracy nie musiała na nie czekać.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Budowanie wszystkich wersji</a></td><td>Po zmianie przebudowuje razem wersje na iPhone, Maca i Vision Pro oraz sprawdza, czy ustawienia testowe nigdy nie trafiają do ustawień gracza.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Podgląd na żywo SwiftUI</a></td><td>Pokazuje jeden ekran w podglądzie na żywo w Xcode i go fotografuje, więc Claude może sprawdzić zmianę układu bez budowania i uruchamiania całej gry.</td><td class="m"><img class="o t" src="icons/square.png" alt="jeszcze niepotwierdzone" title="jeszcze niepotwierdzone" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Stukanie według dostępności</a></td><td>Stuka w przyciski w symulatorze w miejscach, które podaje sama aplikacja, zamiast zgadywać ich położenie ze zrzutu ekranu.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Polecane przez Claude" title="Polecane przez Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Dwa symulatory jako dwie osoby</a></td><td>Uruchamia aplikację na dwóch symulowanych iPhone&#x27;ach jako dwie różne osoby, więc zaproszenia, wyzwania i synchronizację można testować bez dwóch prawdziwych telefonów.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="jeszcze niepotwierdzone" title="jeszcze niepotwierdzone" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Każdy ekran w każdym języku</a></td><td>Fotografuje każdy główny ekran w każdym języku, a także w wymyślonym języku z bardzo długimi słowami, na jednym arkuszu, więc łatwo wypatrzyć tekst, który się nie mieści.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Raporty awarii</a></td><td>Pobiera raport awarii z prawdziwego iPhone&#x27;a i go odczytuje, więc awaria, która zdarza się tylko na telefonie, dostaje konkretną przyczynę.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="jeszcze niepotwierdzone" title="jeszcze niepotwierdzone" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Polecane przez Claude" title="Polecane przez Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Mały zestaw testów</a></td><td>Mały, samodzielny zestaw automatycznych testów narzędzia w Python, który działa wszędzie bez instalowania czegokolwiek.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td></tr>
</tbody>
</table>

## Grafika i gry

<table class="wide">
<thead><tr><th width="190">Środowisko testowe</th><th>Możliwość</th><th width="60">Skąd</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Pochodzenie</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Sterowanie konsolą gry</a></td><td>Wysyła polecenia do wbudowanej konsoli gry ze skryptu i potem czyta jej log, zamiast wpisywać je w oknie gry.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Klatki przed i po</a></td><td>Odtwarza ten sam nagrany fragment gry przed zmianą w grafice i po niej, a następnie porównuje klatki piksel po pikselu.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Ray tracing na Macu</a></td><td>Widoki testowe, które pokazują osobno każdy etap oświetlenia ray tracingiem (cienie, odbicia, światło otoczenia), oraz autotesty, które wypisują wynik: zaliczony albo niezaliczony.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Zrzuty ekranu z Vision Pro</a></td><td>Przechwytuje to, co pokazuje aplikacja na Vision Pro, w tym obraz 3D dla każdego oka, w symulatorze i na goglach.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="jeszcze niepotwierdzone" title="jeszcze niepotwierdzone" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Polecane przez Claude, rozszerzone" title="Polecane przez Claude, rozszerzone" width="16" height="16"><img class="o" src="icons/plus.png" alt="Polecane przez Claude, rozszerzone" title="Polecane przez Claude, rozszerzone" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Kompilacja shaderów offline</a></td><td>Kompiluje na Macu kod graficzny ray tracingu, bo symulator go pomija, a błędy wyszłyby inaczej dopiero na urządzeniu.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">Przechwytywanie klatki GPU</a></td><td>Przechwytuje jedną klatkę na układzie graficznym i pokazuje, ile kosztował każdy krok rysowania, żeby znaleźć, co jest wolne.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="jeszcze niepotwierdzone" title="jeszcze niepotwierdzone" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Polecane przez Claude" title="Polecane przez Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Matematyka shaderów</a></td><td>Przelicza powoli i dokładnie efekty dymu i ognia z Quake 3 i sprawdza, czy szybka wersja graficzna rysuje ten sam obraz.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
</tbody>
</table>

## Głos, język i dane

<table class="wide">
<thead><tr><th width="190">Środowisko testowe</th><th>Możliwość</th><th width="60">Skąd</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Pochodzenie</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Zrzuty ekranu na tekst</a></td><td>Zamienia zrzuty ekranu i skany na tekst na Macu, zanim Claude je przeczyta, co chroni prywatność obrazów i zużywa znacznie mniej pamięci Claude.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac wypowiada frazy testowe syntetycznymi głosami do rozpoznawania mowy w aplikacji, więc polecenia głosowe można testować bez niczyjego mówienia.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="jeszcze niepotwierdzone" title="jeszcze niepotwierdzone" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Odtwarzanie dźwięku na urządzeniu</a></td><td>Mac zamienia każdą rozmowę testową w plik dźwiękowy, a aplikacja na telefonie słucha go zamiast mikrofonu, więc funkcje głosowe można testować na prawdziwym telefonie bez niczyjego mówienia.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Frazy dla Siri</a></td><td>Sprawdza, czy frazy wbudowane w aplikację dla Siri, np. „order my usual”, odpowiadają temu, co mówią ludzie; to, czy Siri poprawnie je kieruje, nadal wymaga telefonu.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Migawka wzorcowa</a></td><td>Zapisuje pełne wyniki aplikacji przed przepisaniem kodu, a potem sprawdza, czy przepisana wersja daje dokładnie te same wyniki.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="jeszcze niepotwierdzone" title="jeszcze niepotwierdzone" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Dokładność transkrypcji</a></td><td>Uruchamia zamianę mowy na tekst w aplikacji na publicznych nagraniach z poprawnymi transkrypcjami i liczy, ile znaków jest błędnych.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Kontrola tłumaczeń</a></td><td>Sprawdza, czy każde tłumaczenie zachowuje nazwy, liczby i uzgodnione terminy oraz czy żaden tekst na ekranie nie został bez tłumaczenia. Używane także w Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Prawdziwe dane</a></td><td>Testuje dopasowywanie tras na zestawie prawdziwych nagranych przejazdów zamiast wymyślonych, co ujawniło błędy, których wymyślone testy nie wykryły.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="jeszcze niepotwierdzone" title="jeszcze niepotwierdzone" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Zgodność z oryginalną aplikacją</a></td><td>Porównuje bazę danych w naszej wersji na iPad z bazą z oryginalnej aplikacji na Windows, tabela po tabeli i wiersz po wierszu.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td></tr>
</tbody>
</table>

## Sprzęt, sieci i usługi

<table class="wide">
<thead><tr><th width="190">Środowisko testowe</th><th>Możliwość</th><th width="60">Skąd</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Pochodzenie</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Porównanie ze sprawdzonym urządzeniem</a></td><td>Nagrywa, jak zachowuje się sprawdzony układ (iPhone połączony bezpośrednio ze słuchawkami), i porównuje z nim nagranie naszego mostka.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Przechwytywanie Bluetooth</a></td><td>Nagrywa sam ruch Bluetooth, żeby zobaczyć, co urządzenia faktycznie wysłały, a nie co zgłosiły.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Polecane przez Claude" title="Polecane przez Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Kontrole działania</a></td><td>Sprawdza, czy każda usługa sieciowa odpowiada z internetu i czy trasa, która powinna być zablokowana, jest odrzucana.</td></tr>
</tbody>
</table>

## Sieć

<table class="wide">
<thead><tr><th width="190">Środowisko testowe</th><th>Możliwość</th><th width="60">Skąd</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Pochodzenie</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Sterowanie przeglądarką</a></td><td>Claude otwiera strony w przeglądarce, wypełnia formularze i czyta wynik, żeby sprawdzić, czy witryna działa i dobrze wygląda.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Polecane przez Claude" title="Polecane przez Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Kontrola wdrożenia witryny</a></td><td>Po aktualizacji witryny sprawdza, czy każdy plik dotarł na serwer w całości, a potem sprawdza układ przy szerokościach telefonu, tabletu i komputera.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Specyficzne dla projektu (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Środowisko testowe</th><th>Możliwość</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Pochodzenie</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Mody do gry</a></td><td>Wczytuje każdy popularny mod wieloosobowy do naszej wersji gry, uruchamia mapę i sprawdza log pod kątem błędów.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="jeszcze niepotwierdzone" title="jeszcze niepotwierdzone" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Obok oryginału</a></td><td>Nagrywa tę samą scenę w naszej wersji i w oryginalnej grze, obok siebie, żeby pokazać wszelkie różnice.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="jeszcze niepotwierdzone" title="jeszcze niepotwierdzone" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Zrzuty poziomów</a></td><td>Robi zdjęcie każdej mapy z ujęcia kamery wybranego przez jej autora i układa je na jednym arkuszu.</td></tr>
</tbody>
</table>

### Prace nad językiem migowym

<table>
<thead><tr><th width="190">Środowisko testowe</th><th>Możliwość</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Pochodzenie</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Porównanie ruchu</a></td><td>Odtwarza wygenerowaną komputerowo migającą dłoń obok prawdziwej osoby migającej, na podstawie której ją stworzono, klatka po klatce, żeby sprawdzić, czy ruch się zgadza.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Środowisko testowe</th><th>Możliwość</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Pochodzenie</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Sprawdzanie cytowanych wartości</a></td><td>Zanim Claude zacytuje datę lub liczbę z dokumentu, sprawdza, czy dokładnie taki tekst naprawdę występuje w tym dokumencie.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
</tbody>
</table>

### Mostek Bluetooth Ranger

<table>
<thead><tr><th width="190">Środowisko testowe</th><th>Możliwość</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Pochodzenie</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Sondy i panel mostka</a></td><td>Małe programy testowe i panel na żywo dla rowerowego mostka audio Bluetooth, pokazujące bufory dźwięku, siłę sygnału i połączenia podczas jazdy.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
</tbody>
</table>

### Portal rezerwacji

<table>
<thead><tr><th width="190">Środowisko testowe</th><th>Możliwość</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Pochodzenie</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Rezerwacja na próbę</a></td><td>Przechodzi przez rezerwację online aż do ostatniego kroku i się zatrzymuje, więc kroki można przetestować bez dokonywania prawdziwej rezerwacji.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Środowisko testowe</th><th>Możliwość</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Pochodzenie</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Kontrola animacji</a></td><td>Mierzy animowany diagram w trakcie odtwarzania, sprawdzając z dokładnością do ułamka piksela, czy elementy są wyrównane i nie nachodzą na siebie.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="działa w tej wersji" title="działa w tej wersji" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Zbudowane przez nas" title="Zbudowane przez nas" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Bardziej techniczna wersja, przeznaczona do wczytania do Claude, to [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) na GitHub.
