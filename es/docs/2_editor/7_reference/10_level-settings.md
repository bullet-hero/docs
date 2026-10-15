---
title: Configuración del nivel
date: 2026-10-15
tags: [level_author]
---

# Configuración del nivel

Aquí se fija todo lo que pertenece al propio nivel: duración, fps, semilla, orientación, metadatos, publicación. Desde aquí también se lanza el nivel, se comprueba con las reglas y se restaura desde una copia

## Jugar

Las opciones de lanzamiento valen **solo para esta partida**. Nada de aquí se guarda en el nivel

`{{ui:settings_level-settings_life-text}}`, `{{ui:field_common_speed}}`, `{{ui:settings_level-settings_checkpoints-toggle}}` y el nivel automático te dejan ensayar un fragmento sin editarlo

> [!tip] Consejo
> La `{{ui:settings_level-settings_seed}}` de aquí tiene prioridad sobre la semilla propia del nivel. Es la de mayor prioridad de las tres. Úsala para repetir exactamente la partida que acabas de ver. `0` significa usar la semilla propia del nivel, o una nueva en cada partida

Más - [[3_difficulty-curve]]

## Núcleo

Duración en fotogramas, frecuencia de fotogramas y las dos semillas del nivel

`{{ui:settings_level-settings_core-seed-value}}` es la semilla propia del nivel. Forma parte del contenido, y cambiarla se puede deshacer.
`0` significa "una semilla nueva en cada partida". Es el valor predeterminado, así que un nivel normal se juega distinto cada vez

> [!tip] Consejo
> `{{ui:settings_level-settings_core-runtime-seed-value}}` solo muestra qué semilla salió en esta sesión del editor. `{{ui:settings_level-settings_core-runtime-seed-regenerate}}` elige una nueva solo para la sesión: no se escribe nada y nada entra en el historial de deshacer. Al recargar el nivel, la semilla se resuelve de nuevo

> [!info] Conviene saber
> **Un fotograma es una celda, y el tiempo es un límite.** Los fotogramas se cuentan desde 1. El fotograma *f* cubre el tiempo desde (*f*-1)/fps hasta *f*/fps, sin incluir este último. Un nivel de N fotogramas contiene los fotogramas 1 a N. N+1 es el límite final, no un fotograma

Más - [[4_frames-and-time]]

## Orientación del nivel

En qué orientación se sostiene el dispositivo durante este nivel

`{{ui:enum_level-orientation_horizontal}}` y `{{ui:enum_level-orientation_vertical}}` giran el dispositivo del jugador mientras dura el nivel. Esta elección tiene prioridad sobre la configuración del jugador.
Un monitor no se puede girar. Por eso en escritorio un nivel vertical se juega con barras a los lados, y así es como debe verse

`{{ui:enum_level-orientation_not-specified}}` deja la elección al jugador. No es un valor predeterminado, sino una afirmación sobre tu nivel: se lee bien en **las dos** orientaciones.
El juego no ajusta nada para ello: nada se desplaza, se recorta ni se escala. El contenido más allá de los bordes horizontales queda fuera de la pantalla en una orientación y se ve en la otra.
Elígelo solo después de comprobar el nivel de las dos maneras

## Zona de peligro

Acciones que eliminan o reescriben archivos, no contenido

> [!caution] Precaución
> Los desplegables `{{ui:settings_level-settings_quot-level-quot-file-format}}` y `{{ui:settings_level-settings_quot-metadata-quot-file-format}}` reescriben el nivel y sus metadatos en el disco. Cambiar de formato **elimina el archivo en el formato anterior**. No pasa nada más: no hay recarga ni nueva simulación, y tu selección y tu historial de deshacer se mantienen. Lo que se escribe es exactamente lo que ya está en memoria

> [!caution] Precaución
> `{{ui:settings_level-settings_delete-level-open}}` borra la carpeta del nivel del disco. Esto no se puede deshacer

Más - [[4_not-losing-work]]

## Reglas

Problemas que la validación encontró en este nivel:
- referencias rotas
- ids duplicados
- ciclos de padres
- prefabs anidados a demasiada profundidad
- segmentos de pulso que se solapan

> [!info] Conviene saber
> **Algunas incidencias se pueden reparar, una a una o con `{{ui:settings_level-settings_rules-fix-all}}`.** Las reparaciones van a un borrador: `{{ui:editor_save_text}}` las aplica como una sola operación que se puede deshacer, `{{ui:settings_level-settings_raw-discard}}` las descarta. Las incidencias del grafo (ids, padres, anidamiento de prefabs) no tienen reparación, y es a propósito: cada una es una decisión sobre el contenido que solo tú puedes tomar, y una corrección automática elegiría en silencio una de varias respuestas válidas

> [!tip] Consejo
> Un hijo que sobresale del tramo de su padre **no** se informa. Son datos legales que se comportan como está previsto. Si quieres que los tiempos de vida encajen, ejecuta el modificador `{{ui:mod_span_fit}}` desde los generadores. Mete los hijos dentro o amplía los padres

