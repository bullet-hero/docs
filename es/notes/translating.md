---
title: Traducir
date: 2026-10-13
tags: [contributor]
---

# Traducir

Una traducción es una copia del archivo en inglés en la misma ruta dentro de la carpeta de tu idioma, en la que solo se traduce el texto. Un dato que aparece en cualquier idioma se lleva a todos los demás

## Rutas espejo

Cada página está en la misma ruta, con el mismo nombre de archivo, en cada carpeta de idioma:

```
en/docs/2_editor/4_craft/3_difficulty-curve.md
ru/docs/2_editor/4_craft/3_difficulty-curve.md
zh/docs/2_editor/4_craft/3_difficulty-curve.md
ja/docs/2_editor/4_craft/3_difficulty-curve.md
ko/docs/2_editor/4_craft/3_difficulty-curve.md
es/docs/2_editor/4_craft/3_difficulty-curve.md
fr/docs/2_editor/4_craft/3_difficulty-curve.md
```

Lo que no cambia:

- el nombre del archivo y el de cada carpeta, prefijos incluidos
- `date` y `tags` en el frontmatter (`title` sí se traduce)
- los `[[wiki-links]]`: sus destinos son nombres de archivo, idénticos en todos los idiomas
- los enlaces externos, los nombres de imágenes, los bloques de código y el código en línea: archivos, campos, claves, valores, comandos
- la estructura: los mismos encabezados en el mismo orden, las mismas listas, tablas y recuadros

Los títulos de los recuadros se traducen al idioma de la página. Más - [[style-guide]]

## El inglés es la alternativa

Cuando falta una página en un idioma, el sitio muestra la página en inglés con un aviso.
Al revés no funciona: una página que solo existe en `ru/` le da un 404 a quien lee en inglés

> [!caution] Precaución
> Nunca añadas una página en otro idioma antes de que aparezca en `en/`. Los lectores de todos los demás idiomas recibirán un enlace roto

## Cada idioma lleva cada dato

El inglés manda solo en las direcciones, no en el contenido.
Un dato puede aparecer primero en cualquier idioma, y después se lleva a todos los demás. Tras un cambio, cada versión contiene todo lo que saben todas las versiones

- **Añadir, nunca quitar.** La información que falta se escribe en cada idioma que no la tiene
- **Las contradicciones no se resuelven adivinando.** ¿Dos versiones dan números distintos o afirmaciones opuestas? Comprueba la fuente (el juego, el SDK) y plantea la duda en el pull request
- **No se elimina nada sin preguntar,** ni siquiera un texto que parece obsoleto

Una diferencia de redacción no es un problema. Una diferencia en lo que aprende el lector sí lo es

## Comparar versiones

El repositorio tiene una skill para Claude Code, `compare-translations` (en `.claude/skills/`). Hace esta comparación. Sin ella, haz las mismas dos pasadas a mano

**La pasada estructural** compara las versiones elemento por elemento: el frontmatter, el H1, el primer párrafo, los encabezados, el número de párrafos, elementos de lista, filas de tabla y recuadros, los destinos de los enlaces, las imágenes, el código

**La pasada de significado** lee cada sección en paralelo y busca datos que una versión tiene y otra no: números y unidades, nombres de campos, botones y teclas, condiciones y excepciones, advertencias, los pasos de un procedimiento y su orden, ejemplos

## El chino tradicional se genera

`zh-Hant/` no se traduce a mano. Un script lo convierte a partir de `zh/`: OpenCC, caracteres tradicionales con el vocabulario de Taiwán. Una corrección en una página en chino tradicional va a la página de `zh/`, y la siguiente conversión la traslada. Una edición hecha directamente en `zh-Hant/` se sobrescribe

## Idioma nuevo

Un idioma nuevo se añade por completo en este repositorio, el código del sitio no cambia:

1. Copia `frontend/en.yaml` a `frontend/<code>.yaml`, por ejemplo `frontend/de.yaml`, y traduce los valores. Son los textos propios del sitio: el menú, los botones, la búsqueda, el aviso de cookies. Deja las claves y cada `{name}` tal como están
2. Crea la carpeta `<code>/` junto a `en/`, `ru/`, `zh/`, `zh-Hant/`, `ja/`, `ko/` y `es/` y traduce las páginas dentro de ella. Una página sin traducción se muestra en inglés con un aviso

Una clave con las formas `one` / `few` / `many` / `other` depende de una cantidad. Dale todas las formas que necesite tu idioma, la build indica las que faltan.
Una clave sin traducir se muestra en inglés. La build lista esas claves como advertencias

Antes de una traducción grande, abre un issue en [bullet-hero/docs](https://github.com/bullet-hero/docs), para que dos personas no traduzcan lo mismo
