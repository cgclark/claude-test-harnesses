# Các bộ khung kiểm thử tự động của Claude

<details class="langs" data-current="vi">
<summary>Ngôn ngữ</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · **Tiếng Việt** · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Những cách để Claude Code tự kiểm tra công việc của mình: chạy ứng dụng, thu lại thứ nó đọc được và quyết định đạt hay không đạt trước khi cần đến người xem. Mỗi tên sẽ mở một trang có hướng dẫn đầy đủ. Bản thân các trang về bộ khung kiểm thử được viết bằng tiếng Anh.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Claude đề xuất" title="Claude đề xuất" width="16" height="16"></td><td><b>Claude đề xuất</b>: một công cụ tiêu chuẩn dùng nguyên trạng</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Claude đề xuất, có mở rộng" title="Claude đề xuất, có mở rộng" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude đề xuất, có mở rộng" title="Claude đề xuất, có mở rộng" width="16" height="16"></td><td><b>Claude đề xuất, có mở rộng</b>: một công cụ tiêu chuẩn mà chúng tôi phải bổ sung thì mới hoạt động</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td><td><b>Do chúng tôi xây dựng</b>: một phương pháp chúng tôi phải tự tìm ra</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"> hoạt động trên phiên bản đó · <img class="o t" src="icons/square.png" alt="chưa được xác nhận" title="chưa được xác nhận" width="16" height="16"> chưa được xác nhận · <img class="o t" src="icons/xmark.square.png" alt="chưa hoạt động trên đó" title="chưa hoạt động trên đó" width="16" height="16"> chưa hoạt động trên đó

Các bộ khung kiểm thử không phụ thuộc vào phiên bản hệ điều hành được tính là hoạt động trên cả hai. Số còn lại được đánh dấu theo lần sử dụng gần nhất; chiếc Mac này đã chuyển lên 27 vào ngày 2 tháng 10 năm 2026, và việc kiểm tra lần lượt từng cái trên kiến trúc 27 vẫn chưa được thực hiện.

**Nguồn**: ứng dụng mà mỗi bộ khung kiểm thử được xây dựng lần đầu

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Ứng dụng trên trình mô phỏng, Mac & thiết bị

