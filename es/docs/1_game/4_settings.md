---
title: Configuración
date: 2026-10-15
tags: [player]
---

# Configuración

Lo más importante se configura en el primer inicio: el juego abre por sí mismo una configuración rápida con el idioma, el volumen, el rendimiento y los efectos. Un restablecimiento solo afecta a la configuración, los niveles se quedan

## Las pestañas

| Pestaña | Qué contiene |
|---|---|
| `{{ui:settings_general_title}}` | el idioma, cada uno con su propio nombre, `Русский (ru)`. `Del sistema (es)` sigue al dispositivo y muestra qué idioma resultó. También cuántos archivos de nivel se cargan a la vez, el tiempo de espera para un archivo en una dirección web, `{{ui:settings_general-open_folder}}` |
| `{{ui:field_common_audio}}` | el volumen: `{{ui:settings_audio_volume}}`, `{{ui:settings_audio_game}}`, `{{ui:settings_audio_ui}}`, `{{ui:settings_audio_editor-ui}}`, `{{ui:settings_audio_editor-game}}` |
| `{{ui:settings_controls_title}}` | los dispositivos y la forma de guiar al avatar, [[3_controls]] |
| `{{ui:settings_keybindings_label}}` | los atajos de teclado, sobre todo los del editor, [[3_speed-and-shortcuts]] |
| `{{ui:settings_graphics_title}}` | la pantalla, la frecuencia de fotogramas, el antialiasing, `{{ui:settings_graphics-colliders-mode_title}}`, `{{ui:settings_graphics-performance_title}}` ([[17_performance-rating]]), las texturas, los efectos, el posprocesado |
| `{{ui:settings_interface_label}}` | la interfaz durante el juego, `{{ui:settings_interface_open-menu-on-lose}}`, `{{ui:settings_interface_menu-background}}`, `{{ui:settings_interface_levels-layout}}`, la orientación de la pantalla, la superposición de estadísticas |
| `{{ui:settings_game-editor_title}}` | la configuración propia del editor, incluida su propia opción `{{ui:settings_interface_levels-layout}}` |
| `{{ui:settings_profile_tab}}` | tus estadísticas, [[10_statistics]] |
| `{{ui:settings_other_title}}` | la limpieza del almacenamiento, la transferencia de perfil y el estado de Steam Cloud ([[14_profile-transfer]]), el acceso a carpetas en Android, el modo anónimo, `{{ui:settings_other_reset}}` |

`{{ui:settings_interface_menu-background}}` elige qué se ve detrás de los botones del menú principal: una arena en vivo donde un bot esquiva ataques, un campo de formas que giran o nada

`{{ui:settings_interface_levels-layout}}` elige cómo se abre la selección de niveles: una `{{ui:enum_level-browser-layout_grid}}` de portadas o una `{{ui:enum_level-browser-layout_list}}` de filas con descripciones. Hay dos opciones así: la de la pestaña `{{ui:settings_interface_label}}` es para el menú (`{{ui:enum_level-browser-layout_grid}}` por defecto), la de la pestaña `{{ui:settings_game-editor_title}}` es para el editor (`{{ui:enum_level-browser-layout_list}}` por defecto). El botón junto al campo de búsqueda sigue cambiando la vista hasta que sales de esa pantalla

## Configuración rápida

`{{ui:settings_quick-setup_title}}`, un botón de la pestaña `{{ui:settings_general_title}}` encima de `{{ui:settings_general-open_folder}}`, hace unas pocas de las preguntas más importantes, una categoría por página. En el primer inicio se abre sola, antes de la oferta del tutorial.
Cada respuesta tiene una línea que dice qué hace. Las páginas se pueden abrir en cualquier orden, `{{ui:settings_quick-setup_next}}` solo sugiere la siguiente

| Página | Pregunta | Respuestas | Qué cambia |
|---|---|---|---|
| `{{ui:settings_quick-setup_page-language}}` | `{{ui:settings_general_language}}` | `{{ui:settings_general_language_system}}` y cada idioma del juego, con su propio nombre | lo mismo que en la pestaña `{{ui:settings_general_title}}` |
| | `{{ui:settings_audio_volume}}` | un control deslizante | lo mismo que en la pestaña `{{ui:field_common_audio}}` |
| `{{ui:settings_graphics_title}}` | `{{ui:settings_quick-setup_performance}}` | `{{ui:settings_quick-setup_performance-minimum}}`, `{{ui:settings_quick-setup_performance-economy}}`, `{{ui:settings_quick-setup_performance-recommended}}`, `{{ui:settings_quick-setup_performance-max}}` | la escala de renderizado (PC), el antialiasing, el tamaño de las texturas, la frecuencia de fotogramas de los efectos, pero no el límite de fotogramas: todas las respuestas van a la frecuencia de la pantalla. `{{ui:settings_quick-setup_performance-minimum}}` además desactiva los efectos de partículas y el posprocesado y limita las imágenes a 512 |
| | `{{ui:settings_quick-setup_comfort}}` | `{{ui:settings_quick-setup_comfort-full}}`, `{{ui:settings_quick-setup_comfort-soft}}`, `{{ui:settings_quick-setup_comfort-minimal}}` | todos los efectos de posprocesado y la fragmentación del avatar. `{{ui:settings_quick-setup_comfort-soft}}` desactiva los glitches, el grano, el desenfoque, la distorsión de lente y la aberración cromática |
| `{{ui:settings_controls_title}}` | | `{{ui:settings_quick-setup_open-tutorial}}` | aquí nada: el tutorial permite probar cada esquema de control y elegir el tuyo. Se abre desde el menú principal o desde el sandbox |

