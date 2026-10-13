---
title: Configuración del editor
date: 2026-10-11
tags: [level_author]
---

# Configuración del editor

Aquí se configuran el autoguardado, la cuadrícula, la selección, los gizmos y los presets de nivel nuevo. El autoguardado está activado por defecto y salta {{v:editor.autosave-delay}} segundos después de una edición

## Editor del juego

Aquí se configuran el autoguardado, la cámara, la selección y los formatos de archivo

| Opción | Qué hace | Por defecto |
|---|---|---|
| `{{ui:settings_game-editor_autosave}}` | activa el autoguardado | activado |
| `{{ui:settings_game-editor_autosave-rate}}` | cuántos segundos pasan desde una edición sin guardar hasta el autoguardado | {{v:editor.autosave-delay}} |
| `{{ui:settings_game-editor_max-autosave-files}}` | cuántas copias se conservan. Al llegar al límite, se elimina la más antigua | {{v:editor.autosave-copies}} |

El temporizador corre solo mientras hay ediciones sin guardar

Un autoguardado hace dos cosas:
1. Escribe una copia del nivel en `<game folder>/backups/<level id>/`
2. Guarda el propio nivel, como hace `Ctrl+S`

Una copia contiene solo el archivo del nivel. Hay dos maneras de restaurarla:
- en la configuración del nivel: `{{ui:settings_level-settings_dangerous-zone}}` → `{{ui:level_backups_open}}`
- a mano: cópiala en la carpeta del nivel con el nombre `level.json` (o `level.blob`)

