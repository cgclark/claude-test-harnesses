# بيئات الاختبار الآلي لـ Claude

<details class="langs" data-current="ar">
<summary>اللغة</summary>

[English](index.md) · **العربية** · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

طرق يتحقق بها Claude Code من عمله بنفسه: يشغّل التطبيق، ويلتقط شيئًا يستطيع قراءته، ويقرر النجاح أو الفشل قبل أن يحتاج أحد إلى النظر. كل اسم يفتح صفحة فيها الطريقة كاملة. صفحات بيئات الاختبار نفسها باللغة الإنجليزية.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="يوصي به Claude" title="يوصي به Claude" width="16" height="16"></td><td><b>يوصي به Claude</b>: أداة قياسية تُستخدم كما هي</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="يوصي به Claude، مع توسيع" title="يوصي به Claude، مع توسيع" width="16" height="16"><img class="o" src="icons/plus.png" alt="يوصي به Claude، مع توسيع" title="يوصي به Claude، مع توسيع" width="16" height="16"></td><td><b>يوصي به Claude، مع توسيع</b>: أداة قياسية اضطررنا إلى الإضافة إليها حتى تعمل</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td><td><b>من صنعنا</b>: طريقة اضطررنا إلى ابتكارها</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"> تعمل على ذلك الإصدار · <img class="o t" src="icons/square.png" alt="لم يتأكد ذلك بعد" title="لم يتأكد ذلك بعد" width="16" height="16"> لم يتأكد ذلك بعد · <img class="o t" src="icons/xmark.square.png" alt="لا تعمل هناك بعد" title="لا تعمل هناك بعد" width="16" height="16"> لا تعمل هناك بعد

بيئات الاختبار التي لا تعتمد على إصدار نظام التشغيل تُعدّ عاملة على الإصدارين. أما البقية فمعلَّمة بحسب آخر استخدام لكل منها؛ انتقل جهاز Mac هذا إلى الإصدار 27 في 2 أكتوبر 2026، ولا يزال فحص كل واحدة منها على حدة وفق بنية 27 قادمًا.

**المصدر**: التطبيق الذي بُنيت فيه كل بيئة اختبار أول مرة

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## التطبيقات على المحاكيات وأجهزة Mac والأجهزة

