---
title: Solución de problemas
date: 2026-10-03
tags: [player]
---

# Solución de problemas

Un nivel copiado a mano aparece en la lista tras una nueva búsqueda. Un nivel de una versión más nueva requiere actualizar el juego, y un archivo .7z hay que volver a comprimirlo como zip. Una contraseña olvidada no se puede recuperar. Discord muestra tu actividad solo en una versión de Steam, con la aplicación de Discord abierta

¿No encuentras tu problema? Dónde informar de él - [[11_help]]

## Un nivel no está en la lista

- **Copiado a mano.** La carpeta del nivel tiene que estar directamente en `levels`, [[1_installation]]. Después de copiarla, pulsa `{{ui:root_level-browser_refresh}}`
- **Un artículo del Workshop.** La versión de Steam solo muestra tus suscripciones. `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general_show-all-found-content}}` añade las carpetas encontradas en el disco. Llevan la marca `{{ui:root_level-entry_not-listed}}`
- **No aparece nada.** Puede que la carpeta de niveles no sea accesible. En ese estado la limpieza del almacenamiento de `{{ui:settings_other_title}}` no se ejecuta y dice `El análisis de niveles no encontró nada, así que se rechazó esta limpieza`

## Un nivel no se carga

La pantalla de carga muestra la etapa: `{{ui:root_loading_reading}}`, `{{ui:root_loading_validating}}`, `{{ui:root_loading_resources}}`, `{{ui:root_loading_building}}`

- **Un archivo en una dirección web.** Un nivel puede tomar un archivo de un enlace en lugar de guardarlo en su carpeta. `{{ui:settings_general_title}}` → `{{ui:settings_general_resource-web-timeout}}` es cuántos segundos espera el juego por ese archivo
- **Un nivel dañado.** Un nivel en `Json` es texto y se puede leer a simple vista. Un `Blob` dañado se rechaza entero. Más - [[4_level-folder-and-backups]]
- **Una ventana de error.** Tiene `{{ui:root_error_copy}}`, `{{ui:root_error_save}}` y `{{ui:root_error_open-reports-folder}}`. El informe va a la carpeta `reports`. Adjúntalo a un informe de errores en [bullet-hero/releases](https://github.com/bullet-hero/releases/issues), [[11_help]]
- **`El nivel necesita más objetos por fotograma de los que permite este dispositivo`.** No es un error de carga. El nivel se juega, pero una parte no se dibuja. Más - [[1_level-budget]]

## "Hay que actualizar"

Una versión antigua del juego no abre archivos de una más nueva. Actualiza el juego

| Mensaje | Qué hacer |
|---|---|
| `Este nivel se hizo en una versión más reciente del juego...` | actualizar el juego |
| `Este archivo comprimido contiene un nivel de una versión más reciente del juego...` | actualizar el juego |
| `El portapapeles contiene contenido del editor copiado en una versión más reciente del juego...` | actualizar el juego |
| `Tu configuración o tus estadísticas las guardó una versión más reciente del juego...` | `{{ui:root_update-required_download}}`, `{{ui:root_update-required_keep}}` o `{{ui:root_update-required_overwrite}}` |

Una tarjeta con la marca `{{ui:root_level-entry_newer-version}}` o `{{ui:root_level-entry_newer-file}}` es el mismo rechazo. Se ve incluso antes de abrir el nivel

### Configuración o estadísticas de una versión más nueva

En este caso el juego funciona con los valores predeterminados. Hasta que se cierra no guarda nada propio, y los archivos más nuevos se quedan intactos. Es el modo anónimo, [[4_settings]].
Con `--suppress-game-saves` no hay botón `{{ui:root_update-required_overwrite}}`

Las estadísticas de un nivel de una versión más nueva no se muestran. Jugar el nivel las sobrescribe, salvo que el guardado esté desactivado

### Por qué el juego se niega

Cada cambio en el formato de archivo recibe un nuevo número de generación. Una versión del juego no lee un archivo de una generación más nueva, para no leerlo mal

## Un nivel protegido

Antes de abrirlo, el juego pide una `{{ui:level_passphrase_password}}`.
La contraseña se pide una vez por sesión y solo se guarda en memoria

Solo se cifra el contenido: objetos, fotogramas clave, temas. El título, la portada y los archivos multimedia siguen siendo legibles, así que la tarjeta se ve incluso sin la contraseña

Eliminar un nivel protegido no requiere la contraseña

> [!caution] Precaución
> Una contraseña olvidada no se puede recuperar. La clave no se guarda en ningún sitio: ni en el juego, ni en el archivo, ni en manos de nadie

## Se rechaza un archivo comprimido

| Mensaje | Causa |
|---|---|
| `{{ui:editor_create-level_archive-unsupported}}` | es `.7z`. Vuelve a comprimirlo como `.zip` |
| `{{ui:editor_create-level_archive-wrong-password}}` | la contraseña no coincide |
| `{{ui:editor_create-level_archive-damaged}}` | el archivo comprimido está roto, pide que te lo envíen otra vez |
| `{{ui:editor_create-level_archive-not-archive}}` | el archivo no es un archivo comprimido de nivel |

Un archivo comprimido con otro nombre no es un problema: el juego reconoce el formato por los bytes del archivo.
Qué archivos comprimidos se aceptan - [[2_playing-levels]]

## Discord no muestra a qué estoy jugando

- **No es una versión de Steam.** Solo las versiones de Steam muestran tu actividad en Discord
- **Discord está cerrado.** La aplicación de escritorio de Discord tiene que estar abierta en el mismo equipo. ¿La abriste después del juego? El estado aparece en el siguiente cambio de pantalla
- **La actividad está oculta.** En Discord: `User Settings` -> `Activity Privacy` -> comparte tus actividades detectadas
- **Un nivel propio no muestra nombre.** Es intencionado: solo se nombra un nivel de Workshop o uno que viene con el juego, y el editor nunca nombra su nivel. Por qué - [[game-privacy-policy#Discord Rich Presence]]
