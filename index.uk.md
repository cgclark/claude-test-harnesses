# Автоматизовані тестові обв’язки Claude

<details class="langs" data-current="uk">
<summary>Мова</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · **Українська** · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Способи, якими Claude Code перевіряє власну роботу: запустити застосунок, отримати те, що він може прочитати, і вирішити, пройдено чи ні, ще до того, як доведеться дивитися людині. Кожна назва відкриває сторінку з повним рецептом. Самі сторінки обв’язок — англійською.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td><td><b>Рекомендовано Claude</b>: стандартний інструмент, використаний як є</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude, доповнено" title="Рекомендовано Claude, доповнено" width="16" height="16"><img class="o" src="icons/plus.png" alt="Рекомендовано Claude, доповнено" title="Рекомендовано Claude, доповнено" width="16" height="16"></td><td><b>Рекомендовано Claude, доповнено</b>: стандартний інструмент, який нам довелося доповнити, щоб він запрацював</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td><td><b>Створено нами</b>: метод, який нам довелося розробити</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"> працює в цій версії · <img class="o t" src="icons/square.png" alt="ще не підтверджено" title="ще не підтверджено" width="16" height="16"> ще не підтверджено · <img class="o t" src="icons/xmark.square.png" alt="там поки не працює" title="там поки не працює" width="16" height="16"> там поки не працює

Обв’язки, що не залежать від версії ОС, вважаються робочими в обох. Решту позначено за станом на момент останнього використання; 2 жовтня 2026 року цей Mac перейшов на 27, а поштучна перевірка на архітектурі 27 ще попереду.

**Звідки**: застосунок, у якому кожну обв’язку створили вперше

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Застосунки на симуляторах, Mac & пристроях

<table class="wide">
<thead><tr><th width="190">Обв’язка</th><th>Можливість</th><th width="60">Звідки</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Походження</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Симулятор у фоні</a></td><td>Claude збирає застосунок для iPhone, запускає його в симуляторі у фоновому режимі й сам робить знімки екрана та збирає журнали, тож може перевірити екран, не захоплюючи ваш.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude, доповнено" title="Рекомендовано Claude, доповнено" width="16" height="16"><img class="o" src="icons/plus.png" alt="Рекомендовано Claude, доповнено" title="Рекомендовано Claude, доповнено" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Зонд розмітки</a></td><td>Claude вимірює, як екран насправді розмістив елементи, наприклад висоту панелей і позиції прокручування, мить за миттю, поки ви переходите між екранами, тож може знайти, чому щось виглядає не так, а не вгадувати.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Хуки аргументів запуску</a></td><td>Приховані перемикачі в тестових збірках, які відкривають застосунок одразу на вибраному екрані з демонстраційними даними, тож Claude може дістатися будь-якого екрана, не проклацуючи весь застосунок.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">Застосунок для iPad на Mac</a></td><td>Запускає iPad-версію застосунку як звичайний застосунок для Mac, тож Claude може тестувати її на Mac із журналами та знімками вікна.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude, доповнено" title="Рекомендовано Claude, доповнено" width="16" height="16"><img class="o" src="icons/plus.png" alt="Рекомендовано Claude, доповнено" title="Рекомендовано Claude, доповнено" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript і захоплення екрана</a></td><td>Коли Claude не може керувати екраном напряму, він керує застосунками Mac через AppleScript і фотографує лише їхнє вікно, щоб побачити результат.</td></tr>
<tr><td><a href="unit-test-suites.md">Модульні тести</a></td><td>Автоматичні тести внутрішньої логіки застосунку, як-от підрахунку балів, маршрутів і черг, що виконуються за секунди без відкриття застосунку.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Перевірки лише для людини</a></td><td>Один поточний список перевірок, які може зробити лише людина, як-от надягнути гарнітуру чи скористатися справжнім телефоном, щоб решта роботи на них не чекала.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Збірка всіх цілей</a></td><td>Після зміни перезбирає разом версії для iPhone, Mac і Vision Pro та перевіряє, що тестові налаштування ніколи не зберігаються у власні налаштування гравця.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Живий попередній перегляд SwiftUI</a></td><td>Показує один екран у живому попередньому перегляді Xcode і фотографує його, тож Claude може перевірити зміну розмітки, не збираючи й не запускаючи всю гру.</td><td class="m"><img class="o t" src="icons/square.png" alt="ще не підтверджено" title="ще не підтверджено" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Натискання за даними доступності</a></td><td>Натискає кнопки в симуляторі в тих позиціях, які повідомляє сам застосунок, а не вгадує їхнє розташування за знімком екрана.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Два симулятори як дві людини</a></td><td>Запускає застосунок на двох симульованих iPhone як дві різні людини, тож запрошення, виклики й синхронізацію можна перевірити без двох справжніх телефонів.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="ще не підтверджено" title="ще не підтверджено" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Кожен екран кожною мовою</a></td><td>Фотографує кожен основний екран кожною мовою, а також вигаданою мовою з надзвичайно довгими словами, на одному аркуші, тож текст, що не вміщується, легко помітити.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Звіти про збої</a></td><td>Забирає звіт про збій зі справжнього iPhone і читає його, тож збій, який трапляється лише на телефоні, отримує конкретну причину.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ще не підтверджено" title="ще не підтверджено" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Невеликий набір тестів</a></td><td>Невеликий самодостатній набір автоматичних перевірок для інструмента на Python, який працює будь-де без встановлення будь-чого.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td></tr>
</tbody>
</table>

