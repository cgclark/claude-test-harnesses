# Claude 自動化測試工具

<details class="langs" data-current="zh-Hant">
<summary>語言</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · **繁體中文**

</details>

讓 Claude Code 檢查自己工作的方法：執行應用程式，擷取它能讀取的內容，並在需要人來看之前判定通過或失敗。點選每個名稱即可開啟含完整做法的頁面。 各測試工具頁面本身為英文。

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Claude 推薦" title="Claude 推薦" width="16" height="16"></td><td><b>Claude 推薦</b>: 直接沿用的標準工具</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Claude 推薦，經擴充" title="Claude 推薦，經擴充" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude 推薦，經擴充" title="Claude 推薦，經擴充" width="16" height="16"></td><td><b>Claude 推薦，經擴充</b>: 我們得先補強才能運作的標準工具</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td><td><b>自行打造</b>: 我們自行摸索出來的方法</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"> 可在該版本上運作 · <img class="o t" src="icons/square.png" alt="尚未確認" title="尚未確認" width="16" height="16"> 尚未確認 · <img class="o t" src="icons/xmark.square.png" alt="在該版本上尚無法運作" title="在該版本上尚無法運作" width="16" height="16"> 在該版本上尚無法運作

不受作業系統版本影響的測試工具，視為在兩個版本上都能運作。其餘則依各自上次使用時的情況勾選；這台 Mac 已於 2026 年 10 月 2 日升級至 27，針對 27 架構的逐一檢查仍有待進行。

**來自**: 每個測試工具最初打造時所屬的應用程式

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## 模擬器、Mac 與裝置上的應用程式

<table class="wide">
<thead><tr><th width="190">測試工具</th><th>能力</th><th width="60">來自</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出處</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">背景模擬器</a></td><td>Claude 建置 iPhone 應用程式，在背景的模擬器中執行，並自行擷取螢幕畫面和記錄檔，因此不必占用你的螢幕就能檢查某個畫面。</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 推薦，經擴充" title="Claude 推薦，經擴充" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude 推薦，經擴充" title="Claude 推薦，經擴充" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">版面探測</a></td><td>在你切換畫面時，Claude 逐時刻測量螢幕實際排出的版面，例如列的高度和捲動位置，藉此找出某處看起來不對的原因，而不是用猜的。</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">啟動參數掛鉤</a></td><td>測試版建置中的隱藏開關，可讓應用程式帶著範例資料直接開啟指定畫面，Claude 不必在應用程式裡一路點按，就能抵達任何畫面。</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">在 Mac 上執行 iPad 應用程式</a></td><td>把應用程式的 iPad 版當作一般 Mac 應用程式執行，Claude 便能在 Mac 上測試，並取得記錄檔和視窗截圖。</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude 推薦，經擴充" title="Claude 推薦，經擴充" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude 推薦，經擴充" title="Claude 推薦，經擴充" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript 與螢幕擷取</a></td><td>當 Claude 無法直接控制螢幕時，就以 AppleScript 操作 Mac 應用程式，並只拍下它們的視窗來查看結果。</td></tr>
<tr><td><a href="unit-test-suites.md">單元測試</a></td><td>針對應用程式內部邏輯（例如計分、路線和佇列）的自動測試，幾秒內就能跑完，不必開啟應用程式。</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 推薦" title="Claude 推薦" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">僅限人工的檢查清單</a></td><td>一份持續更新的清單，列出只有人才能做的檢查，例如戴上頭戴裝置或使用實體手機，讓其餘工作不必等這些檢查。</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">建置所有目標</a></td><td>每次變更後一併重新建置 iPhone、Mac 和 Vision Pro 版本，並檢查測試設定絕不會被存進玩家自己的設定。</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">SwiftUI 即時預覽</a></td><td>在 Xcode 的即時預覽中顯示單一畫面並截圖，Claude 不必建置並執行整個遊戲，就能檢查版面變更。</td><td class="m"><img class="o t" src="icons/square.png" alt="尚未確認" title="尚未確認" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">依輔助使用資訊點按</a></td><td>依應用程式自己回報的位置點按模擬器中的按鈕，而不是從截圖猜測按鈕位置。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 推薦" title="Claude 推薦" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">兩台模擬器扮演兩個人</a></td><td>在兩台模擬 iPhone 上以兩個不同的人執行應用程式，不需要兩支實體手機，就能測試邀請、挑戰和同步。</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="尚未確認" title="尚未確認" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">每種語言的每個畫面</a></td><td>將每個主要畫面在每種語言下的樣子，外加一種單字特別長的虛構語言，拍下來排在同一張總覽圖上，放不下的文字一眼就能看出。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">當機報告</a></td><td>從實體 iPhone 取出當機報告並閱讀，讓只在手機上發生的當機有明確的原因。</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="尚未確認" title="尚未確認" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude 推薦" title="Claude 推薦" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">小型測試套件</a></td><td>為 Python 工具準備的一小組獨立自動檢查，不必安裝任何東西，在哪裡都能執行。</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td></tr>
</tbody>
</table>

