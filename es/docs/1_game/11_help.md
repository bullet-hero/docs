---
title: Ayuda e informes de errores
date: 2026-10-02
tags: [player, level_author]
---

# Ayuda e informes de errores

Los errores del juego van a las issues de releases, las preguntas a Discord. Adjunta la línea de versión de la configuración y los pasos tras los que aparece el error

Mira primero [[5_troubleshooting]]. Allí se explican un nivel que falta, "hay que actualizar el juego" y un archivo comprimido rechazado

## Dónde escribir

| Qué | Dónde |
|---|---|
| un error en el juego o en el editor, una petición para el juego | [bullet-hero/releases](https://github.com/bullet-hero/releases/issues) |
| un error en el SDK o en su código | [bullet-hero/sdk](https://github.com/bullet-hero/sdk/issues) |
| una equivocación o un dato desactualizado en la documentación | [bullet-hero/docs](https://github.com/bullet-hero/docs), [[community]] |
| una pregunta, ayuda con un nivel, una discusión | [Discord](https://discord.gg/gkHQrp9NgS) |

Los mensajes en GitHub son públicos. Cualquiera puede leerlos y añadir algo.
Puedes enviar una issue o una pull request a la documentación

¿No sabes si es un error? Pregunta primero en Discord

Todos los enlaces del proyecto - [[links]]

## Qué incluir en un informe de errores

Un error que se puede reproducir se corrige. "Se ha cerrado" normalmente no se puede corregir: nadie sabe qué repetir

1. **La línea de versión.** Haz clic en la línea de versión de la pantalla de configuración y se copia sola. Tiene este aspecto: `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`, [[4_settings]]
2. **Plataforma y dispositivo:** el sistema y, si es un teléfono, el modelo
3. **Pasos:** qué hiciste, qué esperabas y qué pasó
4. **El nivel,** si el error está ligado a él: su carpeta en un archivo comprimido, o el archivo comprimido que abriste. Si el nivel está protegido, dilo
5. **El informe de error,** si apareció una ventana de error. `{{ui:root_error_save}}` lo escribe en la carpeta `reports`, `{{ui:root_error_open-reports-folder}}` la abre, [[1_installation]]

> [!tip] Consejo
> Adjunta los archivos al mensaje en lugar de pegarlos en el texto. Un log es largo y dentro del texto cuesta leerlo

## Logs

El juego escribe un log mientras funciona. Ayuda cuando no hubo ninguna ventana de error

- **Windows:** `Player.log` en la carpeta de datos del juego, `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` (la ubicación estándar de Unity)
- **Android:** el log va a logcat. Con el dispositivo conectado a un equipo, `adb logcat -s Unity` lo muestra
- **Otros sistemas:** todavía sin describir
