# Claude otomatik test düzenekleri

<details class="langs" data-current="tr">
<summary>Dil</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · **Türkçe** · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Claude Code'un kendi işini denetlemesinin yolları: uygulamayı çalıştırmak, okuyabileceği bir çıktı yakalamak ve bir insanın bakmasına gerek kalmadan geçti ya da kaldı kararı vermek. Her ad, tarifin tamamını içeren bir sayfa açar. Test düzeneği sayfalarının kendisi İngilizcedir.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Claude&#x27;un önerisi" title="Claude&#x27;un önerisi" width="16" height="16"></td><td><b>Claude'un önerisi</b>: olduğu gibi kullanılan standart bir araç</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Claude&#x27;un önerisi, genişletilmiş" title="Claude&#x27;un önerisi, genişletilmiş" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude&#x27;un önerisi, genişletilmiş" title="Claude&#x27;un önerisi, genişletilmiş" width="16" height="16"></td><td><b>Claude'un önerisi, genişletilmiş</b>: çalışması için eklemeler yapmamız gereken standart bir araç</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td><td><b>Bizim geliştirdiğimiz</b>: kendimizin bulması gereken bir yöntem</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"> bu sürümde çalışıyor · <img class="o t" src="icons/square.png" alt="henüz doğrulanmadı" title="henüz doğrulanmadı" width="16" height="16"> henüz doğrulanmadı · <img class="o t" src="icons/xmark.square.png" alt="orada henüz çalışmıyor" title="orada henüz çalışmıyor" width="16" height="16"> orada henüz çalışmıyor

İşletim sistemi sürümüne bağlı olmayan test düzenekleri her ikisinde de çalışıyor sayılır. Diğerleri en son kullanıldıkları zamana göre işaretlenmiştir; bu Mac 2 Ekim 2026'da 27'ye geçti ve 27 mimarisine karşı tek tek kontrol henüz yapılmadı.

**Kaynak**: her test düzeneğinin ilk geliştirildiği uygulama

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Simülatörlerde, Mac'lerde & cihazlarda uygulamalar

