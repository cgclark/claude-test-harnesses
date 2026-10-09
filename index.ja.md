# Claudeの自動テストハーネス

<details class="langs" data-current="ja">
<summary>言語</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · **日本語** · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Claude Codeが自分の作業を自ら確かめる方法です。アプリを実行し、読み取れる形で記録を取り、人が確認する前に合格か不合格かを判定します。各名前から、手順をすべて載せたページが開きます。 各ハーネスのページ自体は英語です。

<img class="c" src="icons/claude-code.svg" alt="Claude推奨" title="Claude推奨" width="16" height="16"> **Claude推奨**: 標準ツールをそのまま使用 (8)<br>
<img class="c" src="icons/claude-code.svg" alt="Claude推奨・拡張あり" title="Claude推奨・拡張あり" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude推奨・拡張あり" title="Claude推奨・拡張あり" width="16" height="16"> **Claude推奨・拡張あり**: 動かすために手を加える必要があった標準ツール (4)<br>
<img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"> **独自開発**: 自分たちで編み出す必要があった手法 (30)

<img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"> そのバージョンで動作 · <img class="o t" src="icons/square.png" alt="未確認" title="未確認" width="16" height="16"> 未確認 · <img class="o t" src="icons/xmark.square.png" alt="そこではまだ動作しない" title="そこではまだ動作しない" width="16" height="16"> そこではまだ動作しない

OSのバージョンに依存しないハーネスは、両方で動作するものとして扱います。それ以外は、それぞれ最後に使ったときの結果でチェックを付けています。このMacは2026年10月2日に27へ移行しており、27のアーキテクチャに対する1つずつの確認はこれからです。

**初出**: 各ハーネスを最初に作ったアプリ

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/big-top.png" alt="" width="20" height="20"> Big Top</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## シミュレータ・Mac・デバイス上のアプリ

<table class="wide">
<thead><tr><th width="190">ハーネス</th><th>機能</th><th width="60">初出</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">由来</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">ヘッドレスシミュレータ</a></td><td>ClaudeがiPhoneアプリをビルドし、バックグラウンドのシミュレータで実行して、スクリーンショットとログを自分で取ります。あなたの画面を占有せずに画面を確認できます。</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude推奨・拡張あり" title="Claude推奨・拡張あり" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude推奨・拡張あり" title="Claude推奨・拡張あり" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">レイアウト計測</a></td><td>バーの高さやスクロール位置など、画面に実際にレイアウトされた値を、画面を移動するあいだ刻々とClaudeが測ります。推測ではなく、見た目がおかしい原因を突き止められます。</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">起動引数フック</a></td><td>テストビルドに仕込んだ隠しスイッチで、サンプルデータ入りの指定画面からアプリを直接開きます。Claudeはアプリ内をタップでたどらずに、どの画面にも行けます。</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">MacでiPadアプリ</a></td><td>アプリのiPad版を通常のMacアプリとして実行し、ClaudeがMac上でログやウインドウのスクリーンショットを使ってテストできるようにします。</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude推奨・拡張あり" title="Claude推奨・拡張あり" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude推奨・拡張あり" title="Claude推奨・拡張あり" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScriptと画面キャプチャ</a></td><td>Claudeが画面を直接操作できないときは、AppleScriptでMacアプリを動かし、そのウインドウだけを撮影して結果を確かめます。</td></tr>
<tr><td><a href="unit-test-suites.md">ユニットテスト</a></td><td>スコア、ルート、キューなど、アプリ内部のロジックを確かめる自動テストです。アプリを開かずに数秒で実行できます。</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude推奨" title="Claude推奨" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">人が行う確認リスト</a></td><td>ヘッドセットを装着する、実際のスマートフォンを使うなど、人にしかできない確認を1つのリストにまとめ続けます。それ以外の作業はその確認を待たずに進められます。</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">全ターゲットのビルド</a></td><td>変更後にiPhone版、Mac版、Vision Pro版をまとめてビルドし直し、テスト用の設定がプレイヤー自身の設定に決して保存されないことを確かめます。</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">SwiftUIライブプレビュー</a></td><td>1つの画面をXcodeのライブプレビューに表示して撮影します。ゲーム全体をビルドして実行しなくても、Claudeがレイアウトの変更を確認できます。</td><td class="m"><img class="o t" src="icons/square.png" alt="未確認" title="未確認" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">アクセシビリティ情報でタップ</a></td><td>スクリーンショットから位置を推測せず、アプリ自身が報告する位置でシミュレータのボタンをタップします。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude推奨" title="Claude推奨" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">2台のシミュレータで2人を再現</a></td><td>シミュレートした2台のiPhoneで、別々の2人としてアプリを動かします。実際のスマートフォン2台なしで、招待、チャレンジ、同期をテストできます。</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="未確認" title="未確認" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">全画面を全言語で</a></td><td>主要な画面をすべての言語で撮影し、極端に長い単語を使った架空の言語も加えて1枚にまとめます。収まらないテキストがすぐに見つかります。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">クラッシュレポート</a></td><td>実機のiPhoneからクラッシュレポートを取り出して読みます。実機でしか起きないクラッシュにも、具体的な原因を特定できます。</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="未確認" title="未確認" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude推奨" title="Claude推奨" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">小さなテストスイート</a></td><td>Pythonツール用の、自己完結した小さな自動チェック一式です。何もインストールせずにどこでも実行できます。</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td></tr>
</tbody>
</table>

