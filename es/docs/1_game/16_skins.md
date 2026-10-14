---
title: Skins
date: 2026-10-15
tags: [player, advanced_player]
---

# Skins

El cuerpo del avatar es una cuadrícula de celdas, y la skin decide qué dibuja cada celda: una forma y uno de los colores de la skin. Una skin también puede apagar los ojos, las manos, la sombra y los efectos. Arma una en el menú principal, en `{{ui:menu_main_avatar-btn}}`, con formas listas, una paleta y un editor de cuadrícula, o escribe el archivo a mano

Una skin cambia solo el aspecto. La hitbox, la velocidad y el anillo de la hitbox son iguales para todas las skins

## El hub del avatar

`{{ui:menu_main_avatar-btn}}` en el menú principal abre una pantalla propia. Tu avatar camina a la izquierda y el panel ocupa la mitad derecha. `{{ui:menu_avatar_bot}}` abajo a la izquierda te pasa el avatar, para que pruebes la skin en movimiento, y el control `{{ui:menu_avatar_damage}}` a su lado muestra cómo la skin pierde celdas al bajar la salud. La barra de arriba del panel salta a cada sección:

| Sección | Qué hace |
|---|---|
| `{{ui:menu_avatar_tab-shapes}}` | formas listas, dibujadas con los ojos y las manos que traen. Un clic pone la forma en tu skin y conserva tus colores. Las formas redondas y poligonales traen ojos, las de patrón no. La primera tarjeta es el avatar clásico: se pone entero, con sus colores |
| `{{ui:menu_avatar_tab-colors}}` | los colores del cuerpo y los ojos. Elige un objetivo y luego un color. Las manos, los rastros y el tono del dash siguen tus colores solos |
| `{{ui:menu_avatar_elements}}` | cada botón activa o desactiva una parte del avatar |
| `{{ui:menu_avatar_editor}}` | la cuadrícula en sí: su tamaño, las piezas de sus celdas, la forma, el color, la rotación, el reflejo y la escala de cada pieza, y formas propias |

`{{ui:menu_avatar_randomize}}` arriba a la derecha le da a tu skin una forma y unos colores al azar. Está desactivado mientras llevas el avatar clásico. `{{ui:menu_avatar_tab-skins}}`, a su lado, lista tus archivos de skin: un clic en uno te lo pone, y los botones exportan, eliminan, importan y duplican. `{{ui:menu_avatar_create}}` crea una skin nueva a partir de una forma al azar con colores al azar. Un archivo que el juego no puede leer se puede eliminar desde ahí de todos modos

Cada cambio se guarda al instante. El primer cambio sobre el avatar clásico crea un archivo de skin nuevo, y desde entonces llevas ese archivo

### El editor

1. `{{ui:menu_avatar_paint}}` pone la pieza seleccionada en una celda, `{{ui:menu_avatar_erase}}` la vacía. Arrastra por la cuadrícula para cambiar varias celdas a la vez
2. `{{ui:menu_avatar_pieces}}` lista lo que pueden dibujar las celdas. `+` copia la pieza seleccionada, `-` la quita y sus celdas toman la primera pieza
3. La pieza seleccionada toma una forma integrada o una de las formas propias de la skin. `{{ui:menu_avatar_new-mesh}}` dibuja una nueva: coloca puntos y luego une tres de ellos en un triángulo
4. `{{ui:menu_avatar_columns}}` y `{{ui:menu_avatar_rows}}` cambian el tamaño de la cuadrícula. Las celdas son cuadradas, así que una cuadrícula más alta que ancha da un cuerpo alto
5. `{{ui:menu_avatar_rotate-left}}` y `{{ui:menu_avatar_rotate-right}}` giran toda la skin un cuarto de vuelta: la cuadrícula y cada pieza con ella

La parte de arriba de una skin es su frente: el avatar gira para que apunte hacia donde se mueve

Un cambio que rompe el cuerpo - muy pocas celdas o celdas en dos trozos - no se guarda. El motivo se muestra bajo la cuadrícula hasta que lo corrijas

## Dónde se guardan las skins

En la carpeta `skins` dentro de la carpeta de datos ([[1_installation]]). Una skin es un archivo `.json`. `selection.json` a su lado recuerda qué skin llevas

- en un PC, `{{ui:menu_avatar_open-folder}}` abre la carpeta
- en un teléfono, usa `{{ui:menu_avatar_import}}` y `{{ui:menu_avatar_export}}`: abren el selector de archivos del sistema

Las skins viajan con la transferencia de perfil y con Steam Cloud - [[14_profile-transfer]]

## El archivo

Así es una skin exportada, abreviada:

