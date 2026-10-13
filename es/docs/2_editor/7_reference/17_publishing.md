---
title: Publicación
date: 2026-10-11
tags: [level_author]
---

# Publicación

Un nivel se envía solo desde la pestaña "Publicación" de la configuración del nivel: como archivo comprimido o al Workshop de Steam. El informe comprueba el nivel por sí solo, y sus errores bloquean el envío

## La pestaña "Publicación"

`Publicación` es una pestaña de la configuración del nivel. Es el único lugar desde el que un nivel se envía a alguna parte

Arriba, `{{ui:editor_share_destination}}` muestra la forma de envío elegida. Hacer clic en él abre `{{ui:editor_share_pick-title}}`: las formas que esta compilación ofrece en este dispositivo, cada una con una descripción de una línea.
`{{ui:editor_share_archive}}` está elegido por defecto. La última elección se recuerda hasta que se cierra el juego

Debajo:
- las opciones propias de esa forma
- su informe
- el botón que la ejecuta: `{{ui:editor_share_export}}` o `Publicar`

Si esta compilación no tiene formas de envío en este dispositivo, la pestaña muestra `{{ui:editor_share_none}}`

## El informe

El informe comprueba por sí solo: cuando se abre una forma de envío y cuando cambia cualquiera de sus opciones. No hay botón para ello.
Empieza con la línea `Errores: N, advertencias: N, consejos: N`, seguida de una línea por incidencia

Los errores bloquean el envío. Las advertencias y los consejos quedan a tu criterio

La forma de envío decide las reglas con las que se juzga el nivel. `{{ui:editor_share_archive}}` comprueba con el conjunto `{{ui:editor_publish_profile-local}}`, `{{ui:editor_share_steam}}` con las reglas del Workshop. Qué exige cada conjunto y qué significa cada veredicto - [[5_publish-readiness]]

## Formas de envío

| Forma | Dónde existe | Qué envía |
|---|---|---|
| `{{ui:editor_share_archive}}` | en cualquier dispositivo con diálogo de guardado. No en iOS | un nivel, una colección o un recurso, como archivo |
| `{{ui:editor_share_steam}}` | solo en la compilación de Steam | un nivel o una colección tuya |

Una forma que esta compilación o este dispositivo no tiene simplemente no aparece en la lista

## Archivo comprimido

Para un nivel:

| Elemento | Qué hace |
|---|---|
| `{{ui:editor_share_format}}` | uno de los siete modos de exportación, desde una carpeta simple hasta un archivo comprimido protegido con contraseña |
| `{{ui:editor_share_passphrase}}` | visible solo en los modos protegidos. Un modo protegido con la contraseña vacía no se ejecuta |
| `{{ui:editor_share_export}}` | escribe el nivel donde le indiques |

