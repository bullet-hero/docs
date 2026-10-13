---
title: Por qué Bullet Hero
date: 2026-10-03
tags: [player, level_author]
---

# Por qué Bullet Hero

Bullet Hero es gratis, funciona en Windows y Android, y su SDK, su documentación y sus builds son abiertos. El núcleo mueve miles de objetos en pantalla en teléfonos y lo cubren más de 8000 tests

## Gratis

El juego es gratis y seguirá siéndolo. No tendrá compras, anuncios ni contenido de pago

No descarto monetizarlo con donaciones voluntarias, pero nada más allá de eso

## Disponible en todas partes, todo es universal

El juego está en todas las plataformas a las que he podido portarlo
- Plataformas: Windows, Android (más adelante iOS, Linux, Mac)
- Tiendas: Steam, Google Play (más adelante App Store)

Todo en el juego funciona con cualquier control, los niveles son los mismos en todas partes, y cada parte del juego (el editor, el multijugador, los servidores) funciona igual en todas partes

## Un alto grado de código abierto

El SDK, la documentación, las builds y el servidor están en repositorios abiertos. Solo el propio juego y el sitio son cerrados.
Todos los repositorios - [[links]]

## El núcleo técnico más rápido

Miles de objetos en pantalla, cientos de efectos y textos a la vez. Y todo eso funciona en teléfonos con un objetivo de 60 FPS (a menudo más)

## Un núcleo técnico muy estable

El juego tiene muchos mecanismos que mantienen estables el juego y sus modelos de datos
- Versionado de todo (más aquí - [[5_versioning]])
- Versionado multimodal y migración de datos, los datos de los niveles no se romperán
- Más de 8k tests en todo el juego, literalmente cada aspecto del juego está cubierto por tests

Y muchas otras comprobaciones. Junto con el núcleo rápido, esto da una relación muy alta entre estabilidad y rendimiento

## Multijugador (en desarrollo)

Multijugador en cualquier forma: en un mismo dispositivo, multijugador local, a través de un servidor, y muchas interacciones interesantes

## Servidores abiertos (en desarrollo)

Un servidor oficial y servidores de la comunidad que cualquiera puede poner en marcha. El código del servidor será abierto. Los catálogos de niveles y la comunicación básica llegarán junto con el servidor.
Más - [[4_server/index]]

## Muchos idiomas

El juego aspira a admitir de serie la mayoría de los idiomas del mundo. Creo que un juego no debería tener ninguna barrera de idioma

Por supuesto, nadie puede saber todos los idiomas del mundo, pero gracias a los avances de la IA y a la comunidad este objetivo es bastante alcanzable

## Política de licencias abierta

Todos los datos del juego vienen con una elección flexible de licencias (sobre todo [Creative Commons](https://creativecommons.org/))
para tus niveles y los recursos que usas. Esto hace más abierta la reutilización de recursos ajenos

Más - [[ugc-licensing-policy]]

## Integración con todos los servicios posibles

El juego tiene más de 10 variantes de build, y cada una tiene sus propias integraciones según la tienda por la que se distribuye

Más - [[download]]

## Determinismo y estabilidad

El juego tiene aleatoriedad determinista, y cada uno de sus factores está ligado a la semilla y a los parámetros del nivel.
Esto significa que la aleatoriedad siempre se puede repetir si conoces el nivel y tienes la semilla

Más - [[8_determinism]]

## Editor

El juego tiene un editor de niveles grande y flexible, en el que puedes crear casi cualquier cosa

El editor tiene muchas funciones únicas: [[8_generators]], depuración y más

## Formato de nivel abierto

El SDK de C# lee y escribe los niveles igual que el juego. El juego y el servidor trabajan a través de él, y tú también puedes.
Con él puedes crear tus propios niveles o recursos únicos, o tus propios servicios construidos sobre él

Más - [[3_sdk/index]]
