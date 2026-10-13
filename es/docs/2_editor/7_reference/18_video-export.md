---
title: Exportación de video
date: 2026-10-03
tags: [level_author]
---

# Exportación de video

El editor renderiza el nivel abierto en un archivo de video mediante el ffmpeg instalado en tu equipo. El renderizado es offline, fotograma a fotograma, así que el video es exacto por lento que sea el equipo

La exportación funciona en Windows, macOS y Linux. No está disponible en teléfonos

## Dónde encontrarla

- `{{ui:editor_video-export_open}}` en la columna lateral de la configuración del nivel
- el comando `{{ui:cmd_editor_export-video}}` en la paleta de comandos

La ventana se abre sobre el editor. Si se abrió desde la configuración del nivel, vuelve a ella al cerrarse. Mientras se renderiza un video, la ventana no se puede cerrar: `{{ui:editor_video-export_stop}}` termina el renderizado

## Instalar ffmpeg

ffmpeg no forma parte del juego. Instálalo una vez, y la ventana lo encuentra por sí sola. Hace falta la versión `{{v:ffmpeg.min-version}}` o posterior. Una más antigua se rechaza, y la ventana indica la versión que encontró

| Sistema | Comando de instalación |
|---|---|
| Windows | `winget install ffmpeg` |
| macOS | `brew install ffmpeg` |
| Linux | el paquete de tu distribución, por ejemplo `sudo apt install ffmpeg` |

> [!warning] Advertencia
> Algunas distribuciones de Linux traen un ffmpeg anterior a `{{v:ffmpeg.min-version}}` (Ubuntu 24.04 trae la 6.1). En ese caso, instala una compilación más reciente desde el sitio de ffmpeg e indícasela a la ventana

La ventana busca ffmpeg en este orden:
1. el archivo que elegiste con `{{ui:editor_video-export_ffmpeg_choose}}`. Entonces no se busca en ningún otro sitio
2. la ruta de la variable de entorno `BH_FFMPEG`
3. `tools/ffmpeg` dentro de la carpeta de datos del juego
4. cada carpeta de `PATH`
5. las carpetas en las que escriben los instaladores habituales

`{{ui:editor_video-export_ffmpeg_auto}}` olvida el archivo elegido y busca de nuevo. `{{ui:editor_video-export_ffmpeg_check}}` repite la comprobación, por ejemplo justo después de instalar

Tu ffmpeg puede incluir codificadores por hardware (NVIDIA, AMD, Intel, Apple). La ventana prueba cada uno con una décima de segundo de negro y usa solo los que de verdad funcionan en este equipo

## Opciones de la ventana

| Opción | Qué hace |
|---|---|
| `{{ui:editor_video-export_container}}`, `{{ui:editor_video-export_codec}}` | el tipo de archivo y cómo se comprime, ver los formatos más abajo |
| `{{ui:editor_video-export_resolution}}` | el tamaño del video. El ancho y el alto son números pares de `{{v:video-export.min-size}}` a `{{v:video-export.max-size}}` |
| `{{ui:editor_video-export_fps}}` | fotogramas por segundo del video, hasta `{{v:video-export.max-fps}}`. No depende de la frecuencia de fotogramas propia del nivel. Por debajo de `{{v:video-export.min-simulation-rate}}`, cada fotograma se simula en varios pasos, para que el bot juegue como en el juego |
| `{{ui:editor_video-export_range}}` | el nivel entero, el rango de bucle de la línea de tiempo o tus propios fotogramas inicial y final |
| `{{ui:editor_video-export_quality}}` | cuánto espacio ocupa el video. Se oculta en los formatos que ya son sin pérdida |
| `{{ui:editor_video-export_full-chroma}}` | color para cada píxel en lugar de para uno de cada dos. Líneas finas de color más nítidas, un archivo más grande |
| `{{ui:editor_video-export_seed}}` | la semilla de la aleatoriedad del nivel. `0` mantiene la semilla que usa el editor |
| `{{ui:editor_video-export_preroll}}` | cuántos segundos antes del inicio se reproducen sin grabarse, para que los efectos ya tengan su historia. `{{v:video-export.default-preroll}}` por defecto, hasta `{{v:video-export.max-preroll}}` |
| `{{ui:editor_video-export_bot}}` | `{{ui:enum_bot-kind_reflex}}` por defecto, `{{ui:enum_bot-kind_warm}}`, o `{{ui:enum_bot-kind_none}}` para un video sin avatar. Los impactos no hacen nada durante una exportación |
| `{{ui:editor_video-export_post-processing}}`, `{{ui:editor_video-export_effects}}` | los mismos interruptores que en el editor, solo para el video |
| `{{ui:editor_video-export_audio}}` | las pistas del nivel en el video |

Cada opción tiene su propio `?` en la ventana

