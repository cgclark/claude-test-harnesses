# Ambientes de teste automatizado do Claude

<details class="langs" data-current="pt-PT">
<summary>Idioma</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · [Español](index.es.md) · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · **Português (Portugal)** · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Formas de o Claude Code verificar o próprio trabalho: executar a aplicação, captar algo que consiga ler e decidir se passou ou falhou antes de uma pessoa ter de olhar. Cada nome abre uma página com a receita completa. As páginas dos ambientes de teste estão em inglês.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td><td><b>Recomendado pelo Claude</b>: uma ferramenta padrão usada tal como está</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude, alargado" title="Recomendado pelo Claude, alargado" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recomendado pelo Claude, alargado" title="Recomendado pelo Claude, alargado" width="16" height="16"></td><td><b>Recomendado pelo Claude, alargado</b>: uma ferramenta padrão que tivemos de complementar para funcionar</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td><td><b>Criado por nós</b>: um método que tivemos de desenvolver</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"> funciona nessa versão · <img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"> ainda não confirmado · <img class="o t" src="icons/xmark.square.png" alt="ainda não funciona nessa versão" title="ainda não funciona nessa versão" width="16" height="16"> ainda não funciona nessa versão

Os ambientes de teste que não dependem da versão do sistema contam como funcionais em ambas. Os restantes estão assinalados conforme a última vez que cada um foi utilizado; este Mac passou para a 27 a 2 de outubro de 2026 e ainda falta verificar um a um face à arquitetura da 27.

**Origem**: a aplicação em que cada ambiente de teste foi criado

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Aplicações em simuladores, Macs & dispositivos

<table class="wide">
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="60">Origem</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Proveniência</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Simulador em segundo plano</a></td><td>O Claude compila uma aplicação para iPhone, executa-a no simulador em segundo plano e faz as suas próprias capturas de ecrã e registos, para poder verificar um ecrã sem ocupar o seu.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude, alargado" title="Recomendado pelo Claude, alargado" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recomendado pelo Claude, alargado" title="Recomendado pelo Claude, alargado" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Sonda de layout</a></td><td>O Claude mede o que o ecrã realmente apresentou, como a altura das barras e a posição de deslocamento, momento a momento enquanto passa de um ecrã para outro, para descobrir porque algo parece errado em vez de adivinhar.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Ganchos por argumento de arranque</a></td><td>Interruptores ocultos nas versões de teste que abrem a aplicação diretamente num ecrã escolhido com dados de exemplo, para o Claude chegar a qualquer ecrã sem ter de tocar por toda a aplicação.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">Aplicação de iPad no Mac</a></td><td>Executa a versão para iPad de uma aplicação como uma aplicação normal do Mac, para o Claude a poder testar no Mac com os registos e capturas da janela.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude, alargado" title="Recomendado pelo Claude, alargado" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recomendado pelo Claude, alargado" title="Recomendado pelo Claude, alargado" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript e captura de ecrã</a></td><td>Quando o Claude não consegue controlar o ecrã diretamente, comanda aplicações do Mac com AppleScript e fotografa apenas a janela delas para ver o resultado.</td></tr>
<tr><td><a href="unit-test-suites.md">Testes unitários</a></td><td>Testes automáticos da lógica interna de uma aplicação, como pontuação, percursos e filas, que correm em segundos sem abrir a aplicação.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Lista só para pessoas</a></td><td>Uma lista única e contínua das verificações que só uma pessoa pode fazer, como pôr o headset ou usar um telemóvel real, para que o resto do trabalho não fique à espera delas.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Compilar todos os destinos</a></td><td>Recompila em conjunto as versões para iPhone, Mac e Vision Pro após uma alteração e verifica que as definições de teste nunca são guardadas nas definições do próprio jogador.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Pré-visualização em direto do SwiftUI</a></td><td>Mostra um ecrã na pré-visualização em direto do Xcode e fotografa-o, para o Claude verificar uma alteração de layout sem compilar e executar o jogo inteiro.</td><td class="m"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Toque por acessibilidade</a></td><td>Toca nos botões do simulador nas posições que a própria aplicação indica, em vez de adivinhar onde estão a partir de uma captura de ecrã.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Dois simuladores como duas pessoas</a></td><td>Executa a aplicação em dois iPhones simulados como duas pessoas diferentes, para testar convites, desafios e sincronização sem dois telemóveis reais.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Todos os ecrãs em todas as línguas</a></td><td>Fotografa todos os ecrãs principais em todas as línguas, mais uma língua inventada com palavras extralongas, numa só folha, para ser fácil detetar texto que não cabe.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Relatórios de falha</a></td><td>Retira o relatório de falha de um iPhone real e lê-o, para que uma falha que só acontece no telemóvel tenha uma causa identificada.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Pequeno conjunto de testes</a></td><td>Um conjunto pequeno e autónomo de verificações automáticas para uma ferramenta em Python, que corre em qualquer lado sem instalar nada.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
</tbody>
</table>

## Gráficos & jogos

