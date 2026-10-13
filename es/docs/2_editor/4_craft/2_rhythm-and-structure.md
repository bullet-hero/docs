---
title: Ritmo y estructura
date: 2026-10-02
tags: [level_author]
---

# Ritmo y estructura

Marca primero la cuadrícula de pulsos: el tempo, luego el desplazamiento, luego los pulsos por compás. Pon el pico del nivel en el pico de la canción, y dale al jugador un respiro en los breaks

Un juego de ritmo se basa en una sola sensación: el jugador no se mueve al ritmo de la música, la toca

## La cuadrícula de pulsos

La cuadrícula de pulsos es para ti, no para el juego. La reproducción no la lee.
La usas para colocar contenido sobre la música, y los generadores trabajan sobre los mismos pulsos

La cuadrícula está hecha de segmentos. **Un segmento es una parte de tempo constante**, y puede haber varios.
Entre segmentos puede haber huecos: una intro sin batería, un break, la cola después de la última nota

Marca solo las partes que llevarán contenido. Una intro normalmente no necesita nada

## Encontrar el tempo

1. Encuentra el tempo
2. Luego el desplazamiento
3. Luego los pulsos por compás

¿No sabes el tempo? Márcalo con toques junto con la canción en la ventana `{{ui:editor_beat-window_title}}` (`Shift+T`).
Redondéalo a un número entero y afínalo con el desplazamiento

Una canción casi siempre está compuesta en un tempo entero. Un valor fraccionario suele significar que lo que está mal es el desplazamiento, no el tempo

## El sonido en movimiento

**Reparte los instrumentos entre distintos tipos de contenido:**
- el bombo - para lo que exige una acción del jugador
- los golpes secundarios - para el movimiento que no exige ninguna acción
- los pads largos y la atmósfera - para el fondo y la cámara

Así el nivel suena con profundidad en lugar de marcar un solo pulso con todo a la vez

**El tamaño de un movimiento transmite la fuerza de un sonido.** Un movimiento pequeño es un golpe débil, uno grande es un golpe fuerte.
Un efecto grande sobre una nota débil se lee como un error de sincronización, aunque los fotogramas sean exactos

**La forma de un movimiento transmite el acento.** Un giro brusco acentúa una nota fuerte, un arco suave acentúa una débil

**En 4/4 los pulsos se ordenan por peso como 1, 3, 2, 4.** Una acción en el primer pulso es la más intuitiva.
La síncopa da groove. Pero una síncopa frecuente o incoherente deja al jugador sin saber dónde está

**Un compás poco común se divide en grupos que el jugador pueda contar.** En 7/4, los grupos 4+4+2+2+2 son más fáciles de seguir que 4+4+4+2

## Estructura

Las secciones son lo que el jugador recuerda.
Un nivel sin ellas son cuatro minutos de lo mismo, aunque cada cinco segundos pase algo nuevo

**La repetición enseña.** Un patrón que vuelve se reconoce y se aprende más rápido. Pero en exceso aburre, y romper sin motivo un patrón ya establecido se lee como descuido, no como variedad

> [!tip] Recomendación
> Coloca marcadores en la estructura de la canción antes de poner el primer objeto: intro, estrofa, estribillo, break, drop, outro. Se ven en todas las líneas de tiempo y no cuestan nada

> [!caution] Precaución
> El pico del nivel tiene que caer en el pico de la canción, y las pausas son obligatorias. Un break es donde el jugador respira. Un nivel sin pausas agota antes de volverse difícil

El final también hay que pensarlo: o un pico final o un desvanecimiento tranquilo. Un nivel no debería cortarse sin más

## Por qué segmentos y no fotogramas clave

La cuadrícula de pulsos es una lista de partes, no una pista de fotogramas clave.
Una pista de fotogramas clave no puede expresar una ausencia: su último fotograma clave se extendería hasta el final del nivel. Y los segmentos necesitan huecos entre ellos

A continuación: [[4_frames-and-time|Fotogramas, tiempo y duración del nivel]], [[3_difficulty-curve|La dificultad y la curva]]
