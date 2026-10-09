# Kerangka ujian automatik Claude

<details class="langs" data-current="ms">
<summary>Bahasa</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · **Bahasa Melayu** · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Cara untuk Claude Code menyemak kerjanya sendiri: menjalankan aplikasi, merakam sesuatu yang boleh dibacanya, dan memutuskan lulus atau gagal sebelum seseorang perlu melihatnya. Setiap nama membuka halaman dengan resipi penuh. Halaman kerangka ujian itu sendiri dalam bahasa Inggeris.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Disyorkan oleh Claude" title="Disyorkan oleh Claude" width="16" height="16"></td><td><b>Disyorkan oleh Claude</b>: alat standard yang digunakan seadanya</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Disyorkan oleh Claude, dilanjutkan" title="Disyorkan oleh Claude, dilanjutkan" width="16" height="16"><img class="o" src="icons/plus.png" alt="Disyorkan oleh Claude, dilanjutkan" title="Disyorkan oleh Claude, dilanjutkan" width="16" height="16"></td><td><b>Disyorkan oleh Claude, dilanjutkan</b>: alat standard yang perlu kami tambah sebelum ia berfungsi</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td><td><b>Dibina oleh kami</b>: kaedah yang perlu kami cari sendiri</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"> berfungsi pada versi itu · <img class="o t" src="icons/square.png" alt="belum disahkan" title="belum disahkan" width="16" height="16"> belum disahkan · <img class="o t" src="icons/xmark.square.png" alt="belum berfungsi di situ" title="belum berfungsi di situ" width="16" height="16"> belum berfungsi di situ

Kerangka ujian yang tidak bergantung pada versi OS dikira berfungsi pada kedua-duanya. Selebihnya ditanda berdasarkan bila setiap satu terakhir digunakan; Mac ini beralih ke 27 pada 2 Oktober 2026, dan semakan satu per satu terhadap seni bina 27 masih belum dibuat.

**Dari**: aplikasi tempat setiap kerangka ujian mula-mula dibina

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Aplikasi pada simulator, Mac & peranti

<table class="wide">
<thead><tr><th width="190">Kerangka ujian</th><th>Keupayaan</th><th width="60">Dari</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Simulator latar belakang</a></td><td>Claude membina aplikasi iPhone, menjalankannya dalam simulator di latar belakang dan mengambil tangkapan skrin serta log sendiri, supaya ia boleh menyemak skrin tanpa mengambil alih skrin anda.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Disyorkan oleh Claude, dilanjutkan" title="Disyorkan oleh Claude, dilanjutkan" width="16" height="16"><img class="o" src="icons/plus.png" alt="Disyorkan oleh Claude, dilanjutkan" title="Disyorkan oleh Claude, dilanjutkan" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Pengukur susun atur</a></td><td>Claude mengukur apa yang sebenarnya disusun pada skrin, seperti ketinggian bar dan kedudukan tatal, dari saat ke saat semasa anda beralih antara skrin, supaya ia boleh mencari sebab sesuatu kelihatan salah dan bukan meneka.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Cangkuk argumen pelancaran</a></td><td>Suis tersembunyi dalam binaan ujian yang membuka aplikasi terus pada skrin pilihan dengan data contoh, supaya Claude boleh sampai ke mana-mana skrin tanpa mengetik melalui aplikasi.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">Aplikasi iPad pada Mac</a></td><td>Menjalankan versi iPad sesebuah aplikasi sebagai aplikasi Mac biasa, supaya Claude boleh mengujinya pada Mac dengan log dan tangkapan skrin tetingkapnya.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Disyorkan oleh Claude, dilanjutkan" title="Disyorkan oleh Claude, dilanjutkan" width="16" height="16"><img class="o" src="icons/plus.png" alt="Disyorkan oleh Claude, dilanjutkan" title="Disyorkan oleh Claude, dilanjutkan" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript dan tangkapan skrin</a></td><td>Apabila Claude tidak dapat mengawal skrin secara langsung, ia mengendalikan aplikasi Mac dengan AppleScript dan mengambil gambar tetingkapnya sahaja untuk melihat hasilnya.</td></tr>
<tr><td><a href="unit-test-suites.md">Ujian unit</a></td><td>Ujian automatik untuk logik dalaman aplikasi, seperti pemarkahan, laluan dan baris gilir, yang berjalan dalam beberapa saat tanpa membuka aplikasi.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Disyorkan oleh Claude" title="Disyorkan oleh Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Senarai semak untuk manusia sahaja</a></td><td>Satu senarai berterusan bagi semakan yang hanya boleh dibuat oleh manusia, seperti memakai set kepala atau menggunakan telefon sebenar, supaya kerja lain tidak perlu menunggunya.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Bina setiap sasaran</a></td><td>Membina semula versi iPhone, Mac dan Vision Pro bersama-sama selepas sesuatu perubahan, dan menyemak bahawa tetapan ujian tidak pernah disimpan ke dalam tetapan pemain sendiri.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Pratonton langsung SwiftUI</a></td><td>Memaparkan satu skrin dalam pratonton langsung Xcode dan mengambil gambarnya, supaya Claude boleh menyemak perubahan susun atur tanpa membina dan menjalankan keseluruhan permainan.</td><td class="m"><img class="o t" src="icons/square.png" alt="belum disahkan" title="belum disahkan" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Ketik melalui kebolehcapaian</a></td><td>Mengetik butang dalam simulator pada kedudukan yang dilaporkan oleh aplikasi itu sendiri, dan bukan meneka kedudukannya daripada tangkapan skrin.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Disyorkan oleh Claude" title="Disyorkan oleh Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Dua simulator sebagai dua orang</a></td><td>Menjalankan aplikasi pada dua iPhone simulasi sebagai dua orang berbeza, supaya jemputan, cabaran dan penyegerakan boleh diuji tanpa dua telefon sebenar.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="belum disahkan" title="belum disahkan" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Setiap skrin dalam setiap bahasa</a></td><td>Mengambil gambar setiap skrin utama dalam setiap bahasa, serta satu bahasa rekaan dengan perkataan yang sangat panjang, pada satu helaian, supaya teks yang tidak muat mudah dikesan.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Laporan ranap</a></td><td>Menarik laporan ranap daripada iPhone sebenar dan membacanya, supaya ranap yang hanya berlaku pada telefon mendapat punca yang jelas.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="belum disahkan" title="belum disahkan" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Disyorkan oleh Claude" title="Disyorkan oleh Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Suite ujian kecil</a></td><td>Satu set kecil semakan automatik yang lengkap sendiri untuk alat Python, yang boleh berjalan di mana-mana tanpa memasang apa-apa.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td></tr>
</tbody>
</table>

