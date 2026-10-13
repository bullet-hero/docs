---
title: Composición y cámara
date: 2026-10-02
tags: [level_author]
---

# Composición y cámara

Mantén el contenido importante lejos del borde: otras pantallas ponen el borde en otro sitio, y el recorte de un teléfono puede tapar un proyectil. La sacudida de cámara funciona durante un compás, el giro rápido y el zoom brusco marean

## Cada pantalla es distinta

El nivel se monta en un monitor 16:9. En un teléfono 20:9 muestra más a lo ancho y menos a lo alto, en una tableta 4:3 es al revés.
Un objeto que estaba justo en el borde acaba o muy dentro del encuadre o fuera de él

**La pista `{{ui:editor_events-timeline_track_screen-limit}}`** define cómo se limita el área visible:
- de ninguna forma
- con una relación de aspecto fija
- con un rango de relaciones de aspecto

La relación fija es la más predecible. Todos ven exactamente lo que viste tú, pero en otras pantallas aparecen franjas en los bordes.
Elige a conciencia. "De ninguna forma" también es una elección, y significa que no sabes qué verá el jugador.
Un nivel nuevo vacío o un nivel creado desde un archivo de audio ya empieza con un fotograma clave de 16:9 fijo en el primer fotograma, salvo que desmarques `Pin Screen Aspect` al crearlo

> [!caution] Precaución
> La interfaz del juego se aparta de la zona no segura de la pantalla, el contenido del nivel no. La cámara encuadra el nivel respecto a toda la pantalla, así que el recorte de un teléfono puede tapar un proyectil. Mantén el contenido importante lejos del borde

## La cámara es una herramienta

La cámara no es un decorado. Tiene pistas de fotogramas clave: `{{ui:editor_dummy_text-15}}`, `{{ui:editor_dummy_text-16}}`, `{{ui:editor_dummy_text-17}}`, `{{ui:editor_dummy_text-18}}`, `{{ui:editor_dummy_text-19}}`

Un giro de 15 grados vuelve difícil un patrón sencillo sin un solo objeto nuevo.
Rompe todas las direcciones a las que el jugador se había acostumbrado

Ese poder también juega en tu contra. La cámara puede hacer que un nivel sea imposible de superar, y no lo notarás, porque sabes adónde mirar

> [!warning] Advertencia
> El giro rápido, la sacudida constante y el zoom brusco hacen que un nivel sea físicamente imposible de terminar. No por dificultad, sino por cómo se siente el jugador. La sacudida funciona durante un compás en un drop y es insoportable durante un minuto

## Capas

El orden de dibujo es relativo: la capa de un objeto se suma a las capas de todos sus padres.
Si arrastras un objeto a otro padre, cambia qué se dibuja encima de qué. Aunque nunca hayas tocado el número de capa

Mantén la decoración y el peligro en rangos de capas distintos. Así la decoración no tapará un proyectil por accidente

## La legibilidad gana a la belleza

Un jugador que no vio un proyectil por culpa de la decoración es un error tuyo, no suyo.
Cuando tengas que elegir, recorta la decoración

A continuación: [[2_mobile-devices|Dispositivos móviles]], [[1_readability-and-fairness|Legibilidad y justicia]]