La interfaz del editor, la cuadrícula, los gizmos, la selección y los límites de la cámara nunca entran en el video. La cámara del nivel encuadra la imagen, y unas barras negras rellenan lo que su relación de aspecto no cubre

## Velocidad de renderizado

El video no depende de lo rápido que sea tu equipo. El tiempo del nivel y el bot avanzan exactamente un fotograma del video por cada fotograma renderizado, así que un equipo lento renderiza el mismo video, solo que más tarde

`{{ui:enum_bot-kind_warm}}` calcula toda su ruta antes del primer fotograma, y la ventana muestra cuánto lleva. Si no encuentra ruta, la exportación se detiene y pide otro bot

## Formatos

Un formato son dos elecciones: `{{ui:editor_video-export_container}}` y `{{ui:editor_video-export_codec}}`. Solo aparecen los pares que tu ffmpeg puede generar. La línea de debajo dice qué sonido va con el par y qué archivo obtienes

| `{{ui:editor_video-export_container}}` | `{{ui:editor_video-export_codec}}` | Sonido | Sirve para |
|---|---|---|---|
| `{{ui:editor_video-export_container_mp4}}` | H.264, HEVC, AV1 | `{{ui:editor_video-export_audio-codec_aac}}` | enviar y subir a cualquier sitio |
| `{{ui:editor_video-export_container_mkv}}` | H.264, HEVC, AV1, VP9, FFV1 | `{{ui:editor_video-export_audio-codec_flac}}` | archivar, FFV1 sin ninguna pérdida |
| `{{ui:editor_video-export_container_mov}}` | H.264, HEVC, ProRes | `{{ui:editor_video-export_audio-codec_pcm}}` | editar en Premiere, DaVinci Resolve, Final Cut |
| `{{ui:editor_video-export_container_webm}}` | VP9, AV1 | `{{ui:editor_video-export_audio-codec_opus}}` | la web |
| `{{ui:editor_video-export_container_gif}}`, `{{ui:editor_video-export_container_webp}}`, `{{ui:editor_video-export_container_apng}}` | - | sin sonido | clips cortos en bucle para chats y páginas |
| `{{ui:editor_video-export_container_sequence}}` | PNG, JPEG, WebP, TIFF | `audio.wav` junto a los fotogramas | lo importa cualquier editor de video |
| `{{ui:editor_video-export_container_audio}}` | WAV, FLAC, MP3, Opus | el propio formato | solo el sonido del nivel, no se renderiza nada |

GIF usa una sola paleta de 256 colores para todo el clip. Que sea corto y pequeño: un GIF de un nivel entero pesa mucho más que un MP4 del mismo nivel

## Adónde va el video

Por defecto, el video va a `recordings/<level id>/` en la carpeta de datos del juego, con el nombre del nivel y la hora de la exportación. `{{ui:editor_video-export_output_folder}}` abre esa carpeta. `{{ui:editor_video-export_output_choose}}` guarda el siguiente video en cualquier otro sitio

Las grabaciones se quedan cuando eliminas el nivel. No forman parte de una transferencia de perfil salvo que marques `{{ui:settings_profile-transfer_category-recordings}}`

## Sonido

El sonido del video no se graba desde los altavoces, y no oyes nada durante una exportación

Con `{{ui:editor_video-export_engine-audio}}` activado (el predeterminado) y efectos en las pistas, el sonido del nivel se reproduce en tiempo real mientras se renderizan los fotogramas, y se graba el sonido propio del juego, efectos incluidos. La exportación dura al menos lo que dura el rango: un equipo rápido espera a que termine el sonido. Desactivado, las pistas se mezclan por separado, con sus fotogramas clave de volumen y paneo pero sin sus efectos. `{{ui:editor_video-export_container_audio}}` siempre mezcla por separado

Bajo la vista previa, la ventana muestra dos barras de progreso, `{{ui:editor_video-export_track_frames}}` y `{{ui:editor_video-export_track_sound}}`: avanzan de forma independiente. En un nivel pesado, el sonido en paralelo puede entrecortarse. En ese caso, activa `{{ui:editor_video-export_sound-after-frames}}`: el sonido se graba después del último fotograma, y la exportación tarda más, tanto como dura el rango

> [!warning] Advertencia
> No cierres el juego mientras se renderiza un video. La ventana lo recuerda durante toda la grabación

## Qué no aparece en el video

- los efectos de las pistas de audio, pero solo con `{{ui:editor_video-export_engine-audio}}` desactivado o en `{{ui:editor_video-export_container_audio}}`. La ventana avisa cuando el nivel los tiene
- un fondo transparente
- una grabación de cómo jugaste tú: en el video solo puede jugar el bot

Lee después: [[13_export-and-protection]], [[7_audio]]
