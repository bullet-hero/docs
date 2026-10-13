---
title: Legibilidad y justicia
date: 2026-10-01
tags: [level_author]
---

# Legibilidad y justicia

El jugador tiene que entender qué lo mató. Muestra un peligro antes de que sea peligroso, da al menos 12 fotogramas para reaccionar y haz que el peligro destaque más que la decoración

Hay una sola prueba de justicia: **al morir, ¿el jugador se culpa a sí mismo o al nivel?**
Todo lo que hay en esta página empuja la respuesta hacia "a sí mismo"

## Aviso previo

Un peligro tiene que verse antes de volverse peligroso

La forma y el colisionador son dos campos separados de un mismo objeto.
Así que avisar es sencillo: un rayo con forma y sin colisionador brilla y no golpea. Medio segundo después aparece otro a su lado, esta vez con colisionador

Lo contrario también es válido: un muro invisible es un objeto sin forma pero con un colisionador real

> [!caution] Precaución
> Un peligro invisible es justo solo en un caso: el jugador ya sabe que está ahí, porque el nivel se lo mostró antes

## Tiempo de reacción

Una persona nota un peligro y reacciona en unos 0.2-0.25 segundos en el mejor de los casos.
A 60 fotogramas de nivel por segundo, eso son 12-15 fotogramas

Un peligro que aparece menos de 12 fotogramas antes del contacto (10, por ejemplo) no se puede superar a la primera. Solo se puede aprender.
Cuándo es aceptable - [[3_difficulty-curve#Memorización]]

## Contraste

Lo peligroso tiene que distinguirse del fondo más que la decoración.
El fallo más común es un proyectil oscuro sobre un fondo oscuro, justo en el momento en que el fondo también está cambiando

> [!tip] Recomendación
> Toma del tema tanto los colores del fondo como los de los proyectiles. Así una sola edición del tema mantiene el contraste en todas partes. Los colores escritos a mano lo mantienen solo hasta la primera edición

## Un peligro, un aspecto

Cada tipo de peligro necesita su propio aspecto reconocible, y su propio sonido si usas sonido. Una vez que el jugador aprendió que algo así golpea, todo lo que se vea igual también tiene que golpear

No contradigas tus propias señales. Si algo que parece decoración mata en un sitio, el jugador deja de fiarse de todo lo que parece decoración

## La estructura gana a la densidad

Una pantalla llena de movimiento se lee como ruido, no como dificultad.
Un jugador no distingue 40 proyectiles. Distingue un muro con un hueco, una ola, una espiral, un pasillo

Ocho objetos con estructura son más difíciles y más justos que cuarenta sin ella

## Un nivel siempre se juega igual

Un nivel no tiene condiciones, contadores ni disparadores que reaccionen al jugador. Todo está escrito en la línea de tiempo.
La aleatoriedad tampoco cambia: el mismo punto da los mismos números en cualquier dispositivo

Por eso un nivel no puede ser reactivo. Pero tampoco puede volverse injusto por accidente, solo a propósito

Entre partidas solo cambia lo que elige el jugador: las vidas, la velocidad de reproducción y los checkpoints.
Más - [[3_difficulty-curve#Lo que elige el jugador]]

A continuación: [[3_difficulty-curve|La dificultad y la curva]], [[5_color-and-postprocessing|Color, temas y posprocesado]]
