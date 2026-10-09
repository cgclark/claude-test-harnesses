# Claude 자동 테스트 하네스

<details class="langs" data-current="ko">
<summary>언어</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · **한국어** · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Claude Code가 자기 작업을 스스로 확인하는 방법입니다. 앱을 실행하고, 읽을 수 있는 결과를 캡처한 다음, 사람이 볼 필요가 생기기 전에 통과인지 실패인지 판단합니다. 각 이름을 누르면 전체 절차가 담긴 페이지가 열립니다. 하네스 페이지 자체는 영어로 되어 있습니다.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Claude 추천" title="Claude 추천" width="16" height="16"></td><td><b>Claude 추천</b>: 표준 도구를 그대로 사용</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Claude 추천, 확장함" title="Claude 추천, 확장함" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude 추천, 확장함" title="Claude 추천, 확장함" width="16" height="16"></td><td><b>Claude 추천, 확장함</b>: 작동하도록 기능을 보태야 했던 표준 도구</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td><td><b>직접 제작</b>: 우리가 직접 고안해야 했던 방법</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"> 해당 버전에서 작동 · <img class="o t" src="icons/square.png" alt="아직 확인되지 않음" title="아직 확인되지 않음" width="16" height="16"> 아직 확인되지 않음 · <img class="o t" src="icons/xmark.square.png" alt="아직 그 버전에서 작동하지 않음" title="아직 그 버전에서 작동하지 않음" width="16" height="16"> 아직 그 버전에서 작동하지 않음

OS 버전에 의존하지 않는 하네스는 두 버전 모두에서 작동하는 것으로 봅니다. 나머지는 각각 마지막으로 사용한 시점을 기준으로 표시했습니다. 이 Mac은 2026년 10월 2일에 27로 옮겨 갔으며, 27 아키텍처에 맞춰 하나씩 확인하는 작업은 아직 남아 있습니다.

**최초 앱**: 각 하네스가 처음 만들어진 앱

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## 시뮬레이터, Mac & 기기의 앱

<table class="wide">
<thead><tr><th width="190">하네스</th><th>기능</th><th width="60">최초 앱</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">출처</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">헤드리스 시뮬레이터</a></td><td>Claude가 iPhone 앱을 빌드해 백그라운드 시뮬레이터에서 실행하고 스크린샷과 로그를 직접 남기므로, 사용자의 화면을 차지하지 않고도 화면을 확인할 수 있습니다.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 추천, 확장함" title="Claude 추천, 확장함" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude 추천, 확장함" title="Claude 추천, 확장함" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">레이아웃 측정</a></td><td>화면 사이를 이동하는 동안 바 높이와 스크롤 위치처럼 화면에 실제로 배치된 값을 Claude가 순간순간 측정하므로, 짐작하지 않고 무언가 이상해 보이는 원인을 찾을 수 있습니다.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">실행 인수 훅</a></td><td>테스트 빌드에 숨겨 둔 스위치로, 샘플 데이터가 들어간 원하는 화면에서 앱을 바로 엽니다. Claude가 앱을 일일이 탭하지 않고도 어느 화면에든 갈 수 있습니다.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">Mac에서 iPad 앱</a></td><td>앱의 iPad 버전을 일반 Mac 앱처럼 실행하므로, Claude가 로그와 창 스크린샷을 이용해 Mac에서 테스트할 수 있습니다.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude 추천, 확장함" title="Claude 추천, 확장함" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude 추천, 확장함" title="Claude 추천, 확장함" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript와 화면 캡처</a></td><td>Claude가 화면을 직접 제어할 수 없을 때는 AppleScript로 Mac 앱을 조작하고 해당 창만 촬영해 결과를 확인합니다.</td></tr>
<tr><td><a href="unit-test-suites.md">단위 테스트</a></td><td>점수, 경로, 대기열 같은 앱 내부 로직을 확인하는 자동 테스트로, 앱을 열지 않고 몇 초 만에 실행됩니다.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 추천" title="Claude 추천" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">사람 전용 체크리스트</a></td><td>헤드셋 착용이나 실제 휴대폰 사용처럼 사람만 할 수 있는 확인 항목을 하나의 목록으로 계속 관리하므로, 나머지 작업은 그 확인을 기다리지 않아도 됩니다.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">모든 타깃 빌드</a></td><td>변경 후 iPhone, Mac, Vision Pro 버전을 함께 다시 빌드하고, 테스트 설정이 플레이어 본인의 설정에 절대 저장되지 않는지 확인합니다.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">SwiftUI 실시간 미리보기</a></td><td>Xcode 실시간 미리보기에 화면 하나를 띄워 촬영하므로, Claude가 게임 전체를 빌드하고 실행하지 않고도 레이아웃 변경을 확인할 수 있습니다.</td><td class="m"><img class="o t" src="icons/square.png" alt="아직 확인되지 않음" title="아직 확인되지 않음" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">접근성 정보로 탭하기</a></td><td>스크린샷을 보고 위치를 짐작하는 대신, 앱이 직접 알려 주는 위치에서 시뮬레이터의 버튼을 탭합니다.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 추천" title="Claude 추천" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">시뮬레이터 두 대로 두 사람</a></td><td>시뮬레이션된 iPhone 두 대에서 서로 다른 두 사람으로 앱을 실행하므로, 실제 휴대폰 두 대 없이도 초대, 도전, 동기화를 테스트할 수 있습니다.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="아직 확인되지 않음" title="아직 확인되지 않음" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">모든 화면, 모든 언어</a></td><td>모든 주요 화면을 모든 언어로, 그리고 단어가 아주 긴 가상의 언어로도 촬영해 한 장에 모으므로, 넘치는 텍스트를 쉽게 찾을 수 있습니다.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">충돌 보고서</a></td><td>실제 iPhone에서 충돌 보고서를 가져와 읽으므로, 휴대폰에서만 일어나는 충돌도 원인을 짚어낼 수 있습니다.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="아직 확인되지 않음" title="아직 확인되지 않음" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude 추천" title="Claude 추천" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">소규모 테스트 모음</a></td><td>Python 도구를 위한 작고 독립적인 자동 검사 모음으로, 아무것도 설치하지 않고 어디서나 실행됩니다.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td></tr>
</tbody>
</table>

