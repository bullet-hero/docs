---
title: Fotogramas clave y suavizado
date: 2026-10-12
tags: [level_author]
---

# Fotogramas clave y suavizado

Un fotograma clave es un valor en un fotograma de una pista, más el suavizado con el que se llega a él. Todo lo que en un nivel se mueve, cambia de color o se activa y desactiva es una lista de fotogramas clave

Las ideas básicas - [[3_how-the-editor-thinks]]. Cada campo del inspector de fotogramas clave - [[5_object-properties]]

## Qué se puede animar

Cada pista tiene sus propios fotogramas clave, independientes de los de las demás:

| Propietario | Pistas |
|---|---|
| cualquier objeto | posición, rotación, escala, tamaño, anclas, pivote |
| forma | color, UV |
| texto | color, tamaño de fuente, `{{ui:editor_dummy_text-11}}` (cuánto del texto está escrito), `{{ui:editor_dummy_text-12}}` (cuánto queda oculto tras la máscara) |
| cámara | posición, rotación, zoom, pivote, sacudida |
| nivel | fondo, tema, límite de pantalla, cada uno de los 12 efectos de posprocesado |
| jugador | tamaño, velocidad, visibilidad, control, colisión |

Un fotograma clave de color de una forma también puede ser un degradado sobre el recuadro del objeto. Su campo `{{ui:editor_keyframe-color_layout}}` elige la disposición: `{{ui:enum_color4-x4-key-type_value}}` (un solo color), `{{ui:enum_color4-x4-key-type_vertical}}` (de abajo arriba), `{{ui:enum_color4-x4-key-type_horizontal}}` (de izquierda a derecha) o `{{ui:enum_color4-x4-key-type_bari-centrical}}` (un color en cada esquina)

Un fotograma clave de tamaño de fuente es o un solo número, un tamaño fijo en unidades del mundo, o una banda con `{{ui:field_common_auto-size}}` activado. El texto se dibuja con el `{{ui:field_common_max}}` de la banda y se reduce hacia su `{{ui:field_common_min}}` hasta que cabe en su recuadro

Los fotogramas clave de un objeto se cuentan desde el inicio de su tramo. Así que mover el objeto en el tiempo arrastra con él toda su animación

La posición se fija respecto al padre. Un fotograma clave guarda el valor en sí, no un incremento sobre el fotograma clave anterior

La visibilidad, el control y la colisión del jugador están o activados o desactivados. Esos fotogramas clave no tienen suavizado: no hay nada que mezclar

El primer fotograma clave en una pista vacía del jugador no cambia nada en pantalla: la visibilidad, el control y la colisión empiezan activados, y el tamaño y la velocidad empiezan en los valores habituales del jugador. Con el control desactivado, o con el jugador oculto, el jugador no se puede manejar: el cursor desaparece y ninguna pulsación se registra. A un jugador oculto se le sigue pudiendo golpear: eso solo lo decide la colisión

## Texto: relleno y aparición

Dos pistas de texto ocultan caracteres de formas distintas. Las dos toman una fracción de 0 a 1 y cuentan los caracteres del texto

**`{{ui:editor_dummy_text-11}}`** es la fracción del texto que está escrita: 0 - nada, 1 - todo. Un carácter sin escribir no se dibuja en absoluto, así que la línea se acorta. Una pista vacía escribe todo el texto. Cada fotograma clave fija la dirección:
- `{{ui:enum_text-fill-direction_forward}}` (la predeterminada) - desde el primer carácter, como una máquina de escribir
- `{{ui:enum_text-fill-direction_backward}}` - desde el último carácter
- `{{ui:enum_text-fill-direction_from-center}}` - crece desde el centro
- `{{ui:enum_text-fill-direction_to-center}}` - crece desde los dos extremos y se junta en el centro

**`{{ui:editor_dummy_text-12}}`** es la fracción de caracteres ocultos tras la máscara: 0 - todos visibles, 1 - todos enmascarados. Un carácter oculto conserva su sitio y se dibuja como un carácter de máscara, `{{v:text.appearing-mask-default}}` de forma predeterminada. La máscara es el campo `{{ui:editor_inspector-appearing_mask}}` del objeto de texto, y si tiene varios caracteres, cada carácter oculto toma uno de ellos. Una pista vacía no oculta nada. Cada fotograma clave fija el modo:
- `{{ui:enum_text-appearing-mode_random}}` (el predeterminado) - disperso, pero con la misma dispersión en cada partida. Un carácter oculto en 0,3 sigue oculto en 0,6, así que el texto se revela en lugar de parpadear
- `{{ui:enum_text-appearing-mode_forward}}` - los caracteres ocultos están al final, el texto aparece desde su principio
- `{{ui:enum_text-appearing-mode_backward}}` - los caracteres ocultos están al principio

