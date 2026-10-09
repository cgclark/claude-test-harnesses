# מערכי בדיקה אוטומטיים ל-Claude

<details class="langs" data-current="he">
<summary>שפה</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · **עברית** · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

דרכים שבהן Claude Code בודק את העבודה של עצמו: מריץ את האפליקציה, לוכד משהו שהוא יכול לקרוא, ומחליט אם הבדיקה עברה או נכשלה לפני שאדם צריך להסתכל. כל שם פותח דף עם המתכון המלא. דפי מערכי הבדיקה עצמם כתובים באנגלית.

<img class="c" src="icons/claude-code.svg" alt="מומלץ על ידי Claude" title="מומלץ על ידי Claude" width="16" height="16"> **מומלץ על ידי Claude**: כלי סטנדרטי בשימוש כמו שהוא (8)<br>
<img class="c" src="icons/claude-code.svg" alt="מומלץ על ידי Claude, מורחב" title="מומלץ על ידי Claude, מורחב" width="16" height="16"><img class="o" src="icons/plus.png" alt="מומלץ על ידי Claude, מורחב" title="מומלץ על ידי Claude, מורחב" width="16" height="16"> **מומלץ על ידי Claude, מורחב**: כלי סטנדרטי שהיינו צריכים להוסיף לו לפני שעבד (4)<br>
<img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"> **נבנה על ידינו**: שיטה שהיינו צריכים לפתח בעצמנו (30)

<img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"> עובד בגרסה הזו · <img class="o t" src="icons/square.png" alt="עדיין לא אומת" title="עדיין לא אומת" width="16" height="16"> עדיין לא אומת · <img class="o t" src="icons/xmark.square.png" alt="עדיין לא עובד שם" title="עדיין לא עובד שם" width="16" height="16"> עדיין לא עובד שם

מערכי בדיקה שאינם תלויים בגרסת מערכת ההפעלה נחשבים כעובדים בשתיהן. השאר מסומנים לפי הפעם האחרונה שבה כל אחד מהם שימש; ה-Mac הזה עבר לגרסה 27 ב-2 באוקטובר 2026, ובדיקה של כל אחד בנפרד מול הארכיטקטורה של 27 עדיין לפנינו.

**מתוך**: האפליקציה שבה כל מערך בדיקה נבנה לראשונה

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/big-top.png" alt="" width="20" height="20"> Big Top</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## אפליקציות בסימולטורים, במחשבי Mac & במכשירים

