---
title: Audio
date: 2026-10-02
tags: [level_author]
---

# Audio

El sonido de una pista de audio pasa por una cadena de efectos: hay 11, desde la normalización y el compresor hasta el eco y la reverberación. La cadena, la velocidad y el volumen se fijan en el inspector de la pista de audio

## Inspector de la pista de audio

Muestra el clip de la pista de audio seleccionada, su velocidad, el volumen del fader y la cadena de efectos.
Los efectos: paso bajo, paso alto, eco, reverberación, chorus, cambio de tono, distorsión, flanger, compresor, normalización y un ecualizador paramétrico

`{{ui:field_common_speed}}` y `{{ui:editor_inspector-audio_volume}}` son controles deslizantes, no campos de entrada. Así se ve el rango permitido

> [!caution] Precaución
> **El volumen de aquí es un fader.** El volumen con fotogramas clave es una pista aparte en la línea de tiempo local. Durante la reproducción los dos se multiplican

Más: [[2_preparing-the-track|Preparar la pista]]

## Normalizar

Lleva la señal constantemente hacia un volumen objetivo. Así los clips de fuentes distintas suenan igual de fuerte sin ajustes a mano.
Úsalo si las pistas del nivel no se mezclaron juntas

Trabaja sobre el volumen general. La dinámica dentro de una pista la cambia [[7_audio#Compresor|Compresor]]

- `Lowest Volume` evita que suba el silencio y el ruido hasta convertirlos en un siseo
- `Maximum Amp` limita cuánto puede amplificar

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todos los campos a su valor predeterminado, `{{ui:field_common_mix-level}}` incluido. Su valor predeterminado es el suelo de -80 dB, así que el restablecimiento también apaga el efecto

Más: [[2_preparing-the-track|Preparar la pista]]

## Compresor

Baja las partes fuertes para que las suaves puedan sonar más alto. Una pista comprimida se oye por debajo de todo lo demás del nivel y no satura.
Se suele usar para arreglar una canción que se pierde detrás de sus propios efectos

- `Threshold` - dónde empieza a actuar
- `Attack` y `Release` - lo rápido que aprieta y suelta. Demasiado rápido y cortas los ataques o se oye un bombeo
- `Make Up Gain` devuelve el volumen que quitó

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todos los campos a su valor predeterminado, `{{ui:field_common_mix-level}}` incluido. Su valor predeterminado es el suelo de -80 dB, así que el restablecimiento también apaga el efecto

Más: [[2_preparing-the-track|Preparar la pista]]

## Paso bajo

Deja pasar los graves y corta todo lo que está por encima de `Cutoff Freq`. Suena como si viniera de debajo del agua o del otro lado de una pared

Baja la frecuencia de corte: la pista pierde primero el aire, luego la claridad y al final todo menos el bajo.
En lo más alto del rango el filtro es casi transparente. La pista suena igual que el archivo

> [!tip] Consejo
> La cadena de efectos pertenece a la **pista** y no se anima con fotogramas clave. No puede cambiar de forma gradual con el tiempo. Corta la pista donde haga falta el cambio y configura las mitades de forma distinta

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todos los campos a su valor predeterminado, `{{ui:field_common_mix-level}}` incluido. Su valor predeterminado es el suelo de -80 dB, así que el restablecimiento también apaga el efecto

Más: [[2_preparing-the-track|Preparar la pista]]

## Paso alto

El espejo del paso bajo: deja pasar los agudos y corta todo lo que está por debajo de `Cutoff Freq`

Sube la frecuencia de corte: la pista se adelgaza hasta sonar como un altavoz diminuto o una llamada de teléfono.
Se suele usar para que todo suene pequeño antes de que se abra

> [!tip] Consejo
> La cadena de efectos pertenece a la **pista** y no se anima con fotogramas clave. No puede cambiar de forma gradual con el tiempo. Corta la pista donde haga falta el cambio y configura las mitades de forma distinta

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todos los campos a su valor predeterminado, `{{ui:field_common_mix-level}}` incluido. Su valor predeterminado es el suelo de -80 dB, así que el restablecimiento también apaga el efecto

Más: [[2_preparing-the-track|Preparar la pista]]

## EQ paramétrico

Una banda paramétrica: realza o recorta una parte elegida del espectro.
A diferencia de [[7_audio#Paso bajo|Paso bajo]] y [[7_audio#Paso alto|Paso alto]], también puede añadir. Por eso se usa para hacer sitio en la mezcla más que para crear un efecto

- `Center Freq` - dónde está la banda
- `Octave Range` - el ancho de la banda. Estrecha para un arreglo preciso, ancha para colorear el conjunto
- `Frequency Gain` por debajo de 1 recorta, por encima de 1 realza

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todos los campos a su valor predeterminado, `{{ui:field_common_mix-level}}` incluido. Su valor predeterminado es el suelo de -80 dB, así que el restablecimiento también apaga el efecto

Más: [[2_preparing-the-track|Preparar la pista]]

## Distorsión

Recorta la forma de onda. El sonido se llena de armónicos que no tenía: sucio, saturado, agresivo.
El efecto más simple de aquí: un solo mando, `Level` - con cuánta fuerza muerde el recorte

Como efecto secundario aplana la dinámica. Una pista muy distorsionada pierde sus partes suaves.
Donde una sección debe sonar implacable, eso es útil. Donde no, es destructivo

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todos los campos a su valor predeterminado, `{{ui:field_common_mix-level}}` incluido. Su valor predeterminado es el suelo de -80 dB, así que el restablecimiento también apaga el efecto

Más: [[2_preparing-the-track|Preparar la pista]]

## Eco

Repite la señal a intervalos iguales. Cada repetición suena más baja que la anterior.
Un eco es rítmico, y las repeticiones se pueden contar. Eso lo distingue de la cola difusa de [[7_audio#Reverberación|Reverberación]]: oyes copias separadas, no una sala

- `Delay` - la distancia entre copias en milisegundos
- `Decay` - qué parte de cada copia pasa a la siguiente

Saca el retardo del tempo de la canción, y el eco caerá sobre el pulso en lugar de emborronarlo

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todos los campos a su valor predeterminado, `{{ui:field_common_mix-level}}` incluido. Su valor predeterminado es el suelo de -80 dB, así que el restablecimiento también apaga el efecto

Más: [[2_preparing-the-track|Preparar la pista]]

## Reverberación

Coloca la pista en un espacio. Primero llegan las primeras reflexiones de las paredes cercanas, luego una cola que se apaga.
Es el efecto más grande de aquí: sus campos describen una sala, no una repetición. Las repeticiones son cosa de [[7_audio#Eco|Eco]]

El sonido principal lo fijan tres campos:
- `Decay Time` - lo grande que es la sala
- `Room` - cuánto de ella se oye
- `Room HF` - si lo recortas, las paredes suenan blandas y absorbentes

El resto es ajuste fino. Pasa a él cuando estos tres campos estén bien

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todos los campos a su valor predeterminado, `{{ui:field_common_mix-level}}` incluido. Su valor predeterminado es el suelo de -80 dB, así que el restablecimiento también apaga el efecto

Más: [[2_preparing-the-track|Preparar la pista]]

## Chorus

Superpone a la señal tres copias ligeramente retrasadas con una altura que oscila. Una sola fuente suena como varias.
El resultado es anchura y cuerpo, no una repetición. Los retardos son demasiado cortos para oírse por separado

Las tres copias lo distinguen de [[7_audio#Flanger|Flanger]], donde oscila una sola copia

- `Rate` - la velocidad de la oscilación
- `Depth` - la amplitud de la oscilación
- `Feedback` - si lo subes, el sonido se acerca a un flanger

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todos los campos a su valor predeterminado, `{{ui:field_common_mix-level}}` incluido. Su valor predeterminado es el suelo de -80 dB, así que el restablecimiento también apaga el efecto

Más: [[2_preparing-the-track|Preparar la pista]]

## Flanger

Mezcla en la señal un retardo muy corto y oscilante de esa misma señal. Las dos se anulan entre sí en frecuencias que se desplazan junto con el retardo.
Esa muesca que se arrastra es el silbido de motor a reacción. El efecto nace de la anulación, no de una copia

Es de la misma familia que [[7_audio#Chorus|Chorus]]. Pero hay una sola copia y el retardo es más corto, así que se oye un barrido, no anchura

La muesca es más profunda cuando `Dry Mix` y `Wet Mix` tienen valores parecidos

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todos los campos a su valor predeterminado, `{{ui:field_common_mix-level}}` incluido. Su valor predeterminado es el suelo de -80 dB, así que el restablecimiento también apaga el efecto

Más: [[2_preparing-the-track|Preparar la pista]]

## Cambio de tono

Cambia la altura de la pista sin cambiar su velocidad.
Ahí está todo el sentido: los tiempos del nivel están ligados a la canción. Por eso la pista no se puede remuestrear sin más, como hace el campo `{{ui:field_common_speed}}` de la propia pista

- `Pitch` - un multiplicador. 1 no cambia nada, 2 la sube una octava
- `FFT Size` y `Overlap` cambian calidad por coste

Con un cambio grande el sonido se seguirá oyendo procesado

> [!tip] Consejo
> La cadena de efectos pertenece a la **pista** y no se anima con fotogramas clave. No puede cambiar de forma gradual con el tiempo. Corta la pista donde haga falta el cambio y configura las mitades de forma distinta

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todos los campos a su valor predeterminado, `{{ui:field_common_mix-level}}` incluido. Su valor predeterminado es el suelo de -80 dB, así que el restablecimiento también apaga el efecto

Más: [[2_preparing-the-track|Preparar la pista]]
