---
title: Presupuesto del nivel
date: 2026-10-01
tags: [level_author]
---

# Presupuesto del nivel

Un teléfono aguanta con holgura unas 1000 formas en un fotograma, un PC débil 5000-10000. El sobredibujado cuesta más que la cantidad: cosas translúcidas sobre toda la pantalla, capa sobre capa

## Cuántas formas aguanta un dispositivo

Lo que cuenta son las **formas** vivas a la vez en un fotograma. Las cifras son aproximadas, pero el orden de magnitud es correcto

| Dispositivo | Con holgura | Límite de lo jugable |
|---|---|---|
| Teléfono | 1000 | 2000 |
| PC débil | 5000-10000 | 20000-40000 |
| PC medio (según la encuesta de Steam) | 50000 | 100000 |

Prueba en el dispositivo más débil que tengas a mano.
En tu propio PC todo irá bien, y eso no significa nada

## Texto y efectos

El texto y los efectos también se cuentan en formas

**Texto:** de 2 a 100 formas por objeto de texto. El coste depende de la complejidad de la fuente, del número de caracteres, del número de estilos y de si el texto está animado

**Efecto:** 10 formas por el propio objeto más 0,1 formas por cada partícula. Un efecto con mil partículas son unas 110 formas

## Sobredibujado

**Lo que cuesta mucho no es la cantidad, sino el sobredibujado.** Es cuando el mismo píxel se pinta una y otra vez

Qué se deduce de esto:
- un solo relleno translúcido sobre toda la pantalla cuesta más que cien proyectiles
- las capas de decoración translúcida unas sobre otras son lo más caro que se puede construir
- si el nivel va lento, busca lo que cubre toda la pantalla en lugar de contar objetos

> [!info] Conviene saber
> En un chip móvil medio, una escena de 1000 objetos con una superposición de 60-70x dedica el 95-97 por ciento del tiempo de GPU a pintar píxeles. Mil formas pequeñas repartidas por toda la pantalla son más baratas que diez formas translúcidas a pantalla completa unas sobre otras

## Opaco y translúcido

Una forma tiene una ruta de dibujo a elegir: `Auto`, `Opaque`, `Transparent`.
La ruta opaca es más barata: la GPU descarta de antemano los píxeles tapados

`Auto` decide por sí mismo, una vez al cargar. Su condición estricta es no cambiar nunca el aspecto del nivel.
Todo lo que no se puede demostrar que es opaco pasa a ser translúcido

> [!warning] Advertencia
> Fija la ruta a mano solo si sabes exactamente lo que haces. Un objeto declarado opaco que no lo es no irá más rápido, se verá mal

## Indicación de capacidad

Al guardar, el nivel registra cuántos objetos necesitó su fotograma más pesado.
Es una indicación para el cargador, no un límite. Un generador la recalcula

A continuación: [[2_mobile-devices|Dispositivos móviles]], [[3_images-and-fonts|Imágenes y fuentes]]