<table class="wide">
<thead><tr><th width="190">מערך בדיקה</th><th>יכולת</th><th width="60">מתוך</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">מקור</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">סימולטור ברקע</a></td><td>Claude בונה אפליקציית iPhone, מריץ אותה בסימולטור ברקע ואוסף בעצמו צילומי מסך ויומנים, כך שהוא יכול לבדוק מסך בלי להשתלט על המסך שלך.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="מומלץ על ידי Claude, מורחב" title="מומלץ על ידי Claude, מורחב" width="16" height="16"><img class="o" src="icons/plus.png" alt="מומלץ על ידי Claude, מורחב" title="מומלץ על ידי Claude, מורחב" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">בודק פריסה</a></td><td>Claude מודד מה המסך פרס בפועל, כמו גובה סרגלים ומיקומי גלילה, רגע אחר רגע בזמן המעבר בין מסכים, כדי למצוא למה משהו נראה לא נכון במקום לנחש.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">הוקים בארגומנטי הפעלה</a></td><td>מתגים נסתרים בגרסאות בדיקה שפותחים אפליקציה ישר במסך נבחר עם נתוני דוגמה, כך ש-Claude יכול להגיע לכל מסך בלי לעבור בהקשות על פני האפליקציה.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">אפליקציית iPad ב-Mac</a></td><td>מריץ את גרסת ה-iPad של אפליקציה כאפליקציית Mac רגילה, כך ש-Claude יכול לבדוק אותה ב-Mac עם היומנים שלה וצילומי מסך של החלון.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="מומלץ על ידי Claude, מורחב" title="מומלץ על ידי Claude, מורחב" width="16" height="16"><img class="o" src="icons/plus.png" alt="מומלץ על ידי Claude, מורחב" title="מומלץ על ידי Claude, מורחב" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript וצילום מסך</a></td><td>כש-Claude לא יכול לשלוט במסך ישירות, הוא מפעיל אפליקציות Mac באמצעות AppleScript ומצלם רק את החלון שלהן כדי לראות את התוצאה.</td></tr>
<tr><td><a href="unit-test-suites.md">בדיקות יחידה</a></td><td>בדיקות אוטומטיות של הלוגיקה הפנימית של אפליקציה, כמו ניקוד, מסלולים ותורים, שרצות תוך שניות בלי לפתוח את האפליקציה.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="מומלץ על ידי Claude" title="מומלץ על ידי Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">רשימת בדיקות לאדם בלבד</a></td><td>רשימה מתעדכנת אחת של הבדיקות שרק אדם יכול לבצע, כמו חבישת המשקפיים או שימוש בטלפון אמיתי, כדי ששאר העבודה לא תחכה להן.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">בניית כל היעדים</a></td><td>בונה מחדש את גרסאות ה-iPhone, ה-Mac וה-Vision Pro יחד אחרי שינוי, ובודק שהגדרות בדיקה אף פעם לא נשמרות בהגדרות האישיות של שחקן.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">תצוגה מקדימה חיה ב-SwiftUI</a></td><td>מציג מסך אחד בתצוגה המקדימה החיה של Xcode ומצלם אותו, כך ש-Claude יכול לבדוק שינוי פריסה בלי לבנות ולהריץ את כל המשחק.</td><td class="m"><img class="o t" src="icons/square.png" alt="עדיין לא אומת" title="עדיין לא אומת" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">הקשה לפי נגישות</a></td><td>מקיש על כפתורים בסימולטור במיקומים שהאפליקציה עצמה מדווחת, במקום לנחש היכן הם נמצאים לפי צילום מסך.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="מומלץ על ידי Claude" title="מומלץ על ידי Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">שני סימולטורים כשני אנשים</a></td><td>מריץ את האפליקציה בשני מכשירי iPhone מדומים כשני אנשים שונים, כך שאפשר לבדוק הזמנות, אתגרים וסנכרון בלי שני טלפונים אמיתיים.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="עדיין לא אומת" title="עדיין לא אומת" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">כל מסך בכל שפה</a></td><td>מצלם כל מסך ראשי בכל שפה, וגם בשפה מומצאת עם מילים ארוכות במיוחד, על גיליון אחד, כך שקל לזהות טקסט שלא נכנס.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">דוחות קריסה</a></td><td>שולף את דוח הקריסה ממכשיר iPhone אמיתי וקורא אותו, כך שלקריסה שקורית רק בטלפון נמצאת סיבה מוגדרת.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="עדיין לא אומת" title="עדיין לא אומת" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="מומלץ על ידי Claude" title="מומלץ על ידי Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">חבילת בדיקות קטנה</a></td><td>סט קטן ועצמאי של בדיקות אוטומטיות לכלי Python, שרץ בכל מקום בלי להתקין דבר.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td></tr>
</tbody>
</table>

## גרפיקה & משחקים