<table class="wide">
<thead><tr><th width="190">بيئة الاختبار</th><th>القدرة</th><th width="60">المصدر</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">الأصل</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">محاكي في الخلفية</a></td><td>يبني Claude تطبيق iPhone، ويشغّله في المحاكي في الخلفية، ويلتقط لقطات الشاشة والسجلات بنفسه، فيستطيع فحص شاشة دون أن يستولي على شاشتك.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="يوصي به Claude، مع توسيع" title="يوصي به Claude، مع توسيع" width="16" height="16"><img class="o" src="icons/plus.png" alt="يوصي به Claude، مع توسيع" title="يوصي به Claude، مع توسيع" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">مسبار التخطيط</a></td><td>يقيس Claude ما رتّبته الشاشة فعلًا، مثل ارتفاع الأشرطة ومواضع التمرير، لحظة بلحظة أثناء تنقّلك بين الشاشات، ليجد سبب ظهور شيء بشكل خاطئ بدل التخمين.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">خطافات وسائط التشغيل</a></td><td>مفاتيح مخفية في نسخ الاختبار تفتح التطبيق مباشرة على شاشة مختارة ببيانات نموذجية، فيصل Claude إلى أي شاشة دون التنقل في التطبيق بالنقر.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">تطبيق iPad على Mac</a></td><td>يشغّل نسخة iPad من التطبيق كتطبيق Mac عادي، فيستطيع Claude اختباره على Mac مع سجلاته ولقطات نافذته.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="يوصي به Claude، مع توسيع" title="يوصي به Claude، مع توسيع" width="16" height="16"><img class="o" src="icons/plus.png" alt="يوصي به Claude، مع توسيع" title="يوصي به Claude، مع توسيع" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript والتقاط الشاشة</a></td><td>عندما لا يستطيع Claude التحكم في الشاشة مباشرة، يقود تطبيقات Mac عبر AppleScript ويصوّر نافذتها وحدها ليرى النتيجة.</td></tr>
<tr><td><a href="unit-test-suites.md">اختبارات الوحدات</a></td><td>اختبارات آلية للمنطق الداخلي للتطبيق، مثل احتساب النقاط والمسارات وقوائم الانتظار، تعمل في ثوانٍ دون فتح التطبيق.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="يوصي به Claude" title="يوصي به Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">قائمة للبشر فقط</a></td><td>قائمة واحدة مستمرة بالفحوص التي لا يقوم بها إلا إنسان، مثل ارتداء النظارة أو استخدام هاتف حقيقي، كي لا ينتظرها بقية العمل.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">بناء كل الأهداف</a></td><td>يعيد بناء نسخ iPhone وMac وVision Pro معًا بعد أي تغيير، ويتحقق من أن إعدادات الاختبار لا تُحفظ أبدًا في إعدادات اللاعب الخاصة.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">معاينة SwiftUI الحية</a></td><td>يعرض شاشة واحدة في المعاينة الحية في Xcode ويصوّرها، فيستطيع Claude فحص تغيير في التخطيط دون بناء اللعبة كلها وتشغيلها.</td><td class="m"><img class="o t" src="icons/square.png" alt="لم يتأكد ذلك بعد" title="لم يتأكد ذلك بعد" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">النقر عبر إمكانية الوصول</a></td><td>ينقر الأزرار في المحاكي في المواضع التي يعلنها التطبيق نفسه، بدل تخمين أماكنها من لقطة شاشة.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="يوصي به Claude" title="يوصي به Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">محاكيان كشخصين</a></td><td>يشغّل التطبيق على جهازي iPhone محاكيين كشخصين مختلفين، فتُختبر الدعوات والتحديات والمزامنة دون هاتفين حقيقيين.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="لم يتأكد ذلك بعد" title="لم يتأكد ذلك بعد" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">كل شاشة بكل لغة</a></td><td>يصوّر كل شاشة رئيسية بكل لغة، إضافة إلى لغة مختلَقة بكلمات طويلة جدًا، على ورقة واحدة، ليسهل رصد النص الذي لا يتسع.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">تقارير الأعطال</a></td><td>يسحب تقرير العطل من جهاز iPhone حقيقي ويقرؤه، فيصبح للعطل الذي لا يحدث إلا على الهاتف سبب محدد.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="لم يتأكد ذلك بعد" title="لم يتأكد ذلك بعد" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="يوصي به Claude" title="يوصي به Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">مجموعة اختبارات صغيرة</a></td><td>مجموعة صغيرة قائمة بذاتها من الفحوص الآلية لأداة Python، تعمل في أي مكان دون تثبيت أي شيء.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td></tr>
</tbody>
</table>

## الرسومات والألعاب

<table class="wide">
<thead><tr><th width="190">بيئة الاختبار</th><th>القدرة</th><th width="60">المصدر</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">الأصل</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">قيادة وحدة تحكم اللعبة</a></td><td>يرسل الأوامر إلى وحدة التحكم المدمجة في اللعبة من سكربت ثم يقرأ سجلها، بدل الكتابة في نافذة اللعبة.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="5"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">لقطات قبل وبعد</a></td><td>يشغّل المقطع المسجّل نفسه من اللعبة قبل تغيير رسومي وبعده، ويقارن الإطارات بكسلًا ببكسل.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">تتبع الأشعة على Mac</a></td><td>عروض اختبار تُظهر كل خطوة من الإضاءة بتتبع الأشعة (الظلال والانعكاسات والضوء المحيط) منفردة، إضافة إلى فحوص ذاتية تطبع النجاح أو الفشل.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">لقطات شاشة Vision Pro</a></td><td>يلتقط ما يعرضه تطبيق Vision Pro، بما في ذلك رؤية كل عين بالأبعاد الثلاثة، في المحاكي وعلى النظارة.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="يوصي به Claude، مع توسيع" title="يوصي به Claude، مع توسيع" width="16" height="16"><img class="o" src="icons/plus.png" alt="يوصي به Claude، مع توسيع" title="يوصي به Claude، مع توسيع" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">تصريف المظللات دون اتصال</a></td><td>يصرّف شيفرة رسومات تتبع الأشعة على Mac، لأن المحاكي يتخطاها ولولا ذلك لما ظهرت الأخطاء إلا على جهاز.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">التقاط إطار GPU</a></td><td>يلتقط إطارًا واحدًا على شريحة الرسومات ويسرد كلفة كل خطوة رسم، ليجد ما هو بطيء.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="لم يتأكد ذلك بعد" title="لم يتأكد ذلك بعد" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="يوصي به Claude" title="يوصي به Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">رياضيات المظللات</a></td><td>يعيد حساب تأثيرات الدخان والنار في Quake 3 ببطء وبدقة، ويتحقق من أن نسخة الرسومات السريعة ترسم الصورة نفسها.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
</tbody>
</table>

