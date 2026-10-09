# ชุดเครื่องมือทดสอบอัตโนมัติของ Claude

<details class="langs" data-current="th">
<summary>ภาษา</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · **ไทย** · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

วิธีที่ Claude Code ใช้ตรวจงานของตัวเอง: เปิดแอป เก็บสิ่งที่มันอ่านได้ แล้วตัดสินว่าผ่านหรือไม่ผ่านก่อนที่คนจะต้องมาดู ชื่อแต่ละรายการจะเปิดหน้าที่มีวิธีทำครบถ้วน หน้าของชุดเครื่องมือทดสอบแต่ละหน้าเป็นภาษาอังกฤษ

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Claude แนะนำ" title="Claude แนะนำ" width="16" height="16"></td><td><b>Claude แนะนำ</b>: เครื่องมือมาตรฐานที่ใช้ตามเดิม</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Claude แนะนำ และต่อยอด" title="Claude แนะนำ และต่อยอด" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude แนะนำ และต่อยอด" title="Claude แนะนำ และต่อยอด" width="16" height="16"></td><td><b>Claude แนะนำ และต่อยอด</b>: เครื่องมือมาตรฐานที่เราต้องเสริมเพิ่มก่อนจึงจะใช้ได้</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td><td><b>เราสร้างเอง</b>: วิธีที่เราต้องคิดขึ้นเอง</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"> ใช้ได้กับเวอร์ชันนั้น · <img class="o t" src="icons/square.png" alt="ยังไม่ได้ยืนยัน" title="ยังไม่ได้ยืนยัน" width="16" height="16"> ยังไม่ได้ยืนยัน · <img class="o t" src="icons/xmark.square.png" alt="ยังใช้ไม่ได้กับเวอร์ชันนั้น" title="ยังใช้ไม่ได้กับเวอร์ชันนั้น" width="16" height="16"> ยังใช้ไม่ได้กับเวอร์ชันนั้น

ชุดเครื่องมือทดสอบที่ไม่ขึ้นกับเวอร์ชันของระบบปฏิบัติการจะนับว่าใช้ได้ทั้งสองเวอร์ชัน ส่วนที่เหลือทำเครื่องหมายตามครั้งล่าสุดที่ใช้งาน Mac เครื่องนี้อัปเดตเป็น 27 เมื่อวันที่ 2 ตุลาคม 2026 และยังต้องตรวจทีละรายการกับสถาปัตยกรรมของ 27 อีกครั้ง

**ที่มา**: แอปที่ชุดเครื่องมือทดสอบแต่ละชุดถูกสร้างขึ้นครั้งแรก

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## แอปบนเครื่องจำลอง, Mac & อุปกรณ์

