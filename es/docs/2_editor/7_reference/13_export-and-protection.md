---
title: Exportación y protección
date: 2026-10-11
tags: [level_author]
---

# Exportación y protección

Exportar guarda el nivel fuera del juego como carpeta o archivo comprimido, junto con todos los archivos que usa. Una contraseña cifra el contenido del nivel en el disco, y una contraseña olvidada no se puede recuperar

## Exportar el nivel

Está en la pestaña `{{ui:settings_level-settings_publication}}` de la configuración del nivel: el destino `{{ui:editor_share_archive}}`, el modo en `{{ui:editor_share_format}}`, y `{{ui:editor_share_passphrase}}` para un modo protegido. Más - [[17_publishing]]

Un archivo comprimido lleva el nivel, sus metadatos y todos los archivos que usa.
Una canción que vive fuera de la carpeta del nivel también se copia dentro. Su referencia se redirige a la copia del archivo comprimido

La carpeta `ai` del nivel, donde un asistente de IA guarda sus notas sobre el nivel, también se empaqueta, salvo que `{{ui:settings_level-settings_metadata-level-ai-share}}` esté desmarcado en los metadatos del nivel. Un modo con contraseña nunca la empaqueta: unas notas de diseño legibles junto a un nivel cifrado anularían la contraseña. El informe avisa cuando la carpeta se dejó fuera. Más - [[7_ai-assistant#La carpeta ai]]

| `{{ui:editor_share_format}}` | Qué obtienes | Con qué se abre |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_folder}}` | la misma carpeta que el nivel tiene en el disco. Comprímela y envíala | no hace falta nada |
| `{{ui:settings_level-settings_export-mode_folder-protected}}` | la misma carpeta, con el documento del nivel cifrado. Los metadatos, la portada y los medios siguen siendo legibles, así que un explorador de niveles sigue mostrando su ficha | gpg para el documento del nivel |
| `{{ui:settings_level-settings_export-mode_zip}}` | un solo archivo | un doble clic en el Explorador de Windows, sin instalar nada |
| `{{ui:settings_level-settings_export-mode_targz}}` | un solo archivo | cualquier compresor |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | un zip con su propio cifrado AES-256. El significado habitual de una contraseña en un archivo comprimido | 7-Zip o cualquier otro compresor, que pide la contraseña |
| `{{ui:settings_level-settings_export-mode_zip-protected}}`, `{{ui:settings_level-settings_export-mode_targz-protected}}` | el mismo archivo comprimido envuelto en `.gpg` | gpg |

El Explorador de Windows no abre ninguna de las opciones con contraseña. Es el precio de la contraseña

Una colección o un solo recurso de la Biblioteca admiten los mismos cinco modos de archivo comprimido, incluidos los de contraseña. Los dos modos de carpeta son solo para un nivel. Más - [[17_publishing#Archivo comprimido]]

> [!tip] Consejo
> Todo lo que no pudo viajar (un recurso detrás de una URL, un archivo al que nada hace referencia) aparece en el informe después de la exportación

> [!warning] Advertencia
> Una contraseña protege el contenido durante el envío y frente a la copia casual. No es DRM: cualquiera que tenga el archivo y la contraseña siempre puede abrirlo

## Proteger el nivel

Cifra el documento del nivel en el disco. Al abrir el nivel se pide la contraseña

Lo que se protege es el **contenido**: objetos, fotogramas clave, temas.
Los metadatos, la portada y los medios siguen siendo legibles. Por eso el explorador de niveles sigue mostrando la ficha del nivel sin la contraseña

La contraseña se pide una vez por sesión y se guarda solo en memoria.
Nunca se escribe en ningún sitio, así que el autoguardado sigue funcionando

Para quitar la protección, deja el campo vacío y haz clic en `{{ui:settings_level-settings_protect-apply}}`

> [!caution] Precaución
> Una contraseña olvidada no se puede recuperar. No se guarda ninguna clave en ningún sitio, y sin ella no hay manera de entrar en el archivo
