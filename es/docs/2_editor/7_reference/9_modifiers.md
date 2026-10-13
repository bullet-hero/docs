---
title: Modificadores
date: 2026-10-12
tags: [level_author]
---

# Modificadores

Un modificador cambia lo que ya hay en el nivel: elimina contenido, recalcula los fps, aplana prefabs, cuantiza fotogramas clave, encaja y desplaza tramos. Una ejecución se deshace en un solo paso

## Eliminar contenido

Elimina el contenido del nivel que cumple las condiciones indicadas

> [!caution] Precaución
> El modificador cambia lo que existe en lugar de añadir. Todo se puede recuperar solo con un paso de deshacer. Lee los parámetros antes de ejecutarlo

Trabaja sobre la ventana de fotogramas de la ventana de generadores. En el modo inverso, en cambio, elimina lo que no comparte ningún fotograma con la ventana. En el modo inverso o con `{{ui:editor_generators-whole_level}}` activado puede eliminar mucho más de lo que se ve en pantalla, así que pide confirmación antes

Más - [[2_reuse]]

## Cambiar frecuencia de fotogramas

Recalcula cada número de fotograma para otra frecuencia de fotogramas.
Los tiempos se quedan en los mismos segundos

> [!warning] Advertencia
> Los fotogramas son números enteros. Todo lo que no se divide exactamente se redondea. Por eso, después de dos recálculos, el nivel puede no volver al original

El formulario muestra como referencia la frecuencia de fotogramas actual del nivel, de solo lectura. Cualquier cambio real de frecuencia pide confirmación antes. El modificador necesita el nivel entero, así que no está disponible en el modo prefab

Más - [[4_frames-and-time]]

## Aplanar prefabs

Convierte cada colocación de prefab de este ámbito en objetos normales.
El vínculo con la plantilla desaparece. Los objetos se quedan exactamente donde estaban

> [!info] Conviene saber
> El nivel se ve igual que antes de la ejecución: no se elimina ni se mueve nada. Los cambios en colocaciones concretas ya están escritos en los propios objetos y no se pierden. Las plantillas se quedan en el nivel salvo que pidas eliminarlas

## Cuantizar fotogramas clave

Lleva los fotogramas clave a un paso regular.
Así una animación hecha a mano e irregular cae sobre el pulso

Trabaja sobre la selección, y no se ejecuta sin ella

La cuadrícula se toma de la primera fuente que aplica:
1. `Use Beat Grid` está activado (de forma predeterminada) y el nivel tiene cuadrícula de pulsos. Las líneas son los pulsos de sus segmentos, cada pulso dividido en `Division` partes. Una plantilla de prefab no tiene cuadrícula de pulsos
2. `Use Bpm` está activado (de forma predeterminada). Una línea en cada pulso de `Bpm` a la frecuencia de fotogramas del nivel, dividido en `Division` partes
3. `Use Bpm` está desactivado. Una línea cada `Step Frames` fotogramas, empezando en el fotograma 1

Cada línea se coloca a partir de su tiempo exacto y solo después se redondea a un fotograma. Así la cuadrícula se mantiene sobre el pulso incluso donde un pulso no es un número entero de fotogramas: 167 BPM a 60 fps son 21,56 fotogramas por pulso

`Offset Frames` desplaza todas las líneas, `Mode` envía un fotograma clave que está entre dos líneas a la más cercana, a la anterior o a la posterior, `Tracks` elige qué pistas se ajustan. Las etiquetas del formulario son los propios nombres de los parámetros y no se traducen

> [!warning] Advertencia
> Un fotograma clave cuya línea ya ocupa otro fotograma clave de la misma pista se queda donde estaba. Por eso una cuantización gruesa deja algunos fotogramas clave fuera de la cuadrícula en lugar de fundirlos. Además, un fotograma clave nunca se mueve antes del inicio de su objeto

Más - [[2_rhythm-and-structure]], la cuadrícula de pulsos - [[3_timelines#Cuadrícula de pulsos]]

## Encajar tramos

Coloca los tiempos de vida de los hijos dentro del tiempo de vida de su padre.
Dos formas: encoger los hijos o estirar los padres.
Las anclas no cambian en ninguna de las dos

> [!info] Conviene saber
> Un hijo que se sale de su padre son datos válidos. Simplemente se reproduce recortado. Encajar es una decisión sobre el contenido, no la corrección de un error, así que nunca se ejecuta por sí solo

Más - [[4_frames-and-time]]

## Escalonar

Desplaza la selección en el tiempo.
Los objetos que empezaban a la vez aparecen uno tras otro

Trabaja sobre la selección, y no se ejecuta sin ella

Más - [[2_reuse]]