## 圖形與遊戲

<table class="wide">
<thead><tr><th width="190">測試工具</th><th>能力</th><th width="60">來自</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出處</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">操控遊戲主控台</a></td><td>透過指令碼將指令傳送到遊戲內建的主控台，事後再讀取其記錄檔，而不是在遊戲視窗中輸入。</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">前後畫格比較</a></td><td>在圖形變更前後播放同一段錄製的遊戲片段，並逐像素比較畫格。</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Mac 上的光線追蹤</a></td><td>可個別顯示光線追蹤照明每個步驟（陰影、反射、環境光）的測試檢視，另有會印出通過或失敗的自我檢查。</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Pro 截圖</a></td><td>在模擬器和頭戴裝置上擷取 Vision Pro 應用程式顯示的內容，包括每隻眼睛看到的 3D 畫面。</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="尚未確認" title="尚未確認" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 推薦，經擴充" title="Claude 推薦，經擴充" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude 推薦，經擴充" title="Claude 推薦，經擴充" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">離線著色器編譯</a></td><td>在 Mac 上編譯光線追蹤的圖形程式碼，因為模擬器會略過這部分程式碼，否則錯誤只會在裝置上才出現。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPU 畫格擷取</a></td><td>在圖形晶片上擷取一個畫格，列出每個繪製步驟的成本，找出慢在哪裡。</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="尚未確認" title="尚未確認" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 推薦" title="Claude 推薦" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">著色器數學</a></td><td>緩慢而精確地重新計算 Quake 3 的煙霧和火焰效果，並檢查快速的圖形版本畫出的畫面是否相同。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
</tbody>
</table>

## 語音、語言與資料

<table class="wide">
<thead><tr><th width="190">測試工具</th><th>能力</th><th width="60">來自</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出處</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">截圖轉文字</a></td><td>在 Claude 讀取之前，先在 Mac 上把截圖和掃描檔轉成文字，既能保護圖片隱私，也能大幅減少 Claude 記憶空間的用量。</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac 以合成語音將測試語句唸給應用程式的語音辨識器聽，不需要任何人開口就能測試語音指令。</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="尚未確認" title="尚未確認" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">實體裝置音訊重播</a></td><td>Mac 將每段測試對話轉成音訊檔，手機上的應用程式改聽這個檔案而非麥克風，不需要任何人開口就能在實體手機上測試語音功能。</td></tr>
<tr><td><a href="siri-phrasing-check.md">Siri 說法檢查</a></td><td>檢查應用程式內建給 Siri 的語句（例如「order my usual」）是否符合大家實際的說法；Siri 能否正確轉送這些語句，仍需在手機上確認。</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">參考快照</a></td><td>在改寫之前儲存應用程式的完整輸出，再檢查改寫後的版本是否產生完全相同的輸出。</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="尚未確認" title="尚未確認" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">轉錄準確度</a></td><td>在附有正確逐字稿的公開錄音上執行應用程式的語音轉文字功能，並依出錯的字元數評分。</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">翻譯檢查</a></td><td>檢查每則翻譯都保留了名稱、數字和約定術語，而且畫面上沒有漏掉未翻譯的文字。Quake 3 也有使用。</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">真實資料</a></td><td>以一組真實記錄的騎乘資料取代編造資料來測試路線比對，找出了編造測試漏掉的錯誤。</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="尚未確認" title="尚未確認" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">與原版應用程式一致</a></td><td>逐表、逐列比較我們 iPad 版本中的資料庫與原版 Windows 應用程式的資料庫。</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td></tr>
</tbody>
</table>

