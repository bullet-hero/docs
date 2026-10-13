---
title: Imágenes y fuentes
date: 2026-10-02
tags: [level_author]
---

# Imágenes y fuentes

Si basta una forma, usa una forma: no tiene archivo, no gasta memoria y no plantea dudas de derechos. Haz la imagen del tamaño de su sitio en pantalla, como mucho {{v:texture.mobile-max-side}} para un nivel móvil y {{v:texture.desktop-max-side}} en general

Redondea el tamaño de la imagen hacia arriba a una potencia de dos

## Formatos y tamaño

Se carga todo lo que el motor sabe decodificar a partir de los bytes de un archivo. En la práctica, eso es `png` y `jpg`

El juego no pone límite al tamaño del archivo, lo pone el hardware:

| Dispositivo | Lado mayor |
|---|---|
| Android, garantizado | 4096 |
| Android, normalmente | 8192-16384 |
| PC de escritorio | hasta 32768 |

## Memoria

**El límite real es la memoria.** En memoria, una imagen se guarda como píxeles sin comprimir, pese lo que pese el archivo.
Un `png` ocupa 4 bytes por píxel. Un `jpg` ocupa 3, porque no tiene transparencia

| Tamaño | Memoria (`png`) |
|---|---|
| 512 por 512 | 1 MB |
| 1024 por 1024 | 4 MB |
| 2048 por 2048 | 16 MB |
| 4096 por 4096 | 64 MB |
| 8192 por 8192 | 256 MB |

> [!caution] Precaución
> Una textura de 8192 es un cuarto de gigabyte para una sola imagen. En un teléfono eso no significa lentitud, significa un cierre del juego

## Lo que decide el jugador

Tres opciones de la configuración de gráficos de cada jugador deciden cuánta memoria ocupa una imagen:
- si las imágenes se comprimen al cargar. La compresión divide las cifras de arriba entre 4 y 8
- el lado mayor de una imagen en memoria. La mitad de lado - un cuarto de memoria
- si se generan mipmaps, copias reducidas para dibujar en pequeño

Un teléfono comprime las imágenes y las limita a {{v:texture.mobile-max-side}} de forma predeterminada. Un PC de escritorio conserva la imagen completa y la limita a {{v:texture.desktop-max-side}}

**Lo que te toca a ti son los campos de la imagen, ante todo qué representa.** Están junto a la imagen en la lista de recursos.
Una fotografía es lo que mejor soporta la reducción y la compresión. Un dibujo con bordes duros las soporta peor

`{{ui:enum_texture-kind_pixel-art}}` nunca recibe mipmaps, prefiera lo que prefiera el dispositivo. Además empieza sin comprimir y sin difuminar, y los campos `{{ui:level_resources_texture-compression}}` y `{{ui:level_resources_texture-sampling}}` pueden cambiarlo

## Mipmaps

Los mipmaps evitan que una imagen pequeña centellee. Son copias reducidas que se dibujan en lugar de la imagen completa mientras se ve pequeña en pantalla.
Cuestan un tercio más de memoria

Sin mipmaps, una imagen reducida no se ve limpia, sino que vibra. Un jugador puede desactivarlos, y `{{ui:enum_texture-kind_pixel-art}}` nunca los recibe

Una imagen de 4096 que ocupa 200 píxeles en pantalla cuesta 256 veces la memoria de la misma imagen reducida a 256 de antemano

## Formas antes que imágenes

Una forma es más barata que una imagen en todo: sin archivo, sin memoria, sin dudas de derechos.
Las formas integradas son geometría real, no una imagen sobre un rectángulo. No tienen márgenes transparentes que se dibujan y se descartan

Esto se nota en un teléfono. En un chip móvil de gama media, una escena de 1000 objetos dedica el 95-97% del tiempo de la GPU a sombrear píxeles.
Una forma cubre el 29,4% de su rectángulo. El resto de un quad con textura es desperdicio transparente

Una imagen hace falta cuando necesitas justo una imagen: un logotipo, una fotografía, arte dibujado a mano.
Para una forma geométrica, usa una forma. Si la que necesitas no existe, dibújala en el `{{ui:hint_level_shape-editor_header}}`

## Fuentes

Las fuentes se cargan como `ttf`, `otf`, `ttc`. Sin una fuente propia, el texto se dibuja con la que tenga el sistema, y eso cambia de un dispositivo a otro

La `{{ui:settings_level-settings_fontcache}}` es el conjunto de caracteres preparados de antemano para dibujarse. Un generador la reconstruye a partir del texto que contiene el nivel.
Ejecuta el generador cuando el texto deje de cambiar

A continuación: [[1_level-budget]], [[2_mobile-devices]]
