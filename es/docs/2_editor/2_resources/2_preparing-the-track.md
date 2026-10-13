---
title: Preparar la pista de audio
date: 2026-10-01
tags: [level_author]
---

# Preparar la pista de audio

Convierte la canción a ogg: pesa entre 8 y 10 veces menos que wav y, a diferencia de mp3, no añade silencio al principio del archivo. Aparte de ogg, solo se cargan mp3 y wav

## Formatos

`oga`, `mp2`, `aiff`, `flac` y los módulos de tracker `mod`, `xm`, `it`, `s3m` no se aceptan

> [!caution] Precaución
> `flac` no se carga en absoluto: el motor no lo decodifica. Conviértelo antes

> [!warning] Advertencia
> Un codificador de `mp3` añade unos milisegundos de silencio al principio, y cada codificador añade una cantidad distinta. Si la canción se vuelve a codificar con otro codificador, todo el marcado de pulsos se desplaza

## Desfase

Incluso en `ogg`, una canción casi nunca empieza justo en el primer pulso. Para eso está el desfase del segmento de pulso.
Se fija en fracciones de fotograma, así que es más fino que un fotograma

El orden es: primero el tempo, luego el desfase y solo después el contenido

## Volumen

Normaliza la canción antes de meterla en el nivel. Una normalización de pico a -1 dB es un valor sensato por defecto

Un nivel bastante más bajo de volumen que el siguiente parece un fallo del juego, no de la canción

## Duración

La duración del nivel y la de la canción son números distintos, no tienen por qué coincidir.
Un nivel puede terminar antes que la canción. Así se puede hacer un final con fundido

## Varias pistas de audio

Puede haber varias pistas de audio. Cada una tiene su propia posición en la línea de tiempo, su propia velocidad, su volumen y su cadena de efectos

Efectos: chorus, compresor, distorsión, eco, flanger, filtros, normalización, ecualizador, cambio de tono, reverberación

Un efecto en una pista de audio se oye en todas partes donde suena esa pista, no solo donde tú querías

A continuación: [[3_where-to-get-resources]], [[2_rhythm-and-structure]]