## Grafik & permainan

<table class="wide">
<thead><tr><th width="190">Kerangka ujian</th><th>Keupayaan</th><th width="60">Dari</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Mengendalikan konsol permainan</a></td><td>Menghantar arahan ke konsol terbina dalam permainan daripada skrip dan membaca lognya selepas itu, dan bukan menaip ke dalam tetingkap permainan.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="5"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Bingkai sebelum dan selepas</a></td><td>Memainkan klip permainan rakaman yang sama sebelum dan selepas perubahan grafik dan membandingkan bingkainya piksel demi piksel.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Penjejakan sinar pada Mac</a></td><td>Paparan ujian yang menunjukkan setiap langkah pencahayaan penjejakan sinar (bayang-bayang, pantulan, cahaya ambien) secara berasingan, serta semakan kendiri yang mencetak lulus atau gagal.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Tangkapan skrin Vision Pro</a></td><td>Merakam apa yang dipaparkan oleh aplikasi Vision Pro, termasuk pandangan setiap mata dalam 3D, dalam simulator dan pada set kepala.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Disyorkan oleh Claude, dilanjutkan" title="Disyorkan oleh Claude, dilanjutkan" width="16" height="16"><img class="o" src="icons/plus.png" alt="Disyorkan oleh Claude, dilanjutkan" title="Disyorkan oleh Claude, dilanjutkan" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Kompilasi shader luar talian</a></td><td>Mengkompil kod grafik penjejakan sinar pada Mac, kerana simulator melangkauinya dan jika tidak, kesilapan hanya akan kelihatan pada peranti.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">Tangkapan bingkai GPU</a></td><td>Menangkap satu bingkai pada cip grafik dan menyenaraikan kos setiap langkah lukisan, untuk mencari apa yang perlahan.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="belum disahkan" title="belum disahkan" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Disyorkan oleh Claude" title="Disyorkan oleh Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Matematik shader</a></td><td>Mengira semula kesan asap dan api Quake 3 secara perlahan dan tepat, dan menyemak bahawa versi grafik yang pantas melukis gambar yang sama.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

## Suara, bahasa & data

<table class="wide">
<thead><tr><th width="190">Kerangka ujian</th><th>Keupayaan</th><th width="60">Dari</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Tangkapan skrin kepada teks</a></td><td>Menukar tangkapan skrin dan imbasan kepada teks pada Mac sebelum Claude membacanya, yang memastikan imej kekal peribadi dan menggunakan jauh kurang memori Claude.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac menuturkan frasa ujian dengan suara sintetik ke dalam pengecam pertuturan aplikasi, supaya arahan suara boleh diuji tanpa sesiapa bercakap.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="belum disahkan" title="belum disahkan" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Main semula audio pada peranti</a></td><td>Mac menukar setiap perbualan ujian kepada fail audio dan aplikasi pada telefon mendengarnya sebagai ganti mikrofon, supaya ciri suara boleh diuji pada telefon sebenar tanpa sesiapa bercakap.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Frasa Siri</a></td><td>Menyemak bahawa frasa yang terbina dalam aplikasi untuk Siri, seperti &quot;order my usual&quot;, sepadan dengan apa yang orang katakan; sama ada Siri menghalakannya dengan betul masih memerlukan telefon.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Syot kilat rujukan</a></td><td>Menyimpan output penuh aplikasi sebelum penulisan semula, kemudian menyemak bahawa versi yang ditulis semula menghasilkan output yang sama persis.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="belum disahkan" title="belum disahkan" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Ketepatan transkripsi</a></td><td>Menjalankan fungsi pertuturan-ke-teks aplikasi pada rakaman awam yang disertakan dengan transkrip yang betul, dan mengira berapa banyak aksara yang salah.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Semakan terjemahan</a></td><td>Menyemak bahawa setiap terjemahan mengekalkan nama, nombor dan istilah yang dipersetujui, dan tiada teks pada skrin yang tertinggal tanpa diterjemah. Digunakan untuk Quake 3 juga.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Data sebenar</a></td><td>Menguji padanan laluan pada satu set kayuhan sebenar yang dirakam dan bukan yang direka, dan ini menemui pepijat yang terlepas oleh ujian rekaan.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="belum disahkan" title="belum disahkan" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Padankan aplikasi asal</a></td><td>Membandingkan pangkalan data dalam versi iPad kami dengan pangkalan data daripada aplikasi Windows asal, jadual demi jadual dan baris demi baris.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td></tr>
</tbody>
</table>

