---
title: Temas
date: 2026-10-02
tags: [level_author]
---

# Temas

Un tema es una paleta de 64 colores a los que los objetos se refieren por número de ranura. Cambia el tema, y todo lo que se refiere a él cambia con él

Un color de tipo `Theme` no guarda un color propio, solo un número de ranura.
Toma lo que contenga esa ranura en el tema activo en el fotograma actual

Por qué esto es mejor que los colores escritos a mano y cómo mantener un nivel legible con cualquier tema - [[5_color-and-postprocessing]]

## Qué contiene un tema

- **Un nombre** - se muestra en las listas y los selectores
- **Un ID**, `ThemeId`. Los fotogramas clave de tema se refieren a un tema por él, no por su nombre
- **64 colores** en una cuadrícula de 8 por 8, cada uno con transparencia
- **Un nombre de ranura** para cada ranura, opcional. Hasta que nombres al menos una ranura, el archivo guarda `null` en lugar de la lista de nombres

Un tema son datos dentro de `level.json`, no un archivo aparte en la carpeta del nivel (ver [[1_level-needs]]).
Un nivel puede contener cualquier cantidad de temas

El juego no asigna ningún papel a una ranura: el propio tema `Balanced` del juego simplemente agrupa sus 64 colores por tono

## Cómo encuentra un color su valor

En dos pasos:
1. La pista `Theme` de la línea de tiempo de eventos dice qué tema está activo en este fotograma
2. Un color de tipo `Theme` nombra una ranura del 0 al 63 del tema activo

Entre lo que puede referirse a un tema están, por ejemplo, el color de una forma (cada una de sus esquinas por separado), el color de un texto y el fondo del nivel

**La posición de una ranura es su identidad.** Mueve un color a otra ranura, y todo lo que se refería a la antigua cambia de color

## Cambiar de tema a lo largo del tiempo

Entre dos fotogramas clave de tema, el juego mezcla suavemente toda la paleta de un tema al otro.
El suavizado lo toma del fotograma clave posterior (ver [[5_keyframes-and-easing]])

Si no hay ningún fotograma clave de tema, todas las ranuras son blancas

> [!warning] Advertencia
> Un fotograma clave nuevo recibe `Linear`, así que la paleta se desplaza a lo largo de todo el intervalo desde el fotograma clave de tema anterior hasta este. Para que el tema cambie exactamente en el drop, pon `Constant` en el fotograma clave del drop

> [!caution] Precaución
> Un fotograma clave de tema puede sobrevivir al propio tema. Elimina un tema al que todavía se refieren fotogramas clave, y todos esos fotogramas se vuelven blancos. Los fotogramas clave se quedan. El editor vuelve a preguntar antes de eliminar un tema así

## Cómo crear y editar un tema

La pestaña `Themes` entre los recursos del nivel muestra los temas del nivel. Tiene `{{ui:settings_level-settings_resources-themes-add}}` e `{{ui:settings_level-settings_resources-themes-import}}`.
Al hacer clic en una fila se abre el `{{ui:settings_level-settings_theme-editor}}`:
- `{{ui:field_common_name}}` del tema
- `Theme Id` y `{{ui:settings_level-settings_theme-editor-regenerate-id}}`
- la cuadrícula de 8 por 8. Hacer clic en una celda la selecciona, muestra `Color:` con su número y carga el color en la rueda bajo la cuadrícula
- `{{ui:editor_theme-editor_color-name}}` para la celda seleccionada

El editor trabaja sobre una copia. Nada llega al nivel hasta que guardas. El propio guardado es un solo paso de deshacer

## Cómo elegir una ranura

Cambia un color a `Theme` y abre `{{ui:editor_select-theme_color}}`

La cuadrícula muestra la paleta tal como está mezclada en el fotograma del fotograma clave que se edita, no en el cabezal.
Al lado están los dos fotogramas clave de tema que rodean ese fotograma y lo que contiene la ranura seleccionada en cada uno. Una ranura sin nombre aparece como `{{ui:editor_search_unnamed}}`

## Cómo compartir e importar

- **La biblioteca del dispositivo.** `{{ui:editor_level-theme-item_export}}` en la fila de un tema lo guarda en `resources/themes` - la biblioteca compartida de todo el dispositivo, donde `resources` está junto a `levels` (ver [[4_level-folder-and-backups]]). `{{ui:settings_level-settings_theme-library}}` la muestra y marca lo que ya está `{{ui:editor_theme-library-item_in-level}}`. `{{ui:editor_library_delete}}` quita un tema de la biblioteca. Importar copia el tema al nivel, así que el nivel nunca depende de tu biblioteca. `{{ui:settings_level-settings_theme-library}}` también muestra los temas de las colecciones, con etiquetas de origen - [[16_library-and-collections]]
- **Los temas del juego.** `{{ui:editor_search-title_theme}}` ofrece los temas que trae el juego junto a los temas del nivel

A continuación: [[5_color-and-postprocessing|Color, temas y posprocesado]], [[1_readability-and-fairness|Legibilidad y justicia]]