La respuesta marcada con `{{ui:settings_quick-setup_default-badge}}` es con la que el juego empieza en tu dispositivo. Una elección se aplica al instante y se ve en la configuración completa.
Si tu configuración no coincide con ninguna respuesta, no se resalta ninguna y una línea lo indica: es tu propia configuración, y pulsar una respuesta la sustituye

## Secciones contraídas

Las pestañas largas se dividen en secciones. Lo que se cambia a menudo está abierto, la configuración fina está contraída: una sección se abre por su encabezado.
El botón junto al restablecimiento de la pestaña contrae o expande todas las secciones a la vez

En la pestaña `{{ui:settings_controls_title}}` solo está abierto el dispositivo que tienes en las manos

## Restablecer

Cada pestaña tiene su propio restablecimiento.
`{{ui:settings_other_reset}}` en `{{ui:settings_other_title}}` restablece todas las pestañas a la vez

Un restablecimiento solo afecta a la configuración. Tus niveles se quedan

## La línea de versión

La pantalla de configuración tiene una línea de versión. Un clic sobre ella la copia

Tiene este aspecto: `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`.
Es la línea que hay que citar en un informe de errores, [[11_help]]

## Gráficos

**Antialiasing.** En PC, el valor predeterminado es `{{ui:enum_anti-aliasing-type_msaa}}`. Un teléfono empieza sin antialiasing. Todas las formas del juego son geometría real, y `{{ui:enum_anti-aliasing-type_msaa}}` les da bordes limpios sin desenfoque en todas las plataformas

`{{ui:enum_anti-aliasing-type_fxaa}}` es para teléfonos poco potentes. Es una sola pasada sobre toda la pantalla, y su coste es constante. El coste de `{{ui:enum_anti-aliasing-type_msaa}}` crece cuando se dibujan muchas formas transparentes unas encima de otras

TAA no se ofrece a propósito. Deja una estela detrás de las balas rápidas, y su vibración interfiere con los efectos de glitch

**Frecuencia de fotogramas.** La frecuencia objetivo se fija a mano, no con la sincronización vertical. Así el ritmo de un nivel es el mismo en una pantalla de 60 Hz y en una de 144 Hz.
Mientras `{{ui:settings_graphics_vsync}}` está activado (solo en PC), el límite de fotogramas no hace nada

> [!tip] Recomendación
> En un dispositivo poco potente, baja primero la **escala de renderizado** por debajo de 1. Solo cuesta nitidez, y la interfaz se mantiene a tamaño completo. Solo en PC

Más - [[2_mobile-devices]]

## Modo solo colisionadores

Un modo para practicar, una sección contraída de la pestaña `{{ui:settings_graphics_title}}`. Con `{{ui:settings_graphics-colliders-mode_active}}` activado, un nivel en juego dibuja cada hitbox como un relleno plano de un solo color sobre un fondo liso, y nada más.
Desaparecen: el aspecto de las propias formas, las formas sin colisionador, los efectos, los textos, el posprocesado y el fondo del tema.
No cambian: la música, las colisiones, la cámara y su sacudida, los checkpoints, la interfaz y las estadísticas. Una partida en este modo cuenta como cualquier otra.
Tu avatar se dibuja como siempre

El modo solo funciona al jugar niveles. El editor, el sandbox y el fondo del menú se dibujan como siempre

| Opción | Qué hace |
|---|---|
| `{{ui:settings_graphics-colliders-mode_use-alpha}}` | activado (lo predeterminado) - los rellenos son semitransparentes según el alfa del color, y los obstáculos superpuestos se ven más oscuros. El alfa nunca baja de 0.15. Desactivado - cada relleno es sólido y el alfa del color queda bloqueado |
| `{{ui:settings_graphics-colliders-mode_color}}` | el color del relleno, rojo con alfa 0.6 por defecto. La vista de colisionadores del editor usa el mismo tono con su propia opacidad |
| `{{ui:settings_graphics-colliders-mode_background}}` | lo que se dibuja detrás de los rellenos, gris oscuro por defecto. No es negro para que el borde del encuadre de la cámara se vea contra las franjas negras que lo rodean |

Los dos colores están contraídos bajo su propio rótulo: expande el que necesites para ver su rueda de color

## Modo anónimo

Se activa en `{{ui:settings_other_title}}` → `{{ui:settings_other_suppress-game-saves}}`

Mientras el modo está activado, el juego no guarda nada propio. `settings.json`, las estadísticas globales y las estadísticas de los niveles se quedan intactas en el disco.
Un cambio de configuración funciona igualmente hasta que se cierra el juego

El trabajo con niveles se guarda como siempre: guardar, exportar, importar, copiar y eliminar.
El autoguardado y las copias de seguridad del editor también funcionan, tienen su propio interruptor

El modo dura hasta que se cierra el juego y no se recuerda en ningún sitio

Si lo desactivas, se guarda la configuración actual. Todo lo jugado durante ese tiempo se descarta

> [!info] Conviene saber
> El modo también se activa solo. El [[12_launch-arguments|argumento de inicio]] `--suppress-game-saves` lo activa durante todo el inicio, y no se puede desactivar en el juego. Una configuración o unas estadísticas de una versión más nueva del juego también lo activan. Entonces el juego pregunta en cada inicio si conservarlas o sobrescribirlas con los valores predeterminados