Para escribir una línea letra a letra, anima `{{ui:editor_dummy_text-11}}` de 0 a 1. Para que surja del ruido, anima `{{ui:editor_dummy_text-12}}` de 1 a 0

## Consejos

- Pon fotogramas clave solo a lo que se mueve. Una pista sin fotogramas clave toma el valor predeterminado
- Para un cambio justo en un pulso, usa `Constant`, por ejemplo para cambiar de tema en el drop
- La rotación no se limita a una vuelta: un fotograma clave a 0 grados y otro a 720 hacen girar el objeto dos veces. En radianes, como los escriben el archivo y el asistente de IA, son 0 y 12,566

## Entre dos fotogramas clave

Antes del primer fotograma clave y después del último, el valor se queda quieto.
Entre dos fotogramas clave, el juego toma la fracción de tiempo transcurrida, la pasa por el suavizado y mezcla los dos valores

La fracción se cuenta en tiempo, no en fotogramas dibujados. Así que la curva es la misma a 30 y a 144 fps

**El suavizado pertenece al fotograma clave posterior del par.** El suavizado de un fotograma clave define el trayecto que llega a él desde el anterior.
Así que el suavizado del primer fotograma clave de una pista nunca se ve. Un fotograma clave nuevo recibe `Linear`

El campo `{{ui:hint_editor_inspector_ease_header}}` abre la ventana `{{ui:editor_search-title_ease}}`, donde cada suavizado se dibuja como su propia curva.
Puedes seleccionar varios fotogramas clave, incluso en pistas distintas, y cambiarlos en un solo paso de deshacer

## 29 suavizados

`Linear` es una línea recta. `Constant` mantiene el valor anterior y salta en el fotograma clave

Los otros 27 son nueve familias de tres: `In`, `Out` e `InOut`. Por ejemplo, `InSine`, `OutSine`, `InOutSine`

| Familia | Forma |
|---|---|
| `Sine` | la curva más suave |
| `Quad`, `Cubic`, `Quart`, `Quint` | potencias 2, 3, 4 y 5 |
| `Expo` | exponencial |
| `Circ` | un cuarto de circunferencia |
| `Back` | se sale del rango y vuelve |
| `Elastic` | oscila alrededor del valor |

`In` empieza despacio y termina rápido. `Out` empieza rápido y se asienta. `InOut` es lento en los dos extremos.
De `Sine` a `Expo`, cada familia es más brusca que la anterior

> [!caution] Precaución
> `Back` y `Elastic` se salen del rango: `Out` se pasa del objetivo, `In` retrocede más allá del inicio. El colisionador se mueve con el objeto. Así que un proyectil que debe detenerse en el borde de una zona segura entra en ella durante unos fotogramas

## Valores aleatorios

Un valor en un fotograma clave no tiene por qué ser un solo número:
- un número: `{{ui:field_common_value}}`, `{{ui:enum_color-type_random-min-max}}`, `{{ui:enum_float-type_random-min-max-step}}`
- un vector (posición, escala y similares): `{{ui:field_common_value}}`, `{{ui:enum_vector-type_random-rect}}`, `{{ui:enum_vector-type_random-rect-step}}`, `{{ui:enum_vector-type_random-circle}}`, `{{ui:enum_color-type_random-lerp}}`, `{{ui:enum_vector-type_random-lerp-step}}`
- un color: `{{ui:field_common_value}}`, `{{ui:editor_events-timeline_track_theme}}`, `{{ui:enum_color-type_random-min-max}}`, `{{ui:enum_color-type_random-lerp}}`

`{{ui:enum_vector-type_random-rect}}` elige cada eje por separado. `{{ui:enum_color-type_random-lerp}}` elige un solo número para todos los ejes, así que el punto cae en la línea entre A y B.
Las variantes con paso redondean el resultado hacia abajo a un múltiplo del paso. Un paso de 0 desactiva la cuadrícula, y el valor se comporta como la variante sin paso.
Después, el fotograma clave se mezcla como cualquier otro

La misma semilla da el mismo nivel. El número aleatorio se calcula a partir de la semilla, el fotograma del fotograma clave, la capa, el fotograma inicial del objeto, la pista y el canal. Más - [[8_determinism]]

A continuación: [[2_rhythm-and-structure|Ritmo y estructura]], [[6_themes|Temas]]