## Perkakasan, rangkaian & perkhidmatan

<table class="wide">
<thead><tr><th width="190">Kerangka ujian</th><th>Keupayaan</th><th width="60">Dari</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Bandingkan dengan peranti yang diketahui baik</a></td><td>Merakam kelakuan persediaan yang diketahui berfungsi dengan baik (iPhone yang berhubung terus dengan fon telinga) dan membandingkan rakaman jambatan kami dengannya.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Rakaman Bluetooth</a></td><td>Merakam trafik Bluetooth itu sendiri, untuk melihat apa yang benar-benar dihantar oleh peranti dan bukan apa yang dilaporkannya.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Disyorkan oleh Claude" title="Disyorkan oleh Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Semakan kesihatan</a></td><td>Menyemak bahawa setiap perkhidmatan web menjawab dari internet, dan laluan yang sepatutnya disekat ditolak.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Kerangka ujian</th><th>Keupayaan</th><th width="60">Dari</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Mengendalikan pelayar</a></td><td>Claude membuka halaman dalam pelayar, mengisi borang dan membaca hasilnya, untuk menyemak bahawa laman berfungsi dan kelihatan betul.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Disyorkan oleh Claude" title="Disyorkan oleh Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Semakan kemas kini laman web</a></td><td>Selepas laman web dikemas kini, menyemak bahawa setiap fail tiba di pelayan dengan utuh, kemudian menyemak susun atur pada lebar telefon, tablet dan desktop.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Khusus projek (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Kerangka ujian</th><th>Keupayaan</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Mod permainan</a></td><td>Memuatkan setiap mod berbilang pemain yang popular ke dalam versi permainan kami, memulakan peta dan menyemak log untuk ralat.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="belum disahkan" title="belum disahkan" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Bersebelahan dengan yang asal</a></td><td>Merakam adegan yang sama dalam versi kami dan dalam permainan asal, bersebelahan, untuk menunjukkan sebarang perbezaan.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="belum disahkan" title="belum disahkan" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Tangkapan skrin peta</a></td><td>Mengambil gambar setiap peta dari sudut kamera yang dipilih oleh pencipta peta, dan menyusunnya pada satu helaian.</td></tr>
</tbody>
</table>

### Kerja bahasa isyarat

<table>
<thead><tr><th width="190">Kerangka ujian</th><th>Keupayaan</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Perbandingan gerakan</a></td><td>Memainkan tangan berisyarat janaan komputer di sebelah pengisyarat sebenar yang menjadi asasnya, bingkai demi bingkai, untuk menyemak bahawa gerakannya sepadan.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Kerangka ujian</th><th>Keupayaan</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Semak nilai yang dipetik</a></td><td>Sebelum Claude memetik tarikh atau angka daripada dokumen, ia menyemak bahawa teks yang tepat itu benar-benar terdapat dalam dokumen tersebut.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

### Jambatan Bluetooth Ranger

<table>
<thead><tr><th width="190">Kerangka ujian</th><th>Keupayaan</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Probe jambatan dan papan pemuka</a></td><td>Program ujian kecil dan papan pemuka langsung untuk jambatan audio Bluetooth basikal, yang menunjukkan penimbal bunyi, kekuatan isyarat dan sambungan semasa berkayuh.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

### Portal tempahan

<table>
<thead><tr><th width="190">Kerangka ujian</th><th>Keupayaan</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Tempahan percubaan</a></td><td>Melalui tempahan dalam talian sehingga langkah terakhir dan berhenti, supaya langkah-langkah boleh diuji tanpa membuat tempahan sebenar.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Kerangka ujian</th><th>Keupayaan</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Semakan animasi</a></td><td>Mengukur rajah animasi semasa ia dimainkan, menyemak bahawa bahagiannya sejajar dan tidak bertindih, hingga ketepatan pecahan piksel.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi pada versi itu" title="berfungsi pada versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibina oleh kami" title="Dibina oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Versi yang lebih teknikal, ditulis untuk dimuatkan ke dalam Claude, ialah [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) di GitHub.
