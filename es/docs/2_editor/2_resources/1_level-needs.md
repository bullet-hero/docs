---
title: Qué necesita un nivel
date: 2026-10-02
tags: [level_author]
---

# Qué necesita un nivel

Lo mínimo es una canción. Todo lo demás es opcional, y casi todo lo traes tú

## Qué puede usar un nivel

| Qué | Detalles | Dónde vive |
|---|---|---|
| Audio | al menos una pista de audio, puede haber varias | la carpeta del nivel |
| Imágenes | cuando una forma no basta | la carpeta del nivel |
| Fuentes | `ttf`, `otf`, `ttc` | la carpeta del nivel |
| Formas | 497 integradas y cualquiera dibujada en el `{{ui:hint_level_shape-editor_header}}` | integradas en el juego o en el nivel |
| Temas, efectos, prefabs | datos, no archivos | dentro de `level.json` |

El audio, las imágenes y las fuentes son archivos reales.
Solo ellos añaden peso a la carpeta, necesitan un registro de su origen antes de publicar y se pueden perder en un traslado

Sin una fuente propia, el texto se dibuja con la que tenga el sistema

**El juego no incluye ni una sola textura.** Las formas integradas son geometría, no imágenes. No tienen píxeles, no pesan nada y no hay de dónde cargarlas

> [!tip] Recomendación
> Recurre a una forma antes que a una imagen, siempre. Una imagen es un archivo que puedes perder en un traslado, memoria al cargar y una línea en el registro de licencias. Una forma no cuesta nada de eso

## El peso de la carpeta

No hay un límite estricto. Pero un nivel se pasa copiándolo, y quien lo recibe ve el peso de la carpeta

Una canción de 4 minutos en `ogg` pesa 4-6 MB. La misma canción en `wav` ronda los 40 MB

## Varios orígenes para un recurso

Un recurso puede tener una lista de lugares de donde obtenerlo: un archivo junto al nivel, una ruta absoluta, un enlace directo.
El juego recorre la lista hasta que algo se carga

> [!tip] Recomendación
> Usa un enlace como complemento del archivo, no en su lugar. Un sitio web puede caerse, mudarse o empezar a servir otra cosa. Un archivo de la carpeta está donde está el nivel

## Derechos sobre los archivos

Si el nivel sale de tu disco, cada archivo que contiene necesita una licencia que lo permita.
Eso se decide con los recursos que eliges desde el principio

Más - [[2_editor/3_rights/index]]

A continuación: [[2_preparing-the-track]], [[3_images-and-fonts]]
