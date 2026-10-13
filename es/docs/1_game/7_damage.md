---
title: Daño y vidas
date: 2026-10-02
tags: [advanced_player]
---

# Daño y vidas

Cada impacto cuesta una vida, empuja al avatar hacia atrás durante {{v:avatar.knockback-time}} s y da {{v:avatar.damage-timeout}} s de invulnerabilidad. Por defecto, una muerte rebobina el nivel hasta el último checkpoint y restaura tus vidas

## Un impacto en tres etapas

1. **El empujón, `{{v:avatar.knockback-time}}` s.** Lo que te golpeó te lanza lejos de sí a `{{v:avatar.knockback-speed}}` unidades por segundo. Son unas {{v:avatar.knockback-distance}} unidades, un dash entero, tres cuartas partes del alto de la pantalla predeterminada. Durante ese tiempo no se acepta la entrada. No puedes salir del empujón con un dash: el retroceso se impone a todo
2. **El control vuelve** después de esos {{v:avatar.knockback-time}} s
3. **Nada puede alcanzarte** durante `{{v:avatar.damage-timeout}}` s a partir del momento del impacto. Cualquier impacto dentro de ese segundo se ignora

Si estás justo encima de lo que te golpeó, no hay hacia dónde empujar. Entonces no hay retroceso en absoluto

Tampoco pueden alcanzarte mientras apareces (`{{v:avatar.spawn-time}}` s) ni durante los `{{v:avatar.dash-invulnerability}}` s de protección del dash, [[6_avatar]]

> [!info] Conviene saber
> Quedarse dentro de una zona de peligro cuesta una vida, no diez. Un empujón hacia una segunda zona de peligro también se puede sobrevivir. Una ráfaga densa parece una muerte instantánea, pero a menudo cuesta menos que una sola bala que llega justo al final del segundo de protección

## Vidas

El número de vidas se elige en la pantalla del nivel: `{{ui:menu_levelview_options-lifes_option-zen}}`, `{{ui:menu_levelview_options-lifes_option-one}}`, `{{ui:menu_levelview_options-lifes_option-three}}` o `{{ui:menu_levelview_options-lifes_option-custom}}` hasta 16, [[2_playing-levels]]

Cada impacto cuesta una vida. Un impacto que se lleva la última es una muerte.
`{{ui:menu_levelview_options-lifes_option-zen}}` reacciona a los impactos como cualquier otra partida (el empujón, el anillo de escudo, la explosión de partículas y el segundo de protección funcionan como siempre, y el impacto cuenta en las estadísticas), pero nunca se gasta una vida, así que la partida nunca termina

Tus vidas se muestran en el anillo de puntos alrededor del avatar: un punto encendido es una vida en reserva, uno apagado es una vida gastada.
La ventana de resultados muestra `{{ui:game_game-result_hits}}` y `{{ui:game_game-result_lives-left}}`

## Qué hace una muerte

Por defecto, una muerte no termina la partida:

1. El reloj del nivel se detiene suavemente a lo largo de `{{v:checkpoint.rewind-time}}` s de tiempo real. La música decae con él
2. El nivel salta hacia atrás hasta el último checkpoint alcanzado. Las vidas se restauran
3. El reloj vuelve a acelerar suavemente hasta la velocidad de la partida durante otros `{{v:checkpoint.rewind-time}}` s. Durante la aceleración nada puede alcanzarte, porque si no, un checkpoint junto a un sitio peligroso se llevaría todas tus vidas en el primer segundo

La pausa también detiene esta aceleración

Si `Checkpoints` está desactivado en la pantalla del nivel, el rebobinado va al inicio del nivel

Para que una muerte abra la ventana de resultados, activa `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_open-menu-on-lose}}`. Entonces la reproducción se detiene.
Desde esa ventana, `{{ui:game_game-result_restart-checkpoint}}` empieza un nuevo intento desde el checkpoint alcanzado

## Checkpoints

Los checkpoints los coloca el autor del nivel. Si cuentan o no lo decides tú, con el interruptor `Checkpoints`

El checkpoint alcanzado es el último que está en la posición actual del nivel o antes. Por eso volver a él no deshace nada, solo rebobina

El autor puede hacer que un checkpoint restaure la salud. Entonces, al cruzarlo, tus vidas se restauran una vez, en plena partida

La barra de progreso de la parte inferior de la pantalla tiene una marca en cada checkpoint. La barra se activa en `{{ui:settings_interface_label}}` → `{{ui:settings_interface_show-game-progress}}`

Los récords con checkpoints y sin ellos se guardan por separado, [[10_statistics]]

## Sin colisiones

`{{ui:menu_levelview_options-no-collision_title}}` es un interruptor independiente de `{{ui:menu_levelview_options-lifes_option-zen}}`, junto a `Checkpoints` en la pantalla del nivel y en el panel de inicio del editor. Actívalo y el avatar atraviesa todo: ya nada puede tocarlo

Una partida `{{ui:menu_levelview_options-no-collision_title}}` guarda sus propios récords, aparte de `{{ui:menu_levelview_options-lifes_option-zen}}` y de las partidas normales, y la ventana de resultados la marca añadiendo `· Sin colisiones` al valor de `{{ui:menu_levelview_options-lifes_title}}`, [[10_statistics]]