<table class="wide">
<thead><tr><th width="190">ชุดเครื่องมือทดสอบ</th><th>ความสามารถ</th><th width="60">ที่มา</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">แหล่งกำเนิด</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">เครื่องจำลองเบื้องหลัง</a></td><td>Claude บิลด์แอป iPhone แล้วรันในเครื่องจำลองเบื้องหลัง พร้อมจับภาพหน้าจอและเก็บล็อกเอง จึงตรวจหน้าจอได้โดยไม่ต้องยึดหน้าจอของคุณ</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude แนะนำ และต่อยอด" title="Claude แนะนำ และต่อยอด" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude แนะนำ และต่อยอด" title="Claude แนะนำ และต่อยอด" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">ตัววัดเลย์เอาต์</a></td><td>Claude วัดสิ่งที่หน้าจอจัดวางจริง เช่น ความสูงของแถบและตำแหน่งการเลื่อน ทีละช่วงขณะที่คุณสลับไปมาระหว่างหน้าจอ จึงหาสาเหตุที่บางอย่างดูผิดได้แทนการเดา</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">สวิตช์ผ่านอาร์กิวเมนต์ตอนเปิดแอป</a></td><td>สวิตช์ที่ซ่อนอยู่ในบิลด์ทดสอบ ซึ่งเปิดแอปไปที่หน้าจอที่เลือกพร้อมข้อมูลตัวอย่างทันที Claude จึงไปถึงหน้าจอใดก็ได้โดยไม่ต้องแตะไล่ไปทั่วแอป</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">แอป iPad บน Mac</a></td><td>รันแอปเวอร์ชัน iPad เป็นแอป Mac ทั่วไป Claude จึงทดสอบบน Mac ได้ พร้อมล็อกและภาพหน้าต่างของแอป</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude แนะนำ และต่อยอด" title="Claude แนะนำ และต่อยอด" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude แนะนำ และต่อยอด" title="Claude แนะนำ และต่อยอด" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript และการจับภาพหน้าจอ</a></td><td>เมื่อ Claude ควบคุมหน้าจอโดยตรงไม่ได้ ก็จะสั่งแอป Mac ด้วย AppleScript แล้วถ่ายภาพเฉพาะหน้าต่างของแอปเพื่อดูผลลัพธ์</td></tr>
<tr><td><a href="unit-test-suites.md">ยูนิตเทสต์</a></td><td>การทดสอบอัตโนมัติสำหรับตรรกะภายในของแอป เช่น การคิดคะแนน เส้นทาง และคิว ซึ่งรันเสร็จในไม่กี่วินาทีโดยไม่ต้องเปิดแอป</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude แนะนำ" title="Claude แนะนำ" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">รายการที่คนต้องตรวจเอง</a></td><td>รายการเดียวที่อัปเดตต่อเนื่องของการตรวจที่มีแต่คนทำได้ เช่น การสวมเฮดเซ็ตหรือใช้โทรศัพท์จริง เพื่อให้งานส่วนที่เหลือไม่ต้องรอ</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">บิลด์ทุกเป้าหมาย</a></td><td>บิลด์เวอร์ชัน iPhone, Mac และ Vision Pro ใหม่พร้อมกันหลังมีการเปลี่ยนแปลง และตรวจว่าค่าทดสอบไม่เคยถูกบันทึกลงในการตั้งค่าของผู้เล่น</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">พรีวิวสด SwiftUI</a></td><td>แสดงหน้าจอเดียวในพรีวิวสดของ Xcode แล้วถ่ายภาพไว้ Claude จึงตรวจการเปลี่ยนเลย์เอาต์ได้โดยไม่ต้องบิลด์และรันทั้งเกม</td><td class="m"><img class="o t" src="icons/square.png" alt="ยังไม่ได้ยืนยัน" title="ยังไม่ได้ยืนยัน" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">แตะตามข้อมูลการช่วยการเข้าถึง</a></td><td>แตะปุ่มในเครื่องจำลองตามตำแหน่งที่แอปรายงานเอง แทนการเดาตำแหน่งจากภาพหน้าจอ</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude แนะนำ" title="Claude แนะนำ" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">เครื่องจำลองสองเครื่องแทนคนสองคน</a></td><td>รันแอปบน iPhone จำลองสองเครื่องในฐานะคนสองคน จึงทดสอบคำเชิญ การท้าแข่ง และการซิงค์ได้โดยไม่ต้องมีโทรศัพท์จริงสองเครื่อง</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="ยังไม่ได้ยืนยัน" title="ยังไม่ได้ยืนยัน" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">ทุกหน้าจอในทุกภาษา</a></td><td>ถ่ายภาพหน้าจอหลักทุกหน้าในทุกภาษา รวมถึงภาษาสมมติที่มีคำยาวเป็นพิเศษ ไว้บนแผ่นเดียว จึงมองเห็นข้อความที่ล้นกรอบได้ง่าย</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">รายงานแอปขัดข้อง</a></td><td>ดึงรายงานการขัดข้องจาก iPhone จริงมาอ่าน ทำให้การขัดข้องที่เกิดเฉพาะบนโทรศัพท์ได้รับการระบุสาเหตุชัดเจน</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ยังไม่ได้ยืนยัน" title="ยังไม่ได้ยืนยัน" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude แนะนำ" title="Claude แนะนำ" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">ชุดทดสอบขนาดเล็ก</a></td><td>ชุดการตรวจอัตโนมัติขนาดเล็กที่ทำงานได้ในตัวสำหรับเครื่องมือ Python ซึ่งรันได้ทุกที่โดยไม่ต้องติดตั้งอะไรเพิ่ม</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td></tr>
</tbody>
</table>

