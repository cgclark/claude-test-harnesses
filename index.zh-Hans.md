# Claude 自动化测试工具

<details class="langs" data-current="zh-Hans">
<summary>语言</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · **简体中文** · [繁體中文](index.zh-Hant.md)

</details>

让 Claude Code 检查自己工作的方法：运行应用，捕获它能读取的内容，并在需要人来查看之前判定通过或失败。点击每个名称可打开包含完整步骤的页面。 各测试工具页面本身为英文。

<img class="c" src="icons/claude-code.svg" alt="Claude 推荐" title="Claude 推荐" width="16" height="16"> **Claude 推荐**: 直接使用的标准工具 (8)<br>
<img class="c" src="icons/claude-code.svg" alt="Claude 推荐，经扩展" title="Claude 推荐，经扩展" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude 推荐，经扩展" title="Claude 推荐，经扩展" width="16" height="16"> **Claude 推荐，经扩展**: 需要我们补充后才能用的标准工具 (4)<br>
<img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"> **自行构建**: 我们自己摸索出的方法 (30)

<img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"> 在该版本上可用 · <img class="o t" src="icons/square.png" alt="尚未确认" title="尚未确认" width="16" height="16"> 尚未确认 · <img class="o t" src="icons/xmark.square.png" alt="在该版本上暂不可用" title="在该版本上暂不可用" width="16" height="16"> 在该版本上暂不可用

不依赖操作系统版本的测试工具视为在两个版本上都可用。其余的按各自最近一次使用时的情况勾选；这台 Mac 已于 2026 年 10 月 2 日升级到 27，针对 27 架构的逐一检查尚待进行。

**来自**: 每个测试工具最初构建时所在的应用

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/big-top.png" alt="" width="20" height="20"> Big Top</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## 模拟器、Mac 与设备上的应用

<table class="wide">
<thead><tr><th width="190">测试工具</th><th>能力</th><th width="60">来自</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出处</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">后台模拟器</a></td><td>Claude 构建 iPhone 应用，在后台的模拟器中运行，并自行截屏、收集日志，因此无需占用你的屏幕就能检查某个界面。</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 推荐，经扩展" title="Claude 推荐，经扩展" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude 推荐，经扩展" title="Claude 推荐，经扩展" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">布局探针</a></td><td>在你切换界面时，Claude 逐时刻测量屏幕实际排出的布局，比如栏的高度和滚动位置，从而找出某处显示不对的原因，而不是靠猜。</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">启动参数钩子</a></td><td>测试版本中的隐藏开关，可让应用带着示例数据直接打开指定界面，Claude 无需在应用里逐步点按就能到达任何界面。</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">在 Mac 上运行 iPad 应用</a></td><td>把应用的 iPad 版本当作普通 Mac 应用运行，Claude 便能在 Mac 上测试它，并获取日志和窗口截图。</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude 推荐，经扩展" title="Claude 推荐，经扩展" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude 推荐，经扩展" title="Claude 推荐，经扩展" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript 与屏幕截取</a></td><td>当 Claude 无法直接控制屏幕时，就用 AppleScript 操作 Mac 应用，并只拍下它们的窗口来查看结果。</td></tr>
<tr><td><a href="unit-test-suites.md">单元测试</a></td><td>针对应用内部逻辑（如计分、路线和队列）的自动化测试，几秒内即可运行完毕，无需打开应用。</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 推荐" title="Claude 推荐" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">仅限人工的检查清单</a></td><td>一份持续更新的清单，列出只有人才能做的检查，比如戴上头显或使用真机，这样其余工作就不必等待这些检查。</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">构建所有目标</a></td><td>每次改动后同时重新构建 iPhone、Mac 和 Vision Pro 版本，并检查测试设置绝不会被保存到玩家自己的设置中。</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">SwiftUI 实时预览</a></td><td>在 Xcode 的实时预览中显示单个界面并截图，Claude 无需构建并运行整个游戏就能检查布局改动。</td><td class="m"><img class="o t" src="icons/square.png" alt="尚未确认" title="尚未确认" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">按辅助功能信息点按</a></td><td>按应用自身报告的位置点按模拟器中的按钮，而不是根据截图猜测按钮在哪里。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 推荐" title="Claude 推荐" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">两台模拟器扮演两个人</a></td><td>在两台模拟 iPhone 上以两个不同的人运行应用，无需两部真机就能测试邀请、挑战和同步。</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="尚未确认" title="尚未确认" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">每种语言的每个界面</a></td><td>把每个主要界面在每种语言下的样子，外加一种单词特别长的虚构语言，拍下来放在同一张总览图上，放不下的文字一眼就能看出。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">崩溃报告</a></td><td>从真实 iPhone 上取出崩溃报告并阅读，让只在手机上出现的崩溃有一个明确的原因。</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="尚未确认" title="尚未确认" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude 推荐" title="Claude 推荐" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">小型测试套件</a></td><td>为 Python 工具准备的一小套独立的自动检查，无需安装任何东西，在哪里都能运行。</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td></tr>
</tbody>
</table>

## 图形与游戏

