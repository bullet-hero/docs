---
title: Qué es un nivel
date: 2026-10-02
tags: [level_author]
---

# Qué es un nivel

Un nivel es una carpeta normal en el disco: el archivo del nivel, los metadatos y todo lo que usa. Créalo en Json y pásalo como una copia de la carpeta, no hace falta instalar nada

## Qué hay en la carpeta

La carpeta no es una fila de una base de datos ni un archivo comprimido cifrado

Hay dos archivos principales:
- `level.json` - el nivel en sí: objetos, fotogramas clave, temas, recursos
- `metadata.json` - la portada: nombre, descripción, autores, etiquetas, duración

Junto a ellos está todo lo que usa el nivel: la canción, las imágenes, las fuentes.
El juego no incluye ni una sola textura. Todo lo que ves en un nivel es una forma integrada o un archivo de esta carpeta

La portada es un archivo aparte, para que mostrar una lista de mil niveles no obligue a abrir mil niveles

La lista completa de archivos - [[4_level-folder-and-backups]]

## Json o Blob

El formato del archivo lo eliges al crear un nivel:

| Formato | Qué es |
|---|---|
| `Json` | texto plano, se abre en cualquier editor y se puede corregir a mano |
| `Blob` | un archivo binario, carga decenas de veces más rápido y ocupa un tercio, no se puede leer a simple vista |

> [!tip] Recomendación
> Crea el nivel en `Json` y conviértelo a `Blob` cuando esté terminado. Si el nivel deja de abrirse, `Json` se puede leer y corregir a mano. `Blob` casi no tiene arreglo: un solo byte dañado no pasa la comprobación de integridad

## Cómo pasar un nivel

Un nivel se pasa copiándolo. Comprimes la carpeta, la envías, la descomprimes, la abres.
No se instala, no se registra ni se importa nada

En PC esto funciona siempre. En un teléfono - allí donde el sistema te deje entrar

Lo que se deduce de esto:
- una copia de seguridad de un nivel es una copia de la carpeta
- no cambies el nombre de los archivos de la carpeta: los recursos se buscan por nombre
- un nivel en `Json` que el editor no abre se puede seguir leyendo a simple vista. La pestaña `{{ui:settings_level-settings_raw}}` solo muestra un nivel que ya está abierto

> [!caution] Precaución
> No edites `level.json` en un editor de texto mientras el nivel está abierto en el juego. Al guardar desde el editor, tus cambios se sobrescriben sin aviso

## El formato es abierto

El modelo de datos del nivel está en un repositorio aparte con licencia MIT - [bullet-hero/sdk](https://github.com/bullet-hero/sdk).
Así que un nivel se puede leer sin el juego, y puedes escribir tu propia herramienta para el formato. Un defecto del formato también se ve desde fuera

Más sobre el formato - [[3_sdk/index]]

A continuación: [[2_first-level]], [[4_level-folder-and-backups]]
