---
title: Biblioteca y colecciones
date: 2026-10-02
tags: [level_author]
---

# Biblioteca y colecciones

Las colecciones guardan los recursos que reutilizas entre niveles. Un nivel nunca hace referencia a una colección: importar copia el recurso dentro, y el nivel se juega en cualquier parte

## Qué es una colección

**Una colección** es una carpeta de recursos reutilizables. Puede contener recursos de siete tipos:

| Tipo | Cómo se guarda |
|---|---|
| prefabs, temas, formas, efectos | datos, un archivo por entrada |
| texturas, fuentes, audio | archivos multimedia |

Una colección no está ligada a un nivel. Está en tu dispositivo y disponible en cualquier nivel que abras

## Orígenes

La biblioteca muestra recursos de tres orígenes. Cada uno es un chip de filtro encima de la lista:

| Chip | Qué es | Se puede cambiar |
|---|---|---|
| `{{ui:editor_library-source_library}}` | la biblioteca del dispositivo: `resources/prefabs`, `themes`, `shapes`, `effects` | sí |
| `{{ui:editor_library-source_local}}` | tus propias colecciones, `resources/collections` | sí |
| `{{ui:editor_library-source_workshop}}` | las colecciones a las que te suscribiste en el Workshop de Steam, leídas en su sitio. Solo en compilaciones de Steam | no |

Una colección de solo lectura se cambia así: sus entradas se copian a una colección tuya

## La pestaña "Biblioteca"

`{{ui:settings_editor-settings_library}}` es la última pestaña de la pantalla de inicio del editor, después de `{{ui:settings_editor-settings_community}}`

Una columna estrecha de botones elige el tipo:
- `{{ui:editor_library_kind-collections}}`
- `{{ui:editor_library_kind-prefabs}}`, `{{ui:editor_library_kind-themes}}`, `{{ui:editor_library_kind-shapes}}`, `{{ui:editor_library_kind-effects}}`
- `{{ui:editor_library_kind-textures}}`, `{{ui:editor_library_kind-fonts}}`, `{{ui:field_common_audio}}`

A su derecha, el título de la página (a la izquierda) y sus botones (a la derecha) están en una misma fila. La lista está debajo.
Una lista vacía lo dice en su centro

En las páginas de los siete tipos, de `{{ui:editor_library_kind-prefabs}}` a `{{ui:field_common_audio}}`, `{{ui:editor_library_copy-target}}` ocupa una fila propia de ancho completo bajo el título. Los chips de origen están en la fila de debajo

Una ventana de la Biblioteca (la ficha de una colección, la imagen de una textura, la ventana de compartir) se cierra con la cruz de su esquina. No hay botón `{{ui:editor_library_close}}`

Cada fila es un botón. Hacer clic en ella hace lo principal para su tipo:

| Tipo | Al hacer clic en una fila |
|---|---|
| colección | abre su página |
| tema, forma, efecto | abre el editor |
| textura | muestra la imagen y su tamaño |
| prefab, fuente, audio | nada. Una fila de audio tiene su propio botón de reproducción |

Los botones pequeños a la derecha de una fila son las demás acciones, y el icono de la papelera elimina o quita

`{{ui:editor_library_open-folder}}` muestra la carpeta de la página actual en el gestor de archivos del sistema. Solo disponible en Windows, macOS y Linux

### Colecciones

`{{ui:editor_library_open-folder}}` y `{{ui:editor_library_refresh}}` están a la derecha del título de la página. `Nueva colección` y `{{ui:editor_library_import-archive}}` están en una fila aparte debajo, alineados a la derecha

- `Nueva colección` crea una colección vacía y abre su ficha
- `{{ui:editor_library_import-archive}}` añade una colección desde un archivo `.zip` o `.tar.gz` o desde un archivo comprimido protegido con contraseña: un `.zip` con su propia contraseña, `.zip.gpg` o `.tar.gz.gpg`. Si esa colección ya está en el dispositivo, el juego pregunta si reemplazarla

Un archivo comprimido protegido con contraseña abre la ventana `{{ui:editor_library_passphrase-title}}`: `{{ui:editor_library_passphrase-needed}}`. Escribe la contraseña y haz clic en `{{ui:editor_library_open}}`.
Una contraseña incorrecta muestra `{{ui:editor_library_passphrase-wrong}}`
- `{{ui:editor_library_open-folder}}` abre `resources/collections`
- `{{ui:editor_library_refresh}}` vuelve a leer las carpetas