<table class="wide">
<thead><tr><th width="190">Test düzeneği</th><th>Yetenek</th><th width="60">Kaynak</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Köken</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Arka planda simülatör</a></td><td>Claude bir iPhone uygulamasını derler, simülatörde arka planda çalıştırır ve kendi ekran görüntülerini ve günlüklerini alır; böylece sizin ekranınızı ele geçirmeden bir ekranı kontrol edebilir.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude&#x27;un önerisi, genişletilmiş" title="Claude&#x27;un önerisi, genişletilmiş" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude&#x27;un önerisi, genişletilmiş" title="Claude&#x27;un önerisi, genişletilmiş" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Yerleşim sondası</a></td><td>Claude, siz ekranlar arasında geçerken ekranın gerçekte nasıl yerleştiğini, örneğin çubuk yüksekliklerini ve kaydırma konumlarını, an be an ölçer; böylece bir şeyin neden yanlış göründüğünü tahmin etmek yerine bulabilir.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Başlatma argümanı kancaları</a></td><td>Test derlemelerindeki gizli anahtarlar, uygulamayı örnek verilerle doğrudan seçilen bir ekranda açar; böylece Claude uygulamada dokuna dokuna ilerlemeden herhangi bir ekrana ulaşabilir.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">Mac&#x27;te iPad uygulaması</a></td><td>Bir uygulamanın iPad sürümünü sıradan bir Mac uygulaması olarak çalıştırır; böylece Claude onu Mac&#x27;te, günlükleri ve pencere ekran görüntüleriyle test edebilir.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude&#x27;un önerisi, genişletilmiş" title="Claude&#x27;un önerisi, genişletilmiş" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude&#x27;un önerisi, genişletilmiş" title="Claude&#x27;un önerisi, genişletilmiş" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript ve ekran yakalama</a></td><td>Claude ekranı doğrudan kontrol edemediğinde Mac uygulamalarını AppleScript ile yönetir ve sonucu görmek için yalnızca pencerelerinin fotoğrafını çeker.</td></tr>
<tr><td><a href="unit-test-suites.md">Birim testleri</a></td><td>Bir uygulamanın puanlama, rotalar ve kuyruklar gibi iç mantığına yönelik, uygulamayı açmadan saniyeler içinde çalışan otomatik testler.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude&#x27;un önerisi" title="Claude&#x27;un önerisi" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Yalnızca insanın yapabileceği kontroller</a></td><td>Başlığı takmak ya da gerçek bir telefon kullanmak gibi yalnızca bir insanın yapabileceği kontrollerin tek bir güncel listesi; böylece işin geri kalanı onları beklemez.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Her hedefi derle</a></td><td>Bir değişiklikten sonra iPhone, Mac ve Vision Pro sürümlerini birlikte yeniden derler ve test ayarlarının hiçbir zaman bir oyuncunun kendi ayarlarına kaydedilmediğini kontrol eder.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">SwiftUI canlı önizleme</a></td><td>Tek bir ekranı Xcode&#x27;un canlı önizlemesinde gösterip fotoğrafını çeker; böylece Claude tüm oyunu derleyip çalıştırmadan bir yerleşim değişikliğini kontrol edebilir.</td><td class="m"><img class="o t" src="icons/square.png" alt="henüz doğrulanmadı" title="henüz doğrulanmadı" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Erişilebilirlik bilgisiyle dokunma</a></td><td>Simülatördeki düğmelere, yerlerini bir ekran görüntüsünden tahmin etmek yerine uygulamanın kendisinin bildirdiği konumlardan dokunur.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude&#x27;un önerisi" title="Claude&#x27;un önerisi" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">İki kişi olarak iki simülatör</a></td><td>Uygulamayı iki simüle iPhone&#x27;da iki farklı kişi olarak çalıştırır; böylece davetler, meydan okumalar ve eşitleme iki gerçek telefon olmadan test edilebilir.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="henüz doğrulanmadı" title="henüz doğrulanmadı" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Her dilde her ekran</a></td><td>Her ana ekranın her dildeki hâlini, ayrıca çok uzun kelimeler içeren uydurma bir dildeki hâlini tek bir sayfada fotoğraflar; böylece sığmayan metin kolayca fark edilir.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Çökme raporları</a></td><td>Çökme raporunu gerçek bir iPhone&#x27;dan çekip okur; böylece yalnızca telefonda yaşanan bir çökmenin adı konmuş bir nedeni olur.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="henüz doğrulanmadı" title="henüz doğrulanmadı" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude&#x27;un önerisi" title="Claude&#x27;un önerisi" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Küçük test paketi</a></td><td>Bir Python aracı için, hiçbir şey kurmadan her yerde çalışan, kendi içinde eksiksiz küçük bir otomatik kontrol kümesi.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td></tr>
</tbody>
</table>

## Grafik & oyunlar

<table class="wide">
<thead><tr><th width="190">Test düzeneği</th><th>Yetenek</th><th width="60">Kaynak</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Köken</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Oyun konsolunu yönetme</a></td><td>Oyun penceresine yazmak yerine oyunun yerleşik konsoluna bir betikten komutlar gönderir ve ardından günlüğünü okur.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="5"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Önce ve sonra kareleri</a></td><td>Aynı kayıtlı oyun klibini bir grafik değişikliğinden önce ve sonra oynatır ve kareleri piksel piksel karşılaştırır.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Mac&#x27;te ışın izleme</a></td><td>Işın izlemeli aydınlatmanın her adımını (gölgeler, yansımalar, ortam ışığı) ayrı ayrı gösteren test görünümleri ve geçti ya da kaldı yazdıran öz denetimler.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Pro ekran görüntüleri</a></td><td>Vision Pro uygulamasının gösterdiğini, her gözün 3D görüntüsü dahil, simülatörde ve başlıkta yakalar.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude&#x27;un önerisi, genişletilmiş" title="Claude&#x27;un önerisi, genişletilmiş" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude&#x27;un önerisi, genişletilmiş" title="Claude&#x27;un önerisi, genişletilmiş" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Çevrimdışı gölgelendirici derleme</a></td><td>Işın izleme grafik kodunu Mac&#x27;te derler; çünkü simülatör bu kodu atlar ve hatalar aksi hâlde yalnızca bir cihazda ortaya çıkar.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPU kare yakalama</a></td><td>Grafik çipinde tek bir kareyi yakalar ve neyin yavaş olduğunu bulmak için her çizim adımının maliyetini listeler.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="henüz doğrulanmadı" title="henüz doğrulanmadı" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude&#x27;un önerisi" title="Claude&#x27;un önerisi" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Gölgelendirici matematiği</a></td><td>Quake 3&#x27;ün duman ve ateş efektlerini yavaşça ve tam olarak yeniden hesaplar ve hızlı grafik sürümünün aynı resmi çizdiğini kontrol eder.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
</tbody>
</table>

