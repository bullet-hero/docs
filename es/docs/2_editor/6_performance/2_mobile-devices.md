---
title: Dispositivos móviles
date: 2026-10-02
tags: [level_author]
---

# Dispositivos móviles

En un teléfono, el dedo tapa la pantalla y el sistema ocupa los bordes. Mantén lo importante lejos de los bordes y prueba el nivel en un teléfono débil: la translucidez a pantalla completa es lo primero que lo frena

Los teléfonos son un objetivo tanto como el PC.
Un nivel que solo se juega en PC está hecho a medias

## Un dedo en lugar de un ratón

**Un dedo tapa la pantalla.** Un ratón es un punto, un dedo es una mancha bajo la que no se ve nada.
No construyas un patrón que exija mirar exactamente donde está el jugador. En PC funciona, en un teléfono es un punto ciego

**El control es distinto.** En PC el cursor fija el objetivo y el personaje se mueve hacia él. En un teléfono la precisión es menor, y un dedo tiene más inercia.
Un hueco que con el ratón se pasa a la primera se convierte en una prueba aparte en un teléfono

**Haz que un hueco estrecho sea corto en el tiempo,** no estrecho en anchura

## Bordes y forma de la pantalla

> [!caution] Precaución
> Los bordes pertenecen al sistema: el recorte de la cámara, las esquinas redondeadas, los gestos de navegación. La interfaz del juego se aparta de la zona no segura, el contenido del nivel no. Mantén lo importante lejos de los bordes, sobre todo del superior

**Relación de aspecto.** Un teléfono es aproximadamente 20:9, bastante más estrecho y alargado que la pantalla en la que trabajas.
Al menos una vez, mira el nivel en el simulador de dispositivos con esta forma antes de darlo por terminado

> [!caution] Precaución
> El simulador de dispositivos muestra proporciones y recortes, pero no dice nada del rendimiento. Una partida en un dispositivo débil real vale más que cualquier razonamiento

## Qué frena antes a un teléfono

Por orden:
1. La translucidez a pantalla completa en varias capas
2. El posprocesado, sobre todo Bloom. Su coste crece con la resolución, no con el número de objetos
3. Las texturas grandes. Una imagen de 4096 ocupa 64 MB de memoria antes de que se dibuje nada. Una cuarta parte de eso solo si la comprime la configuración del propio jugador
4. Los efectos con muchas partículas
5. Y solo después el número de formas

## Antialiasing

El antialiasing es una opción del jugador, no del nivel.
Pero explica por qué el mismo nivel se comporta de forma distinta en dos teléfonos parecidos:
- `{{ui:enum_anti-aliasing-type_msaa}}` se calcula por muestra. Su coste crece con el sobredibujado translúcido, justo donde un teléfono débil ya tiene dificultades
- `{{ui:enum_anti-aliasing-type_fxaa}}` es una sola pasada por la pantalla, su coste no depende de nada

A continuación: [[4_composition-and-camera|Composición y cámara]], [[1_level-budget|Presupuesto del nivel]]
