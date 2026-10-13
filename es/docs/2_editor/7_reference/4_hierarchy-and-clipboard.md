---
title: Jerarquía y portapapeles
date: 2026-10-02
tags: [level_author]
---

# Jerarquía y portapapeles

La jerarquía es un árbol de los objetos del fotograma actual ordenados por padre. Cada línea de tiempo tiene su propio búfer de portapapeles, y la paleta de comandos encuentra cualquier acción del editor por su nombre

## Jerarquía

Muestra todos los objetos vivos en el **fotograma actual**, anidados por padre

Un objeto se ve aquí solo mientras el cabezal está dentro de su tramo. Por eso la lista cambia mientras arrastras el cabezal.
Una jerarquía vacía suele significar que el cabezal está más allá del final del contenido

> [!info] Conviene saber
> **Un padre** transmite su transformación a sus hijos. Las capas se suman a lo largo de la cadena: el orden de dibujo de un hijo es su propia capa más las capas de todos sus antepasados. Por eso cambiar el padre mueve el objeto en el orden de dibujo. También cambia sus valores aleatorios: la aleatoriedad está ligada a la capa resultante

> [!tip] Consejo
> Haz clic derecho en una fila para abrir sus acciones. En una pantalla táctil, mantener pulsado abre el mismo menú

Mantener pulsada una fila también abre el menú con el ratón. Los clips de las líneas de tiempo no tienen menú al mantener pulsado

Arrastra una fila sobre otra para convertir el objeto en su hijo. Si la sueltas en el espacio vacío bajo las filas, pierde su padre. Se rechaza soltarla:
- sobre el propio objeto o sobre el padre que ya tiene
- sobre uno de sus propios hijos
- si la cadena pasaría de 15 niveles de profundidad

La fila `{{ui:editor_search-option_camera}}` está fijada al final de la lista. Una fila que se suelta sobre ella convierte el objeto en hijo de la cámara del nivel. Dentro de una plantilla de prefab la cámara no acepta hijos, pero la raíz de la plantilla sí

Más: [[3_how-the-editor-thinks|Cómo funciona el editor]]

## Seleccionar varios objetos

Un clic con `Ctrl` añade un objeto a la selección o lo quita de ella. Funciona igual en la jerarquía, en las líneas de tiempo y en la vista. `Ctrl` es la única tecla así: un clic con `Shift` en la jerarquía no hace nada, no hay selección por rango. La tecla se puede reasignar

Un clic con `Ctrl`, o un rectángulo que atrapa más de un elemento, activa el **modo de selección múltiple**. Mientras está activo, lo que hace un clic normal depende de `{{ui:settings_game-editor-multi-select-requires_hold}}` - consulta [[14_editor-settings]]

El elemento de selección de la barra de herramientas muestra `{{ui:editor_multi-select_status}}` o `Selección (N)`. Funciona mientras hay algo seleccionado:
- una pulsación borra toda la selección
- un doble clic o un clic con `Shift` activa en cambio el modo de selección múltiple. Activado así, el modo ignora `{{ui:settings_game-editor-multi-select-requires_hold}}`, y cada clic normal añade. Así es como un dedo, que no tiene `Ctrl`, construye una selección

El mismo elemento aparece en los menús contextuales mientras hay algo seleccionado. Ahí una pulsación borra la selección

El modo se desactiva solo cuando no hay nada seleccionado, y con `Escape` si no se está escribiendo en un campo de texto

## Portapapeles

Lleva una selección de un nivel a otro y de un dispositivo a otro. Cada línea de tiempo tiene su propio búfer y su propia línea de estado

`{{ui:editor_clipboard-serialize_copy}}` escribe todos los búferes en el portapapeles del sistema como texto.
`{{ui:editor_clipboard-deserialize_paste}}` vuelve a leer el texto en los búferes - y **se detiene ahí**

> [!info] Conviene saber
> La parada es deliberada. Leer el texto y pegar son dos decisiones distintas. Dónde se pega el contenido depende del cabezal y del ámbito activo. El contenido aparece solo cuando lo **pegas en la línea de tiempo que elegiste**

Si el portapapeles del sistema contiene texto ajeno, el editor informa de un error y no se bloquea. Contiene lo último que copiaste en cualquier sitio

No existe una acción "pegar todos los búferes a la vez". Después de `{{ui:editor_clipboard-deserialize_paste}}`, pega en cada línea de tiempo por tu cuenta

Los fotogramas clave pegados caen en el cabezal. Para cada propietario, su fotograma clave pegado más temprano se coloca en el cabezal, contado dentro del tramo de ese propietario. Los fotogramas clave de eventos se desplazan lo mismo, así que un movimiento de cámara y el efecto que lo acompañaba siguen a la misma distancia

Un fotograma clave se omite si caería fuera de la línea de tiempo de su propietario o en un fotograma ya ocupado en su pista. Los fotogramas clave omitidos se cuentan y se notifican en un solo mensaje

Una copia o un pegado correctos no escriben nada en la consola. Solo se notifican los problemas

Más: [[2_reuse|Reutilizar: prefabs, copia, generadores]]

## Paleta de comandos

Encuentra cualquier acción del editor por su nombre

Lista comandos, no contenido. Son las mismas acciones que ejecutan la barra de herramientas y los menús contextuales

> [!tip] Consejo
> La búsqueda de contenido (`Ctrl+F`) es su gemela. Busca en todos los objetos del ámbito actual y en todas las pistas de audio. Los recursos no están en ella: cada uno se elige desde el campo que lo necesita

Más: [[3_speed-and-shortcuts|Velocidad y atajos]]
