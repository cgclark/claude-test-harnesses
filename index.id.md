# Harness pengujian otomatis untuk Claude

<details class="langs" data-current="id">
<summary>Bahasa</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · **Bahasa Indonesia** · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Cara Claude Code memeriksa pekerjaannya sendiri: menjalankan aplikasi, merekam sesuatu yang bisa dibacanya, lalu memutuskan lulus atau gagal sebelum ada orang yang perlu melihat. Setiap nama membuka halaman berisi resep lengkapnya. Halaman harness itu sendiri berbahasa Inggris.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Direkomendasikan Claude" title="Direkomendasikan Claude" width="16" height="16"></td><td><b>Direkomendasikan Claude</b>: alat standar yang dipakai apa adanya</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Direkomendasikan Claude, diperluas" title="Direkomendasikan Claude, diperluas" width="16" height="16"><img class="o" src="icons/plus.png" alt="Direkomendasikan Claude, diperluas" title="Direkomendasikan Claude, diperluas" width="16" height="16"></td><td><b>Direkomendasikan Claude, diperluas</b>: alat standar yang harus kami tambahi dulu agar berfungsi</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td><td><b>Dibuat oleh kami</b>: metode yang harus kami temukan sendiri</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"> berfungsi di versi itu · <img class="o t" src="icons/square.png" alt="belum dikonfirmasi" title="belum dikonfirmasi" width="16" height="16"> belum dikonfirmasi · <img class="o t" src="icons/xmark.square.png" alt="belum berfungsi di sana" title="belum berfungsi di sana" width="16" height="16"> belum berfungsi di sana

Harness yang tidak bergantung pada versi OS dihitung berfungsi di keduanya. Sisanya dicentang berdasarkan kapan masing-masing terakhir dipakai; Mac ini beralih ke 27 pada 2 Oktober 2026, dan pemeriksaan satu per satu terhadap arsitektur 27 masih akan dilakukan.

**Dari**: aplikasi tempat setiap harness pertama kali dibuat

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Aplikasi di simulator, Mac & perangkat

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Kemampuan</th><th width="60">Dari</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Simulator tanpa tampilan</a></td><td>Claude membangun aplikasi iPhone, menjalankannya di simulator di latar belakang, dan mengambil tangkapan layar serta log sendiri, sehingga bisa memeriksa layar tanpa mengambil alih layar Anda.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Direkomendasikan Claude, diperluas" title="Direkomendasikan Claude, diperluas" width="16" height="16"><img class="o" src="icons/plus.png" alt="Direkomendasikan Claude, diperluas" title="Direkomendasikan Claude, diperluas" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Pengukur tata letak</a></td><td>Claude mengukur apa yang benar-benar ditata di layar, seperti tinggi bilah dan posisi gulir, dari waktu ke waktu saat Anda berpindah antarlayar, sehingga bisa menemukan penyebab sesuatu tampak salah alih-alih menebak.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Pengait argumen peluncuran</a></td><td>Sakelar tersembunyi di build pengujian yang membuka aplikasi langsung di layar pilihan dengan data contoh, sehingga Claude bisa mencapai layar mana pun tanpa mengetuk-ngetuk aplikasi.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">Aplikasi iPad di Mac</a></td><td>Menjalankan versi iPad sebuah aplikasi sebagai aplikasi Mac biasa, sehingga Claude bisa mengujinya di Mac lengkap dengan log dan tangkapan layar jendelanya.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Direkomendasikan Claude, diperluas" title="Direkomendasikan Claude, diperluas" width="16" height="16"><img class="o" src="icons/plus.png" alt="Direkomendasikan Claude, diperluas" title="Direkomendasikan Claude, diperluas" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript dan tangkapan layar</a></td><td>Saat Claude tidak bisa mengendalikan layar secara langsung, ia menjalankan aplikasi Mac dengan AppleScript dan memotret jendelanya saja untuk melihat hasilnya.</td></tr>
<tr><td><a href="unit-test-suites.md">Uji unit</a></td><td>Uji otomatis atas logika internal aplikasi, seperti skor, rute, dan antrean, yang berjalan dalam hitungan detik tanpa membuka aplikasi.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Direkomendasikan Claude" title="Direkomendasikan Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Daftar periksa khusus manusia</a></td><td>Satu daftar berjalan berisi pemeriksaan yang hanya bisa dilakukan manusia, seperti memakai headset atau menggunakan ponsel sungguhan, sehingga sisa pekerjaan tidak perlu menunggunya.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Build semua target</a></td><td>Membangun ulang versi iPhone, Mac, dan Vision Pro sekaligus setelah ada perubahan, dan memeriksa bahwa pengaturan uji tidak pernah tersimpan ke pengaturan milik pemain.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Pratinjau langsung SwiftUI</a></td><td>Menampilkan satu layar di pratinjau langsung Xcode dan memotretnya, sehingga Claude bisa memeriksa perubahan tata letak tanpa membangun dan menjalankan seluruh game.</td><td class="m"><img class="o t" src="icons/square.png" alt="belum dikonfirmasi" title="belum dikonfirmasi" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Ketuk lewat aksesibilitas</a></td><td>Mengetuk tombol di simulator pada posisi yang dilaporkan aplikasi itu sendiri, alih-alih menebak letaknya dari tangkapan layar.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Direkomendasikan Claude" title="Direkomendasikan Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Dua simulator sebagai dua orang</a></td><td>Menjalankan aplikasi di dua iPhone simulasi sebagai dua orang berbeda, sehingga undangan, tantangan, dan sinkronisasi bisa diuji tanpa dua ponsel sungguhan.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="belum dikonfirmasi" title="belum dikonfirmasi" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Setiap layar dalam setiap bahasa</a></td><td>Memotret setiap layar utama dalam setiap bahasa, ditambah bahasa karangan dengan kata-kata ekstra panjang, dalam satu lembar, sehingga teks yang tidak muat mudah terlihat.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Laporan crash</a></td><td>Mengambil laporan crash dari iPhone sungguhan dan membacanya, sehingga crash yang hanya terjadi di ponsel mendapat penyebab yang jelas.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="belum dikonfirmasi" title="belum dikonfirmasi" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Direkomendasikan Claude" title="Direkomendasikan Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Rangkaian uji kecil</a></td><td>Sekumpulan kecil pemeriksaan otomatis yang mandiri untuk alat Python, yang bisa berjalan di mana saja tanpa memasang apa pun.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td></tr>
</tbody>
</table>