## Ses, dil & veri

<table class="wide">
<thead><tr><th width="190">Test düzeneği</th><th>Yetenek</th><th width="60">Kaynak</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Köken</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Ekran görüntülerinden metne</a></td><td>Ekran görüntülerini ve taramaları Claude okumadan önce Mac&#x27;te metne dönüştürür; bu, görüntüleri gizli tutar ve Claude&#x27;un belleğinden çok daha azını kullanır.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac, test ifadelerini sentetik seslerle uygulamanın konuşma tanıyıcısına söyler; böylece sesli komutlar kimse konuşmadan test edilebilir.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="henüz doğrulanmadı" title="henüz doğrulanmadı" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Cihazda ses oynatma</a></td><td>Mac, her test konuşmasını bir ses dosyasına dönüştürür ve telefondaki uygulama mikrofon yerine onu dinler; böylece sesli özellikler kimse konuşmadan gerçek telefonda test edilebilir.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Siri ifadeleri</a></td><td>Uygulamaya Siri için yerleştirilmiş “order my usual” gibi ifadelerin insanların söyledikleriyle eşleştiğini kontrol eder; Siri&#x27;nin bunları doğru yönlendirip yönlendirmediği için hâlâ telefon gerekir.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Referans anlık görüntü</a></td><td>Bir yeniden yazımdan önce uygulamanın tüm çıktısını kaydeder, ardından yeniden yazılmış sürümün tam olarak aynı çıktıyı ürettiğini kontrol eder.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="henüz doğrulanmadı" title="henüz doğrulanmadı" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Transkripsiyon doğruluğu</a></td><td>Uygulamanın konuşmayı metne dönüştürme özelliğini, doğru transkriptleriyle birlikte gelen herkese açık kayıtlarda çalıştırır ve kaç karakteri yanlış yaptığını puanlar.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Çeviri kontrolleri</a></td><td>Her çevirinin adları, sayıları ve üzerinde anlaşılan terimleri koruduğunu ve ekrandaki hiçbir metnin çevrilmeden kalmadığını kontrol eder. Quake 3 için de kullanılır.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Gerçek veriler</a></td><td>Rota eşleştirmeyi uydurma sürüşler yerine gerçek kayıtlı sürüşlerden oluşan bir küme üzerinde test eder; bu yöntem, uydurma testlerin kaçırdığı hataları buldu.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="henüz doğrulanmadı" title="henüz doğrulanmadı" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Orijinal uygulamayla eşleşme</a></td><td>iPad sürümümüzdeki veritabanını orijinal Windows uygulamasındakiyle tablo tablo ve satır satır karşılaştırır.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td></tr>
</tbody>
</table>

## Donanım, ağlar & hizmetler

