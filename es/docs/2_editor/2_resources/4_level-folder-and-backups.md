---
title: La carpeta del nivel y las copias de seguridad
date: 2026-10-11
tags: [level_author]
---

# La carpeta del nivel y las copias de seguridad

Un nivel vive en su propia carpeta dentro de levels, en la carpeta del juego. No cambies el nombre de los archivos que usa, y una copia de seguridad completa es una copia de la carpeta del nivel

## Qué hay en la carpeta

La carpeta del nivel está en `levels`, dentro de la carpeta del juego. Dónde está la carpeta del juego - [[1_installation]]

| Archivo | Qué es |
|---|---|
| `level.json` | el contenido del nivel. En el formato binario - `level.blob` |
| `metadata.json` | nombre, descripción, autores, etiquetas. En el formato binario - `metadata.blob` |
| `logo.png` o `logo.jpg` | la portada |
| la canción, las imágenes, las fuentes | todo lo demás que usa el nivel, justo al lado de `level.json` |

Junto a `levels` está `resources`, con las bibliotecas de todo el dispositivo: `themes`, `effects`, `shapes`, `prefabs`.
No forman parte del nivel. Allí exportas lo que quieres reutilizar, y desde allí lo importas

La misma carpeta `resources` contiene `collections`, una carpeta por colección. Más - [[16_library-and-collections]]

Un nivel enviado a otra persona lleva dentro todo lo que necesita. Las bibliotecas no viajan con él

## Qué no tocar a mano

> [!caution] Precaución
> No cambies el nombre de los archivos que usa el nivel. Las referencias a ellos se guardan por nombre, así que un archivo renombrado es un archivo que falta

No edites `level.json` en un editor de texto mientras el nivel está abierto en el juego. Al guardar desde el editor, tus cambios se sobrescriben sin aviso

No guardes en la carpeta del nivel nada que el nivel no use. Viaja con la carpeta

El formato del archivo lo decide la extensión, no un campo interno. Por eso cambiar el formato en el editor escribe un archivo nuevo y borra el antiguo.
De lo contrario habría dos archivos en el disco, y no habría forma de saber cuál es el bueno

## Cuando falta uno de los dos archivos

Una carpeta que solo tiene uno de los dos, `level.json` o `metadata.json`, sigue apareciendo en la lista de niveles. Los binarios `level.blob` y `metadata.blob` cuentan igual

| Falta | En el juego | En el editor |
|---|---|---|
| `level.json` | la tarjeta está completa, pero el nivel no se puede iniciar | se restaura desde la copia de guardado automático más reciente. Si no hay copias, se escribe un nivel vacío |
| `metadata.json` | la tarjeta muestra el nombre de la carpeta, y el nivel se puede jugar | se escribe un `metadata.json` nuevo con el nombre de la carpeta y la configuración predeterminada |

Un `metadata.json` que el juego no puede leer cuenta como ausente. El editor lo mueve a `metadata.json.bak` antes de escribir el nuevo, así que no se pierde nada

El editor pregunta antes de escribir nada. Un nivel integrado o de `Workshop` nunca se modifica en su sitio: uno sin `metadata.json` se ofrece como copia, y uno sin `level.json` no se puede abrir

## Copias de seguridad y recuperación

**Una copia de seguridad completa es una copia de la carpeta del nivel.** Lo contiene todo, recursos incluidos.
Haz una copia antes de cada cambio grande y ponle la fecha

**El guardado automático solo conserva el archivo del nivel.** Sin metadatos, canción ni imágenes.
Cada guardado automático pone una copia en `backups/<level id>/` en la carpeta del juego, fuera de `levels`. Se conservan `25` copias. Cómo restaurar una copia - [[4_not-losing-work#Guardado automático]]

**Un nivel en `Json` que ha dejado de abrirse no está perdido.** El archivo es texto, así que puedes abrirlo en cualquier editor de texto y corregirlo a simple vista. El propio juego no abre un nivel que falla al cargar, así que la pestaña `{{ui:settings_level-settings_raw}}` no sirve aquí. Muestra el modelo de un nivel que ya está abierto

Un `Blob` no se puede salvar así. Es binario, y un archivo dañado se rechaza entero en lugar de leerse en parte

Qué saber antes de editar en la pestaña `{{ui:settings_level-settings_raw}}` - [[4_not-losing-work#La pestaña de datos sin procesar]]

A continuación: [[4_not-losing-work]], [[2_metadata-and-sharing]]
