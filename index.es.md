# Entornos de pruebas automatizadas para Claude

<details class="langs" data-current="es">
<summary>Idioma</summary>

[English](index.md) · [العربية](index.ar.md) · [Dansk](index.da.md) · [Deutsch](index.de.md) · **Español** · [Suomi](index.fi.md) · [Français](index.fr.md) · [עברית](index.he.md) · [हिन्दी](index.hi.md) · [Bahasa Indonesia](index.id.md) · [Italiano](index.it.md) · [日本語](index.ja.md) · [한국어](index.ko.md) · [Bahasa Melayu](index.ms.md) · [Norsk bokmål](index.nb.md) · [Nederlands](index.nl.md) · [Polski](index.pl.md) · [Português (Brasil)](index.pt-BR.md) · [Português (Portugal)](index.pt-PT.md) · [Русский](index.ru.md) · [Svenska](index.sv.md) · [ไทย](index.th.md) · [Türkçe](index.tr.md) · [Українська](index.uk.md) · [Tiếng Việt](index.vi.md) · [简体中文](index.zh-Hans.md) · [繁體中文](index.zh-Hant.md)

</details>

Formas de que Claude Code compruebe su propio trabajo: ejecutar la app, capturar algo que pueda leer y decidir si pasa o falla antes de que una persona tenga que mirarlo. Cada nombre abre una página con la receta completa. Las páginas de cada entorno de pruebas están en inglés.

<table class="key okey">
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Recomendado por Claude" title="Recomendado por Claude" width="16" height="16"></td><td><b>Recomendado por Claude</b>: una herramienta estándar usada tal cual</td></tr>
<tr><td class="ki"><img class="c" src="icons/claude-code.svg" alt="Recomendado por Claude, ampliado" title="Recomendado por Claude, ampliado" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recomendado por Claude, ampliado" title="Recomendado por Claude, ampliado" width="16" height="16"></td><td><b>Recomendado por Claude, ampliado</b>: una herramienta estándar que tuvimos que ampliar para que funcionara</td></tr>
<tr><td class="ki"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td><td><b>Creado por nosotros</b>: un método que tuvimos que idear</td></tr>
</table>

<img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"> funciona en esa versión · <img class="o t" src="icons/square.png" alt="aún sin confirmar" title="aún sin confirmar" width="16" height="16"> aún sin confirmar · <img class="o t" src="icons/xmark.square.png" alt="aún no funciona ahí" title="aún no funciona ahí" width="16" height="16"> aún no funciona ahí

Los entornos de pruebas que no dependen de la versión del sistema operativo cuentan como funcionales en ambas. El resto se marcan según la última vez que se usó cada uno; este Mac pasó a 27 el 2 de octubre de 2026, y aún falta revisarlos uno por uno con la arquitectura de 27.

**Origen**: la app en la que se creó primero cada entorno de pruebas

<table class="key">
<tr><td><img class="app-sm" src="icons/apps/quake3.png" alt="" width="20" height="20"> Quake 3</td><td><img class="app-sm" src="icons/apps/throwdown.png" alt="" width="20" height="20"> Throwdown</td><td><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="" width="20" height="20"> Frictionless Coffee</td></tr>
<tr><td><img class="app-sm" src="icons/apps/circus.png" alt="" width="20" height="20"> Circus</td><td><img class="app-sm" src="icons/apps/enc0der.png" alt="" width="20" height="20"> Enc0der</td></tr>
</table>

## Apps en simuladores, Macs & dispositivos

