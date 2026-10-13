---
title: Cómo funciona el editor
date: 2026-10-12
tags: [level_author]
---

# Cómo funciona el editor

Objeto, fotograma, tramo, capa, padre, fotograma clave - las seis ideas sobre las que se apoya todo el editor

Cuando estas seis ideas están claras, el resto del editor se entiende solo:

| Idea | En resumen |
|---|---|
| Objeto | una forma (lo que ves) y un colisionador (lo que golpea), dos campos separados |
| Fotograma | una celda de tiempo, no un instante |
| Tramo | la vida de un objeto: un inicio y una duración, sin incluir el final |
| Capa | orden de dibujo, se suma a las capas de todos los padres |
| Padre | transmite a sus hijos su transformación, su estado activo y su tiempo de vida |
| Fotograma clave | el valor de un campo en un fotograma, el juego lleva el valor de un fotograma clave a otro por sí solo |

Una palabra desconocida - [[1_glossary]]

## Objeto

Un objeto es lo que se dibuja y lo que golpea. Son dos campos distintos: una forma (lo que ves) y un colisionador (lo que golpea).
Un rayo que brilla pero nunca te toca es un objeto con forma y sin colisionador. Un muro invisible es lo contrario

## Fotograma y tramo

Un fotograma es una celda de tiempo, no un instante. El fotograma 30 ocupa un intervalo, no un punto.
La línea de tiempo cuenta desde uno. Un nivel de 900 fotogramas contiene los fotogramas del 1 al 900. El número 901 es el límite final, no un fotograma

Un tramo es la vida de un objeto: un inicio y una duración. El final no forma parte del tramo.
Así que dos objetos colocados uno tras otro no se solapan en un fotograma compartido

Más - [[4_frames-and-time]]

## Capa y padre

Una capa es el orden de dibujo. Es relativa: la capa de un objeto se suma a las capas de todos sus padres

Una capa más alta se dibuja delante. De dos formas en la misma capa resultante, la más nueva (la de id más alto) se dibuja detrás. Así que a la forma que tiene que quedar encima se le da una capa más alta

> [!caution] Precaución
> Arrastrar un objeto bajo otro padre cambia su orden de dibujo aunque no hayas tocado el número

Un padre transmite a sus hijos su transformación, su estado activo y su tiempo de vida.
El tramo de un hijo tiene que estar dentro del tramo de su padre

El editor nunca recorta lo que escribiste. Guarda tu valor y calcula el efectivo por separado.
Por eso encoger un padre es reversible: vuelve a ensancharlo y el hijo regresa

## Fotograma clave

Un fotograma clave es el valor de un campo en un fotograma. El juego lleva el valor de un fotograma clave al siguiente por sí solo.
Cada campo tiene su propio conjunto de fotogramas clave: posición, rotación, escala, tamaño, anclas y pivote

> [!info] Conviene saber
> Un campo sin fotogramas clave no está roto, toma el valor predeterminado. No hace falta poner fotogramas clave en todo solo por tenerlo ordenado

Qué guarda un fotograma clave y cómo viaja el valor entre fotogramas clave - [[5_keyframes-and-easing]]

## Coordenadas

Las posiciones, los tamaños y las distancias van en unidades del mundo. El punto (0, 0) es el centro de la pantalla mientras la cámara no tenga fotogramas clave propios. La x crece hacia la derecha, la y crece hacia arriba

El zoom de la cámara es la altura del área visible en unidades, {{v:camera.default-height}} de forma predeterminada. Así que una pantalla 16:9 muestra x desde unos -{{v:camera.default-half-width}} hasta {{v:camera.default-half-width}} e y desde -{{v:camera.default-half-height}} hasta {{v:camera.default-half-height}}. Una pantalla más ancha o más estrecha solo cambia el ancho

Un fotograma clave de posición es relativo al padre. Es el desplazamiento del pivote del objeto respecto al punto de anclaje del padre, y gira y escala junto con el padre. Un objeto sin padre se coloca en coordenadas del mundo. Un hijo de la cámara se mueve con la cámara

- **pivote** - el punto del recuadro propio del objeto que la posición coloca y alrededor del cual actúan la rotación y la escala. `(0.5, 0.5)`, el centro, de forma predeterminada
- **anclas** - el punto del recuadro del padre desde el que se cuenta la posición, de `(0, 0)` (abajo a la izquierda) a `(1, 1)` (arriba a la derecha). El centro de forma predeterminada. Dos anclas distintas estiran al hijo junto con el padre

La rotación gira en sentido antihorario. El archivo la guarda en radianes, y el asistente de IA también escribe radianes. El inspector muestra grados de forma predeterminada, y la opción del editor `{{ui:settings_game-editor_interface-rotation-unit}}` lo cambia a radianes

A continuación: [[4_frames-and-time]], [[5_keyframes-and-easing]], [[1_readability-and-fairness]]
