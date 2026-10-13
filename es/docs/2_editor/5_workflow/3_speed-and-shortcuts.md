---
title: Velocidad y atajos
date: 2026-10-02
tags: [level_author]
---

# Velocidad y atajos

La paleta de comandos (Ctrl+Shift+P), la búsqueda de contenido (Ctrl+F), el botón Localizar y las flechas en una línea de tiempo son lo que más tiempo ahorra. Cualquier tecla se puede reasignar en la configuración

## Los cuatro mayores ahorros de tiempo

- **`{{ui:editor_search-title_command}}`** (`Ctrl+Shift+P`) - todo lo que el editor sabe hacer, con búsqueda por nombre. Es más rápido que recordar en qué panel está un botón
- **`Search Content`** (`Ctrl+F`) - salta a un objeto o a una pista de audio por su nombre. El cabezal va contigo
- **`{{ui:cmd_editor_ping}}`** - la vista encuadra la selección, y la línea de tiempo y la jerarquía se desplazan hasta ella, todo a la vez. Pulsarlo otra vez pasa al siguiente objeto de una selección múltiple
- **Las flechas en una línea de tiempo** - se mueven por dirección, no por posición en una lista. Puedes pasar de un fotograma clave a su vecino sin el ratón

## Valores predeterminados

Los grupos y nombres de abajo son los que muestra `{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`

### Reproducción

| Tecla | Nombre en la configuración | Acción |
|---|---|---|
| `Space` | `{{ui:settings_keybindings_editor_play_pause}}` | reproducir y pausar |

### Edición

| Tecla | Nombre en la configuración | Acción |
|---|---|---|
| `Ctrl+Z` | `{{ui:cmd_editor_undo}}` | deshacer |
| `Ctrl+Y` o `Ctrl+Shift+Z` | `{{ui:cmd_editor_redo}}` | rehacer |
| `Ctrl+S` | `{{ui:settings_keybindings_editor_save}}` | guardar |
| `Ctrl+C` | `{{ui:cmd_editor_copy}}` | copiar |
| `Ctrl+V` | `{{ui:cmd_editor_paste}}` | pegar |
| `Ctrl+D` | `{{ui:cmd_editor_duplicate}}` | duplicar |
| `Ctrl+G` | `{{ui:cmd_editor_pack-prefab}}` | crear un prefab a partir de la selección |

### Selección

| Tecla | Nombre en la configuración | Acción |
|---|---|---|
| `Del` | `{{ui:settings_keybindings_editor_delete}}` | eliminar la selección |
| mantener `Ctrl` | `{{ui:settings_keybindings_editor_multi_select}}` | selección múltiple |
| `Ctrl+Shift+A` | `{{ui:settings_keybindings_editor_deselect}}` | quitar toda la selección a la vez: objetos, fotogramas clave, audio y pulsos |
| `Ctrl+Shift+E` | `{{ui:cmd_editor_exit-prefab}}` | salir del modo prefab y volver al nivel |

### Ver

