---
title: Determinismo
date: 2026-10-02
tags: [advanced_player]
---

# Determinismo

Un nivel con la misma semilla se juega igual en cualquier dispositivo y a cualquier frecuencia de fotogramas. Su aleatoriedad se calcula a partir de la semilla, y tus acciones no afectan al nivel

## Un nivel es una función del tiempo

Un nivel se construye sobre una línea de tiempo. Cada objeto vive en un tramo de fotogramas y se mueve a lo largo de fotogramas clave

El nivel no lee tus acciones. Por eso el fotograma 1200 se ve igual tanto si sigues con vida como si has muerto, si estás en pleno dash o si un bot juega por ti

La influencia va en un solo sentido. Un nivel puede cambiar el tamaño del avatar, ralentizarlo, quitarle el control o desactivar las colisiones. No hay ningún canal de vuelta del avatar al nivel

No hay disparadores. Se están estudiando para versiones futuras, pero no hay nada decidido

Un nivel avanza en tiempo real. La frecuencia de fotogramas solo fija cada cuánto se vuelve a dibujar la pantalla.
La misma partida se juega igual a 30 y a 144 fotogramas por segundo

## La semilla

La semilla se toma del primer sitio donde está fijada:

1. `{{ui:level_level-view_seed-value}}` en la pantalla del nivel (`{{ui:level_level-view_seed-randomize}}` elige una nueva, `{{ui:level_level-view_seed-clear}}` la quita)
2. la semilla propia del nivel, fijada por el autor
3. una semilla nueva para esta partida

`0` significa "sin fijar". Por eso un nivel normal toma una semilla nueva cada vez que se carga

La ventana de resultados muestra la semilla de la partida, y el récord la guarda. Así una partida con suerte se puede repetir

## Cómo funciona la aleatoriedad

Un valor aleatorio de un nivel no sale de un generador que recuerda su estado. Se calcula a partir de su dirección:

`Hash(seed, keyframe frame, layer, start frame, track, channel)`

La misma dirección siempre da el mismo número. En cualquier dispositivo y en cualquier orden de cálculo.
Cada parte de la dirección es algo que edita el autor. Por eso la misma disposición repite la misma partida

## Qué te aporta esto

- **El bot Warm** planifica una ruta por todo el nivel antes de que empiece la partida. Es posible porque se juega exactamente el nivel para el que planificó
- **El bot Reflex** construye fotogramas por delante del actual y esquiva según ellos
- **Rebobinar hasta un checkpoint** vuelve a construir el fotograma necesario en lugar de deshacer nada
- **El editor** construye cualquier fotograma desde cero, así que el arrastre por la línea de tiempo es instantáneo
- **Los récords y las estadísticas** significan lo mismo en cualquier dispositivo

## Límites conocidos

La parte del nivel es determinista. La parte del avatar tiene defectos conocidos que todavía no están corregidos:

- dos obstáculos golpean al avatar en el mismo fotograma. Cuál de ellos fija la dirección del retroceso puede variar entre partidas
- el reloj del avatar no se reinicia al empezar el nivel. Un dash puede durar un fotograma más o menos, según cuánto tardó en cargar el nivel

Al medirlo, repetir la misma partida de un bot en una misma versión del juego coincidió hasta el último dígito. Así que estos defectos no se manifiestan en todos los niveles.
Por ellos, una partida es reproducible en la práctica, pero no está garantizado