<table class="wide">
<thead><tr><th width="190">Test düzeneği</th><th>Yetenek</th><th width="60">Kaynak</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Köken</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Sorunsuz çalışan bir cihazla karşılaştırma</a></td><td>Sorunsuz çalıştığı bilinen bir düzenin (iPhone&#x27;un doğrudan kulaklıklarla konuşması) nasıl davrandığını kaydeder ve köprümüzün bir kaydını bununla karşılaştırır.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetooth yakalamaları</a></td><td>Cihazların bildirdiklerini değil, gerçekte ne gönderdiklerini görmek için Bluetooth trafiğinin kendisini kaydeder.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude&#x27;un önerisi" title="Claude&#x27;un önerisi" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Sağlık kontrolleri</a></td><td>Her web hizmetinin internetten yanıt verdiğini ve engellenmesi gereken yolun reddedildiğini kontrol eder.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Test düzeneği</th><th>Yetenek</th><th width="60">Kaynak</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Köken</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Tarayıcıyı yönetme</a></td><td>Claude, bir sitenin çalıştığını ve doğru göründüğünü kontrol etmek için sayfaları bir tarayıcıda açar, formları doldurur ve sonucu okur.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude&#x27;un önerisi" title="Claude&#x27;un önerisi" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Web sitesi yayın kontrolü</a></td><td>Bir web sitesi güncellemesinden sonra her dosyanın sunucuya eksiksiz ulaştığını, ardından yerleşimi telefon, tablet ve masaüstü genişliklerinde kontrol eder.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Projeye özel (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Test düzeneği</th><th>Yetenek</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Köken</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Oyun modları</a></td><td>Her popüler çok oyunculu modu oyunun bizim sürümümüze yükler, bir harita başlatır ve günlükte hata olup olmadığını kontrol eder.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="henüz doğrulanmadı" title="henüz doğrulanmadı" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Orijinaliyle yan yana</a></td><td>Olası farkları göstermek için aynı sahneyi bizim sürümümüzde ve orijinal oyunda yan yana kaydeder.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="henüz doğrulanmadı" title="henüz doğrulanmadı" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Seviye ekran görüntüleri</a></td><td>Her haritanın, haritanın yazarının seçtiği kamera açısından bir resmini çeker ve hepsini tek bir sayfaya dizer.</td></tr>
</tbody>
</table>

### İşaret dili çalışması

<table>
<thead><tr><th width="190">Test düzeneği</th><th>Yetenek</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Köken</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Hareket karşılaştırma</a></td><td>Bilgisayarla üretilmiş, işaret yapan bir eli, üretildiği gerçek işaretçinin yanında kare kare oynatarak hareketin eşleştiğini kontrol eder.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Test düzeneği</th><th>Yetenek</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Köken</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Alıntılanan değerleri kontrol etme</a></td><td>Claude bir belgeden bir tarih ya da rakam alıntılamadan önce, tam metnin gerçekten o belgede geçtiğini kontrol eder.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger Bluetooth köprüsü

<table>
<thead><tr><th width="190">Test düzeneği</th><th>Yetenek</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Köken</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Köprü sondaları ve pano</a></td><td>Bisikletin Bluetooth ses köprüsü için küçük test programları ve sürüş sırasında ses arabelleklerini, sinyal gücünü ve bağlantıları gösteren canlı bir pano.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
</tbody>
</table>

### Rezervasyon portalı

<table>
<thead><tr><th width="190">Test düzeneği</th><th>Yetenek</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Köken</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Rezervasyon provası</a></td><td>Çevrimiçi bir rezervasyonu son adıma kadar götürür ve durur; böylece adımlar gerçek bir rezervasyon yapmadan test edilebilir.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Test düzeneği</th><th>Yetenek</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Köken</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Animasyon kontrolü</a></td><td>Animasyonlu bir diyagramı oynarken ölçer ve parçaların hizalandığını ve üst üste binmediğini pikselin bir kesrine kadar kontrol eder.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="bu sürümde çalışıyor" title="bu sürümde çalışıyor" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Bizim geliştirdiğimiz" title="Bizim geliştirdiğimiz" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Claude'a yüklenmek üzere yazılmış daha teknik bir sürüm, GitHub'daki [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) dosyasıdır.
