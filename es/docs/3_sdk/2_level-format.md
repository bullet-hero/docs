---
title: Formato de nivel
date: 2026-10-02
tags: [developer, level_author]
---

# Formato de nivel

Un nivel es una carpeta: el contenido en level.json o level.blob, los metadatos en metadata.json o metadata.blob, una portada y archivos multimedia. Las copias de seguridad, los récords y la configuración del jugador se quedan en el dispositivo

## La carpeta del nivel

Cada nombre de archivo de una carpeta de nivel está fijado en `FileNames`:

| Archivo | Modelo | Qué contiene |
|---|---|---|
| `level.json` o `level.blob` | `Level` | el contenido: configuración, objetos y eventos, audio, recursos, ayudas |
| `metadata.json` o `metadata.blob` | `LevelMeta` | título, descripción, autores, licencia, un registro por cada recurso, una referencia a la portada |
| `logo.png` o `logo.jpg` | - | la portada |
| canción, imágenes, fuentes | - | archivos multimedia a los que hace referencia el nivel |

**La extensión es el formato.** No está escrita en ningún sitio dentro de los archivos. El lector mira qué archivo existe: `level.json` o `level.blob`

El nivel y los metadatos eligen su formato por separado. Por ejemplo, el nivel integrado `new-zero-demo` guarda `level.blob` junto a `metadata.json`

**`metadata.json` es un archivo aparte a propósito.** Un catálogo muestra mil niveles a partir de mil archivos pequeños de metadatos. Para eso no se abre ni un solo nivel

## Recursos

Un recurso se direcciona con el par `uri` y `uri_type` (`ResourceUriType`):

| Valor | Tipo | Dónde está el archivo |
|---|---|---|
| 1 | `LevelPath` | dentro de la carpeta del nivel. Solo este tipo hace que un nivel sea portátil |
| 2 | `AbsolutePath` | en otro lugar de este dispositivo |
| 3 | `DirectUrl` | se descarga por la red |
| 4 | `StreamingAssets` | viene con el juego, no con el nivel |

`AbsolutePath` aparece cuando un nivel se crea alrededor de una canción. Al exportar un archivo comprimido, ese archivo se copia dentro. Más - [[4_archives]]

La portada está disponible a través de `LevelMeta.LevelLogo`, como cualquier otro recurso. Si es `logo.png` o `logo.jpg` lo deciden los bytes del propio archivo, no el nombre de la imagen de origen

El registro de autoría de la portada es un `ResourceMeta` con `resource_type` 9 (`LevelLogo`). En él no se rellenan ni `resource_id` ni `resource_guid`: un nivel tiene una sola portada, así que el tipo es toda la dirección

## Declaraciones de IA

`LevelMeta` y cada `ResourceMeta` llevan `ai_generated` de tipo `AiGeneration`:

| Valor | Nombre | Qué significa |
|---|---|---|
| 0 | `NotSpecified` | no se declara nada, desconocido. Es el valor predeterminado, y una clave ausente se lee así |
| 1 | `No` | declarado como hecho sin generación por IA |
| 2 | `Yes` | declarado como generado por IA |

En `LevelMeta` cubre solo el contenido propio del nivel. Cada recurso y la portada se declaran en sus propios registros. Si un nivel contiene contenido de IA no se guarda: eso lo responde `LevelMeta.ContainsAiContent()`, y solo cuenta `Yes`

## Lo que no viaja con un nivel

Estos archivos están junto a la carpeta `levels`, nunca dentro de una carpeta de nivel. Comprimir, enviar o eliminar un nivel no los toca:

| Carpeta o archivo | Qué es | Por qué se queda |
|---|---|---|
| `backups/` | guardados automáticos del editor, una carpeta por id de nivel, `backup_level_<time>.<extension>` | una copia dentro de la carpeta que protege se elimina junto con ella |
| `stats/` | récords y progreso por `LevelId` y `statistics.json` | un nivel que alguien envió llegaría ya completado |
| `settings.json` | `UserSettings`, la configuración del jugador para todo el dispositivo | pertenece al jugador, no al nivel |
| `resources/themes`, `effects`, `shapes`, `prefabs` | las bibliotecas compartidas del dispositivo | las comparten todos los niveles del dispositivo |
| `reports/` | informes de diagnóstico | - |

## Claves JSON

El JSON siempre se escribe compacto, sin sangría. Para leerlo a simple vista, dale formato en un editor de texto

**La longitud de una clave depende de cuántas veces aparece en un nivel:**
- una clave que aparece una vez por archivo se escribe con palabras completas en `snake_case`: `level_id`, `min_generation`
- una clave que se repite miles de veces se acorta a unas pocas letras: `objs`, `f`, `e`, `v`

Las claves ocupan el 52 % de los bytes de un archivo de nivel, así que esto es una regla, no una cuestión de gusto. Todas las claves están declaradas en `Names.cs`

**Un valor polimórfico se escribe como `[tag, data]`.** Una cadena simple es `[0,{"v":"Author"}]`, una localizada es `[1,{"strs":[...]}]`

Los envoltorios de identificadores como `ObjectId` se escriben como un número o una cadena sin más

## Identificadores

**El signo de un identificador entero tiene significado.** `0` siempre significa "sin asignar":

| Identificador | Clave JSON | Positivo | Negativo |
|---|---|---|---|
| `ObjectId` | `id`, y `pid` para el padre | un objeto del nivel | un objeto del juego: `-1` la cámara, `-2` el jugador local, `-3` la raíz de una plantilla de prefab |
| identificadores de recursos | `txid`, `fnid`, `auid`, `byid`, `ttid` | un recurso que viene con el juego | un recurso propio del nivel |
| `AudioId` de una pista de audio | `aid` | una pista de audio de este nivel | no se usa |

Un `pid` igual a `0` significa que el objeto no tiene padre. Los números por debajo de `-3` solo existen mientras el juego se ejecuta y nunca llegan a un archivo

**`Marker`, `Checkpoint` y `BeatSegment` no tienen identificador.** Su dirección es un lugar en el tiempo: para un marcador y un checkpoint es el fotograma `f`, para un segmento de pulso es el primer fotograma de su tramo `sp` (los segmentos no se solapan). Si se mueve un objeto así, su dirección cambia

**Una sobrescritura de prefab nombra un campo por número, no por clave JSON.** Una colocación guarda sus sobrescrituras en la lista `mod`. La `key` de cada sobrescritura contiene tres números:
- `id` - el objeto dentro de la plantilla, no su copia en el nivel
- `f` - el número permanente del campo
- `i` - el elemento de un campo de lista, o `-1` para el campo entero

El número queda ligado al campo para siempre. Cambiar el nombre de la clave JSON de ese campo no rompe las sobrescrituras ya guardadas en los niveles

## La "g" exterior

Cada raíz de serialización va envuelta en un sobre con dos claves:

```json
{"g":2,"v":{"level_id":"18df5f61-3aa4-4812-bf69-d357f2201bc3","vrs":"1.0", ... }}
```

`g` es la generación del modelo (`Names.Generation`), `v` son los datos

Los sobres se anidan. Dentro de `Level`, `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources` y `LevelHints` tienen cada uno su propio sobre. Cómo funcionan las generaciones - [[5_versioning]]

> [!caution] Precaución
> `g` y `vrs` son números distintos. `vrs` es la versión del nivel que pone el autor (`LevelMeta.LevelVersion`) y no tiene nada que ver con el formato. No cambies `g` a mano: un archivo con una `g` mayor que la que conoce la compilación no se lee en absoluto