<table class="wide">
<thead><tr><th width="190">测试工具</th><th>能力</th><th width="60">来自</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出处</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">驱动游戏控制台</a></td><td>通过脚本向游戏内置控制台发送命令，事后读取其日志，而不是在游戏窗口中输入。</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">前后帧对比</a></td><td>在图形改动前后播放同一段录制的游戏片段，并逐像素比较画面帧。</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Mac 上的光线追踪</a></td><td>可单独显示光线追踪照明每一步（阴影、反射、环境光）的测试视图，另有输出通过或失败的自检。</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Pro 截图</a></td><td>在模拟器和头显上截取 Vision Pro 应用显示的内容，包括每只眼睛看到的 3D 画面。</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="尚未确认" title="尚未确认" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 推荐，经扩展" title="Claude 推荐，经扩展" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude 推荐，经扩展" title="Claude 推荐，经扩展" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">离线着色器编译</a></td><td>在 Mac 上编译光线追踪图形代码，因为模拟器会跳过这部分代码，否则错误只有在设备上才会暴露。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPU 帧捕获</a></td><td>在图形芯片上捕获一帧，列出每个绘制步骤的开销，找出慢在哪里。</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="尚未确认" title="尚未确认" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 推荐" title="Claude 推荐" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">着色器数学</a></td><td>缓慢而精确地重新计算 Quake 3 的烟雾和火焰效果，并检查快速的图形版本画出的画面是否相同。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
</tbody>
</table>

## 语音、语言与数据

<table class="wide">
<thead><tr><th width="190">测试工具</th><th>能力</th><th width="60">来自</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出处</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">截图转文字</a></td><td>在 Claude 读取之前，先在 Mac 上把截图和扫描件转成文字，既能保护图片隐私，又能大幅减少对 Claude 记忆空间的占用。</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m" rowspan="8"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac 用合成语音把测试短语读给应用的语音识别器，无需任何人开口就能测试语音命令。</td><td class="app-c"><img class="app-sm" src="icons/apps/big-top.png" alt="Big Top" title="Big Top" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="尚未确认" title="尚未确认" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td></tr>
<tr><td><a href="siri-phrasing-check.md">Siri 说法检查</a></td><td>检查应用内置给 Siri 的短语（如“order my usual”）是否与人们的实际说法一致；Siri 能否正确分派这些短语，仍需在手机上确认。</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">参考快照</a></td><td>在重写之前保存应用的完整输出，然后检查重写后的版本是否产生完全相同的输出。</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="尚未确认" title="尚未确认" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">转写准确率</a></td><td>在附有正确文字稿的公开录音上运行应用的语音转文字功能，并按出错的字符数打分。</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">翻译检查</a></td><td>检查每条翻译都保留了名称、数字和约定术语，且界面上没有遗漏未翻译的文字。也用于 Quake 3。</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">真实数据</a></td><td>用一组真实记录的骑行数据而非编造的数据来测试路线匹配，发现了编造测试遗漏的错误。</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="尚未确认" title="尚未确认" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">与原版应用一致</a></td><td>逐表、逐行比较我们 iPad 版本中的数据库与原版 Windows 应用中的数据库。</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td></tr>
</tbody>
</table>

## 硬件、网络与服务

<table class="wide">
<thead><tr><th width="190">测试工具</th><th>能力</th><th width="60">来自</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出处</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">与已知正常的设备对比</a></td><td>记录一套已知正常的配置（iPhone 直接连接耳机）的表现，并将我们桥接器的录制结果与之对比。</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetooth 抓包</a></td><td>直接记录 Bluetooth 通信本身，查看设备实际发送了什么，而不是它们报告了什么。</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude 推荐" title="Claude 推荐" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">健康检查</a></td><td>检查每个 Web 服务都能从互联网响应，并且本应被拦截的路由确实被拒绝。</td></tr>
</tbody>
</table>

## 网页

<table class="wide">
<thead><tr><th width="190">测试工具</th><th>能力</th><th width="60">来自</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出处</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">驱动浏览器</a></td><td>Claude 在浏览器中打开页面、填写表单并读取结果，检查网站能否正常工作、显示是否正确。</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 推荐" title="Claude 推荐" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">网站部署检查</a></td><td>网站更新后，检查每个文件都完整到达服务器，再在手机、平板和桌面宽度下检查布局。</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>项目专用 (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">测试工具</th><th>能力</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出处</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">游戏模组</a></td><td>把每个热门多人模组加载到我们版本的游戏中，启动一张地图，并检查日志中是否有错误。</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="尚未确认" title="尚未确认" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">与原版并排对比</a></td><td>在我们的版本和原版游戏中录制同一场景并排放置，显示任何差异。</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="尚未确认" title="尚未确认" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">关卡截图</a></td><td>按地图作者选定的镜头角度为每张地图拍一张图，并排在同一张总览图上。</td></tr>
</tbody>
</table>

### 手语项目

<table>
<thead><tr><th width="190">测试工具</th><th>能力</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出处</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">动作对比</a></td><td>将计算机生成的手语手部动画与其所依据的真人手语者逐帧并排播放，检查动作是否一致。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">测试工具</th><th>能力</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出处</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">核对引用值</a></td><td>在 Claude 引用文档中的日期或数字之前，先检查这段原文确实出现在该文档中。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger Bluetooth 桥接器

<table>
<thead><tr><th width="190">测试工具</th><th>能力</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出处</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">桥接器探针与仪表板</a></td><td>为自行车上的 Bluetooth 音频桥接器准备的小型测试程序和实时仪表板，骑行时显示声音缓冲区、信号强度和连接情况。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
</tbody>
</table>

### 预订平台

<table>
<thead><tr><th width="190">测试工具</th><th>能力</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出处</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">预订演练</a></td><td>在线预订一路走到最后一步就停下，无需真正预订即可测试各个步骤。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">测试工具</th><th>能力</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">出处</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">动画检查</a></td><td>在动画图表播放时进行测量，检查各部分是否对齐、互不重叠，精度达到像素的几分之一。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="在该版本上可用" title="在该版本上可用" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="自行构建" title="自行构建" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

更偏技术的版本见 GitHub 上的 [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md)，专为加载到 Claude 而写。