Qué escribe cada modo y con qué se abre - [[13_export-and-protection#Exportar el nivel]]

Para una colección o un recurso, `{{ui:editor_share_format}}` ofrece cinco de esos modos, y todos son archivos comprimidos. No hay modos de carpeta:

| `{{ui:editor_share_format}}` | Qué obtienes | Con qué se abre |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_zip}}` | un solo archivo | un doble clic en el Explorador de Windows, sin instalar nada |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | un zip con cifrado AES-256 integrado | 7-Zip u otro compresor, que pide la contraseña |
| `{{ui:settings_level-settings_export-mode_zip-protected}}` | el zip entero envuelto en OpenPGP | gpg |
| `{{ui:settings_level-settings_export-mode_targz}}` | un solo archivo | cualquier compresor |
| `{{ui:settings_level-settings_export-mode_targz-protected}}` | un tar.gz envuelto en OpenPGP | gpg |

`{{ui:editor_share_passphrase}}` aparece en los tres modos con contraseña. Con la contraseña vacía no se exporta nada.
Se aplica la comprobación de colecciones de más abajo, con las mismas reglas de `{{ui:editor_publish_profile-local}}`

## Workshop de Steam

Solo en compilaciones de Steam. Los elementos:

| Elemento | Qué hace |
|---|---|
| `{{ui:editor_publish_visibility}}` | quién ve el artículo: `{{ui:editor_publish_visibility-public}}`, `{{ui:editor_publish_visibility-friends-only}}` o `{{ui:editor_publish_visibility-private}}`. Por defecto, `{{ui:editor_publish_visibility-private}}` |
| `{{ui:editor_publish_changelog}}` | la nota de cambios de esta subida. Un campo de varias líneas, con su etiqueta en una línea propia |
| `El título y la descripción se suben en` | el idioma en que se toma el texto del artículo (ver más abajo) |
| `{{ui:editor_share_steam-descriptors}}` | cinco casillas, los descriptores de contenido propios de Steam (ver más abajo) |
| `Publicar` | sube el nivel |

El nivel siempre se comprueba con las reglas del Workshop. Aquí no se eligen reglas

El artículo del Workshop se rellena a partir del nivel:
- el título y la descripción son el nombre y la descripción del nivel, en un idioma
- la vista previa es la portada del nivel, png o jpg, de no más de 1 MB. Cualquier otra portada se omite, y el artículo se sube sin imagen
- las etiquetas las pone el propio juego, ver "Etiquetas del Workshop" más abajo

La primera vez que haces clic en `Publicar` se crea el artículo. Las siguientes actualizan el mismo artículo.
El juego lo encuentra por el id propio del nivel entre los artículos que publicaste, así que en el nivel no se guarda nada

Un nivel protegido no se puede publicar. Más - [[13_export-and-protection]]

La subida lleva la carpeta `ai` del nivel, donde un asistente de IA guarda sus notas sobre el nivel, salvo que `{{ui:settings_level-settings_metadata-level-ai-share}}` esté desmarcado en los metadatos del nivel. Todo el que se suscribe la recibe con el nivel. Más - [[7_ai-assistant#La carpeta ai]]

> [!warning] Advertencia
> Si no has aceptado el acuerdo legal del Workshop de Steam, el artículo se sube pero queda oculto. Acepta el acuerdo en la página del artículo. El juego abre esa página en la superposición de Steam

### Idioma del título

Steam muestra un título y una descripción por artículo. El juego toma el primer idioma que encuentra, en este orden:
1. `{{ui:settings_game-editor_publish-language}}` en la configuración `{{ui:settings_game-editor_title}}`: `{{ui:enum_publish-language_english}}` (el predeterminado) o `{{ui:enum_publish-language_system}}`, el idioma del dispositivo. Más - [[14_editor-settings]]
2. tu propio idioma, es decir, el idioma de la interfaz del juego
3. el inglés
4. el primer idioma en que se escribió el texto

La descripción se busca primero en el idioma del título, para que coincidan.
Un nombre que no está localizado (texto simple) se sube tal como está escrito, y la línea dice `{{ui:editor_share_steam-language-as-written}}`

### Descriptores de contenido

`{{ui:editor_share_steam-descriptors}}` tiene cinco casillas, los descriptores de contenido propios de Steam:
- `{{ui:editor_share_steam-descriptor-mature}}`
- `{{ui:editor_share_steam-descriptor-violence}}`
- `{{ui:editor_share_steam-descriptor-some-nudity}}`
- `{{ui:editor_share_steam-descriptor-frequent-nudity}}`
- `{{ui:editor_share_steam-descriptor-adult-only}}`

Se envían con cada publicación y nunca se guardan en el nivel. Cada publicación envía el conjunto entero, así que una casilla desmarcada quita el descriptor también de un artículo ya publicado.
Se suben en una segunda actualización justo después de la subida. Si esa parte falla, el artículo queda publicado de todos modos, y el resultado dice que los descriptores no se fijaron

### Después de publicar

Si todo va bien, el formulario muestra qué artículo se creó o se actualizó, y un botón `{{ui:editor_publish_open-item}}`. Abre la página del artículo en Steam

Si algo falla, el formulario muestra:
- el motivo en palabras sencillas, `No se pudo publicar: ...`
- `Qué se envió y qué respondió Steam: ...` - una línea técnica en inglés. Conviene citarla al desarrollador cuando informes de un problema
- un `?` que despliega por qué Steam rechaza de esta manera, y tres enlaces: `{{ui:editor_publish_help-docs}}` (esta página), `{{ui:editor_publish_help-steam-support}}` y `{{ui:editor_publish_help-agreement}}`

Las líneas de registro propias del juego sobre la publicación están siempre en inglés, sea cual sea el idioma de la interfaz

| Motivo | Qué hacer |
|---|---|
| `{{ui:enum_workshop-failure_steam-not-running}}` | inicia Steam y reinicia el juego desde Steam |
| `{{ui:enum_workshop-failure_not-owner}}` | publica desde esa cuenta, o haz una copia del nivel, que entonces se sube como un artículo nuevo |
| `{{ui:enum_workshop-failure_access-denied}}` | la cuenta no tiene el juego, la cuenta está limitada (todavía sin compras en Steam) o el Workshop está cerrado para ella |
| `{{ui:enum_workshop-failure_invalid-param}}` | el Workshop del juego no está preparado para subidas, o Steam se está ejecutando con el id de otro juego. Reinicia Steam y el juego |
| `{{ui:enum_workshop-failure_limit-exceeded}}` | elimina artículos antiguos en tus archivos del Workshop |
| `{{ui:enum_workshop-failure_connection}}` | comprueba la conexión y el estado de Steam |
| `{{ui:enum_workshop-failure_invalid-request}}` | un título de hasta 128 caracteres, una descripción de hasta 8000, una vista previa png o jpg de hasta 1 MB |
| `{{ui:enum_workshop-failure_staging}}` | comprueba el espacio libre en el disco y que los archivos del nivel no estén abiertos en otro programa |

Si se crea un artículo nuevo pero su subida se rechaza, el juego elimina ese artículo vacío, para que no quede ningún artículo abandonado en el Workshop

## Compilaciones sin Steam

Una compilación sin Steam no muestra `{{ui:editor_share_steam}}` en la lista. `{{ui:editor_share_archive}}` se mantiene

## Cómo compartir una colección

Una colección se comparte desde su página en la pestaña "Biblioteca". `{{ui:editor_share_share}}` abre el mismo panel en una ventana: `{{ui:editor_share_archive}}` y, en la compilación de Steam, también `{{ui:editor_share_steam}}` para una colección tuya

La comprobación de la colección:
- tiene nombre
- tiene una licencia indicada
- no está vacía
- cada archivo que nombra está en ella
- cada recurso al que hacen referencia sus entradas está incluido en ella

La falta de licencia depende de la forma de envío. Para `{{ui:editor_share_archive}}` es una advertencia, y la exportación se ejecuta. Para `{{ui:editor_share_steam}}` es un error.
Los errores bloquean el envío. Más sobre las colecciones - [[16_library-and-collections]]

## Cómo compartir un recurso

Cada fila de tema, forma, efecto y prefab de la Biblioteca también tiene un botón `{{ui:editor_share_share}}`.
Empaqueta el recurso con todo lo que necesita (por ejemplo, las formas, texturas y prefabs anidados de un prefab) como una colección de una sola entrada

Solo está disponible `{{ui:editor_share_archive}}`, con los mismos cinco formatos que para una colección, incluidos los de contraseña. Quien lo recibe importa el archivo con `{{ui:editor_library_import-archive}}`, como cualquier colección

## Etiquetas del Workshop

El juego pone las etiquetas por sí mismo:

| Artículo | Etiquetas |
|---|---|
| nivel | `level` |
| colección | `collection` y una por cada tipo que contiene: `prefabs`, `themes`, `shapes`, `effects` |

Las texturas, fuentes y audio no reciben etiquetas y no van al Workshop por sí solos. Van dentro de una colección, como lo que usan sus prefabs, temas, formas y efectos. Una colección solo de archivos multimedia se rechaza con una línea que da el motivo, y conviene compartirla como archivo comprimido

> [!info] Conviene saber
> Las "Colecciones" propias de Steam son listas seleccionadas de artículos del Workshop, una función de Valve. No tienen nada que ver con las colecciones de Bullet Hero

## Suscripciones

La compilación de Steam lee tus suscripciones:
- los niveles aparecen en la lista de niveles bajo `{{ui:editor_library-source_workshop}}`, [[2_playing-levels]]
- las colecciones aparecen en la biblioteca del editor bajo el chip `{{ui:editor_library-source_workshop}}`, en solo lectura

Siguiente: [[5_publish-readiness]], [[1_licensing-basics]], [[16_library-and-collections]]