## Графіка & ігри

<table class="wide">
<thead><tr><th width="190">Обв’язка</th><th>Можливість</th><th width="60">Звідки</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Походження</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Керування консоллю гри</a></td><td>Надсилає команди у вбудовану консоль гри зі скрипту й потім читає її журнал, замість того щоб вводити текст у вікні гри.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Кадри до і після</a></td><td>Відтворює той самий записаний фрагмент гри до і після зміни графіки та порівнює кадри піксель за пікселем.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Трасування променів на Mac</a></td><td>Тестові режими перегляду, що показують кожен етап освітлення з трасуванням променів (тіні, відбиття, розсіяне світло) окремо, а також самоперевірки, які виводять «пройдено» або «не пройдено».</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Знімки екрана Vision Pro</a></td><td>Захоплює те, що показує застосунок для Vision Pro, зокрема зображення для кожного ока в 3D, у симуляторі та на гарнітурі.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ще не підтверджено" title="ще не підтверджено" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude, доповнено" title="Рекомендовано Claude, доповнено" width="16" height="16"><img class="o" src="icons/plus.png" alt="Рекомендовано Claude, доповнено" title="Рекомендовано Claude, доповнено" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Офлайн-компіляція шейдерів</a></td><td>Компілює графічний код трасування променів на Mac, бо симулятор його пропускає, і помилки інакше проявилися б лише на пристрої.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">Захоплення кадру GPU</a></td><td>Захоплює один кадр на графічному чипі й показує, скільки коштував кожен крок малювання, щоб знайти, що працює повільно.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="ще не підтверджено" title="ще не підтверджено" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Математика шейдерів</a></td><td>Повільно й точно перераховує ефекти диму та вогню з Quake 3 і перевіряє, що швидка графічна версія малює таке саме зображення.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
</tbody>
</table>

## Голос, мова & дані

<table class="wide">
<thead><tr><th width="190">Обв’язка</th><th>Можливість</th><th width="60">Звідки</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Походження</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Знімки екрана в текст</a></td><td>Перетворює знімки екрана та скани на текст на Mac ще до того, як Claude їх прочитає; так зображення залишаються приватними, а пам’яті Claude витрачається значно менше.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac промовляє тестові фрази синтетичними голосами в розпізнавач мовлення застосунку, тож голосові команди можна перевірити без участі людини, що говорить.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ще не підтверджено" title="ще не підтверджено" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Відтворення аудіо на пристрої</a></td><td>Mac перетворює кожну тестову розмову на аудіофайл, і застосунок на телефоні слухає його замість мікрофона, тож голосові функції можна перевірити на справжньому телефоні без участі людини, що говорить.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Фрази для Siri</a></td><td>Перевіряє, що вбудовані в застосунок фрази для Siri, як-от «order my usual», збігаються з тим, що кажуть люди; чи правильно Siri їх спрямовує, досі треба перевіряти на телефоні.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Еталонний знімок</a></td><td>Зберігає повний вивід застосунку перед переписуванням, а потім перевіряє, що переписана версія видає точно такий самий вивід.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ще не підтверджено" title="ще не підтверджено" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Точність транскрипції</a></td><td>Запускає перетворення мовлення на текст у застосунку на загальнодоступних записах із правильними транскриптами й оцінює, у скількох символах воно помиляється.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Перевірка перекладів</a></td><td>Перевіряє, що кожен переклад зберігає назви, числа й узгоджені терміни і що жоден текст на екрані не залишився неперекладеним. Використовується й для Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Реальні дані</a></td><td>Перевіряє зіставлення маршрутів на наборі реальних записаних поїздок замість вигаданих, і це виявило помилки, які вигадані тести пропустили.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ще не підтверджено" title="ще не підтверджено" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Збіг з оригінальним застосунком</a></td><td>Порівнює базу даних у нашій версії для iPad з базою з оригінального застосунку для Windows, таблиця за таблицею й рядок за рядком.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td></tr>
</tbody>
</table>

