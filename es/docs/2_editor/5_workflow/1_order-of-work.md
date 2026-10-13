---
title: El orden de trabajo
date: 2026-10-12
tags: [level_author]
---

# El orden de trabajo

Primero la pista de audio, los fps, el mapa de pulsos y los marcadores, después un esqueleto de formas simples y su prueba de juego. La decoración, el tema y los efectos van al final

Los pasos van del más caro al más barato.
Cuanto antes va un paso, más cuesta rehacerlo cuando ya está todo construido encima

## Los cimientos

1. **La pista terminada.** Convertida, normalizada, recortada. Todo lo demás se mide a partir de ella. Cambiar la pista más tarde desplaza cada fotograma del nivel
2. **Los FPS y la duración del nivel.** Los dos se pueden cambiar, pero lo caro es cambiar los fps: después del cambio se recalculan todos los fotogramas clave. El valor predeterminado es `60`, y normalmente no hay motivo para cambiarlo
3. **El mapa de pulsos.** Segmentos, tempo, desplazamiento, indicación de compás. Mientras el mapa de pulsos esté mal, nada se ajusta bien a los pulsos. Todo lo que se coloque antes habrá que moverlo después
4. **Marcadores sobre la estructura.** Intro, estrofa, estribillo, break, drop, outro. Son diez minutos de trabajo, y los marcadores se ven en todas las líneas de tiempo

## El esqueleto y su prueba de juego

5. **El esqueleto.** Los patrones principales con formas simples. Sin decoración, sin tema, sin efectos
6. **La prueba de juego del esqueleto.** Antes de decorar: una vez decorada una sección, no vas a querer borrarla

> [!caution] Precaución
> El esqueleto es la etapa en la que de verdad se diseña el nivel. Y es la que más a menudo se salta. Un esqueleto que no es divertido de jugar no se vuelve divertido con decoración. Se convierte en un nivel decorado que no es divertido de jugar

## Completar el nivel

7. **El contenido.** Completa los patrones y añade los objetos que hasta ahora solo estaban insinuados
8. **Temas y color.** Desde el principio, define los colores como referencias al tema, no como valores fijos
9. **Efectos y posprocesado.** Al final. Son lo más fácil de exagerar, y cuesta juzgarlos mientras el nivel sigue cambiando
10. **Metadatos.** Nombre, descripción, autores, clasificación por edad. Rellena la ficha de un recurso en cuanto lo añadas, no en este paso

## Tres hábitos que ahorran trabajo

Vale igual si construyes el nivel tú o si lo construye el asistente de IA:
- **Todo lo que se repite es un prefab.** Editas la plantilla una vez y todas las copias la siguen - [[2_reuse]]
- **Un contorno que no da ninguna forma integrada es una forma del nivel**, dibujada en el editor de formas o dada por la IA como polígono. Se dibuja y hace daño como un solo objeto, a diferencia de una pila de rectángulos
- **Usa todo el encuadre 16:9.** Un margen vacío grande es pantalla que el jugador ve y el nivel desperdicia. Mantén el peligro lejos del borde mismo, la decoración sí puede llegar hasta él - [[4_composition-and-camera]]

## Qué es barato y qué es caro cambiar

**Barato de cambiar al final:** los colores a través del tema, la decoración, el posprocesado, la descripción del nivel

**Caro:** los fps, la pista, el mapa de pulsos y la jerarquía

> [!warning] Advertencia
> Cambiar el padre de un objeto cambia a la vez su transformación, su tiempo de vida y su orden de dibujo. Por eso reestructurar un nivel terminado rara vez se queda en una sola edición

Guarda en cada paso. Qué cubren el guardado automático y deshacer - [[4_not-losing-work]]

A continuación: [[2_reuse|Reutilización: prefabs, copia, generadores]], [[4_not-losing-work|No perder tu trabajo]]
