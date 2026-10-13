---
title: "Color, temas y posprocesado"
date: 2026-10-02
tags: [level_author]
---

# Color, temas y posprocesado

Pasa el color del contenido por una referencia al tema y deja los colores literales para lo que de verdad es único. Activa el posprocesado en un pico y vuelve a desactivarlo, o los proyectiles pierden sus bordes

## Referencias al tema y colores literales

Un color se puede definir de dos formas:
- **un color literal** - un valor escrito directamente en el objeto
- **una referencia al tema** - "toma tal ranura del tema activo". Qué tema está activo lo define una pista de fotogramas clave

La diferencia se nota en la segunda pasada. Con referencias, cambiar la paleta es una sola edición del tema. Con literales, es una edición de cada objeto

El fondo también toma su color del tema. Cómo funcionan las ranuras y los fotogramas clave de tema - [[6_themes]]

> [!caution] Precaución
> Comprueba el contraste en cada tema, no solo en el que usaste para trabajar. Un nivel que cambia de tema en el drop tiene que seguir siendo legible en ambos. Los proyectiles oscuros que se leen perfectamente en un tema claro desaparecen en uno oscuro

## Posprocesado

El conjunto estándar de URP más dos efectos de glitch. Todo va con fotogramas clave, así que cada parámetro se puede animar

> [!caution] Precaución
> Es el camino más rápido hacia un nivel al que nadie puede jugar. El Bloom al máximo convierte cualquier objeto brillante en una mancha, y el proyectil pierde su borde. La aberración cromática separa los bordes. Un glitch de más de un compás es una interferencia, no un estilo. El Bloom no tiene umbral: cada píxel brilla, así que un fondo oscuro se aclara hacia el gris a medida que sube la intensidad

Tres reglas mantienen el posprocesado del lado del estilo:
- activa un efecto en un pico y vuelve a desactivarlo, no lo dejes de fondo
- no actives un efecto que empeore la legibilidad de los proyectiles donde haya que esquivarlos
- ¿tuviste que entrecerrar los ojos tras activar un efecto? Desactívalo. El jugador no entrecerrará los ojos, se irá

## Antialiasing

El antialiasing es una opción del jugador, no tuya.
Un nivel que solo se ve bien en un modo no se ve bien para todos

| Modo | Qué hace |
|---|---|
| `{{ui:enum_anti-aliasing-type_msaa}}` | el predeterminado. Alisa exactamente los bordes de la geometría, y cada forma es geometría real |
| `{{ui:enum_anti-aliasing-type_fxaa}}` | cuesta una pasada sobre la pantalla, por mucho que el nivel dibuje sobre sí mismo |
| `TAA`, `STP` | no se ofrecen: dejan una estela detrás de los objetos rápidos, y una estela detrás de un proyectil hace que el nivel sea más difícil de leer |

A continuación: [[1_readability-and-fairness|Legibilidad y justicia]], [[1_level-budget|Presupuesto del nivel]]