## กราฟิก & เกม

<table class="wide">
<thead><tr><th width="190">ชุดเครื่องมือทดสอบ</th><th>ความสามารถ</th><th width="60">ที่มา</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">แหล่งกำเนิด</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">สั่งงานผ่านคอนโซลเกม</a></td><td>ส่งคำสั่งเข้าคอนโซลในตัวของเกมจากสคริปต์ แล้วอ่านล็อกภายหลัง แทนการพิมพ์ลงในหน้าต่างเกม</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="5"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">เฟรมก่อนและหลัง</a></td><td>เล่นคลิปเกมที่บันทึกไว้คลิปเดิมทั้งก่อนและหลังการเปลี่ยนกราฟิก แล้วเปรียบเทียบเฟรมทีละพิกเซล</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">เรย์เทรซิงบน Mac</a></td><td>มุมมองทดสอบที่แสดงแต่ละขั้นของแสงแบบเรย์เทรซิง (เงา การสะท้อน แสงโดยรอบ) แยกกัน พร้อมการตรวจตัวเองที่แสดงผลว่าผ่านหรือไม่ผ่าน</td></tr>
<tr><td><a href="vision-pro-screenshots.md">ภาพหน้าจอ Vision Pro</a></td><td>จับภาพสิ่งที่แอป Vision Pro แสดง รวมถึงภาพของตาแต่ละข้างแบบ 3D ทั้งในเครื่องจำลองและบนเฮดเซ็ต</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude แนะนำ และต่อยอด" title="Claude แนะนำ และต่อยอด" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude แนะนำ และต่อยอด" title="Claude แนะนำ และต่อยอด" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">คอมไพล์เชเดอร์แบบออฟไลน์</a></td><td>คอมไพล์โค้ดกราฟิกเรย์เทรซิงบน Mac เพราะเครื่องจำลองข้ามส่วนนี้ไป และข้อผิดพลาดจะไปโผล่บนอุปกรณ์จริงเท่านั้น</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">จับเฟรม GPU</a></td><td>จับหนึ่งเฟรมบนชิปกราฟิกและแสดงว่าการวาดแต่ละขั้นใช้ทรัพยากรเท่าไร เพื่อหาว่าอะไรช้า</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="ยังไม่ได้ยืนยัน" title="ยังไม่ได้ยืนยัน" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude แนะนำ" title="Claude แนะนำ" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">คณิตศาสตร์ของเชเดอร์</a></td><td>คำนวณเอฟเฟกต์ควันและไฟของ Quake 3 ใหม่อย่างช้า ๆ และแม่นยำ แล้วตรวจว่าเวอร์ชันกราฟิกแบบเร็ววาดภาพออกมาเหมือนกัน</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
</tbody>
</table>

## เสียง, ภาษา & ข้อมูล