## الصوت واللغة والبيانات

<table class="wide">
<thead><tr><th width="190">بيئة الاختبار</th><th>القدرة</th><th width="60">المصدر</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">الأصل</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">من لقطات الشاشة إلى نص</a></td><td>يحوّل لقطات الشاشة والمستندات الممسوحة إلى نص على Mac قبل أن يقرأها Claude، مما يُبقي الصور خاصة ويستهلك قدرًا أقل بكثير من ذاكرة Claude.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>ينطق Mac عبارات اختبار بأصوات اصطناعية في أداة التعرف على الكلام في التطبيق، فتُختبر الأوامر الصوتية دون أن يتكلم أحد.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="لم يتأكد ذلك بعد" title="لم يتأكد ذلك بعد" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">إعادة تشغيل الصوت على جهاز</a></td><td>يحوّل Mac كل محادثة اختبار إلى ملف صوتي، ويستمع إليه تطبيق الهاتف بدلًا من الميكروفون، فتُختبر الميزات الصوتية على الهاتف الحقيقي دون أن يتكلم أحد.</td></tr>
<tr><td><a href="siri-phrasing-check.md">صياغة عبارات Siri</a></td><td>يتحقق من أن العبارات المدمجة في التطبيق لـ Siri، مثل «order my usual»، تطابق ما يقوله الناس؛ أما توجيه Siri لها توجيهًا صحيحًا فلا يزال يحتاج إلى الهاتف.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">لقطة مرجعية</a></td><td>يحفظ المخرجات الكاملة للتطبيق قبل إعادة كتابته، ثم يتحقق من أن النسخة المعاد كتابتها تنتج المخرجات نفسها تمامًا.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="لم يتأكد ذلك بعد" title="لم يتأكد ذلك بعد" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">دقة النسخ</a></td><td>يشغّل تحويل الكلام إلى نص في التطبيق على تسجيلات عامة مرفقة بنصوص صحيحة، ويحسب عدد الحروف التي يخطئ فيها.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">فحوص الترجمة</a></td><td>يتحقق من أن كل ترجمة تحافظ على أسمائها وأرقامها ومصطلحاتها المتفق عليها، وأنه لم يبقَ أي نص على الشاشة دون ترجمة. يُستخدم أيضًا لـ Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">بيانات حقيقية</a></td><td>يختبر مطابقة المسارات على مجموعة من الرحلات الحقيقية المسجلة بدل رحلات مختلَقة، وقد كشف ذلك أخطاء فاتت الاختبارات المختلَقة.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="لم يتأكد ذلك بعد" title="لم يتأكد ذلك بعد" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">مطابقة التطبيق الأصلي</a></td><td>يقارن قاعدة البيانات في نسختنا لـ iPad بقاعدة بيانات تطبيق Windows الأصلي، جدولًا بجدول وصفًا بصف.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td></tr>
</tbody>
</table>

## العتاد والشبكات والخدمات

