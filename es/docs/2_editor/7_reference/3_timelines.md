---
title: Líneas de tiempo
date: 2026-10-02
tags: [level_author]
---

# Líneas de tiempo

Las líneas de tiempo muestran el nivel a lo largo del tiempo: los objetos, los fotogramas clave del objeto seleccionado, la plantilla de un prefab, el audio y los eventos. La cuadrícula de pulsos te ayuda a colocar todo eso sobre la música

## Línea de tiempo del nivel

Muestra todos los objetos del nivel a lo largo del tiempo. Cada objeto es un clip. El carril en el que está un clip es la **capa** del objeto

Un clip es un **tramo** semiabierto. Un objeto en los fotogramas 10-19 termina justo donde empieza un objeto que arranca en el fotograma 20. Nunca se dibujan los dos en un fotograma compartido

> [!info] Conviene saber
> El tramo de un hijo debe estar dentro del de su padre. Eso **se resuelve al leer y nunca se guarda**. Encoge el padre y los hijos se recortan, pero sus valores no cambian. Vuelve a estirarlo y todo regresa. Un objeto raíz más allá del final del nivel son datos válidos, simplemente no se reproduce

> [!tip] Consejo
> En la tira de botones hay cuatro herramientas: `{{ui:editor_timeline-tool-selection_tooltip}}` selecciona y mueve, `Bordes` arrastra un borde, `Tijeras` corta el clip bajo el cursor, `Selección rectangular` añade a la selección cada clip que toque el rectángulo arrastrado. El menú se abre con clic derecho en un *espacio vacío*. Pulsar sobre un clip empieza un arrastre

Una colocación de prefab y los objetos que trae se dibujan en el color del prefab

Cómo tratan las herramientas una colocación:
- Su longitud viene de la plantilla de forma predeterminada. Una longitud distinta en una colocación se guarda como sobrescritura solo de esa colocación
- Si arrastras su borde inicial con `Bordes`, el punto desde el que lee la plantilla se mueve con él. Así la imagen de dentro se queda donde estaba
- `Tijeras` la corta en dos colocaciones de la misma plantilla, y cada una reproduce su propia parte. La plantilla en sí no cambia
- Los objetos que trajo una colocación no se pueden cortar. Corta la colocación en sí, o corta esos objetos en el modo prefab

Más: [[3_how-the-editor-thinks|Cómo funciona el editor]], [[4_composition-and-camera|La composición y la cámara]]

## Línea de tiempo local

Muestra los fotogramas clave del **objeto seleccionado**. Cada propiedad animable tiene su propia pista: posición, rotación, escala, tamaño, anclas, pivote, color, UV, tamaño de fuente

Aquí los fotogramas se cuentan **desde el inicio del tramo del objeto**. Mueve el objeto y toda su animación se mueve con él

> [!info] Conviene saber
> **Una pista vacía son datos válidos**, no un hueco. Una pista sin fotogramas clave toma el valor predeterminado. Por eso un objeto nuevo no anima nada hasta que colocas un fotograma clave

Un valor solo se mezcla entre fotogramas clave vecinos. El tramo decide qué fotogramas existen, pero no cómo se mezclan los valores

En un objeto que viene de un prefab, una pista que aún coincide con la plantilla se dibuja en el color del prefab. Añade, mueve o edita un fotograma clave en ella y el color desaparece: la pista ahora guarda una sobrescritura

En el modo prefab, con la raíz de la plantilla seleccionada, esta línea de tiempo dura lo que toda la plantilla

Más: [[3_how-the-editor-thinks|Cómo funciona el editor]]

## Línea de tiempo del prefab

La línea de tiempo propia del modo prefab. Muestra los objetos de la **plantilla**

> [!info] Conviene saber
> Su longitud es la longitud propia de la plantilla, no el tramo de una de sus colocaciones. Una plantilla se edita como un pequeño nivel independiente. Se puede colocar muchas veces y en momentos distintos