<table class="wide">
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="60">Origem</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Proveniência</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Comando pela consola do jogo</a></td><td>Envia comandos para a consola integrada do jogo a partir de um script e depois lê o registo, em vez de escrever na janela do jogo.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="5"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Fotogramas de antes e depois</a></td><td>Reproduz o mesmo excerto gravado do jogo antes e depois de uma alteração gráfica e compara os fotogramas píxel a píxel.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Ray tracing no Mac</a></td><td>Vistas de teste que mostram cada etapa da iluminação com ray tracing (sombras, reflexos, luz ambiente) em separado, além de autoverificações que indicam se passou ou falhou.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Capturas de ecrã do Vision Pro</a></td><td>Capta o que a aplicação do Vision Pro mostra, incluindo a vista de cada olho em 3D, no simulador e no headset.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude, alargado" title="Recomendado pelo Claude, alargado" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recomendado pelo Claude, alargado" title="Recomendado pelo Claude, alargado" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Compilação de shaders offline</a></td><td>Compila no Mac o código gráfico de ray tracing, porque o simulador o ignora e, caso contrário, os erros só apareceriam num dispositivo.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">Captura de fotograma na GPU</a></td><td>Capta um fotograma no chip gráfico e indica quanto custou cada etapa de desenho, para descobrir o que está lento.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Matemática dos shaders</a></td><td>Recalcula de forma lenta e exata os efeitos de fumo e fogo do Quake 3 e verifica que a versão gráfica rápida desenha a mesma imagem.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

## Voz, língua & dados

<table class="wide">
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="60">Origem</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Proveniência</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">De capturas de ecrã para texto</a></td><td>Converte capturas de ecrã e digitalizações em texto no Mac antes de o Claude as ler, o que mantém as imagens privadas e usa muito menos da memória do Claude.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>O Mac diz frases de teste com vozes sintéticas para o reconhecedor de fala da aplicação, para que os comandos de voz possam ser testados sem ninguém falar.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Reprodução de áudio num dispositivo</a></td><td>O Mac transforma cada conversa de teste num ficheiro de áudio, que a aplicação do telemóvel ouve em vez do microfone, para que as funcionalidades de voz possam ser testadas no telemóvel real sem ninguém falar.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Frases para a Siri</a></td><td>Verifica se as frases integradas na aplicação para a Siri, como «order my usual», correspondem ao que as pessoas dizem; saber se a Siri as encaminha corretamente ainda exige o telemóvel.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Snapshot de referência</a></td><td>Guarda o resultado completo da aplicação antes de uma reescrita e depois verifica que a versão reescrita produz exatamente o mesmo resultado.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Precisão da transcrição</a></td><td>Executa a conversão de fala em texto da aplicação em gravações públicas acompanhadas de transcrições corretas e conta quantos caracteres erra.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Verificação de traduções</a></td><td>Verifica que cada tradução mantém os nomes, números e termos acordados e que nenhum texto do ecrã ficou por traduzir. Também usado no Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Dados reais</a></td><td>Testa a correspondência de percursos num conjunto de voltas de bicicleta reais gravadas em vez de inventadas, o que revelou erros que os testes inventados não tinham detetado.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Igual à aplicação original</a></td><td>Compara a base de dados da nossa versão para iPad com a da aplicação original para Windows, tabela a tabela e linha a linha.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td></tr>
</tbody>
</table>

## Hardware, redes & serviços

<table class="wide">
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="60">Origem</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Proveniência</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Comparar com um dispositivo de confiança</a></td><td>Grava o comportamento de uma configuração que se sabe funcionar (o iPhone ligado diretamente aos auriculares) e compara com ela uma gravação da nossa ponte.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Capturas de Bluetooth</a></td><td>Grava o próprio tráfego Bluetooth, para ver o que os dispositivos realmente enviaram e não o que comunicaram.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Verificações de funcionamento</a></td><td>Verifica que cada serviço web responde a partir da internet e que a rota que deveria estar bloqueada é recusada.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="60">Origem</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Proveniência</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Comando do navegador</a></td><td>O Claude abre páginas num navegador, preenche formulários e lê o resultado, para verificar se um site funciona e tem o aspeto certo.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado pelo Claude" title="Recomendado pelo Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Verificação de publicação do site</a></td><td>Após uma atualização do site, verifica que cada ficheiro chegou intacto ao servidor e depois verifica o layout nas larguras de telemóvel, tablet e computador.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Específicos do projeto (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Proveniência</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Mods do jogo</a></td><td>Carrega cada mod multijogador popular na nossa versão do jogo, inicia um mapa e verifica se há erros no registo.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Lado a lado com o original</a></td><td>Grava a mesma cena na nossa versão e no jogo original, lado a lado, para mostrar qualquer diferença.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="ainda não confirmado" title="ainda não confirmado" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Imagens dos níveis</a></td><td>Tira uma fotografia de cada mapa no ângulo de câmara escolhido pelo autor do mapa e dispõe-nas numa só folha.</td></tr>
</tbody>
</table>

### Trabalho em língua gestual

<table>
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Proveniência</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Comparação de movimento</a></td><td>Reproduz uma mão gerada por computador a fazer gestos ao lado do gestualizador real que lhe serviu de base, fotograma a fotograma, para verificar se o movimento corresponde.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Proveniência</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Verificar valores citados</a></td><td>Antes de o Claude citar uma data ou um número de um documento, verifica que o texto exato aparece mesmo nesse documento.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

### Ponte Bluetooth Ranger

<table>
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Proveniência</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Sondas e painel da ponte</a></td><td>Pequenos programas de teste e um painel em direto para a ponte de áudio Bluetooth da bicicleta, que mostram buffers de som, intensidade do sinal e ligações durante o passeio.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

### Portal de reservas

<table>
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Proveniência</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Reserva de ensaio</a></td><td>Percorre uma reserva online até ao último passo e para, para que os passos possam ser testados sem fazer uma reserva real.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Ambiente de teste</th><th>Capacidade</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Proveniência</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Verificação de animação</a></td><td>Mede um diagrama animado enquanto é reproduzido, verificando que as peças se alinham e não se sobrepõem, com precisão de uma fração de píxel.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona nessa versão" title="funciona nessa versão" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Criado por nós" title="Criado por nós" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Uma versão mais técnica, escrita para ser carregada no Claude, é o [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) no GitHub.