| Tecla | Nombre en la configuración | Acción |
|---|---|---|
| `Ctrl+F` | `Search Content` | buscar contenido |
| `Ctrl+Shift+P` | `{{ui:editor_search-title_command}}` | ejecutar un comando |
| `Ctrl+Left` | `{{ui:settings_keybindings_editor_panel_left}}` | mostrar u ocultar el panel izquierdo |
| `Ctrl+Right` | `{{ui:settings_keybindings_editor_panel_right}}` | mostrar u ocultar el panel derecho |
| `Ctrl+Down` | `{{ui:settings_keybindings_editor_panel_bottom}}` | mostrar u ocultar el panel inferior |
| `Ctrl+Up` | `{{ui:settings_keybindings_editor_viewport_tools}}` | mostrar u ocultar los grupos de herramientas sobre la vista |
| mantener `` ` `` | `{{ui:settings_keybindings_editor_preview}}` | vista previa: la interfaz del editor se oculta mientras la tecla está pulsada |

### Línea de tiempo

| Tecla | Nombre en la configuración | Acción |
|---|---|---|
| `Z` | `{{ui:settings_keybindings_editor_expansion_cycle}}` | recorrer los modos de contracción: todos los subárboles, solo los tipos elegidos, nada |
| `X` | `{{ui:settings_keybindings_editor_tool_snap}}` | activar o desactivar el ajuste |
| `C` | `{{ui:settings_keybindings_editor_tool_selection}}` | la herramienta de selección |
| `V` | `{{ui:settings_keybindings_editor_tool_marquee}}` | la herramienta de selección rectangular |
| `B` | `{{ui:settings_keybindings_editor_tool_scissors}}` | la herramienta de tijeras |
| `N` | `{{ui:settings_keybindings_editor_tool_edges}}` | la herramienta de bordes |
| `Ctrl+E` | `{{ui:settings_keybindings_editor_fold}}` | contraer los objetos seleccionados en la línea de tiempo |
| `Q` | `{{ui:settings_keybindings_editor_tab_timeline_level}}` | abrir la línea de tiempo del nivel |
| `W` | `{{ui:settings_keybindings_editor_tab_timeline_local}}` | abrir la línea de tiempo local |
| `E` | `{{ui:settings_keybindings_editor_tab_timeline_audio}}` | abrir la línea de tiempo de audio |
| `R` | `{{ui:settings_keybindings_editor_tab_timeline_events}}` | abrir la línea de tiempo de eventos |
| `T` | `{{ui:settings_keybindings_editor_tab_timeline_prefab}}` | abrir la línea de tiempo del prefab |
| `Shift+T` | `{{ui:settings_keybindings_editor_beat_window}}` | la ventana de la cuadrícula de pulsos, donde se marca el tempo con toques. `{{ui:settings_keybindings_editor_beat_tap}}` en sí no tiene tecla predeterminada, asígnale una si la necesitas |
| mantener `Ctrl` con la rueda | `{{ui:settings_keybindings_timeline_pan_modifier}}` | paneo |
| mantener `Shift` con la rueda | `{{ui:settings_keybindings_timeline_zoom_modifier}}` | zoom |

`Z X C V B N` siguen la barra de herramientas de la línea de tiempo de izquierda a derecha, y `Q W E R T` siguen la fila de pestañas. Una línea de tiempo con menos herramientas las pierde por la derecha: la línea de tiempo local solo tiene `Z X C V`. Una letra para la que la línea de tiempo abierta no tiene herramienta no hace nada

### Gizmos

| Tecla | Nombre en la configuración | Acción |
|---|---|---|
| `1` | `{{ui:settings_keybindings_editor_gizmo_none}}` | selección |
| `2` | `{{ui:settings_keybindings_editor_gizmo_position}}` | posición |
| `3` | `{{ui:settings_keybindings_editor_gizmo_rotation}}` | rotación |
| `4` | `{{ui:settings_keybindings_editor_gizmo_scale}}` | escala |
| `5` | `{{ui:settings_keybindings_editor_gizmo_size}}` | tamaño |
| `6` | `{{ui:settings_keybindings_editor_gizmo_anchors}}` | anclas |
| `7` | `{{ui:settings_keybindings_editor_gizmo_pivot}}` | pivote |
| `0` | `{{ui:settings_keybindings_editor_gizmo_hidden}}` | oculto: la selección se mantiene, pero no se dibujan ni las asas ni el borde |

### Ventana

| Tecla | Nombre en la configuración | Acción |
|---|---|---|
| `F11` | `{{ui:settings_keybindings_window_toggle_fullscreen}}` | activar o desactivar la pantalla completa. Funciona en cualquier pantalla, solo en escritorio |
| `Ctrl+S` | `{{ui:settings_keybindings_window_settings_save}}` | escribir la configuración en disco ahora mismo, mientras la configuración está abierta. En el editor, `Ctrl+S` guarda el nivel en su lugar |

### Navegación

| Tecla | Nombre en la configuración | Acción |
|---|---|---|
| `Up` | `{{ui:settings_keybindings_nav_up}}` | moverse hacia arriba en la última superficie en la que hiciste clic |
| `Down` | `{{ui:settings_keybindings_nav_down}}` | moverse hacia abajo en la última superficie en la que hiciste clic |
| `Left` | `{{ui:settings_keybindings_nav_left}}` | moverse hacia la izquierda en la última superficie en la que hiciste clic |
| `Right` | `{{ui:settings_keybindings_nav_right}}` | moverse hacia la derecha en la última superficie en la que hiciste clic |

Las teclas sueltas, como los dígitos de los gizmos, las letras de la línea de tiempo y `Space`, no hacen nada mientras escribes en un campo de texto. Un `2` en un campo de fotograma no cambia el gizmo

## Flechas en una línea de tiempo

Una flecha elige el elemento más cercano en esa dirección en la pantalla. La misma pulsación encuentra el mismo elemento con cualquier zoom

- Desde una selección múltiple, una flecha empieza en el elemento más alejado en la dirección pulsada. Nunca retrocede al bloque que seleccionaste
- Un movimiento con flecha siempre reemplaza la selección. Nunca la amplía
- La línea de tiempo se desplaza solo lo necesario para mostrar el elemento nuevo. Hacer clic en el indicador del cabezal sigue centrando la vista
- Mientras el jugador de prueba está activado, las flechas lo controlan a él, no a la línea de tiempo. La jerarquía y la pestaña `{{ui:settings_level-settings_raw}}` conservan sus flechas una vez que haces clic en ellas

## Ver el nivel

**Vista previa.** Mantén pulsada `` ` `` para ocultar la interfaz del editor y ver solo el nivel. Es una pulsación mantenida, no un interruptor: suelta la tecla y todo vuelve. El nivel, las franjas de letterbox, el jugador y los límites de la cámara siguen visibles.
No hay botón ni opción de configuración para esto. La tecla se puede reasignar como `{{ui:settings_keybindings_editor_preview}}`