## Grafis & game

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Kemampuan</th><th width="60">Dari</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Mengendalikan konsol game</a></td><td>Mengirim perintah ke konsol bawaan game dari skrip dan membaca log-nya sesudahnya, alih-alih mengetik di jendela game.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Frame sebelum dan sesudah</a></td><td>Memutar klip game rekaman yang sama sebelum dan sesudah perubahan grafis, lalu membandingkan frame-nya piksel demi piksel.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Ray tracing di Mac</a></td><td>Tampilan uji yang menunjukkan setiap tahap pencahayaan ray tracing (bayangan, pantulan, cahaya sekitar) secara terpisah, ditambah pemeriksaan mandiri yang mencetak lulus atau gagal.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Tangkapan layar Vision Pro</a></td><td>Merekam apa yang ditampilkan aplikasi Vision Pro, termasuk tampilan tiap mata dalam 3D, di simulator dan di headset.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="belum dikonfirmasi" title="belum dikonfirmasi" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Direkomendasikan Claude, diperluas" title="Direkomendasikan Claude, diperluas" width="16" height="16"><img class="o" src="icons/plus.png" alt="Direkomendasikan Claude, diperluas" title="Direkomendasikan Claude, diperluas" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Kompilasi shader offline</a></td><td>Mengompilasi kode grafis ray tracing di Mac, karena simulator melewatinya dan kesalahan baru akan terlihat di perangkat.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">Tangkapan frame GPU</a></td><td>Merekam satu frame di chip grafis dan mencantumkan biaya setiap langkah penggambaran, untuk menemukan apa yang lambat.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="belum dikonfirmasi" title="belum dikonfirmasi" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Direkomendasikan Claude" title="Direkomendasikan Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Matematika shader</a></td><td>Menghitung ulang efek asap dan api Quake 3 secara lambat dan tepat, lalu memeriksa bahwa versi grafis yang cepat menggambar hasil yang sama.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

## Suara, bahasa & data

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Kemampuan</th><th width="60">Dari</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Tangkapan layar ke teks</a></td><td>Mengubah tangkapan layar dan pindaian menjadi teks di Mac sebelum Claude membacanya, sehingga gambar tetap privat dan memori Claude yang terpakai jauh lebih sedikit.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac mengucapkan frasa uji dengan suara sintetis ke pengenal suara aplikasi, sehingga perintah suara bisa diuji tanpa ada yang berbicara.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="belum dikonfirmasi" title="belum dikonfirmasi" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Pemutaran ulang audio di perangkat</a></td><td>Mac mengubah setiap percakapan uji menjadi file audio, lalu aplikasi di ponsel mendengarkannya sebagai ganti mikrofon, sehingga fitur suara bisa diuji di ponsel sungguhan tanpa ada yang berbicara.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Frasa Siri</a></td><td>Memeriksa bahwa frasa yang tertanam di aplikasi untuk Siri, seperti &quot;order my usual&quot;, sesuai dengan yang diucapkan orang; apakah Siri meneruskannya dengan benar masih memerlukan ponsel.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Snapshot referensi</a></td><td>Menyimpan seluruh keluaran aplikasi sebelum ditulis ulang, lalu memeriksa bahwa versi tulis ulangnya menghasilkan keluaran yang persis sama.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="belum dikonfirmasi" title="belum dikonfirmasi" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Akurasi transkripsi</a></td><td>Menjalankan fitur ucapan-ke-teks aplikasi pada rekaman publik yang disertai transkrip yang benar, dan menilai berapa banyak karakter yang salah.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Pemeriksaan terjemahan</a></td><td>Memeriksa bahwa setiap terjemahan mempertahankan nama, angka, dan istilah yang disepakati, serta tidak ada teks di layar yang tertinggal belum diterjemahkan. Juga dipakai untuk Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Data nyata</a></td><td>Menguji pencocokan rute pada sekumpulan perjalanan nyata yang direkam, bukan perjalanan karangan, dan menemukan bug yang terlewat oleh uji karangan.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="belum dikonfirmasi" title="belum dikonfirmasi" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Sama dengan aplikasi asli</a></td><td>Membandingkan database di versi iPad kami dengan database dari aplikasi Windows aslinya, tabel demi tabel dan baris demi baris.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td></tr>
</tbody>
</table>

