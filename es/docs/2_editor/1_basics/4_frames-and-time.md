---
title: "Fotogramas, tiempo y duración de un nivel"
date: 2026-10-12
tags: [level_author]
---

# Fotogramas, tiempo y duración de un nivel

Un nivel cuenta el tiempo en sus propios fotogramas, no en los de la pantalla, así que se juega igual en cualquier equipo. La duración del nivel la fijas tú, y los fps conviene dejarlos en el valor predeterminado, 60

## Fotogramas del nivel y fotogramas de la pantalla

Un fotograma del nivel no tiene nada que ver con un fotograma de la pantalla.
La pantalla dibuja tantos fotogramas por segundo como el equipo pueda. Un nivel cuenta el tiempo en sus propios fotogramas, y cuántos hay por segundo se guarda en el propio nivel. El valor predeterminado es `60`

Así que un nivel se juega igual a 60 Hz, a 144 Hz y en un teléfono que ha bajado a 30. La precisión de los impactos no depende de la tarjeta gráfica

Un fotograma es una celda, no un instante. Si un objeto termina en el fotograma 100 y otro empieza en el fotograma 100, no se solapan

Con más precisión: los fotogramas cuentan desde 1, y el fotograma f cubre el tiempo de (f-1)/fps a f/fps, con el borde izquierdo incluido y el derecho no. Así que el fotograma 1 empieza justo al principio de la canción

## La duración de un nivel

La duración del nivel la fijas tú. La de la canción sale del archivo. No tienen por qué coincidir

Se permite contenido más allá del final del nivel. Simplemente nunca se reproduce, y la validación no lo señala. Un objeto puede pasar del final, pero el asistente de IA no puede crear uno que empiece después de él

Con un hijo que sobresale del tramo de su padre pasa lo mismo. El nivel guarda lo que escribiste, y el tiempo de vida efectivo se calcula por separado

Para encajar entre sí los tiempos de vida de hijos y padres, usa el modificador `{{ui:mod_span_fit}}` en `{{ui:editor_generators_text}}`. O mete a los hijos dentro o ensancha a los padres

## Los fps del nivel

Cuantos más fps, con más precisión caes en el pulso. Y más fotogramas ocupa la misma duración.
El rango es de 1 a 1000, el valor predeterminado es `60`

> [!tip] Recomendación
> Deja los fps en el valor predeterminado. A 60 el oído no distingue un desplazamiento de un fotograma, y el número de fotogramas clave crece con los fps

La línea de tiempo está limitada a `1000000` fotogramas. Son unas 4,6 horas a 60 fps y unos 17 minutos a 1000

> [!warning] Advertencia
> Cambiar los fps de un nivel terminado implica recalcular todos sus fotogramas clave. Lo hace el modificador `{{ui:mod_framerate_remap}}`, hacerlo a mano no es realista

A continuación: [[5_keyframes-and-easing]], [[2_rhythm-and-structure]], [[1_order-of-work]]
