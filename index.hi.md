# Claude के ऑटोमेटेड टेस्ट हार्नेस

<details class="langs" data-current="hi">
<summary>भाषा</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · **हिन्दी** · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Claude Code के लिए अपने काम की खुद जाँच करने के तरीके: ऐप चलाना, कुछ ऐसा कैप्चर करना जिसे वह पढ़ सके, और किसी व्यक्ति के देखने से पहले तय करना कि नतीजा पास है या फ़ेल। हर नाम पर पूरी विधि वाला पेज खुलता है। हार्नेस के पेज खुद अंग्रेज़ी में हैं।

<img class="c" src="icons/claude-code.svg" alt="Claude की सिफ़ारिश" title="Claude की सिफ़ारिश" width="16" height="16"> **Claude की सिफ़ारिश**: एक मानक टूल, जैसा है वैसा इस्तेमाल किया गया (8)<br>
<img class="c" src="icons/claude-code.svg" alt="Claude की सिफ़ारिश, विस्तारित" title="Claude की सिफ़ारिश, विस्तारित" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude की सिफ़ारिश, विस्तारित" title="Claude की सिफ़ारिश, विस्तारित" width="16" height="16"> **Claude की सिफ़ारिश, विस्तारित**: एक मानक टूल, जिसके काम करने से पहले हमें उसमें कुछ जोड़ना पड़ा (4)<br>
<img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"> **हमारा बनाया**: एक तरीका, जो हमें खुद निकालना पड़ा (30)

<img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"> उस वर्शन पर काम करता है · <img class="o t" src="icons/square.png" alt="अभी पुष्टि नहीं हुई" title="अभी पुष्टि नहीं हुई" width="16" height="16"> अभी पुष्टि नहीं हुई · <img class="o t" src="icons/xmark.square.png" alt="वहाँ अभी काम नहीं करता" title="वहाँ अभी काम नहीं करता" width="16" height="16"> वहाँ अभी काम नहीं करता

जो हार्नेस OS वर्शन पर निर्भर नहीं हैं, उन्हें दोनों पर काम करता हुआ माना गया है। बाकी पर निशान इस आधार पर लगे हैं कि हर एक आख़िरी बार कब इस्तेमाल हुआ; यह Mac 2 अक्टूबर 2026 को 27 पर गया, और 27 के आर्किटेक्चर पर एक-एक करके जाँच अभी बाकी है।

**कहाँ से**: वह ऐप जिसमें हर हार्नेस पहली बार बना

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/big-top.png" alt="" width="20" height="20"> Big Top</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## सिम्युलेटर, Mac & डिवाइस पर ऐप