<table class="wide">
<thead><tr><th width="190">Bộ khung kiểm thử</th><th>Khả năng</th><th width="60">Nguồn</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Xuất xứ</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Trình mô phỏng chạy nền</a></td><td>Claude biên dịch một ứng dụng iPhone, chạy nó trong trình mô phỏng ở chế độ nền và tự chụp ảnh màn hình, lấy nhật ký, nên có thể kiểm tra một màn hình mà không chiếm màn hình của bạn.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude đề xuất, có mở rộng" title="Claude đề xuất, có mở rộng" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude đề xuất, có mở rộng" title="Claude đề xuất, có mở rộng" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Đầu dò bố cục</a></td><td>Claude đo những gì màn hình thực sự bố trí, như chiều cao các thanh và vị trí cuộn, theo từng khoảnh khắc khi bạn chuyển giữa các màn hình, nên có thể tìm ra vì sao có gì đó trông sai thay vì đoán.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Móc tham số khởi chạy</a></td><td>Các công tắc ẩn trong bản dựng thử nghiệm giúp mở ứng dụng thẳng vào một màn hình được chọn với dữ liệu mẫu, nên Claude có thể đến bất kỳ màn hình nào mà không phải chạm qua từng bước trong ứng dụng.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">Ứng dụng iPad trên Mac</a></td><td>Chạy phiên bản iPad của một ứng dụng như một ứng dụng Mac bình thường, nên Claude có thể kiểm thử nó trên Mac cùng với nhật ký và ảnh chụp cửa sổ.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude đề xuất, có mở rộng" title="Claude đề xuất, có mở rộng" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude đề xuất, có mở rộng" title="Claude đề xuất, có mở rộng" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript và chụp màn hình</a></td><td>Khi Claude không thể điều khiển màn hình trực tiếp, nó điều khiển các ứng dụng Mac bằng AppleScript và chỉ chụp riêng cửa sổ của chúng để xem kết quả.</td></tr>
<tr><td><a href="unit-test-suites.md">Kiểm thử đơn vị</a></td><td>Các bài kiểm thử tự động cho logic bên trong của ứng dụng, như tính điểm, tuyến đường và hàng đợi, chạy trong vài giây mà không cần mở ứng dụng.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude đề xuất" title="Claude đề xuất" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Danh sách việc chỉ người làm được</a></td><td>Một danh sách duy nhất, liên tục cập nhật, gồm các bước kiểm tra chỉ con người mới làm được, như đeo kính hay dùng điện thoại thật, để phần việc còn lại không phải chờ chúng.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Biên dịch mọi đích</a></td><td>Biên dịch lại cùng lúc các phiên bản iPhone, Mac và Vision Pro sau một thay đổi, và kiểm tra rằng các thiết lập thử nghiệm không bao giờ bị lưu vào thiết lập riêng của người chơi.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Xem trước trực tiếp SwiftUI</a></td><td>Hiển thị một màn hình trong chế độ xem trước trực tiếp của Xcode và chụp lại, nên Claude có thể kiểm tra một thay đổi bố cục mà không cần biên dịch và chạy cả trò chơi.</td><td class="m"><img class="o t" src="icons/square.png" alt="chưa được xác nhận" title="chưa được xác nhận" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Chạm theo dữ liệu trợ năng</a></td><td>Chạm vào các nút trong trình mô phỏng tại vị trí mà chính ứng dụng báo cáo, thay vì đoán vị trí của chúng từ ảnh chụp màn hình.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude đề xuất" title="Claude đề xuất" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Hai trình mô phỏng như hai người</a></td><td>Chạy ứng dụng trên hai iPhone mô phỏng như hai người khác nhau, nên có thể kiểm thử lời mời, thử thách và đồng bộ mà không cần hai điện thoại thật.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="chưa được xác nhận" title="chưa được xác nhận" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Mọi màn hình bằng mọi ngôn ngữ</a></td><td>Chụp mọi màn hình chính bằng mọi ngôn ngữ, cùng một ngôn ngữ giả lập có từ cực dài, trên một trang, nên dễ phát hiện chữ bị tràn.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Báo cáo sự cố</a></td><td>Lấy báo cáo sự cố từ một iPhone thật và đọc nó, nên một sự cố chỉ xảy ra trên điện thoại sẽ có nguyên nhân được gọi tên cụ thể.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="chưa được xác nhận" title="chưa được xác nhận" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude đề xuất" title="Claude đề xuất" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Bộ kiểm thử nhỏ</a></td><td>Một tập nhỏ, khép kín các bước kiểm tra tự động cho một công cụ Python, chạy được ở bất cứ đâu mà không cần cài đặt gì.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td></tr>
</tbody>
</table>

## Đồ họa & trò chơi

<table class="wide">
<thead><tr><th width="190">Bộ khung kiểm thử</th><th>Khả năng</th><th width="60">Nguồn</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Xuất xứ</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Điều khiển console trò chơi</a></td><td>Gửi lệnh vào console tích hợp của trò chơi từ một script rồi đọc nhật ký của nó sau đó, thay vì gõ vào cửa sổ trò chơi.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Khung hình trước và sau</a></td><td>Phát cùng một đoạn trò chơi đã ghi trước và sau một thay đổi đồ họa, rồi so sánh các khung hình theo từng điểm ảnh.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Dò tia trên Mac</a></td><td>Các chế độ xem thử nghiệm hiển thị riêng từng bước của ánh sáng dò tia (bóng đổ, phản chiếu, ánh sáng môi trường), cùng các bước tự kiểm tra in ra đạt hoặc không đạt.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Ảnh chụp màn hình Vision Pro</a></td><td>Ghi lại những gì ứng dụng Vision Pro hiển thị, bao gồm hình ảnh 3D của từng mắt, trên trình mô phỏng và trên kính.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="chưa được xác nhận" title="chưa được xác nhận" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude đề xuất, có mở rộng" title="Claude đề xuất, có mở rộng" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude đề xuất, có mở rộng" title="Claude đề xuất, có mở rộng" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Biên dịch shader ngoại tuyến</a></td><td>Biên dịch mã đồ họa dò tia trên Mac, vì trình mô phỏng bỏ qua phần này và nếu không thì lỗi chỉ lộ ra trên thiết bị.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">Chụp khung hình GPU</a></td><td>Chụp một khung hình trên chip đồ họa và liệt kê chi phí của từng bước vẽ, để tìm ra phần nào chậm.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="chưa được xác nhận" title="chưa được xác nhận" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude đề xuất" title="Claude đề xuất" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Toán shader</a></td><td>Tính lại chậm rãi và chính xác các hiệu ứng khói và lửa của Quake 3, rồi kiểm tra phiên bản đồ họa nhanh có vẽ ra đúng hình ảnh đó không.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
</tbody>
</table>

