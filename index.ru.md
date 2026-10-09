# Автоматические тестовые обвязки Claude

<details class="langs" data-current="ru">
<summary>Язык</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · **Русский** · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Способы, которыми Claude Code проверяет собственную работу: запустить приложение, снять то, что он может прочитать, и решить, пройдена проверка или нет, прежде чем человеку придётся смотреть. Каждое название открывает страницу с полным рецептом. Сами страницы тестовых обвязок написаны на английском.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td><td><b>Рекомендовано Claude</b>: стандартный инструмент, используется как есть</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude, доработано" title="Рекомендовано Claude, доработано" width="16" height="16"><img class="o" src="icons/plus.png" alt="Рекомендовано Claude, доработано" title="Рекомендовано Claude, доработано" width="16" height="16"></td><td><b>Рекомендовано Claude, доработано</b>: стандартный инструмент, который пришлось дополнить, чтобы он заработал</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td><td><b>Создано нами</b>: метод, который нам пришлось придумать</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"> работает в этой версии · <img class="o t" src="icons/square.png" alt="пока не подтверждено" title="пока не подтверждено" width="16" height="16"> пока не подтверждено · <img class="o t" src="icons/xmark.square.png" alt="там пока не работает" title="там пока не работает" width="16" height="16"> там пока не работает

Обвязки, не зависящие от версии ОС, считаются работающими в обеих. Остальные отмечены по тому, когда каждая использовалась в последний раз; этот Mac перешёл на 27 2 октября 2026 года, а поочерёдная проверка каждой на архитектуре 27 ещё впереди.

**Откуда**: приложение, в котором каждая обвязка была создана

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Приложения на симуляторах, Mac & устройствах

<table class="wide">
<thead><tr><th width="190">Тестовая обвязка</th><th>Возможность</th><th width="60">Откуда</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Происхождение</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Симулятор в фоне</a></td><td>Claude собирает приложение для iPhone, запускает его в симуляторе в фоновом режиме и сам делает снимки экрана и собирает логи, так что может проверить экран, не занимая ваш.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude, доработано" title="Рекомендовано Claude, доработано" width="16" height="16"><img class="o" src="icons/plus.png" alt="Рекомендовано Claude, доработано" title="Рекомендовано Claude, доработано" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Зонд вёрстки</a></td><td>Claude измеряет, как экран на самом деле разместил элементы, например высоту панелей и положение прокрутки, момент за моментом при переходе между экранами, чтобы найти причину проблемы, а не гадать.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Переключатели в аргументах запуска</a></td><td>Скрытые переключатели в тестовых сборках, которые открывают приложение сразу на нужном экране с примерными данными, так что Claude может попасть на любой экран, не пролистывая всё приложение.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">Приложение для iPad на Mac</a></td><td>Запускает версию приложения для iPad как обычное приложение для Mac, так что Claude может тестировать его на Mac по логам и снимкам окна.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude, доработано" title="Рекомендовано Claude, доработано" width="16" height="16"><img class="o" src="icons/plus.png" alt="Рекомендовано Claude, доработано" title="Рекомендовано Claude, доработано" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript и снимки экрана</a></td><td>Когда Claude не может управлять экраном напрямую, он управляет приложениями Mac через AppleScript и снимает только их окно, чтобы увидеть результат.</td></tr>
<tr><td><a href="unit-test-suites.md">Модульные тесты</a></td><td>Автоматические тесты внутренней логики приложения, например подсчёта очков, маршрутов и очередей, которые выполняются за секунды без открытия приложения.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Список только для человека</a></td><td>Единый текущий список проверок, которые может сделать только человек, например надеть гарнитуру или взять настоящий телефон, чтобы остальная работа их не ждала.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Сборка всех целей</a></td><td>После изменения пересобирает вместе версии для iPhone, Mac и Vision Pro и проверяет, что тестовые настройки никогда не сохраняются в собственные настройки игрока.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Живой предпросмотр SwiftUI</a></td><td>Показывает один экран в живом предпросмотре Xcode и снимает его, так что Claude может проверить изменение вёрстки, не собирая и не запуская всю игру.</td><td class="m"><img class="o t" src="icons/square.png" alt="пока не подтверждено" title="пока не подтверждено" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Нажатия по данным доступности</a></td><td>Нажимает кнопки в симуляторе в тех местах, которые сообщает само приложение, а не угадывает их положение по снимку экрана.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Два симулятора как два человека</a></td><td>Запускает приложение на двух симулированных iPhone от имени двух разных людей, так что приглашения, вызовы и синхронизацию можно проверить без двух настоящих телефонов.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="пока не подтверждено" title="пока не подтверждено" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Каждый экран на каждом языке</a></td><td>Снимает каждый основной экран на каждом языке, а также на выдуманном языке с очень длинными словами, на одном листе, так что текст, который не помещается, легко заметить.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Отчёты о сбоях</a></td><td>Забирает отчёт о сбое с настоящего iPhone и читает его, так что у сбоя, который происходит только на телефоне, появляется конкретная причина.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="пока не подтверждено" title="пока не подтверждено" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Небольшой набор тестов</a></td><td>Небольшой самодостаточный набор автоматических проверок для инструмента на Python, который работает где угодно без установки чего-либо.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td></tr>
</tbody>
</table>