## Обладнання, мережі & сервіси

<table class="wide">
<thead><tr><th width="190">Обв’язка</th><th>Можливість</th><th width="60">Звідки</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Походження</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Порівняння зі справним пристроєм</a></td><td>Записує, як поводиться свідомо справна конфігурація (iPhone, з’єднаний напряму з навушниками), і порівнює з нею запис нашого моста.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Захоплення Bluetooth</a></td><td>Записує сам трафік Bluetooth, щоб побачити, що пристрої насправді надіслали, а не що вони повідомили.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Перевірки працездатності</a></td><td>Перевіряє, що кожен вебсервіс відповідає з інтернету і що маршрут, який має бути заблокований, відхиляється.</td></tr>
</tbody>
</table>

## Веб

<table class="wide">
<thead><tr><th width="190">Обв’язка</th><th>Можливість</th><th width="60">Звідки</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Походження</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Керування браузером</a></td><td>Claude відкриває сторінки в браузері, заповнює форми й читає результат, щоб перевірити, що сайт працює й виглядає правильно.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Рекомендовано Claude" title="Рекомендовано Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Перевірка розгортання сайту</a></td><td>Після оновлення сайту перевіряє, що кожен файл дійшов на сервер неушкодженим, а потім перевіряє розмітку на ширині телефона, планшета й комп’ютера.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Для конкретних проєктів (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Обв’язка</th><th>Можливість</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Походження</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Ігрові моди</a></td><td>Завантажує кожен популярний мультиплеєрний мод у нашу версію гри, запускає мапу й перевіряє журнал на помилки.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="ще не підтверджено" title="ще не підтверджено" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Поруч з оригіналом</a></td><td>Записує ту саму сцену в нашій версії та в оригінальній грі поруч, щоб показати будь-яку різницю.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ще не підтверджено" title="ще не підтверджено" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Знімки рівнів</a></td><td>Робить знімок кожної мапи з того ракурсу камери, який обрав автор мапи, і розкладає їх на одному аркуші.</td></tr>
</tbody>
</table>

### Робота з мовою жестів

<table>
<thead><tr><th width="190">Обв’язка</th><th>Можливість</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Походження</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Порівняння рухів</a></td><td>Відтворює згенеровану комп’ютером руку, що показує жести, поруч зі справжнім виконавцем, з якого її створено, кадр за кадром, щоб перевірити, чи збігаються рухи.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Обв’язка</th><th>Можливість</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Походження</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Перевірка цитованих значень</a></td><td>Перш ніж Claude процитує дату чи число з документа, перевіряє, що точний текст справді є в цьому документі.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
</tbody>
</table>

### Bluetooth-міст Ranger

<table>
<thead><tr><th width="190">Обв’язка</th><th>Можливість</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Походження</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Зонди й панель моста</a></td><td>Невеликі тестові програми та панель у реальному часі для велосипедного аудіомоста Bluetooth, що показують звукові буфери, рівень сигналу й з’єднання під час їзди.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
</tbody>
</table>

### Портал бронювання

<table>
<thead><tr><th width="190">Обв’язка</th><th>Можливість</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Походження</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Пробне бронювання</a></td><td>Проходить онлайн-бронювання аж до останнього кроку й зупиняється, тож кроки можна перевірити без справжнього бронювання.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Обв’язка</th><th>Можливість</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Походження</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Перевірка анімації</a></td><td>Вимірює анімовану діаграму під час відтворення й перевіряє, що частини вирівняні й не перекриваються, з точністю до частки пікселя.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="працює в цій версії" title="працює в цій версії" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Створено нами" title="Створено нами" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Технічніша версія, написана для завантаження в Claude, — це [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) на GitHub.