## 그래픽 & 게임

<table class="wide">
<thead><tr><th width="190">하네스</th><th>기능</th><th width="60">최초 앱</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">출처</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">게임 콘솔 조작</a></td><td>게임 창에 직접 입력하는 대신, 스크립트로 게임 내장 콘솔에 명령을 보내고 나중에 로그를 읽습니다.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">변경 전후 프레임</a></td><td>그래픽 변경 전과 후에 같은 녹화 게임 클립을 재생하고 프레임을 픽셀 단위로 비교합니다.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Mac에서 레이 트레이싱</a></td><td>레이 트레이싱 조명의 각 단계(그림자, 반사, 주변광)를 따로 보여 주는 테스트 뷰와, 통과 또는 실패를 출력하는 자체 검사입니다.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Pro 스크린샷</a></td><td>시뮬레이터와 헤드셋에서 Vision Pro 앱이 보여 주는 화면을, 각 눈에 보이는 3D 화면까지 포함해 캡처합니다.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="아직 확인되지 않음" title="아직 확인되지 않음" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 추천, 확장함" title="Claude 추천, 확장함" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude 추천, 확장함" title="Claude 추천, 확장함" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">오프라인 셰이더 컴파일</a></td><td>레이 트레이싱 그래픽 코드를 Mac에서 컴파일합니다. 시뮬레이터는 이 코드를 건너뛰기 때문에, 그러지 않으면 실수가 기기에서야 드러납니다.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPU 프레임 캡처</a></td><td>그래픽 칩에서 프레임 하나를 캡처해 각 그리기 단계의 비용을 나열하고, 느린 부분을 찾습니다.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="아직 확인되지 않음" title="아직 확인되지 않음" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 추천" title="Claude 추천" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">셰이더 수학</a></td><td>Quake 3의 연기와 불 효과를 느리지만 정확하게 다시 계산해, 빠른 그래픽 버전이 같은 그림을 그리는지 확인합니다.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
</tbody>
</table>

## 음성, 언어 & 데이터

<table class="wide">
<thead><tr><th width="190">하네스</th><th>기능</th><th width="60">최초 앱</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">출처</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">스크린샷을 텍스트로</a></td><td>Claude가 읽기 전에 Mac에서 스크린샷과 스캔을 텍스트로 바꾸므로, 이미지를 비공개로 유지하고 Claude의 메모리를 훨씬 적게 씁니다.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Mac이 합성 음성으로 테스트 문구를 말해 앱의 음성 인식기에 들려주므로, 아무도 말하지 않아도 음성 명령을 테스트할 수 있습니다.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="아직 확인되지 않음" title="아직 확인되지 않음" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">기기에서 오디오 재생</a></td><td>Mac이 각 테스트 대화를 오디오 파일로 바꾸고 휴대폰 앱이 마이크 대신 그 파일을 들으므로, 아무도 말하지 않아도 실제 휴대폰에서 음성 기능을 테스트할 수 있습니다.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Siri 문구</a></td><td>&quot;order my usual&quot;처럼 Siri용으로 앱에 넣어 둔 문구가 사람들이 실제로 하는 말과 맞는지 확인합니다. Siri가 이를 올바르게 전달하는지는 아직 휴대폰에서 확인해야 합니다.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">기준 스냅샷</a></td><td>코드를 다시 작성하기 전에 앱의 전체 출력을 저장해 두고, 다시 작성한 버전이 정확히 같은 출력을 내는지 확인합니다.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="아직 확인되지 않음" title="아직 확인되지 않음" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">받아쓰기 정확도</a></td><td>정답 대본이 함께 제공되는 공개 녹음으로 앱의 음성 텍스트 변환을 실행하고, 틀린 글자 수로 점수를 매깁니다.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">번역 검사</a></td><td>모든 번역이 이름, 숫자, 합의한 용어를 그대로 유지하는지, 그리고 번역되지 않은 화면 텍스트가 없는지 확인합니다. Quake 3에도 사용합니다.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">실제 데이터</a></td><td>지어낸 데이터 대신 실제로 기록한 주행 기록으로 경로 매칭을 테스트하며, 지어낸 테스트가 놓친 버그를 찾아냈습니다.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="아직 확인되지 않음" title="아직 확인되지 않음" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">원래 앱과 일치</a></td><td>우리 iPad 버전의 데이터베이스를 원래 Windows 앱의 데이터베이스와 테이블별, 행별로 비교합니다.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td></tr>
</tbody>
</table>