Tus propias colecciones tienen `{{ui:editor_library_edit}}` y el icono de la papelera. La papelera pregunta antes y luego elimina la colección con todos sus archivos

### La ficha de una colección

`{{ui:editor_library_edit}}` abre una ventana con la ficha de la colección:
- `{{ui:editor_library_field-name}}`, `{{ui:field_common_description}}`
- `{{ui:editor_library_field-authors}}`, separados por comas
- `{{ui:editor_library_field-license}}`: `{{ui:editor_library_license-unspecified}}` o una de las licencias habituales
- `{{ui:editor_library_set-cover}}` elige una imagen png. La línea de al lado dice si hay portada

`{{ui:editor_save_text}}` escribe la ficha. `{{ui:editor_cancel_text}}`, la cruz o un clic fuera de la ventana descartan los cambios

### La página de una colección

| Elemento | Qué hace |
|---|---|
| `{{ui:settings_common_back}}` | vuelve a la lista |
| `{{ui:editor_library_edit}}` | abre la ficha. Solo en tus propias colecciones |
| `{{ui:editor_share_share}}` | abre la ventana de compartir: `{{ui:editor_share_archive}}` como `.zip` o `.tar.gz`, con o sin contraseña, y en la compilación de Steam también `{{ui:editor_share_steam}}` para una colección tuya |
| `{{ui:editor_library_open-folder}}` | abre la carpeta propia de la colección |
| `{{ui:editor_library_delete}}` | elimina la colección, preguntando antes |

Debajo está el contenido. Una fila abre la entrada igual que la página de su tipo, y el icono de la papelera quita la entrada de la colección

Una colección de solo lectura dice `{{ui:editor_library_read-only}}`

Más sobre `{{ui:editor_share_share}}` - [[17_publishing]]

### Prefabs, temas, formas, efectos

Cada una de estas páginas muestra todas las entradas de todos los orígenes. Los chips acotan la lista

`{{ui:editor_library_copy-target}}` elige una de tus propias colecciones. Por defecto es `{{ui:editor_library_copy-target-none}}`. Una vez elegido un destino, cada fila de otro sitio recibe `{{ui:editor_library_copy-to}}`

Un tema, una forma o un efecto se abren en el mismo editor que en la configuración del nivel. `{{ui:editor_save_text}}` escribe el cambio donde vive la entrada: en `{{ui:editor_library-source_library}}` o en tu colección.
Una entrada del Workshop se abre en solo lectura, y `{{ui:editor_save_text}}` está desactivado. Para cambiarla, cópiala a una colección tuya

`{{ui:editor_library_new-entry}}` crea un tema, una forma o un efecto nuevos en el editor. La entrada se guarda en la colección de destino, o en `{{ui:editor_library-source_library}}` si no hay destino elegido. Los prefabs se crean en un nivel, y no tienen `{{ui:editor_library_new-entry}}`

Las entradas que puedes cambiar tienen el icono de la papelera, y este pregunta antes

Cada fila tiene `{{ui:editor_share_share}}`. El botón empaqueta la entrada con todo lo que necesita (por ejemplo, las formas, texturas y prefabs anidados de un prefab) en un `.zip` o `.tar.gz`, con o sin contraseña, como una colección de una sola entrada. Quien lo recibe importa ese archivo con `{{ui:editor_library_import-archive}}`, como cualquier colección

`{{ui:editor_library_open-folder}}` abre la carpeta de la biblioteca del dispositivo para ese tipo, por ejemplo `resources/themes`

### Texturas, fuentes, audio

Estas páginas muestran los archivos de todas las colecciones. No hay biblioteca personal para archivos, así que estos tipos viven solo en colecciones

- una fila de textura muestra la imagen
- una fila de audio tiene un botón de reproducción. Suena una pista a la vez, y se detiene cuando sales de la página
- una fila de fuente no tiene vista previa

`{{ui:editor_library_add-file}}` pone un archivo del dispositivo en la colección de destino, así que sin destino el botón está desactivado. Una textura es png o jpg, una fuente ttf u otf, el audio mp3, wav u ogg.
Si la colección ya tiene un archivo con los mismos bytes, no se añade nada, y el juego lo dice

Las filas tienen `{{ui:editor_library_copy-to}}` y el icono de la papelera

### Qué se lleva una copia

Una copia se lleva todo lo que necesita la entrada: las formas, texturas, fuentes y prefabs anidados de un prefab, la forma de partícula de un efecto.
La información de autoría de esos recursos también va con ellos