## グラフィックスとゲーム

<table class="wide">
<thead><tr><th width="190">ハーネス</th><th>機能</th><th width="60">初出</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">由来</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">ゲームコンソールの操作</a></td><td>ゲームのウインドウに入力する代わりに、スクリプトからゲーム内蔵のコンソールにコマンドを送り、あとでログを読みます。</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">変更前後のフレーム</a></td><td>グラフィックスの変更前と変更後に同じ録画済みのゲーム映像を再生し、フレームを1ピクセルずつ比較します。</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Macでのレイトレーシング</a></td><td>レイトレーシングによるライティングの各段階（影、反射、環境光）を個別に表示するテスト用ビューと、合格か不合格かを出力するセルフチェックです。</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Vision Proのスクリーンショット</a></td><td>シミュレータとヘッドセットの両方で、Vision Proアプリの表示内容を、左右それぞれの目の3D映像も含めて取り込みます。</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="未確認" title="未確認" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude推奨・拡張あり" title="Claude推奨・拡張あり" width="16" height="16"><img class="o" src="icons/plus.png" alt="Claude推奨・拡張あり" title="Claude推奨・拡張あり" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">シェーダーのオフラインコンパイル</a></td><td>レイトレーシングのグラフィックスコードをMac上でコンパイルします。シミュレータではこの処理が省かれるため、そうしないと誤りが実機で初めて表面化します。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">GPUフレームキャプチャ</a></td><td>グラフィックスチップ上の1フレームを取り込み、描画の各ステップにかかったコストを一覧にして、遅い部分を見つけます。</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="未確認" title="未確認" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude推奨" title="Claude推奨" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">シェーダーの数学</a></td><td>Quake 3の煙や炎のエフェクトを時間をかけて厳密に計算し直し、高速なグラフィックス版が同じ絵を描くことを確かめます。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
</tbody>
</table>

## 音声・言語・データ

<table class="wide">
<thead><tr><th width="190">ハーネス</th><th>機能</th><th width="60">初出</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">由来</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">スクリーンショットをテキストに</a></td><td>Claudeが読む前に、スクリーンショットやスキャンをMac上でテキストに変換します。画像を外に出さずに済み、Claudeのメモリ使用量も大幅に減ります。</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m" rowspan="8"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>Macが合成音声でテストフレーズを話し、アプリの音声認識に聞かせます。誰も話さなくても音声コマンドをテストできます。</td><td class="app-c"><img class="app-sm" src="icons/apps/big-top.png" alt="Big Top" title="Big Top" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="未確認" title="未確認" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td></tr>
<tr><td><a href="siri-phrasing-check.md">Siriのフレーズ</a></td><td>「order my usual」など、アプリにSiri用として組み込んだフレーズが、人が実際に言う言い方と合っているか確かめます。Siriがそれを正しく振り分けるかは、まだ実機での確認が必要です。</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">リファレンススナップショット</a></td><td>書き直しの前にアプリの出力をすべて保存し、書き直したバージョンがまったく同じ出力を生むかを確かめます。</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="未確認" title="未確認" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">文字起こしの精度</a></td><td>正しい書き起こし付きの公開録音でアプリの音声テキスト変換を実行し、誤った文字の数をスコア化します。</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">翻訳チェック</a></td><td>各翻訳で名前、数値、取り決めた用語が保たれていること、画面上のテキストが未翻訳のまま残っていないことを確かめます。Quake 3でも使用しています。</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">実データ</a></td><td>作り物ではなく、実際に記録した走行データ一式でルート照合をテストします。作り物のテストでは見逃していたバグが見つかりました。</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="未確認" title="未確認" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">元のアプリとの一致</a></td><td>自分たちのiPad版のデータベースを、元のWindowsアプリのデータベースと、テーブルごと、行ごとに比較します。</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td></tr>
</tbody>
</table>