## Giọng nói, ngôn ngữ & dữ liệu

<table class="wide">
<thead><tr><th width="190">Bộ khung kiểm thử</th><th>Khả năng</th><th width="60">Nguồn</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Xuất xứ</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">Ảnh chụp màn hình thành văn bản</a></td><td>Chuyển ảnh chụp màn hình và bản quét thành văn bản ngay trên Mac trước khi Claude đọc, giúp giữ hình ảnh riêng tư và dùng ít bộ nhớ của Claude hơn nhiều.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac đọc các câu thử bằng giọng tổng hợp vào bộ nhận dạng giọng nói của ứng dụng, nên có thể kiểm thử lệnh thoại mà không cần ai nói.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="chưa được xác nhận" title="chưa được xác nhận" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Phát lại âm thanh trên thiết bị</a></td><td>Mac chuyển mỗi cuộc hội thoại thử thành một tệp âm thanh và ứng dụng trên điện thoại nghe tệp đó thay cho micrô, nên có thể kiểm thử các tính năng giọng nói trên điện thoại thật mà không cần ai nói.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Câu lệnh Siri</a></td><td>Kiểm tra rằng các câu dành cho Siri được tích hợp trong ứng dụng, như “order my usual”, khớp với cách mọi người nói; còn Siri có chuyển chúng đúng chỗ hay không thì vẫn cần đến điện thoại.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Bản chụp tham chiếu</a></td><td>Lưu toàn bộ đầu ra của ứng dụng trước khi viết lại, rồi kiểm tra phiên bản viết lại cho ra đầu ra y hệt.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="chưa được xác nhận" title="chưa được xác nhận" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Độ chính xác chép lời</a></td><td>Chạy tính năng chuyển giọng nói thành văn bản của ứng dụng trên các bản ghi âm công khai có kèm bản chép lời đúng, và chấm điểm theo số ký tự bị sai.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Kiểm tra bản dịch</a></td><td>Kiểm tra rằng mỗi bản dịch giữ nguyên tên, con số và các thuật ngữ đã thống nhất, và không có chữ nào trên màn hình bị bỏ sót chưa dịch. Cũng được dùng cho Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Dữ liệu thật</a></td><td>Kiểm thử việc khớp tuyến đường trên một tập các chuyến đi thật đã ghi lại thay vì các chuyến bịa ra, và đã tìm ra những lỗi mà các bài kiểm thử bịa ra bỏ sót.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="chưa được xác nhận" title="chưa được xác nhận" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Khớp với ứng dụng gốc</a></td><td>So sánh cơ sở dữ liệu trong phiên bản iPad của chúng tôi với cơ sở dữ liệu của ứng dụng Windows gốc, từng bảng và từng hàng.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td></tr>
</tbody>
</table>

## Phần cứng, mạng & dịch vụ