<table class="wide">
<thead><tr><th width="190">हार्नेस</th><th>क्षमता</th><th width="60">कहाँ से</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">स्रोत</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">हेडलेस सिम्युलेटर</a></td><td>Claude एक iPhone ऐप बनाता है, उसे बैकग्राउंड में सिम्युलेटर में चलाता है और खुद स्क्रीनशॉट और लॉग लेता है, ताकि आपकी स्क्रीन पर कब्ज़ा किए बिना किसी स्क्रीन की जाँच कर सके।</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude की सिफ़ारिश, विस्तारित" title="Claude की सिफ़ारिश, विस्तारित" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude की सिफ़ारिश, विस्तारित" title="Claude की सिफ़ारिश, विस्तारित" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">लेआउट प्रोब</a></td><td>जब आप स्क्रीनों के बीच जाते हैं, तब Claude पल-पल मापता है कि स्क्रीन पर असल में क्या लेआउट हुआ, जैसे बार की ऊँचाई और स्क्रॉल की स्थिति, ताकि अंदाज़ा लगाने के बजाय पता लगा सके कि कुछ गलत क्यों दिख रहा है।</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">लॉन्च-आर्ग्युमेंट हुक</a></td><td>टेस्ट बिल्ड में छिपे स्विच, जो ऐप को सैंपल डेटा के साथ सीधे चुनी हुई स्क्रीन पर खोलते हैं, ताकि Claude ऐप में एक-एक करके टैप किए बिना किसी भी स्क्रीन तक पहुँच सके।</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">Mac पर iPad ऐप</a></td><td>किसी ऐप का iPad वर्शन सामान्य Mac ऐप की तरह चलाता है, ताकि Claude उसके लॉग और विंडो स्क्रीनशॉट के साथ Mac पर उसकी जाँच कर सके।</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude की सिफ़ारिश, विस्तारित" title="Claude की सिफ़ारिश, विस्तारित" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude की सिफ़ारिश, विस्तारित" title="Claude की सिफ़ारिश, विस्तारित" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript और स्क्रीन कैप्चर</a></td><td>जब Claude स्क्रीन को सीधे नियंत्रित नहीं कर पाता, तो वह AppleScript से Mac ऐप चलाता है और नतीजा देखने के लिए सिर्फ़ उनकी विंडो की तस्वीर लेता है।</td></tr>
<tr><td><a href="unit-test-suites.md">यूनिट टेस्ट</a></td><td>ऐप के अंदरूनी लॉजिक, जैसे स्कोरिंग, रूट और कतारों, के स्वचालित टेस्ट, जो ऐप खोले बिना कुछ ही सेकंड में चलते हैं।</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude की सिफ़ारिश" title="Claude की सिफ़ारिश" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">सिर्फ़ इंसानों के लिए चेकलिस्ट</a></td><td>उन जाँचों की एक चालू सूची जो सिर्फ़ कोई व्यक्ति कर सकता है, जैसे हेडसेट पहनना या असली फ़ोन इस्तेमाल करना, ताकि बाकी काम उनके इंतज़ार में न रुके।</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">हर टारगेट बिल्ड करें</a></td><td>किसी बदलाव के बाद iPhone, Mac और Vision Pro वर्शन एक साथ फिर से बनाता है, और जाँचता है कि टेस्ट सेटिंग्स कभी किसी खिलाड़ी की अपनी सेटिंग्स में सेव न हों।</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">SwiftUI लाइव प्रीव्यू</a></td><td>Xcode के लाइव प्रीव्यू में एक स्क्रीन दिखाता है और उसकी तस्वीर लेता है, ताकि Claude पूरा गेम बनाए और चलाए बिना लेआउट बदलाव की जाँच कर सके।</td><td class="m"><img class="o t" src="icons/square.png" alt="अभी पुष्टि नहीं हुई" title="अभी पुष्टि नहीं हुई" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">एक्सेसिबिलिटी से टैप</a></td><td>स्क्रीनशॉट से बटनों की जगह का अंदाज़ा लगाने के बजाय, सिम्युलेटर में उन्हें उन जगहों पर टैप करता है जो ऐप खुद बताता है।</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude की सिफ़ारिश" title="Claude की सिफ़ारिश" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">दो सिम्युलेटर, दो लोग</a></td><td>ऐप को दो सिम्युलेटेड iPhone पर दो अलग-अलग लोगों के रूप में चलाता है, ताकि न्योते, चुनौतियाँ और सिंकिंग दो असली फ़ोन के बिना टेस्ट हो सकें।</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="अभी पुष्टि नहीं हुई" title="अभी पुष्टि नहीं हुई" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">हर स्क्रीन, हर भाषा में</a></td><td>हर मुख्य स्क्रीन की हर भाषा में तस्वीर लेता है, साथ में बहुत लंबे शब्दों वाली एक गढ़ी हुई भाषा में भी, और सब एक शीट पर रखता है, ताकि जो टेक्स्ट फ़िट नहीं होता वह आसानी से दिख जाए।</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">क्रैश रिपोर्ट</a></td><td>असली iPhone से क्रैश रिपोर्ट निकालकर पढ़ता है, ताकि जो क्रैश सिर्फ़ फ़ोन पर होता है उसका कारण साफ़ पता चले।</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="अभी पुष्टि नहीं हुई" title="अभी पुष्टि नहीं हुई" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude की सिफ़ारिश" title="Claude की सिफ़ारिश" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">छोटा टेस्ट सूट</a></td><td>Python टूल के लिए स्वचालित जाँचों का एक छोटा, आत्मनिर्भर सेट, जो कुछ भी इंस्टॉल किए बिना कहीं भी चलता है।</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td></tr>
</tbody>
</table>