<table class="wide">
<thead><tr><th width="190">Entorno de pruebas</th><th>Capacidad</th><th width="60">Origen</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedencia</th></tr></thead>
<tbody>
<tr><td><a href="headless-ios.md">Simulador en segundo plano</a></td><td>Claude compila una app de iPhone, la ejecuta en el simulador en segundo plano y toma sus propias capturas y registros, así puede revisar una pantalla sin ocupar la tuya.</td><td class="app-c" rowspan="7"></td><td class="m" colspan="2" rowspan="8"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado por Claude, ampliado" title="Recomendado por Claude, ampliado" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recomendado por Claude, ampliado" title="Recomendado por Claude, ampliado" width="16" height="16"></td></tr>
<tr><td><a href="uikit-layout-probe.md">Sonda de diseño</a></td><td>Claude mide lo que la pantalla realmente dispuso, como la altura de las barras y la posición de desplazamiento, momento a momento mientras pasas de una pantalla a otra, para encontrar por qué algo se ve mal en lugar de adivinar.</td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
<tr><td><a href="launch-argument-test-hooks.md">Ganchos por argumento de inicio</a></td><td>Interruptores ocultos en las versiones de prueba que abren una app directamente en una pantalla elegida con datos de ejemplo, así Claude llega a cualquier pantalla sin recorrer la app a toques.</td></tr>
<tr><td><a href="designed-for-ipad-on-mac.md">App de iPad en el Mac</a></td><td>Ejecuta la versión para iPad de una app como una app normal de Mac, así Claude puede probarla en el Mac con sus registros y capturas de la ventana.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Recomendado por Claude, ampliado" title="Recomendado por Claude, ampliado" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recomendado por Claude, ampliado" title="Recomendado por Claude, ampliado" width="16" height="16"></td></tr>
<tr><td><a href="applescript-screencapture-fallback.md">AppleScript y captura de pantalla</a></td><td>Cuando Claude no puede controlar la pantalla directamente, maneja las apps del Mac con AppleScript y fotografía solo su ventana para ver el resultado.</td></tr>
<tr><td><a href="unit-test-suites.md">Pruebas unitarias</a></td><td>Pruebas automáticas de la lógica interna de una app, como la puntuación, las rutas y las colas, que se ejecutan en segundos sin abrir la app.</td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado por Claude" title="Recomendado por Claude" width="16" height="16"></td></tr>
<tr><td><a href="human-verify-queue.md">Lista solo para personas</a></td><td>Una lista continua de las comprobaciones que solo puede hacer una persona, como ponerse el visor o usar un teléfono real, para que el resto del trabajo no tenga que esperarlas.</td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
<tr><td><a href="build-check-all-targets.md">Compilar todos los destinos</a></td><td>Vuelve a compilar juntas las versiones para iPhone, Mac y Vision Pro tras un cambio, y comprueba que los ajustes de prueba nunca se guardan en los ajustes propios de un jugador.</td><td class="app-c" rowspan="3"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td></tr>
<tr><td><a href="swiftui-live-preview.md">Vista previa en vivo de SwiftUI</a></td><td>Muestra una pantalla en la vista previa en vivo de Xcode y la fotografía, así Claude puede revisar un cambio de diseño sin compilar ni ejecutar el juego entero.</td><td class="m"><img class="o t" src="icons/square.png" alt="aún sin confirmar" title="aún sin confirmar" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td></tr>
<tr><td><a href="accessibility-tree-tapping.md">Tocar por accesibilidad</a></td><td>Toca botones en el simulador en las posiciones que indica la propia app, en lugar de adivinar dónde están a partir de una captura.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado por Claude" title="Recomendado por Claude" width="16" height="16"></td></tr>
<tr><td><a href="two-simulator-peer-test.md">Dos simuladores como dos personas</a></td><td>Ejecuta la app en dos iPhone simulados como dos personas distintas, así se pueden probar invitaciones, retos y sincronización sin dos teléfonos reales.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m"><img class="o t" src="icons/square.png" alt="aún sin confirmar" title="aún sin confirmar" width="16" height="16"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m" rowspan="2"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
<tr><td><a href="localized-screens-contact-sheets.md">Cada pantalla en cada idioma</a></td><td>Fotografía cada pantalla principal en cada idioma, más un idioma inventado con palabras extralargas, en una sola hoja, para que el texto que no cabe salte a la vista.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td></tr>
<tr><td><a href="device-crashlog-pull.md">Informes de fallos</a></td><td>Extrae el informe de fallo de un iPhone real y lo lee, para que un fallo que solo ocurre en el teléfono tenga una causa identificada.</td><td class="app-c"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="aún sin confirmar" title="aún sin confirmar" width="16" height="16"></td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Recomendado por Claude" title="Recomendado por Claude" width="16" height="16"></td></tr>
<tr><td><a href="stdlib-test-suite.md">Pequeño conjunto de pruebas</a></td><td>Un conjunto pequeño y autónomo de comprobaciones automáticas para una herramienta en Python, que funciona en cualquier sitio sin instalar nada.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td></tr>
</tbody>
</table>

