---
title: Jugar niveles
date: 2026-10-15
tags: [player]
---

# Jugar niveles

Elige un nivel en la lista de niveles, fija las condiciones de la partida y empieza. El nivel de otra persona es una carpeta normal: cópiala en la carpeta de niveles y actualiza la lista

## Menú principal

| Botón | Qué hace |
|---|---|
| `{{ui:menu_main_levels-btn}}` | la lista de niveles, descrita más abajo |
| `{{ui:menu_main_editor-btn}}` | el editor de niveles, [[2_editor/1_basics/index]] |
| `{{ui:menu_main_sandbox-btn}}` | una arena sin nivel y el tutorial, [[13_sandbox]] |
| `{{ui:settings_common_title}}` | toda la configuración, [[4_settings]] |
| `{{ui:menu_main_story-btn}}` | todavía no funciona |
| `{{ui:menu_main_multiplayer-btn}}` | todavía no funciona |

## La lista de niveles

`{{ui:menu_main_levels-btn}}` en el menú principal abre la lista de niveles. Los niveles vienen de tres sitios:

- `{{ui:root_level-source_local}}` - la carpeta `levels`, [[1_installation]]
- `{{ui:root_level-source_builtin}}` - los niveles que vienen con el juego
- `Workshop` - solo en las versiones de Steam. Muestra los niveles a los que te has suscrito. Las colecciones de recursos a las que te has suscrito no son niveles: aparecen en la biblioteca del editor, [[16_library-and-collections]]

Arriba están el campo de búsqueda, `{{ui:root_level-browser_sort}}`, `{{ui:root_level-browser_layout}}` (cuadrícula o lista) y `{{ui:root_level-browser_filters}}`. La lista se abre como cuadrícula.
Se puede ordenar por `{{ui:root_level-browser_sort-relevance}}`, `{{ui:root_level-browser_sort-title}}`, `{{ui:root_level-browser_sort-duration}}`, `{{ui:root_level-browser_sort-progress}}` y `{{ui:root_level-browser_sort-recent}}`. La flecha junto al botón de ordenar (`{{ui:root_level-browser_reverse}}`) invierte el orden. `{{ui:root_level-browser_sort-relevance}}` no tiene dirección

La búsqueda mira primero los nombres de los niveles, luego los autores y luego las etiquetas

`{{ui:root_level-browser_filters}}` abre una ventana con más filtros. La lista de detrás cambia a medida que pulsas:

- `{{ui:root_level-filters_ai}}` - `{{ui:root_level-filters_ai-yes}}`, `{{ui:root_level-filters_ai-no}}` y `{{ui:root_level-filters_ai-unspecified}}`
- `{{ui:root_level-filters_length}}` - el nivel más corto y el más largo, y si mostrar los niveles cuya duración se desconoce
- `{{ui:root_level-filters_progress}}` - `{{ui:root_level-filters_progress-unplayed}}`, `{{ui:root_level-filters_progress-started}}`, `{{ui:root_level-filters_progress-cleared}}`, `{{ui:root_level-filters_progress-bot}}`
- `{{ui:root_level-filters_recent}}` - las últimas 24 horas, 7 días o 30 días
- `{{ui:root_level-filters_age}}` - la clasificación por edad más alta que se muestra
- `{{ui:root_level-filters_other}}` - ocultar los niveles con contraseña, ocultar los niveles de una versión más nueva del juego
- `{{ui:root_level-filters_tags}}` - pulsa una etiqueta una vez para exigirla y dos veces para excluirla

`{{ui:root_level-filters_progress}}` y `{{ui:root_level-filters_recent}}` solo están en la lista del menú principal. La lista del editor tiene sus propios filtros.
El botón muestra cuántos filtros hay activados, y `{{ui:root_level-browser_reset}}` los desactiva todos. Los filtros se mantienen hasta que cierras el juego

¿Has copiado un nivel en la carpeta? Pulsa `{{ui:root_level-browser_refresh}}` y la lista se actualiza

Un candado en una tarjeta significa que el nivel está protegido con contraseña

Mantener pulsada una tarjeta o hacer clic derecho sobre ella abre un menú: `{{ui:level_passphrase_open}}` y `{{ui:root_level-browser_delete}}`.
`{{ui:root_level-browser_delete}}` en un nivel de `Workshop` cancela tu suscripción al elemento y borra sus archivos. Para eso Steam tiene que estar abierto: si no, Steam vuelve a descargar el nivel. Los niveles integrados no se pueden eliminar

## Añadir el nivel de otra persona