## Графика & игры

<table class="wide">
<thead><tr><th width="190">Тестовая обвязка</th><th>Возможность</th><th width="60">Откуда</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Происхождение</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Управление через консоль игры</a></td><td>Отправляет команды во встроенную консоль игры из скрипта и затем читает её лог, вместо того чтобы печатать в окне игры.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Кадры до и после</a></td><td>Проигрывает один и тот же записанный фрагмент игры до и после изменения графики и сравнивает кадры пиксель за пикселем.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Трассировка лучей на Mac</a></td><td>Тестовые режимы, которые показывают каждый этап освещения с трассировкой лучей (тени, отражения, фоновый свет) по отдельности, а также самопроверки, выводящие «пройдено» или «не пройдено».</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Снимки экрана Vision Pro</a></td><td>Снимает то, что показывает приложение для Vision Pro, включая изображение для каждого глаза в 3D, в симуляторе и на гарнитуре.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="пока не подтверждено" title="пока не подтверждено" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude, доработано" title="Рекомендовано Claude, доработано" width="16" height="16"><img class="o" src="icons/plus.png" alt="Рекомендовано Claude, доработано" title="Рекомендовано Claude, доработано" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Офлайн-компиляция шейдеров</a></td><td>Компилирует графический код трассировки лучей на Mac, потому что симулятор его пропускает, и иначе ошибки проявились бы только на устройстве.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">Захват кадра GPU</a></td><td>Захватывает один кадр на графическом чипе и показывает, сколько стоил каждый шаг отрисовки, чтобы найти, что тормозит.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="пока не подтверждено" title="пока не подтверждено" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Математика шейдеров</a></td><td>Медленно и точно пересчитывает эффекты дыма и огня из Quake 3 и проверяет, что быстрая графическая версия рисует ту же картинку.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
</tbody>
</table>

## Голос, язык & данные

<table class="wide">
<thead><tr><th width="190">Тестовая обвязка</th><th>Возможность</th><th width="60">Откуда</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Происхождение</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Снимки экрана в текст</a></td><td>Превращает снимки экрана и сканы в текст на Mac до того, как их прочитает Claude: изображения остаются приватными, а памяти Claude тратится гораздо меньше.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac произносит тестовые фразы синтетическими голосами в распознаватель речи приложения, так что голосовые команды можно проверять, и никому не нужно ничего говорить.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="пока не подтверждено" title="пока не подтверждено" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Воспроизведение аудио на устройстве</a></td><td>Mac превращает каждый тестовый разговор в аудиофайл, и приложение на телефоне слушает его вместо микрофона, так что голосовые функции можно проверять на настоящем телефоне, и никому не нужно ничего говорить.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Фразы для Siri</a></td><td>Проверяет, что встроенные в приложение фразы для Siri, например «order my usual», совпадают с тем, что говорят люди; правильно ли Siri их направляет, по-прежнему можно проверить только на телефоне.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Эталонный снимок</a></td><td>Сохраняет полный вывод приложения перед переписыванием, а затем проверяет, что переписанная версия выдаёт точно такой же вывод.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="пока не подтверждено" title="пока не подтверждено" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Точность транскрипции</a></td><td>Прогоняет распознавание речи приложения на открытых записях с правильными расшифровками и подсчитывает, сколько символов оно распознаёт неверно.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Проверка переводов</a></td><td>Проверяет, что каждый перевод сохраняет названия, числа и согласованные термины и что ни один текст на экране не остался без перевода. Используется и для Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Реальные данные</a></td><td>Проверяет сопоставление маршрутов на наборе реальных записанных поездок вместо выдуманных, и это выявило ошибки, которые выдуманные тесты пропустили.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="пока не подтверждено" title="пока не подтверждено" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Совпадение с оригинальным приложением</a></td><td>Сравнивает базу данных в нашей версии для iPad с базой из оригинального приложения для Windows, таблица за таблицей и строка за строкой.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td></tr>
</tbody>
</table>

