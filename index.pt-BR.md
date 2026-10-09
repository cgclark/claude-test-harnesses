# Ambientes de teste automatizado do Claude

<details class="langs" data-current="pt-BR">
<summary>Idioma</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · **Português (Brasil)** · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Formas de o Claude Code verificar o próprio trabalho: executar o app, capturar algo que ele consiga ler e decidir se passou ou falhou antes que uma pessoa precise olhar. Cada nome abre uma página com a receita completa. As páginas dos ambientes de teste estão em inglês.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td><td><b>Recomendado pelo Claude</b>: uma ferramenta padrão usada como está</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude, ampliado" title="Recomendado pelo Claude, ampliado" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recomendado pelo Claude, ampliado" title="Recomendado pelo Claude, ampliado" width="16" height="16"></td><td><b>Recomendado pelo Claude, ampliado</b>: uma ferramenta padrão que precisamos complementar para funcionar</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td><td><b>Criado por nós</b>: um método que tivemos de desenvolver</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"> funciona nessa versão · <img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"> ainda não confirmado · <img class="o t" src="icons/xmark.square.png" alt="ainda não funciona nessa versão" title="ainda não funciona nessa versão" width="16" height="16"> ainda não funciona nessa versão

Ambientes de teste que não dependem da versão do sistema contam como funcionando nas duas. Os demais foram marcados conforme a última vez em que cada um foi usado; este Mac passou para a 27 em 2 de outubro de 2026, e ainda falta conferir um por um com a arquitetura da 27.

**Origem**: o app em que cada ambiente de teste foi criado

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Apps em simuladores, Macs & dispositivos

<table class="wide">
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="60">Origem</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedência</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Simulador em segundo plano</a></td><td>O Claude compila um app de iPhone, executa no simulador em segundo plano e faz as próprias capturas de tela e logs, para verificar uma tela sem tomar conta da sua.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude, ampliado" title="Recomendado pelo Claude, ampliado" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recomendado pelo Claude, ampliado" title="Recomendado pelo Claude, ampliado" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Sonda de layout</a></td><td>O Claude mede o que a tela realmente exibiu, como altura das barras e posição de rolagem, instante a instante enquanto você navega entre as telas, para descobrir por que algo parece errado em vez de adivinhar.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Ganchos por argumento de inicialização</a></td><td>Chaves ocultas nas versões de teste que abrem o app direto numa tela escolhida com dados de exemplo, para o Claude chegar a qualquer tela sem ter que tocar pelo app inteiro.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">App de iPad no Mac</a></td><td>Executa a versão de iPad de um app como um app comum de Mac, para o Claude testá-lo no Mac com os logs e capturas da janela.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude, ampliado" title="Recomendado pelo Claude, ampliado" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recomendado pelo Claude, ampliado" title="Recomendado pelo Claude, ampliado" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript e captura de tela</a></td><td>Quando o Claude não consegue controlar a tela diretamente, ele comanda apps do Mac com AppleScript e fotografa só a janela deles para ver o resultado.</td></tr>
<tr><td><a href="unit-test-suites.md">Testes de unidade</a></td><td>Testes automáticos da lógica interna de um app, como pontuação, rotas e filas, que rodam em segundos sem abrir o app.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Lista só para pessoas</a></td><td>Uma lista única e contínua das verificações que só uma pessoa pode fazer, como usar o headset ou um celular de verdade, para que o resto do trabalho não fique esperando por elas.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Compilar todos os destinos</a></td><td>Recompila juntas as versões de iPhone, Mac e Vision Pro após uma mudança e verifica se configurações de teste nunca são salvas nas configurações do próprio jogador.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Pré-visualização ao vivo do SwiftUI</a></td><td>Mostra uma tela na pré-visualização ao vivo do Xcode e a fotografa, para o Claude conferir uma mudança de layout sem compilar e executar o jogo inteiro.</td><td class="m"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Toque por acessibilidade</a></td><td>Toca nos botões do simulador nas posições que o próprio app informa, em vez de adivinhar onde estão a partir de uma captura de tela.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Dois simuladores como duas pessoas</a></td><td>Executa o app em dois iPhones simulados como duas pessoas diferentes, para testar convites, desafios e sincronização sem dois celulares de verdade.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Todas as telas em todos os idiomas</a></td><td>Fotografa todas as telas principais em todos os idiomas, além de um idioma inventado com palavras extralongas, numa só folha, para que texto que não cabe seja fácil de achar.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Relatórios de falha</a></td><td>Puxa o relatório de falha de um iPhone de verdade e o lê, para que uma falha que só acontece no celular ganhe uma causa definida.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Pequeno conjunto de testes</a></td><td>Um conjunto pequeno e independente de verificações automáticas para uma ferramenta em Python, que roda em qualquer lugar sem instalar nada.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
</tbody>
</table>

## Gráficos & jogos