Una fila es la **raíz** de la plantilla, y dura toda la plantilla. Todos los demás objetos de la plantilla cuelgan de ella:
- la fila de la raíz se puede seleccionar. Entonces el inspector y la línea de tiempo local muestran la raíz
- no se puede arrastrar, estirar ni cortar
- se contrae como cualquier padre. Una raíz contraída oculta toda la plantilla en esta línea de tiempo

> [!warning] Advertencia
> La selección no se comparte con el resto del editor. No hay vista previa en vivo de una colocación concreta. Los cambios modifican la plantilla y se extienden a todas las colocaciones que la referencian

Más: [[2_reuse|Reutilizar: prefabs, copia, generadores]]

## Línea de tiempo de audio

Muestra las pistas de audio del nivel con su forma de onda. Así es fácil alinear el contenido con lo que se oye

> [!tip] Consejo
> `{{ui:editor_inspector-audio-span_fit}}` en el inspector encaja la pista con la longitud real del clip. El botón no está disponible si no hay clip o la velocidad es 0: una pista congelada no tiene longitud
> `{{ui:editor_inspector-audio-span_fit-level}}` además alarga el nivel hasta que cabe el clip entero. Los dos botones piden confirmación antes

> [!caution] Precaución
> El control deslizante `{{ui:editor_inspector-audio_volume}}` del inspector es el fader de la pista. El volumen con fotogramas clave es una pista Volume aparte en la línea de tiempo local. En la reproducción los dos se multiplican

Más: [[2_preparing-the-track|Preparar la pista]]

## Línea de tiempo de eventos

Muestra los fotogramas clave del nivel que no pertenecen a ningún objeto:
- posición, rotación, zoom, pivote y sacudida de la cámara
- marcadores y checkpoints
- el límite de pantalla
- el fondo y el tema
- todos los efectos de posprocesado
- la visibilidad, el control, la colisión, el tamaño y la velocidad del jugador

> [!info] Conviene saber
> La pista **Beat** es aquí la excepción. Sus elementos tienen tramo, y es la única pista sobre la que actúan `Bordes` y `Tijeras`

> [!tip] Consejo
> Un color puede referirse al tema del nivel en lugar de a un valor fijo. Entonces cambiar el tema recolorea de una vez todo lo que se refiere a él

Más: [[4_composition-and-camera|La composición y la cámara]], [[6_themes]]

## Cuadrícula de pulsos

Te ayuda a colocar el contenido sobre la música. Los generadores trabajan sobre los mismos pulsos que ves

Son metadatos de autoría, no una mecánica. **La reproducción no lee la cuadrícula**

La cuadrícula es una lista de **segmentos**. Cada uno tiene un tempo constante: BPM, desplazamiento de fase, pulsos por compás.
Los segmentos no se solapan. Los huecos entre ellos hacen falta: una intro sin batería, un break, la cola después de la canción. Una única pista de tempo no podría expresarlo

> [!tip] Consejo
> `TAP` registra toques en el cabezal. `{{ui:editor_beat-tap_commit}}` los convierte en un segmento que va del primer toque al último. Los pulsos siempre se cuentan desde el inicio del segmento y no se acumulan, así que el error es de menos de medio fotograma

Más: [[2_rhythm-and-structure|Ritmo y estructura]]

## Segmento de pulso

Una parte de tempo constante: BPM, desplazamiento de fase en fotogramas fraccionarios, pulsos por compás, un nombre y un color

Se muestra exactamente un segmento, aunque haya varios seleccionados. Todos los campos menos el nombre son únicos de cada segmento. Editarlos a la vez los fundiría unos con otros

> [!caution] Precaución
> Un segmento se identifica por su fotograma inicial. Por eso **moverlo cambia su identidad**. Después de moverlo, vuelve a seleccionar el segmento en su nuevo inicio

> [!tip] Consejo
> Aquí los toques recalculan la fase del segmento seleccionado en lugar de crear uno nuevo. El BPM y el desplazamiento cambian en un solo paso de deshacer

Más: [[2_rhythm-and-structure|Ritmo y estructura]]