## Оборудование, сети & сервисы

<table class="wide">
<thead><tr><th width="190">Тестовая обвязка</th><th>Возможность</th><th width="60">Откуда</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Происхождение</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Сравнение с заведомо исправным устройством</a></td><td>Записывает поведение заведомо исправной связки (iPhone, подключённый напрямую к наушникам) и сравнивает с ней запись нашего моста.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Захват Bluetooth</a></td><td>Записывает сам Bluetooth-трафик, чтобы увидеть, что устройства на самом деле отправили, а не что они сообщили.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Проверки работоспособности</a></td><td>Проверяет, что каждый веб-сервис отвечает из интернета и что маршрут, который должен быть заблокирован, отклоняется.</td></tr>
</tbody>
</table>

## Веб

<table class="wide">
<thead><tr><th width="190">Тестовая обвязка</th><th>Возможность</th><th width="60">Откуда</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Происхождение</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Управление браузером</a></td><td>Claude открывает страницы в браузере, заполняет формы и читает результат, чтобы проверить, что сайт работает и выглядит правильно.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Проверка выкладки сайта</a></td><td>После обновления сайта проверяет, что каждый файл дошёл до сервера целым, а затем проверяет вёрстку при ширине телефона, планшета и компьютера.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Для отдельных проектов (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Тестовая обвязка</th><th>Возможность</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Происхождение</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Моды для игры</a></td><td>Загружает каждый популярный многопользовательский мод в нашу версию игры, запускает карту и проверяет лог на ошибки.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="пока не подтверждено" title="пока не подтверждено" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Рядом с оригиналом</a></td><td>Записывает одну и ту же сцену в нашей версии и в оригинальной игре рядом друг с другом, чтобы показать любые различия.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="пока не подтверждено" title="пока не подтверждено" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Снимки уровней</a></td><td>Делает снимок каждой карты с ракурса камеры, выбранного её автором, и раскладывает их на одном листе.</td></tr>
</tbody>
</table>

### Работа с жестовым языком

<table>
<thead><tr><th width="190">Тестовая обвязка</th><th>Возможность</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Происхождение</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Сравнение движений</a></td><td>Показывает сгенерированную компьютером жестикулирующую руку рядом с реальным жестовиком, с которого она сделана, кадр за кадром, чтобы проверить совпадение движений.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Тестовая обвязка</th><th>Возможность</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Происхождение</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Проверка цитируемых значений</a></td><td>Прежде чем Claude процитирует дату или число из документа, проверяет, что именно такой текст действительно есть в этом документе.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
</tbody>
</table>

### Bluetooth-мост Ranger

<table>
<thead><tr><th width="190">Тестовая обвязка</th><th>Возможность</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Происхождение</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Зонды и панель моста</a></td><td>Небольшие тестовые программы и живая панель для велосипедного Bluetooth-аудиомоста, показывающие звуковые буферы, уровень сигнала и подключения во время поездки.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
</tbody>
</table>

### Портал бронирования

<table>
<thead><tr><th width="190">Тестовая обвязка</th><th>Возможность</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Происхождение</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Пробное бронирование</a></td><td>Проходит онлайн-бронирование до последнего шага и останавливается, так что шаги можно проверить, не делая настоящего бронирования.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Тестовая обвязка</th><th>Возможность</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Происхождение</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Проверка анимации</a></td><td>Измеряет анимированную диаграмму во время воспроизведения и проверяет с точностью до доли пикселя, что части совпадают и не перекрываются.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="работает в этой версии" title="работает в этой версии" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Создано нами" title="Создано нами" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Более техническая версия, написанная для загрузки в Claude, — это [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) на GitHub.