## Gráficos & juegos

<table class="wide">
<thead><tr><th width="190">Entorno de pruebas</th><th>Capacidad</th><th width="60">Origen</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedencia</th></tr></thead>
<tbody>
<tr><td><a href="game-console-driving.md">Control de la consola del juego</a></td><td>Envía comandos a la consola integrada del juego desde un script y lee después su registro, en lugar de escribir en la ventana del juego.</td><td class="app-c" rowspan="7"><img class="app-sm" src="icons/apps/quake3.png" alt="Quake 3" title="Quake 3" width="22" height="22"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
<tr><td><a href="renderer-ab-on-demos.md">Fotogramas antes y después</a></td><td>Reproduce el mismo clip grabado del juego antes y después de un cambio gráfico y compara los fotogramas píxel a píxel.</td></tr>
<tr><td><a href="realtime-raytracing-on-mac.md">Trazado de rayos en el Mac</a></td><td>Vistas de prueba que muestran por separado cada paso de la iluminación por trazado de rayos (sombras, reflejos, luz ambiental), más autocomprobaciones que indican si pasa o falla.</td></tr>
<tr><td><a href="vision-pro-screenshots.md">Capturas de Vision Pro</a></td><td>Captura lo que muestra la app de Vision Pro, incluida la vista de cada ojo en 3D, en el simulador y en el visor.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="aún sin confirmar" title="aún sin confirmar" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado por Claude, ampliado" title="Recomendado por Claude, ampliado" width="16" height="16"><img class="o" src="icons/plus.png" alt="Recomendado por Claude, ampliado" title="Recomendado por Claude, ampliado" width="16" height="16"></td></tr>
<tr><td><a href="offline-shader-compile.md">Compilación de shaders sin conexión</a></td><td>Compila el código gráfico de trazado de rayos en el Mac, porque el simulador lo omite y los errores solo aparecerían en un dispositivo.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
<tr><td><a href="gpu-frame-capture.md">Captura de fotogramas de GPU</a></td><td>Captura un fotograma en el chip gráfico y enumera lo que costó cada paso de dibujo, para encontrar qué va lento.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="aún sin confirmar" title="aún sin confirmar" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado por Claude" title="Recomendado por Claude" width="16" height="16"></td></tr>
<tr><td><a href="shader-math-verifiers.md">Matemáticas de shaders</a></td><td>Recalcula los efectos de humo y fuego de Quake 3 de forma lenta y exacta, y comprueba que la versión gráfica rápida dibuja la misma imagen.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
</tbody>
</table>

## Voz, idiomas & datos