<table class="wide">
<thead><tr><th width="190">מערך בדיקה</th><th>יכולת</th><th width="60">מתוך</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">מקור</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">הפעלת קונסולת המשחק</a></td><td>שולח פקודות לקונסולה המובנית של המשחק מתוך סקריפט וקורא אחר כך את היומן שלה, במקום להקליד בחלון המשחק.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">פריימים לפני ואחרי</a></td><td>מריץ את אותו קטע משחק מוקלט לפני שינוי גרפי ואחריו, ומשווה את הפריימים פיקסל אחר פיקסל.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">מעקב קרניים ב-Mac</a></td><td>תצוגות בדיקה שמציגות כל שלב בתאורת מעקב הקרניים (צללים, השתקפויות, אור סביבתי) בנפרד, וגם בדיקות עצמיות שמדפיסות עבר או נכשל.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">צילומי מסך של Vision Pro</a></td><td>לוכד את מה שאפליקציית ה-Vision Pro מציגה, כולל התמונה של כל עין ב-3D, בסימולטור ובמכשיר עצמו.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="עדיין לא אומת" title="עדיין לא אומת" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="מומלץ על ידי Claude, מורחב" title="מומלץ על ידי Claude, מורחב" width="16" height="16"><img class="o" src="icons/plus.png" alt="מומלץ על ידי Claude, מורחב" title="מומלץ על ידי Claude, מורחב" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">הידור שיידרים מראש</a></td><td>מהדר את קוד הגרפיקה של מעקב הקרניים ב-Mac, כי הסימולטור מדלג עליו, ואחרת טעויות היו מתגלות רק במכשיר.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">לכידת פריים ב-GPU</a></td><td>לוכד פריים אחד בשבב הגרפי ומפרט כמה עלה כל שלב ציור, כדי למצוא מה איטי.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="עדיין לא אומת" title="עדיין לא אומת" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="מומלץ על ידי Claude" title="מומלץ על ידי Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">מתמטיקת שיידרים</a></td><td>מחשב מחדש את אפקטי העשן והאש של Quake 3 לאט ובדיוק, ובודק שהגרסה הגרפית המהירה מציירת את אותה תמונה.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
</tbody>
</table>

## קול, שפה & נתונים

<table class="wide">
<thead><tr><th width="190">מערך בדיקה</th><th>יכולת</th><th width="60">מתוך</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">מקור</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">מצילומי מסך לטקסט</a></td><td>ממיר צילומי מסך וסריקות לטקסט ב-Mac לפני ש-Claude קורא אותם, וכך התמונות נשארות פרטיות ומנוצל הרבה פחות מהזיכרון של Claude.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m" rowspan="8"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>ה-Mac משמיע משפטי בדיקה בקולות סינתטיים אל מזהה הדיבור של האפליקציה, כך שאפשר לבדוק פקודות קוליות בלי שאף אחד ידבר.</td><td class="app-c"><img class="app-sm" src="icons/apps/big-top.png" alt="Big Top" title="Big Top" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="עדיין לא אומת" title="עדיין לא אומת" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td></tr>
<tr><td><a href="siri-phrasing-check.md">ניסוחים ל-Siri</a></td><td>בודק שהביטויים שמובנים באפליקציה עבור Siri, כמו &quot;order my usual&quot;, תואמים את מה שאנשים אומרים; כדי לבדוק אם Siri מנתבת אותם נכון עדיין צריך את הטלפון.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">תמונת מצב לייחוס</a></td><td>שומר את הפלט המלא של האפליקציה לפני שכתוב, ואז בודק שהגרסה המשוכתבת מפיקה בדיוק את אותו פלט.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="עדיין לא אומת" title="עדיין לא אומת" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">דיוק התמלול</a></td><td>מריץ את המרת הדיבור לטקסט של האפליקציה על הקלטות ציבוריות שמגיעות עם תמלולים נכונים, ומודד בכמה תווים היא טועה.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">בדיקות תרגום</a></td><td>בודק שכל תרגום שומר על השמות, המספרים והמונחים המוסכמים שלו, ושלא נשאר על המסך טקסט שלא תורגם. משמש גם ל-Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">נתונים אמיתיים</a></td><td>בודק התאמת מסלולים על אוסף של רכיבות אמיתיות שהוקלטו במקום רכיבות מומצאות, וכך נמצאו באגים שהבדיקות המומצאות פספסו.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="עדיין לא אומת" title="עדיין לא אומת" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">התאמה לאפליקציה המקורית</a></td><td>משווה את מסד הנתונים בגרסת ה-iPad שלנו לזה של אפליקציית Windows המקורית, טבלה אחר טבלה ושורה אחר שורה.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td></tr>
</tbody>
</table>

## חומרה, רשתות & שירותים

