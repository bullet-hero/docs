---
title: No perder tu trabajo
date: 2026-10-02
tags: [level_author]
---

# No perder tu trabajo

Tu trabajo lo protegen el guardado automático, deshacer y una copia de la carpeta del nivel. Solo una copia de la carpeta es una instantánea completa del nivel. Cambiar el formato del archivo y eliminar un nivel no se pueden deshacer

Cada protección cubre lo que las demás no cubren. El guardado automático y deshacer no sustituyen a una copia de la carpeta, porque todo el nivel es una sola carpeta

## El hábito

> [!tip] Recomendación
> `Ctrl+S` después de cada sección terminada. Una copia de la carpeta del nivel antes de cada reestructuración. La comprobación `{{ui:settings_level-settings_rules}}` antes de dar el nivel por terminado

## Guardado automático

El guardado automático está activado por defecto. Funciona así:
1. Aparece una edición sin guardar - empieza una cuenta atrás de `60` segundos
2. El juego escribe una copia del nivel en `backups/<level id>/` dentro de la carpeta del juego, fuera de `levels`
3. Después guarda el propio nivel, como haría `Ctrl+S`

Un editor abierto sin cambios no escribe nada.
Todo lo que ha cambiado desde el último guardado, tuyo o automático, existe solo en memoria

Se conservan `25` copias, y la más antigua se elimina primero.
Una copia contiene solo el archivo del nivel, sin metadatos, pista ni imágenes. Sobrevive a la eliminación del nivel, a menos que marques `{{ui:root_level-delete_backups}}`.
La copia de un nivel protegido queda cerrada con la contraseña de ese mismo nivel

El interruptor, el intervalo y el número de copias se configuran en `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}`

**Restaurar:** configuración del nivel, pestaña `{{ui:settings_level-settings_dangerous-zone}}`, `{{ui:level_backups_open}}`. Las copias van de la más reciente a la más antigua, y cada una lleva por nombre el momento en que se hizo.
El archivo actual se copia antes en `backups`, así que una restauración también se puede revertir

También puedes restaurar a mano: copia la copia de seguridad en la carpeta del nivel como `level.json` (o `level.blob`)

## Cambios sin guardar

Una acción que reemplazaría el nivel abierto o saldría de él pregunta primero qué hacer con las ediciones sin guardar:
- abrir otro nivel desde la lista de niveles, incluido copiar un nivel y abrir la copia
- crear un nivel
- `{{ui:settings_level-settings_quit}}` desde la configuración del editor y desde la configuración del nivel
- `{{ui:level_backups_open}}`
- en `{{ui:settings_level-settings_dangerous-zone}}`: copiar el nivel y abrir la copia, cambiar el formato del archivo, poner una contraseña

El diálogo tiene tres respuestas:
- `{{ui:editor_save_text}}` - guarda el nivel y continúa la acción
- `{{ui:editor_unsaved-changes_discard}}` - el botón rojo, la única respuesta que pierde ediciones
- `{{ui:editor_cancel_text}}` - no hace nada

Jugar desde la configuración del nivel también pregunta, pero con dos respuestas: `{{ui:editor_unsaved-changes_save-play}}` y `{{ui:editor_cancel_text}}`. Aquí no se pueden descartar las ediciones, porque al volver del juego el nivel se lee otra vez del disco.
Si no hay nada sin guardar, el diálogo no aparece

## Qué cubre deshacer

Deshacer cubre las ediciones del nivel, y solo esas. Cada cambio en objetos, fotogramas clave, recursos, temas, prefabs y configuración pasa por un único búfer de operaciones

Lo que no cambia el nivel no se deshace:
- el gizmo elegido, la herramienta de la línea de tiempo, si el ajuste y la cuadrícula están activados
- la disposición de los paneles, la pestaña abierta, la posición del cabezal
- los portapapeles
- una semilla de sesión regenerada. Al recargar el nivel se elige otra vez
- **el guardado**. Deshacer revierte el nivel en memoria, no el archivo en disco

## Lo que no se puede deshacer en absoluto

Dos acciones escriben directamente en disco:
- **Cambiar el formato de archivo del nivel.** Escribir el nivel como `Blob` elimina el `Json` anterior. Y un `Blob` no se puede leer ni reparar a simple vista
- **Eliminar un nivel.** Por eso está escondido en `{{ui:settings_level-settings_dangerous-zone}}`

## La pestaña de datos sin procesar

La pestaña `{{ui:settings_level-settings_raw}}` muestra todo el archivo guardado como un árbol de campos. No comprueba nada: ni reglas ni límites

Es el último recurso. Todas las ediciones de una sesión se aplican como una sola operación, y esa operación se puede deshacer

> [!caution] Precaución
> Nada ha comprobado lo que escribiste en la pestaña `{{ui:settings_level-settings_raw}}`. Ten a mano una copia de la carpeta del nivel. Más - [[4_level-folder-and-backups#Copias de seguridad y recuperación]]

## Reglas

La comprobación que vale la pena ejecutar es la pestaña `{{ui:settings_level-settings_rules}}`. Muestra lo que encontró la validación: referencias rotas, ids duplicados, ciclos de padres, prefabs anidados a demasiada profundidad, segmentos de pulso superpuestos

El juego puede corregir algunas incidencias: una por una o todas a la vez con el botón `{{ui:settings_level-settings_rules-fix-all}}`.
Las correcciones se aplican con el botón `{{ui:editor_save_text}}`, como una sola operación que se puede deshacer. `{{ui:settings_level-settings_raw-discard}}` las descarta.
Las incidencias del grafo no tienen corrección

Que el tramo de un hijo se salga del de su padre no es un error. Son datos normales, y se comportan como está previsto.
Para encajar los tiempos de vida, ejecuta el modificador `{{ui:mod_span_fit}}`

A continuación: [[4_level-folder-and-backups|La carpeta del nivel y las copias de seguridad]], [[1_order-of-work|El orden de trabajo]]