## ग्राफ़िक्स & गेम

<table class="wide">
<thead><tr><th width="190">हार्नेस</th><th>क्षमता</th><th width="60">कहाँ से</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">स्रोत</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">गेम कंसोल चलाना</a></td><td>गेम विंडो में टाइप करने के बजाय, स्क्रिप्ट से गेम के बिल्ट-इन कंसोल को कमांड भेजता है और बाद में उसका लॉग पढ़ता है।</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">पहले और बाद के फ़्रेम</a></td><td>ग्राफ़िक्स में बदलाव से पहले और बाद में वही रिकॉर्ड की गई गेम क्लिप चलाता है और फ़्रेमों की पिक्सेल-दर-पिक्सेल तुलना करता है।</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Mac पर रे ट्रेसिंग</a></td><td>टेस्ट व्यू, जो रे-ट्रेस्ड लाइटिंग के हर चरण (परछाइयाँ, प्रतिबिंब, आसपास की रोशनी) को अलग-अलग दिखाते हैं, साथ ही सेल्फ़-चेक जो पास या फ़ेल प्रिंट करते हैं।</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Pro स्क्रीनशॉट</a></td><td>सिम्युलेटर और हेडसेट दोनों पर कैप्चर करता है कि Vision Pro ऐप क्या दिखाता है, जिसमें 3D में हर आँख का व्यू भी शामिल है।</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="अभी पुष्टि नहीं हुई" title="अभी पुष्टि नहीं हुई" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude की सिफ़ारिश, विस्तारित" title="Claude की सिफ़ारिश, विस्तारित" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude की सिफ़ारिश, विस्तारित" title="Claude की सिफ़ारिश, विस्तारित" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">ऑफ़लाइन शेडर कंपाइल</a></td><td>रे-ट्रेसिंग ग्राफ़िक्स कोड को Mac पर कंपाइल करता है, क्योंकि सिम्युलेटर उसे छोड़ देता है और वरना गलतियाँ सिर्फ़ डिवाइस पर ही सामने आतीं।</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPU फ़्रेम कैप्चर</a></td><td>ग्राफ़िक्स चिप पर एक फ़्रेम कैप्चर करता है और बताता है कि ड्रॉइंग के हर चरण में कितनी लागत आई, ताकि पता चले कि क्या धीमा है।</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="अभी पुष्टि नहीं हुई" title="अभी पुष्टि नहीं हुई" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude की सिफ़ारिश" title="Claude की सिफ़ारिश" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">शेडर गणित</a></td><td>Quake 3 के धुएँ और आग के इफ़ेक्ट धीरे-धीरे और सटीक रूप से दोबारा गणना करता है, और जाँचता है कि तेज़ ग्राफ़िक्स वर्शन वही तस्वीर बनाता है।</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
</tbody>
</table>

## आवाज़, भाषा & डेटा