<table class="wide">
<thead><tr><th width="190">بيئة الاختبار</th><th>القدرة</th><th width="60">المصدر</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">الأصل</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">المقارنة بجهاز موثوق</a></td><td>يسجّل سلوك إعداد معروف بسلامته (iPhone متصل بالسماعات مباشرة) ويقارن به تسجيلًا لجسرنا.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">التقاطات Bluetooth</a></td><td>يسجّل حركة Bluetooth نفسها، ليرى ما أرسلته الأجهزة فعلًا لا ما أبلغت عنه.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="يوصي به Claude" title="يوصي به Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">فحوص السلامة</a></td><td>يتحقق من أن كل خدمة ويب تستجيب من الإنترنت، وأن المسار الذي يجب حظره مرفوض.</td></tr>
</tbody>
</table>

## الويب

<table class="wide">
<thead><tr><th width="190">بيئة الاختبار</th><th>القدرة</th><th width="60">المصدر</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">الأصل</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">قيادة المتصفح</a></td><td>يفتح Claude صفحات في متصفح، ويملأ النماذج، ويقرأ النتيجة، للتحقق من أن الموقع يعمل ويظهر كما ينبغي.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="يوصي به Claude" title="يوصي به Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">فحص نشر الموقع</a></td><td>بعد تحديث الموقع، يتحقق من وصول كل ملف سليمًا إلى الخادم، ثم يفحص التخطيط بعروض الهاتف والجهاز اللوحي وسطح المكتب.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>خاصة بمشروع (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">بيئة الاختبار</th><th>القدرة</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">الأصل</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">تعديلات اللعبة</a></td><td>يحمّل كل تعديل شائع للعب الجماعي في نسختنا من اللعبة، ويبدأ خريطة، ويفحص السجل بحثًا عن أخطاء.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="لم يتأكد ذلك بعد" title="لم يتأكد ذلك بعد" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">جنبًا إلى جنب مع الأصل</a></td><td>يسجّل المشهد نفسه في نسختنا وفي اللعبة الأصلية جنبًا إلى جنب، ليُظهر أي اختلاف.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="لم يتأكد ذلك بعد" title="لم يتأكد ذلك بعد" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">لقطات المراحل</a></td><td>يلتقط صورة لكل خريطة من زاوية الكاميرا التي اختارها مؤلفها، ويرصّها على ورقة واحدة.</td></tr>
</tbody>
</table>

### مشروع لغة الإشارة

<table>
<thead><tr><th width="190">بيئة الاختبار</th><th>القدرة</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">الأصل</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">مقارنة الحركة</a></td><td>يعرض يدًا تؤدي الإشارات مولّدة بالحاسوب بجانب المؤدي الحقيقي الذي صُنعت منه، إطارًا بإطار، للتحقق من تطابق الحركة.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">بيئة الاختبار</th><th>القدرة</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">الأصل</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">التحقق من القيم المقتبسة</a></td><td>قبل أن يقتبس Claude تاريخًا أو رقمًا من مستند، يتحقق من أن النص نفسه موجود فعلًا في ذلك المستند.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
</tbody>
</table>

### جسر Bluetooth من Ranger

<table>
<thead><tr><th width="190">بيئة الاختبار</th><th>القدرة</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">الأصل</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">مجسات الجسر ولوحة المتابعة</a></td><td>برامج اختبار صغيرة ولوحة متابعة حية لجسر الصوت عبر Bluetooth في الدراجة، تعرض مخازن الصوت وقوة الإشارة والاتصالات أثناء القيادة.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
</tbody>
</table>

### بوابة الحجز

<table>
<thead><tr><th width="190">بيئة الاختبار</th><th>القدرة</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">الأصل</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">حجز تجريبي</a></td><td>يمضي في حجز عبر الإنترنت حتى الخطوة الأخيرة ويتوقف، فتُختبر الخطوات دون إجراء حجز حقيقي.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">بيئة الاختبار</th><th>القدرة</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">الأصل</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">فحص الرسوم المتحركة</a></td><td>يقيس مخططًا متحركًا أثناء تشغيله، ويتحقق بدقة جزء من البكسل من أن القطع متراصفة ولا تتداخل.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="تعمل على ذلك الإصدار" title="تعمل على ذلك الإصدار" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="من صنعنا" title="من صنعنا" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

توجد نسخة أكثر تقنية، مكتوبة لتحميلها في Claude، هي ملف [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) على GitHub.
