---
title: Preguntas frecuentes
date: 2026-10-02
tags: [player, level_author]
---

# Preguntas frecuentes

Bullet Hero es un híbrido gratuito de juego de ritmo y bullet hell. No hace falta cuenta y todavía no hay servidor. Los jugadores crean los niveles en el editor integrado y se los pasan como carpeta o como archivo comprimido

## El juego

### ¿Qué es Bullet Hero?

Un híbrido de *juego de ritmo* y *bullet hell*. Un nivel es música y formas que se mueven con ella. Controlas un pequeño cuadrado, y tiene que sobrevivir hasta el final de la canción

Bullet Hero se construye como un motor para el género. Por eso la mayoría de los niveles los crean los jugadores en el editor integrado.
Más - [[1_game/index]]

### ¿El juego es gratuito?

Sí. El juego no tiene compras, ni anuncios, ni contenido de pago.
Más - [[1_licensing-basics]]

### ¿Dónde se consigue?

Todas las compilaciones y tiendas - [[download]]

El juego ya está publicado, versión `gv {{v:version.gv}}`. Las compilaciones no están firmadas

### ¿Hace falta una cuenta o internet?

No. No hay cuentas ni servidor, y el juego no envía nada a ningún sitio

Internet solo lo necesita un tipo de nivel: el que carga un archivo desde la dirección web de su autor.
Más - [[1_installation]]

### ¿Dónde se guardan los niveles?

En la carpeta `levels`, dentro de la carpeta de datos del juego. Para abrirla: `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general-open_folder}}`.
Más - [[1_installation]]

## Jugar niveles

### ¿Cómo se juega un nivel que te han enviado?

Pon la carpeta en `levels` y haz clic en `{{ui:root_level-browser_refresh}}` en la lista de niveles.
Un archivo comprimido (`.zip`, `.tar.gz`) se abre desde el editor, con el generador `{{ui:gen_level_archive}}`.
Más - [[2_playing-levels]]

### El juego dice que el nivel es de una versión más nueva. ¿Qué hago?

Actualiza el juego. Una versión antigua no abre archivos de una más nueva, para no leerlos nunca de forma incorrecta.
Más - [[5_troubleshooting]]

### ¿Se puede recuperar la contraseña olvidada de un nivel?

No. La clave no se guarda en ningún sitio: ni en el juego, ni en el archivo, ni en manos de nadie.
Más - [[5_troubleshooting]]

### ¿Puede el juego pasarse un nivel por sí solo?

Sí, con la condición `{{ui:menu_levelview_options-bot}}` en la pantalla del nivel: `{{ui:enum_bot-kind_reflex}}` o `{{ui:enum_bot-kind_warm}}`. Un bot tiene los mismos controles que tú, y también puede perder.
Más - [[9_bots]]

## Crear niveles

### ¿Cómo se crea un primer nivel?

`{{ui:menu_main_editor-btn}}` en el menú principal, luego `{{ui:settings_editor-settings_editor-settings}}`, luego `{{ui:settings_editor-settings_create-level}}`.
Copia una canción en la carpeta del nivel, fija el tempo (BPM), coloca un objeto con dos fotogramas clave y haz una prueba de juego.
Más - [[2_first-level]]

### ¿Qué archivos de música funcionan?

`ogg`, `mp3` y `wav`, nada más. `flac`, `aiff` y los módulos de tracker no se cargan

`ogg` es la mejor opción. Ocupa 8-10 veces menos que `wav` y, a diferencia de `mp3`, no añade silencio al principio.
Más - [[2_preparing-the-track]]

### ¿Puedo usar cualquier canción?

En tu propio disco no se comprueba nada. La licencia de la música importa cuando un nivel se ofrece a un servicio, y todavía no existen esos servicios.
Más - [[1_licensing-basics]]

### ¿Cómo se comparte un nivel?

A mano, como carpeta o como archivo comprimido. Una compilación de Steam también puede publicar un nivel en Steam Workshop. Todavía no hay servidor oficial.
Más - [[6_sharing-by-hand]], [[17_publishing]]

## El proyecto

### ¿Hay clasificaciones en línea o un catálogo de niveles?

Todavía no. El servidor oficial y los servidores de la comunidad están en desarrollo.
Más - [[4_server/index]]

### ¿Por qué el código del juego es cerrado?

Tengo motivos personales para ello.
Cuando el desarrollo se detenga definitivamente, todos los repositorios pasarán a ser abiertos, y la organización [bullet-hero](https://github.com/bullet-hero) quizá pase a manos de otra persona

El SDK, la documentación y el futuro servidor ya son abiertos. Más - [[index]]

### ¿Has encontrado un error?

Informa de los errores del juego en [bullet-hero/releases](https://github.com/bullet-hero/releases/issues). Las preguntas, en [Discord](https://discord.gg/gkHQrp9NgS).
Dónde escribir y qué adjuntar - [[11_help]]

Todos los enlaces del proyecto - [[links]]