<table class="wide">
<thead><tr><th width="190">हार्नेस</th><th>क्षमता</th><th width="60">कहाँ से</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">स्रोत</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">स्क्रीनशॉट से टेक्स्ट</a></td><td>Claude के पढ़ने से पहले Mac पर ही स्क्रीनशॉट और स्कैन को टेक्स्ट में बदलता है, जिससे तस्वीरें निजी रहती हैं और Claude की मेमोरी बहुत कम खर्च होती है।</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m" rowspan="8"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac सिंथेटिक आवाज़ों में टेस्ट वाक्य ऐप के स्पीच रिकग्नाइज़र को सुनाता है, ताकि किसी के बोले बिना वॉइस कमांड टेस्ट हो सकें।</td><td class="app-c"><img class="app-sm" src="icons/apps/big-top.png" alt="Big Top" title="Big Top" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="अभी पुष्टि नहीं हुई" title="अभी पुष्टि नहीं हुई" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td></tr>
<tr><td><a href="siri-phrasing-check.md">Siri वाक्यांश</a></td><td>जाँचता है कि ऐप में Siri के लिए बनाए गए वाक्यांश, जैसे &quot;order my usual&quot;, लोगों के बोलने के तरीके से मेल खाते हैं; Siri उन्हें सही जगह भेजता है या नहीं, इसके लिए अभी भी फ़ोन चाहिए।</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">रेफ़रेंस स्नैपशॉट</a></td><td>दोबारा लिखने से पहले ऐप का पूरा आउटपुट सेव करता है, फिर जाँचता है कि दोबारा लिखा गया वर्शन ठीक वही आउटपुट देता है।</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="अभी पुष्टि नहीं हुई" title="अभी पुष्टि नहीं हुई" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">ट्रांसक्रिप्शन की सटीकता</a></td><td>ऐप का स्पीच-टू-टेक्स्ट ऐसी सार्वजनिक रिकॉर्डिंग पर चलाता है जिनके साथ सही ट्रांसक्रिप्ट आते हैं, और स्कोर करता है कि वह कितने अक्षर गलत करता है।</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">अनुवाद जाँच</a></td><td>जाँचता है कि हर अनुवाद में नाम, संख्याएँ और तय किए गए शब्द बने रहें, और स्क्रीन का कोई टेक्स्ट बिना अनुवाद के न छूटे। Quake 3 के लिए भी इस्तेमाल होता है।</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">असली डेटा</a></td><td>गढ़ी हुई राइड के बजाय रिकॉर्ड की गई असली राइड के सेट पर रूट मिलान को टेस्ट करता है, जिससे वे बग मिले जो गढ़े हुए टेस्ट से छूट गए थे।</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="अभी पुष्टि नहीं हुई" title="अभी पुष्टि नहीं हुई" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">मूल ऐप से मिलान</a></td><td>हमारे iPad वर्शन के डेटाबेस की तुलना मूल Windows ऐप के डेटाबेस से करता है, टेबल-दर-टेबल और पंक्ति-दर-पंक्ति।</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td></tr>
</tbody>
</table>

## हार्डवेयर, नेटवर्क & सेवाएँ

<table class="wide">
<thead><tr><th width="190">हार्नेस</th><th>क्षमता</th><th width="60">कहाँ से</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">स्रोत</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">भरोसेमंद डिवाइस से तुलना</a></td><td>रिकॉर्ड करता है कि एक भरोसेमंद सेटअप (iPhone का सीधे ईयरबड से बात करना) कैसे बर्ताव करता है, और हमारे ब्रिज की रिकॉर्डिंग की उससे तुलना करता है।</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetooth कैप्चर</a></td><td>Bluetooth ट्रैफ़िक को ही रिकॉर्ड करता है, ताकि दिखे कि डिवाइसों ने असल में क्या भेजा, न कि उन्होंने क्या बताया।</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude की सिफ़ारिश" title="Claude की सिफ़ारिश" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">हेल्थ चेक</a></td><td>जाँचता है कि हर वेब सेवा इंटरनेट से जवाब देती है, और जिस रूट को ब्लॉक होना चाहिए वह अस्वीकार होता है।</td></tr>
</tbody>
</table>

## वेब

