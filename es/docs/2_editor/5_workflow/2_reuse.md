---
title: "Reutilización: prefabs, copia, generadores"
date: 2026-10-02
tags: [level_author]
---

# Reutilización: prefabs, copia, generadores

Los objetos que más tarde tendrás que cambiar todos a la vez forman un prefab, sean cuantos sean. El contenido que se puede describir con una regla es un generador. En cualquier otro caso, simplemente copia

Un generador vale la pena incluso para ocho objetos: una ejecución de un generador es una sola operación que deshacer.
Ocho objetos colocados a mano son ocho ocasiones de fallar con alguno

## Copiar

Para una forma que necesitas repetir unas cuantas veces y que ya no tiene que estar vinculada al original

Hay cinco búferes de portapapeles, uno por línea de tiempo. Los clips copiados en una línea de tiempo no se pegan sobre los fotogramas clave de otra

Copiar y pegar se dirigen de forma distinta:
- **Pegar** siempre va a la línea de tiempo que estás mirando
- **Copiar** toma lo que está seleccionado. Gana la línea de tiempo abierta si tiene una selección propia. Si no, se copia la selección esté donde esté, así que un objeto seleccionado con la línea de tiempo local abierta se copia igualmente

Duplicar (`Ctrl+D`) no escribe en ningún búfer. Lo que copiaste antes no se pierde

Duplicar y pegar tratan el padre de forma distinta:
- **Un duplicado** conserva el padre. La copia queda junto al original en la jerarquía
- **Pegar** descarta el padre, y los objetos pegados acaban en lo más alto de la jerarquía. La excepción es un padre `{{ui:editor_search-option_camera}}` o `{{ui:editor_search-option_local-player}}`: en el ámbito del nivel sobrevive al pegado

Los dos buscan una capa libre solo en los fotogramas en los que cae cada objeto copiado. Pegar en una zona vacía de la línea de tiempo conserva las capas que tenían los objetos

El nombre de una copia se renumera. Un sufijo de `_` y dígitos es el id del objeto, así que `Shape_12` pasa a ser `Shape_` con un id nuevo. Un nombre sin ese sufijo no lo recibe, y un sufijo que no es solo de dígitos (`Wave_2b`) se queda como está. Las pistas de audio se renombran igual

Los objetos copiados en el modo prefab se pegan de vuelta en la plantilla, no en el nivel

> [!caution] Precaución
> Los búferes se vacían al cargar un nivel. Todos los ids y fotogramas que contienen pertenecen al nivel que estaba abierto

## Prefabs

Para algo que necesitas muchas veces y quieres cambiar en todas partes a la vez

Un prefab es una plantilla y sus colocaciones. Cuando le das una plantilla a una colocación, la colocación recibe copias reales de sus objetos con ids permanentes. El archivo del nivel guarda solo la colocación en sí: la plantilla, los ids de las copias y tus sobrescrituras. Las copias se reconstruyen a partir de la plantilla cada vez que se carga el nivel

Una edición de la plantilla se extiende a todas las colocaciones que hacen referencia a ella.
Una edición de una copia en una colocación (fuera de la edición de la plantilla) se registra como sobrescritura solo de esa instancia.
Las sobrescrituras sobreviven a las ediciones posteriores de la plantilla. Por eso un prefab sirve también para variaciones, no solo para clones

Los prefabs se pueden anidar unos dentro de otros. Una plantilla anidada se puede editar desde dentro de otra: las plantillas se abren una encima de otra y se cierran en orden inverso

### Un prefab a partir de una selección

Selecciona objetos y pulsa `Ctrl+G` (`{{ui:cmd_editor_pack-prefab}}`). La misma acción está también:
- en la paleta de comandos
- en el menú contextual de la vista, mientras haya algo seleccionado
- en el menú de una fila de la jerarquía, como `{{ui:editor_context-menu_pack-prefab}}`
- en la configuración del nivel, pestaña `{{ui:editor_library_kind-prefabs}}`, `{{ui:settings_level-settings_resources-prefabs-pack}}`

Los objetos seleccionados pasan a una plantilla nueva, una colocación de ella ocupa su lugar y esa colocación queda seleccionada. Es una sola operación que deshacer.
Un solo objeto da su nombre a la plantilla. Varios objetos dan una plantilla llamada `Prefab`

Una colocación y un objeto que le pertenece no se pueden empaquetar otra vez. Sus menús ofrecen en su lugar `{{ui:editor_context-menu_open-prefab}}`, y se abre su plantilla.
En el modo prefab no se puede empaquetar

## Generadores y modificadores

**Los generadores** crean contenido según una regla: una espiral, una cuadrícula, un fractal, una onda, una lluvia de balas, un abanico de rayos. Fijas una ventana de fotogramas, una capa y una semilla, y obtienes objetos. La estimación del resultado se ve antes de confirmar nada

**Los modificadores** funcionan igual, pero con lo que ya existe: encajan tramos, los separan, cuantizan fotogramas clave, recalculan la frecuencia de fotogramas, eliminan el contenido de una ventana

## Entre niveles: las bibliotecas compartidas del dispositivo

Todo lo anterior funciona dentro de un nivel. De un nivel a otro solo pasan las bibliotecas compartidas del dispositivo y las colecciones

Los temas, efectos, formas y prefabs se exportan desde un nivel y se importan en otro.
Las bibliotecas están junto a la carpeta de niveles, así que un nivel que envías lleva su propia copia

Una colección guarda recursos de cualquiera de siete tipos, texturas, fuentes y audio incluidos, y viaja como archivo comprimido o a través de Steam Workshop. Más - [[16_library-and-collections]]

A continuación: [[3_speed-and-shortcuts|Velocidad y atajos]], [[4_level-folder-and-backups|La carpeta del nivel y las copias de seguridad]]