<table class="wide">
<thead><tr><th width="190">ชุดเครื่องมือทดสอบ</th><th>ความสามารถ</th><th width="60">ที่มา</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">แหล่งกำเนิด</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">แปลงภาพหน้าจอเป็นข้อความ</a></td><td>แปลงภาพหน้าจอและภาพสแกนเป็นข้อความบน Mac ก่อนที่ Claude จะอ่าน ทำให้ภาพยังเป็นส่วนตัวและใช้หน่วยความจำของ Claude น้อยลงมาก</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac พูดประโยคทดสอบด้วยเสียงสังเคราะห์เข้าไปยังตัวรู้จำเสียงพูดของแอป จึงทดสอบคำสั่งเสียงได้โดยไม่ต้องมีใครพูด</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ยังไม่ได้ยืนยัน" title="ยังไม่ได้ยืนยัน" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">เล่นเสียงซ้ำบนอุปกรณ์</a></td><td>Mac แปลงบทสนทนาทดสอบแต่ละชุดเป็นไฟล์เสียง แล้วแอปบนโทรศัพท์จะฟังไฟล์นั้นแทนไมโครโฟน จึงทดสอบฟีเจอร์เสียงบนโทรศัพท์จริงได้โดยไม่ต้องมีใครพูด</td></tr>
<tr><td><a href="siri-phrasing-check.md">ประโยคสำหรับ Siri</a></td><td>ตรวจว่าประโยคที่ฝังไว้ในแอปสำหรับ Siri เช่น &quot;order my usual&quot; ตรงกับสิ่งที่คนพูดจริง ส่วน Siri จะส่งต่อคำสั่งได้ถูกต้องหรือไม่ยังต้องทดสอบบนโทรศัพท์</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">สแนปช็อตอ้างอิง</a></td><td>บันทึกผลลัพธ์ทั้งหมดของแอปไว้ก่อนเขียนโค้ดใหม่ แล้วตรวจว่าเวอร์ชันที่เขียนใหม่ให้ผลลัพธ์เหมือนเดิมทุกประการ</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ยังไม่ได้ยืนยัน" title="ยังไม่ได้ยืนยัน" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">ความแม่นยำของการถอดเสียง</a></td><td>รันระบบแปลงเสียงพูดเป็นข้อความของแอปกับไฟล์เสียงสาธารณะที่มีบทถอดความที่ถูกต้องมาด้วย แล้วนับว่าผิดไปกี่ตัวอักษร</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">ตรวจคำแปล</a></td><td>ตรวจว่าคำแปลทุกรายการยังคงชื่อ ตัวเลข และคำศัพท์ที่ตกลงกันไว้ และไม่มีข้อความบนหน้าจอที่ถูกปล่อยไว้โดยไม่ได้แปล ใช้กับ Quake 3 ด้วย</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">ข้อมูลจริง</a></td><td>ทดสอบการจับคู่เส้นทางกับชุดการปั่นจักรยานจริงที่บันทึกไว้แทนข้อมูลสมมติ ซึ่งพบบั๊กที่การทดสอบด้วยข้อมูลสมมติตรวจไม่เจอ</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ยังไม่ได้ยืนยัน" title="ยังไม่ได้ยืนยัน" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">ให้ตรงกับแอปต้นฉบับ</a></td><td>เปรียบเทียบฐานข้อมูลในเวอร์ชัน iPad ของเรากับฐานข้อมูลจากแอป Windows ต้นฉบับ ทีละตารางและทีละแถว</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td></tr>
</tbody>
</table>

## ฮาร์ดแวร์, เครือข่าย & บริการ

<table class="wide">
<thead><tr><th width="190">ชุดเครื่องมือทดสอบ</th><th>ความสามารถ</th><th width="60">ที่มา</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">แหล่งกำเนิด</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">เทียบกับอุปกรณ์ที่รู้ว่าทำงานดี</a></td><td>บันทึกพฤติกรรมของชุดอุปกรณ์ที่รู้ว่าทำงานดี (iPhone เชื่อมต่อกับหูฟังโดยตรง) แล้วเปรียบเทียบกับไฟล์บันทึกจากบริดจ์ของเรา</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">ดักจับ Bluetooth</a></td><td>บันทึกทราฟฟิก Bluetooth โดยตรง เพื่อดูว่าอุปกรณ์ส่งอะไรจริง ๆ ไม่ใช่แค่สิ่งที่อุปกรณ์รายงาน</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude แนะนำ" title="Claude แนะนำ" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">ตรวจสถานะบริการ</a></td><td>ตรวจว่าบริการเว็บแต่ละตัวตอบสนองจากอินเทอร์เน็ต และเส้นทางที่ควรถูกบล็อกถูกปฏิเสธจริง</td></tr>
</tbody>
</table>

## เว็บ