Más - [[4_not-losing-work#Guardado automático]]

`{{ui:settings_game-editor_camera-min-size}}` y `{{ui:settings_game-editor_camera-max-size}}` limitan cuánto se puede acercar y alejar la vista del editor

`{{ui:settings_game-editor-multi-select-requires_hold}}` y `{{ui:settings_game-editor-pick-invisible_aabb}}` cambian lo que significa un clic en la vista.
Revísalas si la selección se comporta de pronto de otra manera de la habitual

`{{ui:settings_game-editor-level-serialize_mode}}` y `{{ui:settings_game-editor-resources-serialize_mode}}` fijan el formato predeterminado para escribir en el disco

`{{ui:settings_game-editor_publish-language}}` elige en qué idioma se publican primero el título y la descripción de un artículo del Workshop: `{{ui:enum_publish-language_english}}` (el predeterminado) o `{{ui:enum_publish-language_system}}`, el idioma del dispositivo

Más - [[3_speed-and-shortcuts]]

## Cuadrícula

La cuadrícula de la vista se dibuja detrás del nivel y ayuda a colocar objetos

| Opción | Qué hace | Por defecto |
|---|---|---|
| `{{ui:settings_game-editor_grid-active-default}}` | si la cuadrícula está activada al abrir el editor. Es solo el estado inicial | desactivado |
| `{{ui:settings_game-editor-grid_size}}` | el lado de una celda, en unidades del mundo | 1 |
| `{{ui:settings_game-editor-grid_opacity}}` | lo visibles que son las líneas, de 0 a 1 | 0.25 |

El botón de la cuadrícula en la barra de herramientas la activa y la desactiva. Ese estado no se guarda entre sesiones

Cómo se ve la cuadrícula:
- No tiene borde. La celda cambia en pasos de 10 al hacer zoom, y la cuadrícula más fina aparece poco a poco
- Si un nivel de la cuadrícula necesitara demasiadas líneas, ese nivel se desactiva en lugar de aclararse
- El color de las líneas es siempre el inverso del fondo de la cámara en el fotograma actual, así que la cuadrícula sigue visible cuando cambia el fondo. Tú solo fijas la opacidad

Con el ajuste activado, arrastrar una posición se pega a media celda: a los cruces y a los centros de las celdas. Usa la cuadrícula que ves. Con la cuadrícula desactivada, la posición se pega a un paso fijo

## Selección

| Opción | Qué hace | Por defecto |
|---|---|---|
| `{{ui:settings_game-editor-multi-select-requires_hold}}` | activado: en el modo de multiselección un clic añade solo mientras se mantiene `Ctrl`, y un clic normal reemplaza la selección. Desactivado: mientras el modo está activo, cada clic añade | activado |
| `{{ui:settings_game-editor-preview-collider-on_select}}` | dibuja la hitbox de cada objeto seleccionado como un relleno translúcido | desactivado |
| `{{ui:settings_game-editor-pick-invisible_aabb}}` | un clic selecciona un objeto por todo su rectángulo, no por lo que dibuja | desactivado |
| `{{ui:settings_game-editor_selection-long-press-delay}}` | cuánto dura una pulsación mantenida antes de que se abra un menú, en segundos | 0.5 |
| `{{ui:settings_game-editor_selection-long-press-threshold}}` | cuánto se puede mover el cursor durante la pulsación antes de que se convierta en un arrastre | 8 |
| `{{ui:settings_game-editor_selection-collider-opacity}}` | lo sólida que se dibuja la hitbox de un objeto seleccionado | 0.5 |
| `{{ui:settings_game-editor_selection-collider-opacity-view}}` | lo mismo para la vista de todas las hitboxes, más tenue porque allí se solapan cientos | 0.25 |

Soltar `Ctrl` en el modo de multiselección no borra nada ni sale del modo. Solo el siguiente clic normal reemplaza la selección. Más sobre el modo - [[4_hierarchy-and-clipboard]]

El botón de colisionadores en la barra de herramientas muestra las hitboxes de todo lo que hay en el fotograma, incluido el círculo del jugador. Ese estado no se guarda entre sesiones. Si hay demasiadas hitboxes en pantalla, la vista se desactiva sola con un mensaje en lugar de dibujar solo algunas

Un objeto sin colisionador no dibuja hitbox en ninguna de las dos vistas, y un objeto inactivo tampoco

El color de relleno de las dos vistas es `Configuración > Gráficos > Modo solo colisionadores > Color de relleno`, compartido con el modo "Solo colisionadores" del juego ([[4_settings]]). Las dos opacidades de arriba siguen siendo opciones propias del editor

## Gizmos

| Opción | Qué hace | Por defecto |
|---|---|---|
| `{{ui:settings_game-editor_gizmos-scale}}` | lo grandes que son las asas de arrastre en la vista, de 0.1 a 10. Un asa pensada para el ratón es difícil de acertar con el dedo | 1 |

Las asas mantienen el mismo tamaño en pantalla con cualquier zoom

## Agente de IA

`{{ui:settings_game-editor_mcp_title}}` deja que un cliente de IA que habla MCP edite el nivel abierto. Solo en Windows, Linux y Mac: los teléfonos y las tabletas no muestran esta sección

| Opción | Qué hace | Por defecto |
|---|---|---|
| `{{ui:settings_game-editor_mcp-enabled}}` | deja que un cliente se conecte. Solo se puede conectar este equipo, un cliente a la vez | desactivado |
| `{{ui:settings_game-editor_mcp-port}}` | el puerto en el que escucha el editor. `0` elige uno libre en cada inicio, si no, de {{v:mcp.port-min}} a {{v:mcp.port-max}}. Cualquier otro número se revierte | 0 |
| `{{ui:settings_game-editor_mcp-follow-ai}}` | adónde va el cabezal después de que la IA mire un fotograma. Desactivado: vuelve a donde lo dejaste. Activado: se queda en ese fotograma, en pausa | activado |
| `{{ui:settings_game-editor_mcp-reveal-edits}}` | después de cada edición de la IA, selecciona y localiza lo que creó o cambió. Nunca mientras arrastras, escribes o reproduces | activado |
| `{{ui:settings_game-editor_mcp-operation-delay}}` | segundos que espera el editor entre dos operaciones de la IA, de 0 a {{v:mcp.operation-delay-max}}. `0` aplica cada una al instante. Reproducir, pausar y mover el cabezal nunca se retrasan, y tampoco nada que la IA solo lee | {{v:mcp.operation-delay}} |

`{{ui:settings_game-editor_mcp-copy-config}}` copia la configuración que acepta un cliente MCP, con la ruta al servidor y al archivo de conexión del juego ya rellenadas

La línea bajo las opciones dice qué está haciendo el editor: desactivado, escuchando en un puerto, conectado o detenido desde la insignia de IA del editor

Estas opciones se guardan solo en este dispositivo

Más - [[7_ai-assistant]]

## Crear un nivel

`{{ui:settings_editor-settings_level-presets}}` fijan con qué empieza un nivel nuevo: vacío o con un pequeño andamiaje.
Sin un preset tendrías que montar ese andamiaje a mano cada vez

> [!caution] Precaución
> `{{ui:settings_editor-settings_parameters}}` fija lo que luego es incómodo cambiar: la duración en fotogramas y la frecuencia de fotogramas

> [!tip] Consejo
> Las listas `{{ui:settings_editor-settings_quot-level-quot-file-format}}` y `{{ui:settings_editor-settings_quot-metadata-quot-file-format}}` eligen el formato en que el nivel y sus metadatos se escriben en el disco. Los dos se pueden cambiar más tarde en `{{ui:settings_level-settings_dangerous-zone}}` del nivel

Más - [[2_first-level]]

## Biblioteca

`{{ui:settings_editor-settings_library}}` es la última pestaña, después de `{{ui:settings_editor-settings_community}}`. Contiene los recursos que reutilizas entre niveles: la biblioteca del dispositivo, tus propias colecciones y, en la compilación de Steam, las colecciones a las que te suscribiste en el Workshop de Steam

La columna de la izquierda elige el tipo: `{{ui:settings_level-settings_collections}}`, después prefabs, temas, formas y efectos, después texturas, fuentes y audio.
Aquí creas y editas colecciones, copias entradas entre ellas, las importas y exportas y, en la compilación de Steam, publicas las tuyas

Más - [[16_library-and-collections]]

## Usar el trabajo de otros

Cada recurso externo de un nivel (música, imágenes, fuentes, textos) tiene que encajar en una de dos opciones:
- una licencia al menos tan libre como `CC BY-NC`
- el permiso del propio titular de los derechos para la distribución pública no comercial

> [!caution] Precaución
> Un "claro, sin problema" en privado no basta. Un nivel bajo `CC BY-NC` se distribuye públicamente. El permiso tiene que cubrir exactamente eso, no solo tu uso personal

Un nivel que se queda en tu dispositivo no se comprueba.
Las reglas se aplican en un momento concreto: cuando el nivel se entrega a un servicio

Las reglas completas, la lista de licencias aceptadas, la plantilla de solicitud y dónde buscar recursos:
- [[2_legal-resource-paths]]
- [[6_asking-permission]]
- [[3_where-to-get-resources]]