## 하드웨어, 네트워크 & 서비스

<table class="wide">
<thead><tr><th width="190">하네스</th><th>기능</th><th width="60">최초 앱</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">출처</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">정상 기기와 비교</a></td><td>정상 작동이 확인된 구성(iPhone이 이어버드와 직접 연결된 상태)의 동작을 기록하고, 우리 브리지의 기록과 비교합니다.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetooth 캡처</a></td><td>Bluetooth 통신 자체를 기록해, 기기들이 보고한 내용이 아니라 실제로 보낸 내용을 확인합니다.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude 추천" title="Claude 추천" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">상태 점검</a></td><td>각 웹 서비스가 인터넷에서 응답하는지, 그리고 차단되어야 할 경로가 거부되는지 확인합니다.</td></tr>
</tbody>
</table>

## 웹

<table class="wide">
<thead><tr><th width="190">하네스</th><th>기능</th><th width="60">최초 앱</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">출처</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">브라우저 조작</a></td><td>Claude가 브라우저에서 페이지를 열고 양식을 채운 뒤 결과를 읽어, 사이트가 제대로 작동하고 제대로 보이는지 확인합니다.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude 추천" title="Claude 추천" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">웹사이트 배포 확인</a></td><td>웹사이트를 업데이트한 뒤 모든 파일이 서버에 온전히 도착했는지 확인하고, 이어서 휴대폰, 태블릿, 데스크톱 너비에서 레이아웃을 확인합니다.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>프로젝트별 (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">하네스</th><th>기능</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">출처</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">게임 모드</a></td><td>인기 있는 멀티플레이어 모드를 하나씩 우리 버전의 게임에 불러와 맵을 시작하고, 로그에 오류가 있는지 확인합니다.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="아직 확인되지 않음" title="아직 확인되지 않음" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">원작과 나란히 비교</a></td><td>같은 장면을 우리 버전과 원작 게임에서 나란히 녹화해 차이를 모두 드러냅니다.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="아직 확인되지 않음" title="아직 확인되지 않음" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">레벨 스크린샷</a></td><td>각 맵을 맵 제작자가 고른 카메라 각도에서 촬영해 한 장에 배치합니다.</td></tr>
</tbody>
</table>

### 수어 작업

<table>
<thead><tr><th width="190">하네스</th><th>기능</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">출처</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">동작 비교</a></td><td>컴퓨터로 생성한 수어 손동작을 그 바탕이 된 실제 수어 사용자 옆에서 프레임 단위로 재생해 동작이 일치하는지 확인합니다.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">하네스</th><th>기능</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">출처</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">인용 값 확인</a></td><td>Claude가 문서에서 날짜나 수치를 인용하기 전에, 정확히 그 텍스트가 해당 문서에 실제로 있는지 확인합니다.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger Bluetooth 브리지

<table>
<thead><tr><th width="190">하네스</th><th>기능</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">출처</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">브리지 프로브와 대시보드</a></td><td>자전거의 Bluetooth 오디오 브리지를 위한 작은 테스트 프로그램과 실시간 대시보드로, 주행 중 사운드 버퍼, 신호 세기, 연결 상태를 보여 줍니다.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
</tbody>
</table>

### 예약 포털

<table>
<thead><tr><th width="190">하네스</th><th>기능</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">출처</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">예약 모의 실행</a></td><td>온라인 예약을 마지막 단계까지 진행한 뒤 멈추므로, 실제로 예약하지 않고도 각 단계를 테스트할 수 있습니다.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">하네스</th><th>기능</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">출처</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">애니메이션 검사</a></td><td>애니메이션 다이어그램이 재생되는 동안 측정해, 조각들이 잘 맞물리고 겹치지 않는지 픽셀 이하 단위까지 확인합니다.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="해당 버전에서 작동" title="해당 버전에서 작동" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="직접 제작" title="직접 제작" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Claude에 불러오도록 작성한 더 기술적인 버전은 GitHub의 [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md)입니다.