<table class="wide">
<thead><tr><th width="190">Entorno de pruebas</th><th>Capacidad</th><th width="60">Origen</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedencia</th></tr></thead>
<tbody>
<tr><td><a href="on-device-image-reduction.md">De capturas a texto</a></td><td>Convierte capturas y escaneos en texto en el Mac antes de que Claude los lea, lo que mantiene las imágenes privadas y usa mucha menos memoria de Claude.</td><td class="app-c"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m" rowspan="9"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
<tr><td><a href="voice-bench.md">voice-bench</a></td><td>El Mac pronuncia frases de prueba con voces sintéticas hacia el reconocedor de voz de la app, así se pueden probar los comandos de voz sin que nadie hable.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/circus.png" alt="Circus" title="Circus" width="22" height="22"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="aún sin confirmar" title="aún sin confirmar" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td></tr>
<tr><td><a href="device-audio-replay.md">Reproducción de audio en un dispositivo</a></td><td>El Mac convierte cada conversación de prueba en un archivo de audio y la app del teléfono lo escucha en lugar del micrófono, así se pueden probar las funciones de voz en el teléfono real sin que nadie hable.</td></tr>
<tr><td><a href="siri-phrasing-check.md">Frases para Siri</a></td><td>Comprueba que las frases integradas en la app para Siri, como «order my usual», coinciden con lo que dice la gente; si Siri las dirige bien sigue necesitando el teléfono.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/frictionless-coffee.png" alt="Frictionless Coffee" title="Frictionless Coffee" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td></tr>
<tr><td><a href="golden-snapshot.md">Instantánea de referencia</a></td><td>Guarda la salida completa de la app antes de reescribirla y luego comprueba que la versión reescrita produce exactamente la misma salida.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="aún sin confirmar" title="aún sin confirmar" width="16" height="16"></td></tr>
<tr><td><a href="transcription-accuracy-scoring.md">Precisión de la transcripción</a></td><td>Pasa el reconocimiento de voz a texto de la app por grabaciones públicas que incluyen transcripciones correctas, y puntúa cuántos caracteres falla.</td><td class="app-c"></td></tr>
<tr><td><a href="translation-lint.md">Comprobación de traducciones</a></td><td>Comprueba que cada traducción conserva sus nombres, números y términos acordados, y que no quedó ningún texto en pantalla sin traducir. También se usa para Quake 3.</td><td class="app-c" rowspan="2"><img class="app-sm" src="icons/apps/throwdown.png" alt="Throwdown" title="Throwdown" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td></tr>
<tr><td><a href="real-data-fixtures.md">Datos reales</a></td><td>Prueba la coincidencia de rutas con un conjunto de recorridos reales grabados en lugar de inventados, lo que encontró errores que las pruebas inventadas habían pasado por alto.</td><td class="m"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="o t" src="icons/square.png" alt="aún sin confirmar" title="aún sin confirmar" width="16" height="16"></td></tr>
<tr><td><a href="baseline-parity.md">Igual que la app original</a></td><td>Compara la base de datos de nuestra versión para iPad con la de la app original de Windows, tabla por tabla y fila por fila.</td><td class="app-c"><img class="app-sm" src="icons/apps/enc0der.png" alt="Enc0der" title="Enc0der" width="22" height="22"></td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td></tr>
</tbody>
</table>

## Hardware, redes & servicios

<table class="wide">
<thead><tr><th width="190">Entorno de pruebas</th><th>Capacidad</th><th width="60">Origen</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedencia</th></tr></thead>
<tbody>
<tr><td><a href="reference-device-benchmarking.md">Comparar con un dispositivo fiable</a></td><td>Graba cómo se comporta una configuración que se sabe que funciona (el iPhone conectado directamente a los auriculares) y compara con ella una grabación de nuestro puente.</td><td class="app-c" rowspan="3"></td><td class="m" colspan="2" rowspan="3"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
<tr><td><a href="bluetooth-packet-captures.md">Capturas de Bluetooth</a></td><td>Graba el propio tráfico Bluetooth, para ver lo que los dispositivos enviaron realmente y no lo que informaron.</td><td class="m" rowspan="2"><img class="c" src="icons/claude-code.svg" alt="Recomendado por Claude" title="Recomendado por Claude" width="16" height="16"></td></tr>
<tr><td><a href="health-endpoint-checks.md">Comprobaciones de estado</a></td><td>Comprueba que cada servicio web responde desde internet y que la ruta que debe estar bloqueada se rechaza.</td></tr>
</tbody>
</table>

## Web

<table class="wide">
<thead><tr><th width="190">Entorno de pruebas</th><th>Capacidad</th><th width="60">Origen</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedencia</th></tr></thead>
<tbody>
<tr><td><a href="browser-driving.md">Control del navegador</a></td><td>Claude abre páginas en un navegador, rellena formularios y lee el resultado, para comprobar que un sitio funciona y se ve bien.</td><td class="app-c" rowspan="2"></td><td class="m" colspan="2" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="c" src="icons/claude-code.svg" alt="Recomendado por Claude" title="Recomendado por Claude" width="16" height="16"></td></tr>
<tr><td><a href="deploy-verification-breakpoint-sweep.md">Comprobación de despliegue web</a></td><td>Tras actualizar un sitio web, comprueba que cada archivo llegó íntegro al servidor y luego revisa el diseño en anchos de teléfono, tableta y escritorio.</td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
</tbody>
</table>