## Perangkat keras, jaringan & layanan

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Kemampuan</th><th width="60">Dari</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Bandingkan dengan perangkat yang terbukti baik</a></td><td>Merekam perilaku penyiapan yang terbukti baik (iPhone yang terhubung langsung ke earbud) dan membandingkan rekaman jembatan kami dengannya.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Tangkapan Bluetooth</a></td><td>Merekam lalu lintas Bluetooth itu sendiri, untuk melihat apa yang sebenarnya dikirim perangkat, bukan apa yang mereka laporkan.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Direkomendasikan Claude" title="Direkomendasikan Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Pemeriksaan kesehatan</a></td><td>Memeriksa bahwa setiap layanan web merespons dari internet, dan bahwa rute yang seharusnya diblokir memang ditolak.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Harness</th><th>Kemampuan</th><th width="60">Dari</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Mengendalikan browser</a></td><td>Claude membuka halaman di browser, mengisi formulir, dan membaca hasilnya, untuk memeriksa bahwa situs berfungsi dan tampil dengan benar.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Direkomendasikan Claude" title="Direkomendasikan Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Pemeriksaan deploy situs web</a></td><td>Setelah situs web diperbarui, memeriksa bahwa setiap file tiba utuh di server, lalu memeriksa tata letak pada lebar ponsel, tablet, dan desktop.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Khusus proyek (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Harness</th><th>Kemampuan</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Mod game</a></td><td>Memuat setiap mod multiplayer populer ke versi game kami, memulai sebuah map, lalu memeriksa log untuk mencari error.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="belum dikonfirmasi" title="belum dikonfirmasi" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Berdampingan dengan aslinya</a></td><td>Merekam adegan yang sama di versi kami dan di game aslinya, berdampingan, untuk menunjukkan perbedaan apa pun.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="belum dikonfirmasi" title="belum dikonfirmasi" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Tangkapan layar level</a></td><td>Mengambil gambar setiap map dari sudut kamera yang dipilih pembuat map, lalu menatanya dalam satu lembar.</td></tr>
</tbody>
</table>

### Pekerjaan bahasa isyarat

<table>
<thead><tr><th width="190">Harness</th><th>Kemampuan</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Perbandingan gerakan</a></td><td>Memutar tangan berisyarat buatan komputer di samping penutur isyarat asli yang menjadi sumbernya, frame demi frame, untuk memeriksa apakah gerakannya cocok.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Harness</th><th>Kemampuan</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Periksa nilai yang dikutip</a></td><td>Sebelum Claude mengutip tanggal atau angka dari dokumen, memeriksa bahwa teks persisnya memang ada di dokumen itu.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

### Jembatan Bluetooth Ranger

<table>
<thead><tr><th width="190">Harness</th><th>Kemampuan</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Probe dan dasbor jembatan</a></td><td>Program uji kecil dan dasbor langsung untuk jembatan audio Bluetooth di sepeda, yang menampilkan buffer suara, kekuatan sinyal, dan koneksi selama bersepeda.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

### Portal pemesanan

<table>
<thead><tr><th width="190">Harness</th><th>Kemampuan</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Uji coba pemesanan</a></td><td>Menjalani pemesanan online sampai langkah terakhir lalu berhenti, sehingga langkah-langkahnya bisa diuji tanpa membuat pemesanan sungguhan.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Harness</th><th>Kemampuan</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Asal</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Pemeriksaan animasi</a></td><td>Mengukur diagram animasi selagi diputar, memeriksa bahwa bagian-bagiannya sejajar dan tidak bertumpuk, hingga ketelitian sepersekian piksel.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="berfungsi di versi itu" title="berfungsi di versi itu" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Dibuat oleh kami" title="Dibuat oleh kami" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Versi yang lebih teknis, ditulis untuk dimuat ke Claude, adalah [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) di GitHub.