<table class="wide">
<thead><tr><th width="190">ชุดเครื่องมือทดสอบ</th><th>ความสามารถ</th><th width="60">ที่มา</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">แหล่งกำเนิด</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">สั่งงานเบราว์เซอร์</a></td><td>Claude เปิดหน้าเว็บในเบราว์เซอร์ กรอกฟอร์ม และอ่านผลลัพธ์ เพื่อตรวจว่าเว็บไซต์ทำงานได้และแสดงผลถูกต้อง</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude แนะนำ" title="Claude แนะนำ" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">ตรวจการอัปเดตเว็บไซต์</a></td><td>หลังอัปเดตเว็บไซต์ จะตรวจว่าไฟล์ทุกไฟล์ไปถึงเซิร์ฟเวอร์ครบถ้วน แล้วตรวจเลย์เอาต์ที่ความกว้างของโทรศัพท์ แท็บเล็ต และเดสก์ท็อป</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>เฉพาะโปรเจกต์ (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">ชุดเครื่องมือทดสอบ</th><th>ความสามารถ</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">แหล่งกำเนิด</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">ม็อดเกม</a></td><td>โหลดม็อดผู้เล่นหลายคนยอดนิยมแต่ละตัวเข้าเกมเวอร์ชันของเรา เริ่มแผนที่ แล้วตรวจล็อกหาข้อผิดพลาด</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="ยังไม่ได้ยืนยัน" title="ยังไม่ได้ยืนยัน" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">เทียบข้างกันกับต้นฉบับ</a></td><td>บันทึกฉากเดียวกันในเวอร์ชันของเราและในเกมต้นฉบับ วางข้างกัน เพื่อแสดงความแตกต่างใด ๆ</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ยังไม่ได้ยืนยัน" title="ยังไม่ได้ยืนยัน" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">ภาพด่าน</a></td><td>ถ่ายภาพแผนที่แต่ละแผนที่จากมุมกล้องที่ผู้สร้างแผนที่เลือกไว้ แล้วจัดวางรวมไว้บนแผ่นเดียว</td></tr>
</tbody>
</table>

### งานภาษามือ

<table>
<thead><tr><th width="190">ชุดเครื่องมือทดสอบ</th><th>ความสามารถ</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">แหล่งกำเนิด</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">เปรียบเทียบการเคลื่อนไหว</a></td><td>เล่นมือที่ทำภาษามือซึ่งสร้างด้วยคอมพิวเตอร์เคียงข้างผู้ใช้ภาษามือตัวจริงที่เป็นต้นแบบ ทีละเฟรม เพื่อตรวจว่าการเคลื่อนไหวตรงกัน</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">ชุดเครื่องมือทดสอบ</th><th>ความสามารถ</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">แหล่งกำเนิด</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">ตรวจค่าที่อ้างอิง</a></td><td>ก่อนที่ Claude จะอ้างวันที่หรือตัวเลขจากเอกสาร จะตรวจว่าข้อความนั้นปรากฏในเอกสารนั้นจริงตรงตามตัวอักษร</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
</tbody>
</table>

### บริดจ์ Bluetooth Ranger

<table>
<thead><tr><th width="190">ชุดเครื่องมือทดสอบ</th><th>ความสามารถ</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">แหล่งกำเนิด</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">ตัวตรวจวัดและแดชบอร์ดของบริดจ์</a></td><td>โปรแกรมทดสอบขนาดเล็กและแดชบอร์ดแบบเรียลไทม์สำหรับบริดจ์เสียง Bluetooth ของจักรยาน แสดงบัฟเฟอร์เสียง ความแรงสัญญาณ และการเชื่อมต่อขณะปั่น</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
</tbody>
</table>

### พอร์ทัลการจอง

<table>
<thead><tr><th width="190">ชุดเครื่องมือทดสอบ</th><th>ความสามารถ</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">แหล่งกำเนิด</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">ทดลองจองโดยไม่จองจริง</a></td><td>ทำการจองออนไลน์ไปจนถึงขั้นตอนสุดท้ายแล้วหยุด จึงทดสอบขั้นตอนต่าง ๆ ได้โดยไม่เกิดการจองจริง</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">ชุดเครื่องมือทดสอบ</th><th>ความสามารถ</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">แหล่งกำเนิด</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">ตรวจแอนิเมชัน</a></td><td>วัดแผนภาพเคลื่อนไหวขณะเล่น ตรวจว่าชิ้นส่วนต่าง ๆ เรียงตรงกันและไม่ซ้อนทับ ละเอียดถึงเศษส่วนของพิกเซล</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="ใช้ได้กับเวอร์ชันนั้น" title="ใช้ได้กับเวอร์ชันนั้น" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="เราสร้างเอง" title="เราสร้างเอง" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

เวอร์ชันที่เป็นเทคนิคมากกว่า ซึ่งเขียนไว้สำหรับโหลดเข้า Claude คือ [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) บน GitHub
