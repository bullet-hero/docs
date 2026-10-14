---
title: Logros
date: 2026-10-14
tags: [player]
---

# Logros

Los logros se desbloquean solos a partir de tus estadísticas. Solo cuentan los niveles creados por otras personas y solo las partidas jugadas de forma justa. La lista está en el menú principal, en `{{ui:menu_main_achievements-btn}}`

## La lista

`{{ui:menu_main_achievements-btn}}` en el menú principal abre todos los logros de tu versión, por grupos. Uno bloqueado muestra cuánto te falta, uno desbloqueado muestra el día en que se desbloqueó. Un logro secreto aparece como `{{ui:menu_achievements_hidden_name}}` hasta que se desbloquea

## Qué cuenta

**Una partida justa** es aquella en la que:

- no juega ningún bot
- las colisiones están activadas
- la velocidad es `{{v:achievements.fair-min-speed}}` o mayor
- tienes vidas: una partida en `{{ui:menu_levelview_options-lifes_option-zen}}` solo cuenta donde un logro lo pide

Los checkpoints están permitidos. Una partida iniciada desde el editor nunca cuenta, tampoco establece récord - [[10_statistics]]

**Que no sea tu propio nivel.** Un nivel que abriste en el editor en este dispositivo es tuyo. Superarlo solo cuenta para el logro de probar tu propio nivel. Los niveles incluidos, los del Workshop y los de tus amigos cuentan

## Dónde se guarda

`stats/achievements.json`, junto a las estadísticas. Solo recuerda cuándo se desbloqueó cada logro. Si un logro está desbloqueado se decide cada vez a partir de las estadísticas, así que el archivo no se puede perder: bórralo y en el siguiente inicio vuelve todo lo que ganaste, con la fecha de ese día

Borrar las estadísticas en los ajustes conserva tus logros. La transferencia de perfil y Steam Cloud llevan el archivo: dos dispositivos acaban con todos los logros que cualquiera de los dos desbloqueó - [[14_profile-transfer]]

## Steam

En una versión de Steam cada logro también se desbloquea en Steam, y Steam muestra su propia notificación. Gana el registro de Steam: un logro que Steam tiene se desbloquea en el juego con la fecha de Steam. Uno que el juego tiene y Steam no se desbloquea de nuevo si tus estadísticas todavía lo justifican

Las demás versiones muestran la notificación propia del juego en la parte superior de la pantalla
