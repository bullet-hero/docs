---
title: Escribir páginas
date: 2026-10-13
tags: [contributor]
---

# Escribir páginas

Las páginas son archivos markdown en el repositorio abierto bullet-hero/docs. Un cambio llega como pull request: un fork, una rama, el cambio en todos los idiomas, una revisión según la guía de estilo

## Repositorios

Todos los repositorios del proyecto están en la organización [bullet-hero](https://github.com/bullet-hero). Los abiertos:

| Repositorio | Qué contiene |
|---|---|
| [bullet-hero/releases](https://github.com/bullet-hero/releases) | las releases contienen todas las builds públicas del juego, los issues contienen los bugs y las peticiones de los jugadores sobre el juego |
| [bullet-hero/sdk](https://github.com/bullet-hero/sdk) | el código del SDK, los issues contienen los bugs y las peticiones sobre el SDK |
| [bullet-hero/docs](https://github.com/bullet-hero/docs) | estas páginas y sus traducciones |
| [bullet-hero/backend](https://github.com/bullet-hero/backend) | el servidor, vacío por ahora |

El código del juego (`bullet-hero/game`) y el del sitio (`bullet-hero/frontend`) son cerrados

Esta página trata de bullet-hero/docs

## Cómo enviar un cambio

1. Haz un fork de [bullet-hero/docs](https://github.com/bullet-hero/docs) y crea una rama
2. Edita o añade páginas con el formato que se describe abajo
3. Cambia la página en todos los idiomas, o indica en el pull request qué idiomas aún necesitan el cambio. Más - [[translating]]
4. Revisa el texto según la [[style-guide]]
5. Abre un pull request con una descripción breve de qué cambió y por qué

**Los datos salen del juego, del SDK o de su documentación.** Los números, los nombres de campos y de archivos, los atajos y las direcciones nunca se adivinan. ¿No sabes con seguridad si algo es cierto? Dilo en el pull request, no en la página

Un cambio aceptado aparece en [bullethero.space](https://bullethero.space/) en pocos minutos: cada push a `master` vuelve a generar el sitio

> [!tip] Consejo
> No puedes generar el sitio tú mismo, porque su código es cerrado. La vista previa más cercana es Obsidian: un enlace que Obsidian no encuentra tampoco lo encontrará el sitio

## Cómo funciona el repositorio

- **Solo markdown.** No tiene build propia ni scripts
- **Es una bóveda de [Obsidian](https://obsidian.md/).** Abre la carpeta raíz del repositorio como bóveda, y los enlaces, las inserciones y las vistas previas funcionan igual que en el sitio. Cualquier otro editor de markdown también sirve
- **Es un submódulo del sitio.** El sitio incluye el repositorio como su carpeta `content/`, compila las páginas al generarse y prerrenderiza cada una. El sitio se genera a partir del último `master` de este repositorio

## Qué va en cada sitio

| Ruta | Qué contiene | Dirección en el sitio |
|---|---|---|
| `<lang>/docs/1_game/` | para jugadores: instalar, jugar, la configuración, las mecánicas | `/docs/game` |
| `<lang>/docs/2_editor/` | para autores de niveles: la guía y la referencia del editor | `/docs/editor` |
| `<lang>/docs/3_sdk/` | para desarrolladores: el SDK abierto y el formato de nivel | `/docs/sdk` |
| `<lang>/docs/4_server/` | para quienes alojan servidores: los servidores oficiales y de la comunidad | `/docs/server` |
| `<lang>/docs/5_changelog/` | el registro de cambios, una página por versión del juego | `/docs/changelog` |
| `<lang>/notes/` | artículos, comunidad, reglas de edición, documentos públicos y políticas, por fecha | `/notes/<name>` |
| `<lang>/tags/` | páginas de etiquetas | `/tags/<tag>` |
| `<lang>/download.md` | la página de descarga | `/download` |
| `assets/` | imágenes para todos los idiomas | insertadas en las páginas |

`<lang>` es una carpeta de idioma: `en`, `ru`, `zh`, `zh-Hant`, `ja`, `ko`, `es`, `pt` o `fr`. Un archivo fuera de `docs/`, `notes/`, `tags/` y `download.md` no se convierte en página

**La documentación describe cómo funcionan las cosas ahora.** Un historial de cambios, una opinión o un ensayo es una nota en `notes/`

## Nombres de archivo y orden

- **El orden en la barra lateral lo fija un prefijo `N_`** en cada archivo y carpeta dentro de `docs/`: `1_`, `2_` y así sucesivamente, hasta `10_` y más allá
- **El prefijo nunca llega a la dirección.** `1_game/3_controls.md` se abre en `/docs/game/controls`
- **`index.md` no tiene prefijo.** Es la página de inicio de su carpeta. Ocupa la posición de la carpeta y da nombre al grupo de la barra lateral
- **Para cambiar el orden, cambia el nombre de los archivos.** Activa "Automatically update internal links" en Obsidian y corregirá todos los enlaces por sí solo
- **Un nombre sin su prefijo es único dentro de un idioma.** Si dos archivos acaban en la misma dirección, la build del sitio lo indica
- **Un nombre con prefijo es idéntico en todos los idiomas.** `en/docs/2_editor/4_craft/3_difficulty-curve.md` y `ru/docs/2_editor/4_craft/3_difficulty-curve.md` son la misma página
- **`notes/` no tiene prefijos ni subcarpetas.** Nunca cambies el nombre de `notes/cookie-policy`: el aviso de cookies del sitio enlaza a ella

## Frontmatter, título y descripción

Cada página empieza así:

```md
---
title: Difficulty and the curve
date: 2026-09-24
tags: [level_author]
---

# Difficulty and the curve

One line that says what the page is, up to 200 characters, no markup
```

- **`title`, el H1 y la descripción se escriben en el idioma de la página.** El ejemplo de arriba es de la versión en inglés
- **El frontmatter es `title`, `date` y `tags`.** No se lee nada más. `date` en formato `YYYY-MM-DD` es la fecha de la última actualización, no de la creación. Cuando edites un archivo, pon en `date` el día de la edición
- **`# H1` es obligatorio y es igual a `title`.** El sitio muestra solo el cuerpo de la página, así que el H1 es el título visible
- **El primer párrafo después del H1 es la descripción** en listados, búsqueda y vistas previas de enlaces. Se corta a los 200 caracteres. Escríbelo en una sola línea, sin enlaces ni formato. Responde brevemente a la pregunta de la página en lugar de describir lo que hay en ella, [[style-guide#Inicio de la página]]
- **Las secciones son `##`, las subsecciones `###`.** Generan anclas y la tabla de contenidos. No hacen falta niveles más profundos

## Etiquetas de público

Cada página de documentación tiene de 1 a 3 etiquetas de esta lista. Las etiquetas se escriben en `snake_case` sin `#`. El sitio las muestra en la página

| Etiqueta | En el sitio | Quién |
|---|---|---|
| `player` | [[player]] | un jugador normal |
| `advanced_player` | [[advanced_player]] | un jugador interesado en las mecánicas |
| `level_author` | [[level_author]] | hace niveles en el editor |
| `developer` | [[developer]] | construye algo sobre el SDK o amplía el juego |
| `server_host` | [[server_host]] | aloja un servidor para sí y sus amigos |
| `server_advanced` | [[server_advanced]] | aloja un servidor grande y está dispuesto a ampliar o escribir un servidor |
| `contributor` | [[contributor]] | edita los textos y las traducciones de este repositorio |

Las notas de `notes/` usan etiquetas de tema en su lugar, por ahora `legal` ([[legal]])

El lector nunca ve el código de la etiqueta. El nombre visible sale de la página de la etiqueta `<lang>/tags/<code>.md`:

- su `title` es el nombre visible
- su primer párrafo describe al público
- el sitio añade por sí mismo la lista de páginas etiquetadas

Una etiqueta nueva necesita esa página en todos los idiomas

Para mencionar una etiqueta en el texto, enlaza su página: `[[level_author]]`. El enlace muestra el nombre visible en el idioma del lector

## Enlaces

| Qué | Cómo |
|---|---|
| Otra página | `[[3_difficulty-curve]]`, por el nombre completo del archivo con su prefijo |
| Una sección de una página | `[[3_difficulty-curve#Anchor]]` |
| La página de inicio de una carpeta | `[[2_editor/4_craft/index]]`, con la ruta, porque todas esas páginas se llaman `index` |
| Un sitio externo | `[text](https://…)`, con la dirección completa y el esquema |

Los enlaces llevan a una dirección sin idioma, así que un mismo texto fuente funciona en todos los idiomas. `[[cookie-policy]]` lleva a un lector en inglés a la página en inglés, a un lector en ruso a la rusa, a un lector en chino a la china, a un lector en japonés a la japonesa, a un lector en coreano a la coreana, a un lector en español a la española, a un lector en portugués a la portuguesa y a un lector en francés a la francesa

Enlaza solo a páginas que existen. La build del sitio indica cada enlace que no pudo resolver

## Imágenes

Las imágenes están en `assets/`, en la raíz del repositorio, y se insertan con `![[file.png]]`

Una sola carpeta sirve a todos los idiomas. El texto dibujado en una imagen no se traduce con la página

## Recuadros

| Sintaxis | Color | Uso |
|---|---|---|
| `> [!note]`, `> [!info]`, `> [!tip]` | azul | contexto, un atajo, una recomendación |
| `> [!warning]`, `> [!caution]` | amarillo | cuesta tiempo o calidad, destruye trabajo |
| `> [!danger]`, `> [!bug]` | rojo | se muestran, pero la guía de estilo no los usa |

Qué recuadro elegir, su título y el límite de dos por página - [[style-guide]]

## Números, versiones y textos de la interfaz

Un número que decide el juego - la velocidad del avatar, un valor predeterminado de la configuración, un límite de tamaño - y la versión actual no se escriben a mano en la página. Están en `values.yaml`, en la raíz del repositorio, y la página escribe un marcador que el sitio rellena al generarse:

- `\{{v:avatar.move-speed}}` es un valor de `values.yaml`. El sitio lo escribe como escribe los números el idioma de la página, `0.15` en inglés y `0,15` en ruso
- `\{{ui:menu_main_sandbox-btn}}` es un texto de la interfaz de `game/<lang>.yaml`, en el idioma de la propia página
- `\{{` es un par literal de llaves

Una clave que no existe detiene la build del sitio, así que un número nuevo va primero a `values.yaml`. Una versión nombrada como un momento de la historia ("desde `gv 1.0.0`") se queda como texto. Obsidian muestra el marcador tal como está escrito

## Código y otro marcado

- **El resaltado de código** existe solo para `ts`, `tsx`, `js`, `json`, `csharp`, `bash`, `yaml`, `css` y `md`. Los demás lenguajes se muestran como texto plano
- **Las tablas GFM, las listas de tareas, las notas al pie y los `==highlights==`** funcionan
- **Sin MDX y sin JSX.** `{` y `<` se muestran tal cual