<table class="wide">
<thead><tr><th width="190">हार्नेस</th><th>क्षमता</th><th width="60">कहाँ से</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">स्रोत</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">ब्राउज़र चलाना</a></td><td>Claude ब्राउज़र में पेज खोलता है, फ़ॉर्म भरता है और नतीजा पढ़ता है, ताकि जाँच सके कि साइट काम करती है और सही दिखती है।</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude की सिफ़ारिश" title="Claude की सिफ़ारिश" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">वेबसाइट डिप्लॉय जाँच</a></td><td>वेबसाइट अपडेट के बाद जाँचता है कि हर फ़ाइल सर्वर पर सही-सलामत पहुँची, फिर फ़ोन, टैबलेट और डेस्कटॉप की चौड़ाई पर लेआउट जाँचता है।</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>प्रोजेक्ट-विशेष (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">हार्नेस</th><th>क्षमता</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">स्रोत</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">गेम मॉड</a></td><td>हर लोकप्रिय मल्टीप्लेयर मॉड को गेम के हमारे वर्शन में लोड करता है, एक मैप शुरू करता है, और लॉग में त्रुटियाँ जाँचता है।</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="अभी पुष्टि नहीं हुई" title="अभी पुष्टि नहीं हुई" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">मूल गेम के साथ-साथ</a></td><td>एक ही सीन को हमारे वर्शन और मूल गेम में साथ-साथ रिकॉर्ड करता है, ताकि कोई भी अंतर दिख जाए।</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="अभी पुष्टि नहीं हुई" title="अभी पुष्टि नहीं हुई" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">लेवल स्क्रीनशॉट</a></td><td>हर मैप की तस्वीर उस कैमरा एंगल से लेता है जो मैप बनाने वाले ने चुना था, और उन्हें एक शीट पर सजाता है।</td></tr>
</tbody>
</table>

### सांकेतिक भाषा का काम

<table>
<thead><tr><th width="190">हार्नेस</th><th>क्षमता</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">स्रोत</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">मोशन तुलना</a></td><td>कंप्यूटर से बने, संकेत करते हाथ को उस असली संकेतकर्ता के बगल में फ़्रेम-दर-फ़्रेम चलाता है जिससे उसे बनाया गया, ताकि जाँचा जा सके कि हरकत मेल खाती है।</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">हार्नेस</th><th>क्षमता</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">स्रोत</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">उद्धृत मानों की जाँच</a></td><td>Claude किसी दस्तावेज़ से तारीख या आँकड़ा उद्धृत करे, उससे पहले जाँचता है कि ठीक वही टेक्स्ट सचमुच उस दस्तावेज़ में है।</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger Bluetooth ब्रिज

<table>
<thead><tr><th width="190">हार्नेस</th><th>क्षमता</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">स्रोत</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">ब्रिज प्रोब और डैशबोर्ड</a></td><td>बाइक के Bluetooth ऑडियो ब्रिज के लिए छोटे टेस्ट प्रोग्राम और एक लाइव डैशबोर्ड, जो राइड के दौरान साउंड बफ़र, सिग्नल की ताकत और कनेक्शन दिखाते हैं।</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
</tbody>
</table>

### बुकिंग पोर्टल

<table>
<thead><tr><th width="190">हार्नेस</th><th>क्षमता</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">स्रोत</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">बुकिंग का ड्राई रन</a></td><td>ऑनलाइन बुकिंग को आख़िरी चरण तक ले जाकर रुक जाता है, ताकि असली बुकिंग किए बिना सारे चरण टेस्ट हो सकें।</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">हार्नेस</th><th>क्षमता</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">स्रोत</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">एनिमेशन जाँच</a></td><td>चलते हुए एनिमेटेड डायग्राम को मापता है, और पिक्सेल के एक अंश तक जाँचता है कि हिस्से ठीक से मिलते हैं और एक-दूसरे पर नहीं चढ़ते।</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="उस वर्शन पर काम करता है" title="उस वर्शन पर काम करता है" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="हमारा बनाया" title="हमारा बनाया" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Claude में लोड करने के लिए लिखा गया एक ज़्यादा तकनीकी वर्शन GitHub पर [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) है।
