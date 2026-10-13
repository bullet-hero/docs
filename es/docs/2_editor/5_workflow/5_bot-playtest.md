---
title: Cómo juega un bot tu nivel
date: 2026-10-02
tags: [level_author]
---

# Cómo juega un bot tu nivel

Un bot juega el nivel con los mismos controles que tú y comprueba la legibilidad, no la dificultad. No garantiza que el nivel se pueda superar

Observa lo que vuela, busca espacio libre y mueve el mismo personaje que tú.
Camina, hace dash, recibe daño y muere

El bot se elige antes de empezar un nivel, junto a las vidas y la velocidad

## Un bot en el editor

En el editor, un bot dirige al jugador de prueba:
1. Abre `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_player_title}}`
2. Marca `{{ui:settings_game-editor-player_bot}}`
3. Activa el jugador de prueba en la barra de herramientas

El jugador de prueba no permite elegir bot, siempre es `{{ui:enum_bot-kind_reflex}}`. Solo este bot no necesita nada preparado de antemano.
Sigue funcionando mientras editas el nivel, a cualquier velocidad de reproducción, hacia atrás incluida

Justo después de arrastrar el cabezal, el bot juega peor durante un momento: vuelve a aprender lo que tiene por delante

Mientras arrastras un asa del gizmo o escribes en un campo de texto, el jugador de prueba no atiende a tus controles

**`{{ui:settings_game-editor-player_bot-debug}}`** en la misma configuración dibuja sobre el nivel. Está desactivado por defecto y sus tres partes están activadas, así que en cuanto lo activas ves el cuadro completo de una vez:
- `{{ui:settings_game-editor-player_bot-debug-grid}}` - cuánto espacio libre cree el bot que tiene cada parte de la pantalla. El rojo es donde espera un impacto, y el color se desvanece a medida que crece el espacio. No se dibuja nada donde se considera a salvo
- `{{ui:settings_game-editor-player_bot-debug-target}}` - el punto hacia el que se dirige. Un objetivo que no se mueve significa que el bot está conforme, no atascado
- `{{ui:settings_game-editor-player_bot-debug-reach}}` - hasta dónde espera llegar: el anillo interior caminando, el exterior con un dash. Nunca elige un objetivo fuera de ellos

Solo se dibuja `{{ui:enum_bot-kind_reflex}}`. Actívalo en pausa, donde la imagen se queda quieta

**Una partida completa con cualquier bot.** En la configuración del nivel, en la pestaña `{{ui:settings_level-settings_play}}`, está la misma lista `{{ui:settings_level-settings_bot}}` que en la pantalla del nivel del menú: `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}`, `{{ui:enum_bot-kind_warm}}`. Esto inicia una partida real del nivel, no el jugador de prueba

## Leer el resultado

Un bot comprueba la legibilidad, no la dificultad:
- el bot supera con calma una sección que a ti te cuesta. Entonces la sección se lee bien, y lo que te falta es práctica
- el bot recibe un impacto en el mismo sitio una y otra vez. Mira ese sitio: normalmente es un peligro que no deja espacio para escapar. Una persona no lo leerá mejor

## Qué promete un bot y qué no

**Un bot no garantiza que el nivel se pueda superar.** Es un jugador que no se cansa, no un jugador que no pierde.
Si una sección exige entrar bien en un patrón un segundo antes de que llegue, el bot recibirá un impacto. No es un error

> [!info] Conviene saber
> Un bot no puede hacer trampas, así está construido. Tiene los mismos controles que un jugador y nada más: la misma velocidad, el mismo dash, la misma hitbox, el mismo daño. Donde un jugador no puede pasar, el bot tampoco

**Un bot carga el dispositivo.** Busca espacio libre en cada fotograma.
En un dispositivo débil, cuenta con caídas de fotogramas. En un nivel pesado, los primeros segundos serán los peores

## Un nivel que ha vencido al bot

Los bots solo mejoran con niveles que todavía no han visto. Los niveles que un bot ya supera no le enseñan nada

¿Tu nivel ha vencido al bot? Envíalo:
1. Abre un issue en [bullet-hero/releases](https://github.com/bullet-hero/releases/issues)
2. Escribe qué bot perdió y dónde
3. Adjunta la carpeta del nivel

A continuación: [[1_readability-and-fairness|Legibilidad y justicia]], [[3_difficulty-curve|Dificultad]]