## 硬體、網路與服務

<table class="wide">
<thead><tr><th width="190">測試工具</th><th>能力</th><th width="60">來自</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出處</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">與已知正常的裝置比較</a></td><td>記錄一套已知正常的配置（iPhone 直接連接耳機）的表現，並將我們橋接器的錄製結果與之比較。</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetooth 封包擷取</a></td><td>直接錄下 Bluetooth 傳輸內容本身，查看裝置實際傳送了什麼，而不是它們回報了什麼。</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude 推薦" title="Claude 推薦" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">健康檢查</a></td><td>檢查每個網路服務都能從網際網路回應，而且應該封鎖的路徑確實遭到拒絕。</td></tr>
</tbody>
</table>

## 網頁

<table class="wide">
<thead><tr><th width="190">測試工具</th><th>能力</th><th width="60">來自</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出處</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">操控瀏覽器</a></td><td>Claude 在瀏覽器中開啟網頁、填寫表單並讀取結果，檢查網站是否正常運作、外觀是否正確。</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 推薦" title="Claude 推薦" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">網站部署檢查</a></td><td>網站更新後，檢查每個檔案都完整抵達伺服器，再於手機、平板和桌機寬度下檢查版面。</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>專案專屬 (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">測試工具</th><th>能力</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出處</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">遊戲模組</a></td><td>將每個熱門多人模組載入我們版本的遊戲，啟動一張地圖，並檢查記錄檔中是否有錯誤。</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="尚未確認" title="尚未確認" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">與原版並排比較</a></td><td>在我們的版本和原版遊戲中錄下同一場景並排呈現，顯示任何差異。</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="尚未確認" title="尚未確認" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">關卡截圖</a></td><td>以地圖作者選定的鏡頭角度為每張地圖拍一張圖，並排在同一張總覽圖上。</td></tr>
</tbody>
</table>

### 手語專案

<table>
<thead><tr><th width="190">測試工具</th><th>能力</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出處</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">動作比對</a></td><td>將電腦產生的手語手部動畫，與其所依據的真人手語者逐格並排播放，檢查動作是否一致。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">測試工具</th><th>能力</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出處</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">核對引用數值</a></td><td>在 Claude 引用文件中的日期或數字之前，先檢查這段原文確實出現在該文件中。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger Bluetooth 橋接器

<table>
<thead><tr><th width="190">測試工具</th><th>能力</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出處</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">橋接器探測程式與儀表板</a></td><td>為自行車上 Bluetooth 音訊橋接器準備的小型測試程式與即時儀表板，騎乘時顯示聲音緩衝區、訊號強度和連線狀況。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
</tbody>
</table>

### 預約平台

<table>
<thead><tr><th width="190">測試工具</th><th>能力</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出處</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">預約演練</a></td><td>將線上預約一路走到最後一步就停下，不必真的完成預約就能測試各個步驟。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">測試工具</th><th>能力</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出處</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">動畫檢查</a></td><td>在動畫圖表播放時進行測量，檢查各部分是否對齊、互不重疊，精確到像素的幾分之一。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="可在該版本上運作" title="可在該版本上運作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行打造" title="自行打造" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

更偏技術的版本見 GitHub 上的 [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md)，專為載入 Claude 而撰寫。