<table class="wide">
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="60">Origem</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedência</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Comando pelo console do jogo</a></td><td>Envia comandos ao console embutido do jogo a partir de um script e depois lê o log, em vez de digitar na janela do jogo.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="5"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Quadros de antes e depois</a></td><td>Reproduz o mesmo trecho gravado do jogo antes e depois de uma mudança gráfica e compara os quadros pixel a pixel.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Ray tracing no Mac</a></td><td>Visualizações de teste que mostram cada etapa da iluminação com ray tracing (sombras, reflexos, luz ambiente) separadamente, além de autoverificações que indicam se passou ou falhou.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Capturas de tela do Vision Pro</a></td><td>Captura o que o app do Vision Pro mostra, incluindo a visão de cada olho em 3D, no simulador e no headset.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude, ampliado" title="Recomendado pelo Claude, ampliado" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recomendado pelo Claude, ampliado" title="Recomendado pelo Claude, ampliado" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Compilação de shaders offline</a></td><td>Compila no Mac o código gráfico de ray tracing, porque o simulador o ignora e os erros, de outra forma, só apareceriam num dispositivo.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">Captura de quadro na GPU</a></td><td>Captura um quadro no chip gráfico e lista quanto custou cada etapa de desenho, para descobrir o que está lento.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Matemática dos shaders</a></td><td>Recalcula de forma lenta e exata os efeitos de fumaça e fogo do Quake 3 e verifica se a versão gráfica rápida desenha a mesma imagem.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

## Voz, idioma & dados

<table class="wide">
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="60">Origem</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedência</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">De capturas de tela para texto</a></td><td>Transforma capturas de tela e digitalizações em texto no Mac antes que o Claude as leia, o que mantém as imagens privadas e usa bem menos da memória do Claude.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>O Mac fala frases de teste com vozes sintéticas para o reconhecedor de fala do app, para testar comandos de voz sem ninguém falar.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Reprodução de áudio em um dispositivo</a></td><td>O Mac transforma cada conversa de teste em um arquivo de áudio, e o app do celular o ouve no lugar do microfone, para testar os recursos de voz no celular de verdade sem ninguém falar.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Frases para a Siri</a></td><td>Verifica se as frases embutidas no app para a Siri, como “order my usual”, correspondem ao que as pessoas dizem; se a Siri as encaminha corretamente ainda precisa ser testado no celular.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Snapshot de referência</a></td><td>Salva a saída completa do app antes de uma reescrita e depois verifica se a versão reescrita produz exatamente a mesma saída.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Precisão da transcrição</a></td><td>Executa a conversão de fala em texto do app em gravações públicas que vêm com transcrições corretas e calcula quantos caracteres ela erra.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Verificação de traduções</a></td><td>Verifica se cada tradução mantém nomes, números e termos combinados e se nenhum texto da tela ficou sem tradução. Também usado no Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Dados reais</a></td><td>Testa a correspondência de rotas num conjunto de pedaladas reais gravadas em vez de inventadas, o que encontrou bugs que os testes inventados não tinham pegado.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Igual ao app original</a></td><td>Compara o banco de dados da nossa versão para iPad com o do app original para Windows, tabela por tabela e linha por linha.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
</tbody>
</table>

## Hardware, redes & serviços

<table class="wide">
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="60">Origem</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedência</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Comparar com um dispositivo confiável</a></td><td>Grava como se comporta uma configuração que sabidamente funciona (o iPhone conectado direto aos fones) e compara com ela uma gravação da nossa ponte.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Capturas de Bluetooth</a></td><td>Grava o próprio tráfego Bluetooth, para ver o que os dispositivos realmente enviaram, e não o que informaram.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Verificações de funcionamento</a></td><td>Verifica se cada serviço web responde pela internet e se a rota que deveria estar bloqueada é recusada.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="60">Origem</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedência</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Comando do navegador</a></td><td>O Claude abre páginas num navegador, preenche formulários e lê o resultado, para verificar se um site funciona e tem a aparência certa.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Verificação de publicação do site</a></td><td>Depois de uma atualização do site, verifica se cada arquivo chegou íntegro ao servidor e depois confere o layout nas larguras de celular, tablet e computador.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Específicos do projeto (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedência</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Mods do jogo</a></td><td>Carrega cada mod multijogador popular na nossa versão do jogo, inicia um mapa e verifica se há erros no log.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Lado a lado com o original</a></td><td>Grava a mesma cena na nossa versão e no jogo original, lado a lado, para mostrar qualquer diferença.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Imagens dos níveis</a></td><td>Tira uma foto de cada mapa no ângulo de câmera escolhido pelo autor do mapa e organiza todas numa só folha.</td></tr>
</tbody>
</table>

### Trabalho com língua de sinais

<table>
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedência</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Comparação de movimento</a></td><td>Reproduz uma mão sinalizando gerada por computador ao lado do sinalizador real que serviu de base, quadro a quadro, para conferir se o movimento corresponde.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedência</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Conferir valores citados</a></td><td>Antes de o Claude citar uma data ou um número de um documento, verifica se o texto exato aparece mesmo naquele documento.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

### Ponte Bluetooth Ranger

<table>
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedência</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Sondas e painel da ponte</a></td><td>Pequenos programas de teste e um painel ao vivo para a ponte de áudio Bluetooth da bicicleta, mostrando buffers de som, intensidade do sinal e conexões durante a pedalada.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

### Portal de reservas

<table>
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedência</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Reserva de ensaio</a></td><td>Percorre uma reserva online até a etapa final e para, para que as etapas possam ser testadas sem fazer uma reserva de verdade.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedência</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Verificação de animação</a></td><td>Mede um diagrama animado enquanto ele roda, verificando se as peças se alinham e não se sobrepõem, com precisão de fração de pixel.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Uma versão mais técnica, escrita para ser carregada no Claude, é o [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) no GitHub.