<details class="sec">
<summary>Específicos de un proyecto (8)</summary>

### <img class="app" src="icons/apps/quake3.png" alt="" width="24" height="24"> Quake 3

<table>
<thead><tr><th width="190">Entorno de pruebas</th><th>Capacidad</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedencia</th></tr></thead>
<tbody>
<tr><td><a href="plugin-test-cases.md">Mods del juego</a></td><td>Carga cada mod multijugador popular en nuestra versión del juego, inicia un mapa y busca errores en el registro.</td><td class="m" colspan="2"><img class="o t" src="icons/square.png" alt="aún sin confirmar" title="aún sin confirmar" width="16" height="16"></td><td class="m" rowspan="3"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
<tr><td><a href="side-by-side-reference-engine.md">Junto al original</a></td><td>Graba la misma escena en nuestra versión y en el juego original, una junto a otra, para mostrar cualquier diferencia.</td><td class="m" rowspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m" rowspan="2"><img class="o t" src="icons/square.png" alt="aún sin confirmar" title="aún sin confirmar" width="16" height="16"></td></tr>
<tr><td><a href="levelshot-capture.md">Capturas de niveles</a></td><td>Toma una imagen de cada mapa desde el ángulo de cámara que eligió su autor y las reúne en una sola hoja.</td></tr>
</tbody>
</table>

### Proyecto de lengua de signos

<table>
<thead><tr><th width="190">Entorno de pruebas</th><th>Capacidad</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedencia</th></tr></thead>
<tbody>
<tr><td><a href="motion-compare.md">Comparación de movimiento</a></td><td>Reproduce una mano que signa generada por ordenador junto a la persona signante real de la que se creó, fotograma a fotograma, para comprobar que el movimiento coincide.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
</tbody>
</table>

### Dossier

<table>
<thead><tr><th width="190">Entorno de pruebas</th><th>Capacidad</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedencia</th></tr></thead>
<tbody>
<tr><td><a href="document-value-verification.md">Verificar valores citados</a></td><td>Antes de que Claude cite una fecha o una cifra de un documento, comprueba que el texto exacto aparece de verdad en ese documento.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
</tbody>
</table>

### Puente Bluetooth Ranger

<table>
<thead><tr><th width="190">Entorno de pruebas</th><th>Capacidad</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedencia</th></tr></thead>
<tbody>
<tr><td><a href="bridge-probes-dashboard.md">Sondas y panel del puente</a></td><td>Pequeños programas de prueba y un panel en vivo para el puente de audio Bluetooth de la bici, que muestran búferes de sonido, intensidad de señal y conexiones mientras se rueda.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
</tbody>
</table>

### Portal de reservas

<table>
<thead><tr><th width="190">Entorno de pruebas</th><th>Capacidad</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedencia</th></tr></thead>
<tbody>
<tr><td><a href="booking-dry-run.md">Reserva de prueba</a></td><td>Recorre una reserva en línea hasta el último paso y se detiene, así se pueden probar los pasos sin hacer una reserva real.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
</tbody>
</table>

### Map in Motion

<table>
<thead><tr><th width="190">Entorno de pruebas</th><th>Capacidad</th><th width="80">macOS<br>/ iOS 26</th><th width="80">macOS<br>/ iOS 27</th><th width="70">Procedencia</th></tr></thead>
<tbody>
<tr><td><a href="animation-self-check.md">Comprobación de animaciones</a></td><td>Mide un diagrama animado mientras se reproduce y comprueba que las piezas encajan y no se solapan, con precisión de una fracción de píxel.</td><td class="m" colspan="2"><img class="o t" src="icons/checkmark.square.png" alt="funciona en esa versión" title="funciona en esa versión" width="16" height="16"></td><td class="m"><img class="o" src="icons/hammer.fill.png" alt="Creado por nosotros" title="Creado por nosotros" width="16" height="16"></td></tr>
</tbody>
</table>

</details>

Una versión más técnica, escrita para cargarla en Claude, es el [README](https://github.com/cgclark/claude-test-harnesses/blob/main/README.md) en GitHub.