Un nivel es una carpeta normal de archivos. Puedes comprimirla y enviársela a alguien

**Una carpeta.** Copia la carpeta del nivel en `levels` y pulsa `{{ui:root_level-browser_refresh}}`.
Copia la propia carpeta del nivel: la que contiene `level.json` (o `level.blob`) y `metadata.json`

**Un archivo comprimido.** Abre el editor y crea un nivel nuevo con el generador `{{ui:gen_level_archive}}`.
Después elige el archivo con el botón `{{ui:editor_create-level_archive-choose}}`

| Archivo | Resultado |
|---|---|
| `.zip`, `.tar.gz` | se abre |
| `.zip` con su propia contraseña, `.zip.gpg`, `.tar.gz.gpg` | se abre después de `{{ui:editor_create-level_archive-protected}}` |
| `.7z` | se rechaza por ahora. Vuelve a comprimirlo como zip |
| cualquier otro | se rechaza, [[5_troubleshooting]] |

Un archivo comprimido con otro nombre se abre igual: el juego reconoce el formato por los bytes del archivo.
Un archivo comprimido de una versión antigua del juego se actualiza al importarlo

Por defecto, un nivel importado recibe un id propio. Así no sobrescribe un nivel que ya esté en el dispositivo

Más - [[6_sharing-by-hand]]

## La pantalla del nivel

La pantalla del nivel muestra la portada, los autores, la descripción y el autor de la música. También tiene los botones `{{ui:level_level-view_authors}}` y `{{ui:level_level-view_licenses}}`

El nombre del autor y la línea de la música abren su propio enlace si los metadatos del nivel lo incluyen

La clasificación por edad la fija el autor del nivel. El juego no la comprueba

"Contiene contenido generado por IA" aparece cuando el autor declaró que el nivel, su portada o uno de sus recursos se generó con IA. También es una declaración del propio autor. Que no aparezca esa línea no significa "sin IA": puede que el autor simplemente no haya dicho nada

Antes de una partida puedes elegir las condiciones:

| Condición | Opciones |
|---|---|
| `{{ui:menu_levelview_options-lifes_title}}` | `{{ui:menu_levelview_options-lifes_option-zen}}` (la partida nunca termina), `{{ui:menu_levelview_options-lifes_option-one}}`, `{{ui:menu_levelview_options-lifes_option-three}}`, `{{ui:menu_levelview_options-lifes_option-custom}}` (un control deslizante hasta 16) |
| `{{ui:field_common_speed}}` | `0.5`, `1.0`, `2.0`, `{{ui:menu_levelview_options-lifes_option-custom}}` (un control deslizante hasta 2). El nivel y la música cambian a la vez |
| `Checkpoints` | activado o desactivado, [[7_damage]] |
| `{{ui:menu_levelview_options-no-collision_title}}` | activado o desactivado. El avatar atraviesa todo, [[7_damage]] |
| `{{ui:menu_levelview_options-bot}}` | `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}`, `{{ui:enum_bot-kind_warm}}`, [[9_bots]] |
| `{{ui:level_level-view_seed-value}}` | un número, `{{ui:level_level-view_seed-randomize}}`, `{{ui:level_level-view_seed-clear}}`. `0` - una semilla nueva en cada partida, [[8_determinism]] |

`Jugar` empieza la partida

La pausa tiene `{{ui:game_pause-window_continue-btn}}`, `{{ui:game_pause-window_restart-btn}}`, `{{ui:game_game-result_restart-checkpoint}}` (una vez alcanzado un checkpoint), `{{ui:settings_common_title}}`, `{{ui:game_game-result_back-to-options}}` y `{{ui:game_game-result_back-to-menu}}`. `{{ui:game_game-result_back-to-options}}` vuelve a la pantalla del nivel con las condiciones con las que empezó la partida, o a la pestaña `Jugar` del editor si la partida se empezó desde allí

## La ventana de resultados

La ventana muestra `Superado` o `{{ui:game_game-result_lose}}` y tres secciones: `Progreso`, `{{ui:game_game-result_section-damage}}` y `{{ui:game_game-result_section-conditions}}`