```json
{"g":3,"v":{
  "id":"9b2f0d64-1c3a-4e8b-8f21-6a0c5d7e9f13",
  "name":"Hex knight",
  "size":1.0,
  "columns":5,"rows":5,
  "mask":60651675406,
  "cells":[0,0,0,0,1,1,1,0,0,1,2,1,0,0,1,1,1,0,0,0,0],
  "parts":[
    {"shape":"00000000-0000-0000-0000-000000016000","color":0},
    {"shape":"00000000-0000-0000-0000-000000001000","color":1,"scale":0.9},
    {"shape":"4d1f6c2a-7b3e-4f10-9a55-2c8e01b7d001","color":2,"rotation":90.0,"mirror":true}
  ],
  "colors":[[0,{"r":0.51,"g":0.76,"b":0.96,"a":1.0}],[0,{"r":0.2,"g":0.4,"b":0.9,"a":1.0}],[0,{"r":1.0,"g":1.0,"b":1.0,"a":1.0}]],
  "meshes":[{"id":"4d1f6c2a-7b3e-4f10-9a55-2c8e01b7d001","vts":[[0,{"x":-0.5,"y":-0.5}],[0,{"x":0.5,"y":-0.5}],[0,{"x":0.0,"y":0.5}]],"idxs":[0,1,2]}],
  "elements":125
}}
```

`g` es la generación del formato del archivo, `v` contiene la skin. Lo más fácil es exportar una skin y editar la copia

| Clave | Qué es |
|---|---|
| `id` | quién es la skin: un GUID propio. El juego nombra el archivo según él, pero encuentra una skin por esta clave, así que el nombre del archivo no importa |
| `name` | el nombre que se ve en la lista |
| `size` | qué tan grande se dibuja el cuerpo, de `{{v:skin.size-min}}` a `{{v:skin.size-max}}` del clásico. La hitbox no cambia |
| `columns`, `rows` | el ancho y el alto de la cuadrícula, de `{{v:skin.grid-min}}` a `{{v:skin.grid-max}}`. Las celdas son cuadradas: el lado más largo abarca todo el cuerpo |
| `mask` | qué celdas están llenas, como un único número de 64 bits: la celda de la columna `x` y la fila `y` es el bit `y * 8 + x`, con la fila 0 abajo. La fila siempre mide 8 bits, diga lo que diga `columns` |
| `cells` | la pieza que dibuja cada celda llena, un índice en `parts`, en el orden de los bits desde el más bajo. Si lo dejas vacío, todas las celdas dibujan la pieza 0 |
| `parts` | qué dibuja una celda: `shape` (el id de una forma integrada o el `id` de una de las `meshes` de la skin), `color` (un índice en `colors`), `rotation` (grados), `mirror` y `scale` (de `{{v:skin.part-scale-min}}` a `{{v:skin.part-scale-max}}` de la celda) |
| `colors` | los colores del cuerpo, de 1 a `{{v:skin.colors-max}}`. Un color se escribe `[0,{"r":…,"g":…,"b":…,"a":…}]`, cada canal de 0 a 1 |
| `meshes` | hasta `{{v:skin.meshes-max}}` formas propias de la skin: un `id` (cualquier GUID que no sea el de una forma integrada), puntos `vts` dentro de la caja de -0.5 a 0.5 y triángulos `idxs`, de tres puntos cada uno |
| `elements` | qué partes del avatar se dibujan, como la suma de: ojos 1, manos 2, sombra 4, estela 8, estela del dash 16, destello de golpe 32, tono del dash 64. 127 dibuja todo, una skin nueva empieza en 125: todo menos las manos. La cuadrícula siempre se dibuja |
| `eyes`, `hands`, `shadow`, `move_effect`, `dash_effect`, `damage_effect`, `dash_body` | los colores del resto del avatar, en la misma forma que `colors`. Una parte apagada en `elements` conserva su color |

Una clave que omitas toma el valor del avatar clásico. El id de una forma integrada es más fácil de copiar de una skin exportada: los presets con patrón de `{{ui:menu_avatar_tab-shapes}}` usan solo formas integradas. Un archivo escrito a mano puede omitir `id` - `{{ui:menu_avatar_import}}` le da uno

## Lo que debe cumplir una skin

- `columns` y `rows` van de `{{v:skin.grid-min}}` a `{{v:skin.grid-max}}`, y `mask` no llena ninguna celda fuera de ellas
- al menos `{{v:skin.filled-min}}` celdas están llenas, y todas se tocan por un lado: el cuerpo es una sola pieza
- `cells` está vacío o tiene exactamente una pieza por cada celda llena
- como máximo `{{v:skin.parts-max}}` piezas, y la forma y el color de cada pieza existen
- el cuerpo y la sombra se dibujan con una opacidad de al menos `{{v:skin.body-alpha-min}}`

Una skin que rompe una regla aparece en gris en `{{ui:menu_avatar_tab-skins}}` con el motivo, y no se puede poner. Lo mismo pasa con un segundo archivo con el mismo `id`. Si se rompe la skin que llevas, se dibuja el avatar clásico y tu elección se conserva. Una skin escrita por una versión más reciente del juego dice `{{ui:menu_avatar_newer}}`

## Salud

La salud la muestran solo las celdas llenas. Las celdas perdidas quedan como fantasmas oscuros, del borde hacia el centro, y la última celda aguanta mientras quede algo de salud. Con menos celdas llenas, cada una vale más salud - [[7_damage]]