## La pestaña "Colecciones"

`{{ui:editor_library_kind-collections}}` es una pestaña de la configuración del nivel, justo después de `{{ui:editor_library_kind-prefabs}}`. Arriba hay dos modos: `Importar` y `{{ui:editor_collections_mode-build}}`

### Importar

1. La pestaña muestra una lista de colecciones. Haz clic en la que necesitas
2. Marca las entradas que necesitas. `{{ui:editor_collections_select-all}}` y `{{ui:editor_collections_select-none}}` lo marcan todo o quitan todas las marcas
3. La línea `Seleccionados: N, dependencias añadidas: M` muestra lo que entrará en el nivel. Las dependencias se añaden solas
4. Haz clic en `Importar`

Toda la importación es un solo paso de deshacer

Las texturas, fuentes y audio reciben ids nuevos en el nivel, y sus archivos se copian a la carpeta del nivel con un nombre único.
Un archivo que el nivel ya tiene byte a byte no se copia una segunda vez: la importación toma la textura, la fuente o la pista propia del nivel

### Crear una colección

1. `{{ui:editor_collections_target}}` elige `Una colección nueva` o una de las tuyas. Una nueva toma su nombre del campo `{{ui:editor_library_field-name}}`
2. Marca los recursos del nivel, de cualquiera de los siete tipos
3. Haz clic en `{{ui:editor_collections_build}}`

Una colección nueva recibe los autores del nivel

No se puede crear una colección a partir de un nivel protegido. Más - [[13_export-and-protection]]

## Elegir recursos y buscar

La búsqueda y las ventanas para elegir recursos tienen un nivel `{{ui:settings_editor-settings_library}}` para prefabs, temas, formas y efectos. Muestra todos los orígenes.
Las ventanas para elegir son los campos de forma, colisionador, efecto y tema y `{{ui:cmd_editor_place-prefab}}`

Elegir una entrada de la biblioteca la importa al nivel con sus dependencias y la asigna. Un conflicto hace la misma pregunta que en la pestaña "Colecciones"

Los exploradores de la biblioteca dentro de las pestañas de recursos del nivel funcionan igual y muestran los chips de origen. Más - [[11_level-resources]]

## Conflictos

Una entrada importada puede estar ya en el nivel con el mismo id:
- el mismo contenido - no hay que hacer nada
- otro contenido - se abre la ventana `{{ui:editor_resource-conflict_title}}`

La ventana lista cada conflicto, cada uno con un interruptor `{{ui:editor_resource-conflict_copy}}`:

| Elección | Resultado |
|---|---|
| conservar (interruptor desactivado) | la versión del nivel se queda y se usa |
| `{{ui:editor_resource-conflict_copy}}` | la versión de la colección se añade con un id nuevo. Todo lo que se importó junto con ella hace referencia a la copia |

`{{ui:editor_resource-conflict_all-keep}}` y `{{ui:editor_resource-conflict_all-copy}}` fijan todos los interruptores a la vez. `Importar` aplica la elección, `{{ui:editor_cancel_text}}` no importa nada

Ninguna versión gana en silencio. Cada conflicto con contenido distinto se decide en esta ventana

## Autoría

Los registros sobre los recursos de un nivel cubren temas, efectos, formas y prefabs igual que texturas, fuentes y audio.
Importar copia al nivel los registros necesarios, así que la autoría llega junto con el recurso

Más - [[4_resource-record]]

## En el disco

Las colecciones viven en `resources/collections/<collection-guid>/` en la carpeta de datos del juego. Es la misma carpeta `resources` junto a `levels` donde vive la biblioteca del dispositivo. Más - [[4_level-folder-and-backups]]

| Ruta | Qué contiene |
|---|---|
| `collection.json` o `collection.blob` | el manifiesto: nombre, descripción, autores, licencia, las entradas de textura, fuente y audio y la información de autoría de todo lo que hay dentro |
| `cover.png` | la portada, opcional |
| `prefabs/`, `themes/`, `shapes/`, `effects/` | un `<guid>.json` o `<guid>.blob` por entrada, los mismos archivos que en la biblioteca del dispositivo |
| `media/` | archivos de textura, fuente y audio |

Una colección se pasa como archivo comprimido: `{{ui:editor_share_share}}` en su página, `{{ui:editor_library_import-archive}}` en la lista.
Un archivo comprimido que no es una colección se rechaza

Siguiente: [[17_publishing]], [[2_reuse]], [[4_resource-record]]