## ハードウェア・ネットワーク・サービス

<table class="wide">
<thead><tr><th width="190">ハーネス</th><th>機能</th><th width="60">初出</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">由来</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">正常な機器との比較</a></td><td>正常に動作するとわかっている構成（iPhoneがイヤホンと直接通信する状態）の動きを記録し、自分たちのブリッジの記録と比較します。</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Bluetoothキャプチャ</a></td><td>Bluetoothの通信そのものを記録し、機器が報告した内容ではなく、実際に送った内容を確かめます。</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Claude推奨" title="Claude推奨" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">ヘルスチェック</a></td><td>各Webサービスがインターネットから応答すること、そしてブロックされるべきルートが拒否されることを確かめます。</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">ハーネス</th><th>機能</th><th width="60">初出</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">由来</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">ブラウザ操作</a></td><td>Claudeがブラウザでページを開き、フォームに入力して結果を読み取り、サイトが正しく動作し、正しく表示されるか確かめます。</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Claude推奨" title="Claude推奨" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Webサイトのデプロイ確認</a></td><td>Webサイトの更新後、すべてのファイルが欠けることなくサーバに届いたかを確かめ、続いてスマートフォン、タブレット、デスクトップの幅でレイアウトを確認します。</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>プロジェクト固有 (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">ハーネス</th><th>機能</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">由来</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">ゲームMOD</a></td><td>人気のマルチプレイヤーMODを1つずつ自分たちのバージョンのゲームに読み込み、マップを開始して、ログにエラーがないか確かめます。</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="未確認" title="未確認" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">オリジナルと並べて比較</a></td><td>同じシーンを自分たちのバージョンとオリジナルのゲームで録画して並べ、違いがあれば見えるようにします。</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="未確認" title="未確認" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">レベルのスクリーンショット</a></td><td>各マップを、そのマップの作者が選んだカメラアングルから撮影し、1枚にまとめて並べます。</td></tr>
</tbody>
</table>

### 手話の取り組み

<table>
<thead><tr><th width="190">ハーネス</th><th>機能</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">由来</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">動きの比較</a></td><td>コンピュータで生成した手話の手を、その元になった実際の手話者の隣で1フレームずつ再生し、動きが一致するか確かめます。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">ハーネス</th><th>機能</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">由来</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">引用値の確認</a></td><td>Claudeが文書から日付や数値を引用する前に、その文言が本当にその文書に含まれているか確かめます。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
</tbody>
</table>

### Ranger Bluetoothブリッジ

<table>
<thead><tr><th width="190">ハーネス</th><th>機能</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">由来</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">ブリッジのプローブとダッシュボード</a></td><td>自転車用Bluetoothオーディオブリッジ向けの小さなテストプログラムとライブダッシュボードです。走行中に、音声バッファ、信号強度、接続状況を表示します。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
</tbody>
</table>

### 予約ポータル

<table>
<thead><tr><th width="190">ハーネス</th><th>機能</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">由来</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">予約の予行演習</a></td><td>オンライン予約を最終ステップまで進めて、そこで止めます。実際に予約することなく、各ステップをテストできます。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">ハーネス</th><th>機能</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">由来</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">アニメーションのチェック</a></td><td>アニメーション図を再生しながら計測し、各パーツがずれずに揃い、重ならないことを1ピクセル未満の精度で確かめます。</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="そのバージョンで動作" title="そのバージョンで動作" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="独自開発" title="独自開発" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Claudeに読み込ませる用に書いた、より技術的なバージョンは、GitHubの[README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md)です。