Más - [[4_not-losing-work]]

## Metadatos

Todo lo que trata del nivel sin ser el nivel: nombre, descripción, portada, licencia, clasificación por edad, dificultad y autores

El nombre y la descripción se escriben por idioma, aquí mismo.
Un jugador cuyo idioma no rellenaste recibe el primero que sí rellenaste

> [!info] Conviene saber
> Aquí no hacen falta claves de traducción. Un nivel es contenido, no parte de la interfaz del juego

La licencia y los autores viajan con el nivel allá donde se comparta. Así se conserva la autoría cuando alguien lo vuelve a subir

`{{ui:settings_level-settings_difficulty}}` muestra un icono grande del grado y un botón con el número guardado y el nombre del grado, por ejemplo `3 · {{ui:enum_difficulty-tier_rain}}`.
El botón abre un menú con todos los grados, cada uno con su número y su icono: `0` es `{{ui:enum_difficulty-tier_undefined}}`, de `1` a `{{v:difficulty.scale-max}}` son los grados de `{{ui:enum_difficulty-tier_auto}}` a `{{ui:enum_difficulty-tier_singularity}}`

El valor por defecto es `{{ui:enum_difficulty-tier_undefined}}`: entonces el jugador no ve ningún icono.
Un moderador que vuelve a publicar el nivel puede sobrescribir el grado. Sigue siendo un solo valor, no dos.
Un valor mayor que `{{v:difficulty.scale-max}}` aparece en el botón con su propio número junto a `{{ui:enum_difficulty-tier_singularity}}` y se queda tal como está escrito hasta que elijas otro grado

Más - [[2_metadata-and-sharing]]

## Etiquetas del nivel

Las etiquetas son tus propias palabras. Se muestran tal como están escritas y nunca se traducen.
El jugador filtra los niveles por ellas en el explorador de niveles

Escribe las etiquetas separadas por comas. Que sean cortas y generales: un género, un ambiente, una mecánica.
Una etiqueta solo ayuda si otros niveles también la usan. Una etiqueta que nadie más va a escribir no filtra nada

## Colecciones

Trae recursos de una colección al nivel, o crea una colección a partir de los recursos propios del nivel. La pestaña está justo después de `{{ui:editor_library_kind-prefabs}}`

- `Importar` - abre una colección, marca entradas y haz clic en `Importar`. Las dependencias vienen con ellas, y toda la importación es un solo paso de deshacer
- `{{ui:editor_collections_mode-build}}` - marca los recursos del nivel y haz clic en `{{ui:editor_collections_build}}`, en `{{ui:editor_collections_target-new}}` o en una de las tuyas

Una entrada que el nivel ya tiene en otra versión abre `{{ui:editor_resource-conflict_title}}`. Nada se sobrescribe en silencio

Más - [[16_library-and-collections]]

## Publicación

El único lugar desde el que un nivel se envía a alguna parte: como archivo comprimido o al Workshop de Steam

`{{ui:editor_share_destination}}` elige el destino. Debajo están los controles propios de ese destino, su informe y el botón que lo ejecuta.
El informe comprueba el nivel por sí solo, sin ningún botón. Los errores bloquean el envío, las advertencias y los consejos no

Más - [[17_publishing]]

## Historial

Cada edición de esta sesión es una fila aquí. Las más recientes arriba, como en un `git log`

La columna de más a la izquierda es la línea principal.
Una columna propia es una rama. Es una línea que dejaste atrás cuando deshiciste una edición y tomaste otro camino

El anillo marca dónde estás. El círculo verde marca el último guardado

Hacer clic en una fila lleva el nivel de vuelta exactamente a ese estado.
El recorrido aplica una operación por fotograma. Así ves cómo cambia el nivel en lugar de esperar ante una pantalla congelada

> [!warning] Advertencia
> Mientras dura un recorrido, el editor es de solo lectura. Puedes mover la cámara y desplazarte por la línea de tiempo, pero no editar. Cancelar detiene el recorrido donde esté, y ese siempre es un estado real del nivel

> [!tip] Consejo
> El historial vive solo en la sesión actual. Nunca se escribe en el disco, y al volver a abrir el nivel empieza de cero. Su tamaño es limitado: primero se van las ramas abandonadas más antiguas, después las ediciones más antiguas

## Datos sin procesar

Todo el modelo guardado del nivel como un árbol de campos. Es el propio archivo, antes de que el editor lo procese

> [!caution] Precaución
> **Aquí no se valida nada.** Es la salida de emergencia para lo que todavía no cubre ninguna otra pantalla. Escribirá un valor que el resto del editor considera imposible

Un punto relleno junto a un campo significa que lo cambiaste en esta sesión.
Un punto hueco significa que cambió algo dentro de él. Sin él, un cambio tres niveles más abajo en una rama contraída sería invisible

El botón `{{ui:settings_level-settings_raw-apply}}` se oculta, no se desactiva, cuando no hay nada que aplicar.
Una aplicación vacía metería en la pila de deshacer un cambio de nivel sin motivo

Más - [[4_not-losing-work]]
