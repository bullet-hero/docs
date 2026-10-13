---
title: Servidor para amigos
date: 2026-10-01
tags: [server_host]
---

# Servidor para amigos

Necesitarás las herramientas abiertas del servidor, la compilación completa del juego para cada jugador y un archivo PublishProfile. La moderación y el respeto de las licencias de los niveles corren a cargo del dueño del servidor

> [!warning] Advertencia
> Las herramientas del servidor no se han publicado, el protocolo no está diseñado. Esta página recoge solo lo que ya está decidido

## Qué necesitarás

- **Herramientas del servidor.** Serán abiertas, bajo MIT. Es el mismo código con el que funciona el servidor oficial. Puedes montar tu propio servidor con estas herramientas o con cualquier cosa basada en ellas
- **La compilación completa del juego para todos los que se conecten.** Las compilaciones de Google Play y App Store no se conectan a servidores comunitarios. La compilación completa está en [GitHub](https://github.com/bullet-hero/releases) y en el sitio web del proyecto
- **Un perfil de publicación.** El archivo `PublishProfile` decide qué niveles acepta tu servidor. Más - [[7_publish-profiles]]
- **Una máquina para el servidor.** Los requisitos del sistema, el entorno de ejecución, los puertos y la forma de iniciarlo todavía no se conocen

## Perfil de publicación

El perfil fija qué licencias se aceptan, de dónde puede obtener archivos un nivel y cuál es su límite de tamaño.
Para eso no hace falta cambiar código

El servidor oficial funciona con el preset `standard`, que se fija en la configuración del servidor. Empieza por él y relájalo o endurécelo a tu medida

## Qué asumes

- **La moderación.** Bullet Hero no modera los servidores comunitarios. El EULA de la compilación completa se lo dice a cada jugador
- **Nada de comercio.** De forma predeterminada un nivel se distribuye bajo *CC BY-NC*, y el autor puede elegir otra licencia. Respeta la licencia de cada nivel. Un nivel bajo *CC BY-NC* puede alojarse y compartirse gratis, pero no puedes cobrar por él ni ganar dinero con él de ninguna otra forma
- **Los derechos sobre los recursos.** Un nivel puede contener música y gráficos ajenos. Con qué rigor comprobarlo lo decide tu perfil. Pero una reclamación por una obra ajena te llegará a ti. Las reglas del servidor oficial - [[ugc-licensing-policy]]

El permiso para la distribución no comercial lo da el autor de cada nivel, no el juego. Por eso solo el autor puede hacer una excepción

## Qué no se sabe

- cómo encuentra el juego un servidor y cómo se conecta a él
- si un servidor comunitario tendrá cuentas
- cómo se suben los niveles y cómo llegan a la lista
- si un servidor para unas pocas personas se configurará de otra forma que uno público

Lo que ya existe para un servidor grande - [[3_advanced-hosting]]