<table class="wide">
<thead><tr><th width="190">Bộ khung kiểm thử</th><th>Khả năng</th><th width="60">Nguồn</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Xuất xứ</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">So sánh với thiết bị chuẩn</a></td><td>Ghi lại cách một hệ thống đã biết là hoạt động tốt vận hành (iPhone kết nối thẳng với tai nghe) và so sánh bản ghi của cầu nối của chúng tôi với nó.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bắt gói Bluetooth</a></td><td>Ghi lại chính lưu lượng Bluetooth, để thấy các thiết bị thực sự đã gửi gì thay vì những gì chúng báo cáo.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude đề xuất" title="Claude đề xuất" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Kiểm tra tình trạng</a></td><td>Kiểm tra rằng mỗi dịch vụ web đều phản hồi từ internet, và đường dẫn lẽ ra phải bị chặn thì bị từ chối.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Bộ khung kiểm thử</th><th>Khả năng</th><th width="60">Nguồn</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Xuất xứ</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Điều khiển trình duyệt</a></td><td>Claude mở các trang trong trình duyệt, điền biểu mẫu và đọc kết quả, để kiểm tra trang web hoạt động và hiển thị đúng.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude đề xuất" title="Claude đề xuất" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Kiểm tra triển khai trang web</a></td><td>Sau khi cập nhật trang web, kiểm tra mọi tệp đã đến máy chủ nguyên vẹn, rồi kiểm tra bố cục ở độ rộng của điện thoại, máy tính bảng và máy tính để bàn.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Theo từng dự án (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Bộ khung kiểm thử</th><th>Khả năng</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Xuất xứ</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Bản mod trò chơi</a></td><td>Nạp từng bản mod nhiều người chơi phổ biến vào phiên bản trò chơi của chúng tôi, khởi động một bản đồ và kiểm tra nhật ký xem có lỗi không.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="chưa được xác nhận" title="chưa được xác nhận" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Song song với bản gốc</a></td><td>Ghi cùng một cảnh trong phiên bản của chúng tôi và trong trò chơi gốc, đặt cạnh nhau, để thấy mọi khác biệt.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="chưa được xác nhận" title="chưa được xác nhận" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Ảnh chụp màn chơi</a></td><td>Chụp ảnh từng bản đồ từ góc máy mà tác giả bản đồ đã chọn, rồi xếp chúng lên một trang.</td></tr>
</tbody>
</table>

### Công việc về ngôn ngữ ký hiệu

<table>
<thead><tr><th width="190">Bộ khung kiểm thử</th><th>Khả năng</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Xuất xứ</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">So sánh chuyển động</a></td><td>Phát một bàn tay ra dấu do máy tính tạo cạnh người ra dấu thật đã làm mẫu cho nó, theo từng khung hình, để kiểm tra chuyển động có khớp không.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Bộ khung kiểm thử</th><th>Khả năng</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Xuất xứ</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Kiểm tra giá trị trích dẫn</a></td><td>Trước khi Claude trích dẫn một ngày hoặc con số từ tài liệu, kiểm tra rằng đúng đoạn văn bản đó thực sự có trong tài liệu ấy.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
</tbody>
</table>

### Cầu nối Bluetooth Ranger

<table>
<thead><tr><th width="190">Bộ khung kiểm thử</th><th>Khả năng</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Xuất xứ</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Đầu dò và bảng điều khiển cầu nối</a></td><td>Các chương trình thử nghiệm nhỏ và một bảng điều khiển trực tiếp cho cầu nối âm thanh Bluetooth trên xe đạp, hiển thị bộ đệm âm thanh, cường độ tín hiệu và kết nối khi đang đạp xe.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
</tbody>
</table>

### Cổng đặt chỗ

<table>
<thead><tr><th width="190">Bộ khung kiểm thử</th><th>Khả năng</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Xuất xứ</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Chạy thử đặt chỗ</a></td><td>Đi qua quy trình đặt chỗ trực tuyến đến bước cuối cùng rồi dừng lại, nên có thể kiểm thử các bước mà không tạo một lượt đặt thật.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Bộ khung kiểm thử</th><th>Khả năng</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Xuất xứ</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Kiểm tra hoạt ảnh</a></td><td>Đo một sơ đồ động trong khi nó chạy, kiểm tra các phần thẳng hàng và không chồng lên nhau, chính xác đến một phần nhỏ của điểm ảnh.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="hoạt động trên phiên bản đó" title="hoạt động trên phiên bản đó" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Do chúng tôi xây dựng" title="Do chúng tôi xây dựng" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Phiên bản kỹ thuật hơn, được viết để nạp vào Claude, là [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) trên GitHub.
