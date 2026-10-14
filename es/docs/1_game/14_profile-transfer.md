---
title: Transferencia de perfil
date: 2026-10-14
tags: [player]
---

# Transferencia de perfil

Todo tu perfil cabe en un solo archivo zip: niveles, estadísticas, configuración y la biblioteca. Expórtalo antes de reinstalar o de pasar a otro dispositivo, y luego impórtalo allí

Los botones están en `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_profile-transfer_title}}`. Funciona en Windows, Mac, Linux y Android. No está disponible en iOS

## Qué entra en el archivo

| Parte | En la carpeta de datos | Marcada por defecto |
|---|---|---|
| `{{ui:settings_profile-transfer_category-levels}}` | `levels` | sí |
| `{{ui:settings_profile-transfer_category-statistics}}` | `stats` | sí |
| `{{ui:settings_profile-transfer_category-settings}}` | `settings.json` | sí |
| `{{ui:settings_profile-transfer_category-library}}` | `resources` | sí |
| `{{ui:settings_profile-transfer_category-skins}}` | `skins` | sí |
| `{{ui:settings_profile-transfer_category-backups}}` | `backups` | no |
| `{{ui:settings_profile-transfer_category-reports}}` | `reports` | no |
| `{{ui:settings_profile-transfer_category-recordings}}` | `recordings` | no |

El archivo es un zip normal y se abre con cualquier compresor. Dentro están las mismas carpetas que en la carpeta de datos ([[1_installation]]), más `profile.json`, que describe el archivo

## Exportar

1. Pulsa `{{ui:settings_profile-transfer_export}}`
2. Marca las partes que necesitas
3. Elige dónde guardar el archivo

Exportar funciona en cualquier sitio donde se abra la configuración: en el menú principal, en una partida en pausa y en el editor. Las estadísticas se escriben antes en el disco, así que el archivo está al día

## Importar

1. Abre la configuración desde el menú principal y pulsa `{{ui:settings_profile-transfer_import}}`
2. Elige el archivo zip
3. Marca las partes y elige el modo
4. Confirma

Importar solo funciona desde el menú principal. Un nivel en curso o un editor abierto mantienen sus archivos en uso, y no se pueden sustituir mientras tanto

| Modo | Qué pasa |
|---|---|
| `{{ui:settings_profile-transfer_mode-replace}}` | cada parte marcada se vacía y se rellena desde el archivo |
| `{{ui:settings_profile-transfer_mode-merge}}` | los niveles se añaden. Un nivel que está en los dos lados se sustituye entero por la copia más nueva. Las estadísticas conservan el valor mayor de cada contador y el mejor récord. Los archivos de la biblioteca, los autoguardados y los informes solo se añaden, los tuyos se quedan |

Cada importación vuelve a preguntar antes de escribir nada. Un reemplazo nombra las partes que vacía, una fusión dice cuántos niveles añade, sustituye y conserva

**Configuración de otro tipo de dispositivo.** Un perfil de un teléfono importado en un PC (o al revés) conserva tus propios controles y gráficos. Todo lo demás viene del archivo

El juego rechaza un archivo de una versión más nueva del juego: actualiza antes el juego. También rechaza un archivo que no es un zip, un zip que no es un perfil, un zip con contraseña y un archivo dañado. En ninguno de estos casos se cambia nada

## Copia de seguridad

Antes de cualquier importación, el juego guarda en una copia de seguridad las partes que está a punto de sustituir. Está en la carpeta `profile-backups`, dentro de la carpeta de datos. Solo hay una: la siguiente importación la sobrescribe

- `{{ui:settings_profile-transfer_backup-restore}}` vuelve a poner la copia de seguridad. Lo que sustituye pasa a ser la nueva copia de seguridad, así que una restauración también se puede deshacer
- `{{ui:settings_profile-transfer_backup-save-as}}` guarda una copia donde elijas
- `{{ui:settings_profile-transfer_backup-delete}}` la elimina
- `{{ui:settings_profile-transfer_clear-cache}}` elimina toda la carpeta `profile-backups`: la copia de seguridad y lo que haya dejado una transferencia interrumpida

`{{ui:settings_profile-transfer_backup-to-folder}}` está marcado por defecto durante una importación: el juego pregunta en ese momento dónde guardar una copia fuera del juego

> [!caution] Precaución
> En Android, la copia de seguridad está en la carpeta de datos del juego y se borra junto con el juego. Antes de desinstalar, exporta el perfil o guarda la copia de seguridad en otro sitio

Si el juego se cierra a mitad de una importación, el siguiente inicio deja el perfil como estaba

## Steam Cloud

En la versión de Steam tu perfil sigue a tu cuenta de Steam por sí solo. No hay ningún botón: el juego se sincroniza una vez al iniciarse, envía lo que cambia mientras juegas y se sincroniza una última vez al cerrarse

El interruptor es de Steam: la casilla Steam Cloud en las propiedades del juego en Steam. Si está activada y cuándo fue la última sincronización se muestra en `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_cloud_title}}`

| Parte | Cuando la cambiaron los dos dispositivos |
|---|---|
| `{{ui:settings_profile-transfer_category-statistics}}` | cada contador conserva el valor mayor y el mejor récord, no se pierde nada |
| `{{ui:settings_profile-transfer_category-settings}}` | gana la copia más reciente. `{{ui:settings_graphics_title}}` y `{{ui:settings_controls_title}}` siempre siguen siendo los de cada dispositivo |
| `{{ui:settings_profile-transfer_category-levels}}` | la copia más reciente de un nivel gana entera. La otra va a las copias de seguridad del editor en el dispositivo donde perdió |
| `{{ui:settings_profile-transfer_category-library}}` | gana la copia más reciente de cada archivo |
| `{{ui:settings_profile-transfer_category-skins}}` | gana la copia más reciente de cada archivo |

- Un nivel eliminado en un dispositivo se elimina también en los demás. Cada uno guarda su último estado en las copias de seguridad del editor
- Las estadísticas eliminadas en un dispositivo se eliminan también en los demás. Si otro dispositivo jugó después de la última sincronización, su progreso se conserva
- Un nivel más grande que el espacio que Steam deja al juego se queda solo en su dispositivo
- `{{ui:settings_profile-transfer_category-backups}}`, `{{ui:settings_profile-transfer_category-reports}}` y `{{ui:settings_profile-transfer_category-recordings}}` no se sincronizan
- Una copia en la nube escrita por una versión más nueva del juego no se toca hasta que actualices el juego en este dispositivo
- El nivel abierto en el editor no se reemplaza: se sincroniza en el siguiente inicio
- Con `{{ui:settings_other_suppress-game-saves}}` activado no se sincroniza nada

## Cambiar de versión en Android

Una copia del juego instalada desde un archivo (itch.io y similares) no se puede actualizar desde Google Play, ni al revés. Las versiones están firmadas de forma distinta, así que Android rechaza la actualización. Para cambiar:

1. Exporta el perfil y guarda el archivo fuera del juego
2. Desinstala el juego
3. Instala la otra versión
4. Importa el perfil