- filas: `Completado`, `{{ui:game_game-result_checkpoint}}`, `{{ui:field_common_time}}`, `{{ui:game_game-result_length}}`, `{{ui:game_game-result_hits}}`, `{{ui:game_game-result_lives-left}}`, `{{ui:game_game-result_streak}}`
- condiciones de la partida: `{{ui:field_common_speed}}`, `{{ui:menu_levelview_options-lifes_title}}`, `{{ui:menu_levelview_options-bot}}`, `{{ui:game_game-result_seed}}`, `Checkpoints`. En una partida `{{ui:menu_levelview_options-no-collision_title}}`, a `{{ui:menu_levelview_options-lifes_title}}` se le añade `· Sin colisiones`
- botones: `{{ui:game_pause-window_restart-btn}}`, `{{ui:game_game-result_restart-checkpoint}}`, `{{ui:settings_common_title}}`, `{{ui:game_game-result_back-to-options}}`, `{{ui:game_game-result_back-to-menu}}`

Por defecto, la ventana no se abre al perder. En su lugar, la partida se rebobina hasta el último checkpoint.
Para cambiarlo - `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_open-menu-on-lose}}`

## Récords

La pantalla del nivel tiene un bloque de récord: `{{ui:menu_levelview_record-best}}`, `{{ui:menu_levelview_record-attempts}}` y `{{ui:menu_levelview_record-clears}}` (o `{{ui:menu_levelview_record-none}}`)

Cada conjunto de condiciones tiene su propio récord: vidas, velocidad, checkpoints, colisiones y el bot. El bloque muestra el récord de las condiciones elegidas en este momento.
Los intentos y los completados se cuentan en cualquier partida

Cómo se elige un récord - [[10_statistics]]

## Dificultad

En la lista, la dificultad de un nivel es un icono al principio de la línea bajo su nombre, antes de la duración. La pantalla del nivel muestra el icono y el nombre del grado junto a la clasificación por edad

El grado lo fija el autor del nivel. Un moderador que vuelve a publicar el nivel puede cambiarlo.
Un nivel sin grado no muestra icono: es `{{ui:enum_difficulty-tier_undefined}}`

| Icono | Grado |
|---|---|
| ![[difficulty-auto.svg]] | `{{ui:enum_difficulty-tier_auto}}` - el nivel se juega solo, no hace falta ninguna entrada |
| ![[difficulty-drizzle.svg]] | `{{ui:enum_difficulty-tier_drizzle}}` |
| ![[difficulty-rain.svg]] | `{{ui:enum_difficulty-tier_rain}}` |
| ![[difficulty-downpour.svg]] | `{{ui:enum_difficulty-tier_downpour}}` |
| ![[difficulty-hail.svg]] | `{{ui:enum_difficulty-tier_hail}}` |
| ![[difficulty-barrage.svg]] | `{{ui:enum_difficulty-tier_barrage}}` |
| ![[difficulty-onslaught.svg]] | `{{ui:enum_difficulty-tier_onslaught}}` |
| ![[difficulty-deluge.svg]] | `{{ui:enum_difficulty-tier_deluge}}` |
| ![[difficulty-inferno.svg]] | `{{ui:enum_difficulty-tier_inferno}}` |
| ![[difficulty-singularity.svg]] | `{{ui:enum_difficulty-tier_singularity}}` |

Los grados van del más fácil al más difícil. Por ahora la escala termina en `{{ui:enum_difficulty-tier_singularity}}`. Los grados más difíciles llegarán más adelante, a partir de los niveles que la gente realmente haga

## Marcas de las tarjetas

| Marca | Qué significa |
|---|---|
| `{{ui:root_level-entry_not-listed}}` | la carpeta de Workshop está en el disco, pero no tienes suscripción a ella. Solo se ve si `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general_show-all-found-content}}` está activado |
| `{{ui:root_level-entry_unverified}}` | la fuente del nivel no respondió |
| `{{ui:root_level-entry_newer-version}}`, `{{ui:root_level-entry_newer-file}}` | esta versión del juego no abre el nivel, [[5_troubleshooting]] |
| `{{ui:root_level-entry_level-missing-badge}}` | la carpeta no tiene `level.json`, así que el nivel no se puede empezar, [[4_level-folder-and-backups]] |
| `{{ui:root_level-entry_meta-missing-badge}}` | la carpeta no tiene un `metadata.json` legible. La tarjeta muestra el nombre de la carpeta, y el nivel se puede jugar, [[4_level-folder-and-backups]] |

## Eliminar un nivel

Mantén pulsada una tarjeta o haz clic derecho sobre ella → `{{ui:root_level-browser_delete}}`. El juego pide confirmación antes

Junto con el nivel puedes eliminar sus estadísticas (`{{ui:root_level-delete_statistics}}`) y sus copias de seguridad (`{{ui:root_level-delete_backups}}`)

Eliminar un nivel protegido no requiere contraseña