<table class="wide">
<thead><tr><th width="190">מערך בדיקה</th><th>יכולת</th><th width="60">מתוך</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">מקור</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">השוואה למכשיר שידוע שעובד</a></td><td>מקליט איך מערך שידוע שעובד מתנהג (ה-iPhone שמדבר ישירות עם האוזניות) ומשווה אליו הקלטה של הגשר שלנו.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">לכידות Bluetooth</a></td><td>מקליט את תעבורת ה-Bluetooth עצמה, כדי לראות מה המכשירים שלחו בפועל ולא מה הם דיווחו.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="מומלץ על ידי Claude" title="מומלץ על ידי Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">בדיקות תקינות</a></td><td>בודק שכל שירות ווב עונה מהאינטרנט, ושהנתיב שאמור להיות חסום נדחה.</td></tr>
</tbody>
</table>

## ווב

<table class="wide">
<thead><tr><th width="190">מערך בדיקה</th><th>יכולת</th><th width="60">מתוך</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">מקור</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">הפעלת דפדפן</a></td><td>Claude פותח דפים בדפדפן, ממלא טפסים וקורא את התוצאה, כדי לבדוק שאתר עובד ונראה כמו שצריך.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="מומלץ על ידי Claude" title="מומלץ על ידי Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">בדיקת העלאת אתר</a></td><td>אחרי עדכון אתר, בודק שכל קובץ הגיע לשרת שלם, ואז בודק את הפריסה ברוחב של טלפון, טאבלט ומחשב שולחני.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>ייעודיים לפרויקט (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">מערך בדיקה</th><th>יכולת</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">מקור</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">מודים למשחק</a></td><td>טוען כל מוד פופולרי למשחק מרובה משתתפים לגרסה שלנו של המשחק, מפעיל מפה ובודק ביומן אם יש שגיאות.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="עדיין לא אומת" title="עדיין לא אומת" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">זה לצד זה עם המקור</a></td><td>מקליט את אותה סצנה בגרסה שלנו ובמשחק המקורי, זו לצד זו, כדי להראות כל הבדל.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="עדיין לא אומת" title="עדיין לא אומת" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">צילומי מפות</a></td><td>מצלם כל מפה מזווית המצלמה שבחר יוצר המפה, ומסדר את הצילומים על גיליון אחד.</td></tr>
</tbody>
</table>

### עבודה על שפת סימנים

<table>
<thead><tr><th width="190">מערך בדיקה</th><th>יכולת</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">מקור</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">השוואת תנועה</a></td><td>מציג יד מסמנת שנוצרה במחשב לצד המסמן האמיתי שממנו נוצרה, פריים אחר פריים, כדי לבדוק שהתנועה תואמת.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">מערך בדיקה</th><th>יכולת</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">מקור</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">בדיקת ערכים מצוטטים</a></td><td>לפני ש-Claude מצטט תאריך או נתון ממסמך, נבדק שהטקסט המדויק באמת מופיע במסמך.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
</tbody>
</table>

### גשר ה-Bluetooth Ranger

<table>
<thead><tr><th width="190">מערך בדיקה</th><th>יכולת</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">מקור</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">בדיקות הגשר ולוח מחוונים</a></td><td>תוכניות בדיקה קטנות ולוח מחוונים חי לגשר האודיו ב-Bluetooth של האופניים, שמציגים מאגרי שמע, עוצמת אות וחיבורים בזמן הרכיבה.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
</tbody>
</table>

### פורטל הזמנות

<table>
<thead><tr><th width="190">מערך בדיקה</th><th>יכולת</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">מקור</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">הזמנת ניסיון</a></td><td>עובר על הזמנה מקוונת עד השלב האחרון ועוצר, כך שאפשר לבדוק את השלבים בלי לבצע הזמנה אמיתית.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">מערך בדיקה</th><th>יכולת</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">מקור</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">בדיקת אנימציה</a></td><td>מודד תרשים מונפש בזמן שהוא מתנגן, ובודק שהחלקים מיושרים ולא חופפים, ברמת דיוק של שבריר פיקסל.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="עובד בגרסה הזו" title="עובד בגרסה הזו" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="נבנה על ידינו" title="נבנה על ידינו" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

גרסה טכנית יותר, שנכתבה לטעינה ל-Claude, היא ה-[README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) ב-GitHub.