**La cuadrícula de la vista** se activa con su botón de la barra de herramientas o con el comando `{{ui:cmd_editor_viewport-grid}}`. Empieza desactivada. Esto se cambia en `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_grid-active-default}}`, y que la hayas activado no se recuerda entre sesiones

**El imán del gizmo** ajusta a la cuadrícula lo que arrastra un gizmo. Está activado por defecto y no depende del modo del gizmo. Se alterna con su botón de la barra de herramientas y con el comando `{{ui:cmd_editor_gizmo-magnet}}`

**La pausa es el estado normal para observar.** La cuadrícula, los colisionadores, la superposición del bot, las asas del gizmo y el borde de la selección se siguen dibujando mientras la reproducción está en pausa. Al sujetar un asa del gizmo, la reproducción se pausa

## Reasignar teclas

Cualquier tecla se puede reasignar: `{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`

Solo se guardan las teclas que cambiaste. El resto viene de los valores predeterminados.
Así, un valor predeterminado mejorado te llega si no has tocado esa tecla.
`{{ui:settings_keybindings_reset}}` simplemente elimina tus cambios, y todas las teclas vuelven a los valores predeterminados

> [!tip] Consejo
> Las etiquetas de las teclas no están fijadas en la interfaz. Tras una reasignación, la paleta de comandos y todos los menús contextuales muestran la tecla nueva al instante

## Teclas pulsadas y mantenidas

Una tecla pulsada solo se activa si sus teclas modificadoras coinciden exactamente.
`Ctrl+Shift+P` no se activa también como `Ctrl+P`, y una `T` suelta no se activa mientras se mantiene `Ctrl`

Una tecla mantenida se activa si sus teclas modificadoras están entre las que se mantienen pulsadas. Afina un gesto que ya está en curso

> [!info] Conviene saber
> Por eso dos teclas mantenidas pueden compartir un botón a propósito. La selección múltiple y el paneo de la línea de tiempo están los dos en `Ctrl` y no se estorban

A continuación: [[1_order-of-work|El orden de trabajo]], [[2_reuse|Reutilización: prefabs, copia, generadores]]
