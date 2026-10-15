---
title: Argumentos de inicio
date: 2026-10-15
tags: [advanced_player, developer]
---

# Argumentos de inicio

Los argumentos de inicio abren de inmediato una pantalla, un nivel o una partida, y los interruptores cambian un solo inicio del juego. Van después del ejecutable: en un acceso directo, en una terminal o en las opciones de lanzamiento de Steam

Sin argumentos, el juego abre el menú principal

Un asistente de IA conectado por MCP puede enviar los mismos argumentos a un juego que ya está abierto - [[7_ai-assistant]]

## Sintaxis

- cada argumento empieza con dos guiones: `--editor`
- un valor va después de un espacio o después de `=`: `--speed 1.5` y `--speed=1.5` son lo mismo
- las mayúsculas y minúsculas de la clave dan igual: `--Editor` también funciona
- los números usan punto sea cual sea el idioma del sistema: `1.5`, nunca `1,5`
- un valor con espacios va entre comillas dobles: `--level "D:\My Levels\Volcano"`

**Un argumento que el juego no puede usar nunca detiene el inicio.** Se descarta, se escribe una línea sobre él en el log, y el juego abre su pantalla habitual. Dónde está el log - [[11_help#Logs]]

**Los argumentos desconocidos se ignoran.** El juego solo lee sus propios argumentos, los de dos guiones. Los argumentos propios de Unity, de un guion, por ejemplo `-screen-width`, pasan sin tocarse. La resolución y la pantalla completa se fijan con ellos

## Pantallas

| Argumento | Qué se abre |
|---|---|
| `--menu` | el menú principal, lo mismo que sin argumentos |
| `--editor` | el editor de niveles |
| `--game` | el nivel indicado en `--level`, y la partida empieza al momento |
| `--settings` | el menú principal con la pantalla de configuración encima |

Se pasa como mucho un argumento de pantalla. Dos distintos se anulan entre sí, y se abre el menú con una advertencia en el log

`--settings` puede indicar una pestaña: `general`, `audio`, `controls`, `keybindings`, `graphics`, `interface`, `game-editor`, `profile`, `other`. Sin nombre, la configuración se abre en la pestaña en la que estuviste la última vez. Un nombre desconocido se descarta, y la configuración se abre igualmente

La configuración se abre una vez por inicio. Si más tarde vuelves al menú, no se abre de nuevo. Qué contiene cada pestaña - [[4_settings]]

## Elegir un nivel

`--level` indica un nivel por su identificador (`LevelId`) o por la ruta de su carpeta. Un título nunca funciona: los títulos se repiten, se traducen y se editan. Un valor que se puede leer como identificador siempre se toma como identificador

El nivel se busca entre los que el juego ya muestra en su lista. El juego no encuentra una carpeta que no esté en la lista

| Junto con | Qué pasa |
|---|---|
| nada | el menú se abre en la pantalla del nivel y espera a `{{ui:menu_levelview_play-btn}}` |
| `--editor` | el editor se abre con este nivel |
| `--game` | la partida empieza al momento |

Una contraseña nunca se pasa como argumento. Un nivel protegido la pide en pantalla y se abre después de la respuesta

## Condiciones de la partida

Estas condiciones rellenan los controles de la pantalla del nivel, y la partida empieza como si hubieras pulsado `{{ui:menu_levelview_play-btn}}`. Solo funcionan junto con `--game`. Sin él se ignoran, con una advertencia en el log

| Argumento | Valor | Control en la pantalla del nivel |
|---|---|---|
| `--speed` | más de `0` y hasta `2`, redondeado a `0.1` | `{{ui:field_common_speed}}` |
| `--lives` | de `0` a `16`, `0` es `{{ui:menu_levelview_options-lifes_option-zen}}` | `{{ui:menu_levelview_options-lifes_title}}` |
| `--seed` | `0` o un entero positivo, `0` significa una semilla nueva en cada partida | `{{ui:level_level-view_seed-value}}` |
| `--bot` | `none`, `reflex`, `warm` | `{{ui:menu_levelview_options-bot}}` |
| `--checkpoints`, `--no-checkpoints` | - | `{{ui:menu_levelview_options-checkpoints_title}}` |
| `--no-collision` | - | `{{ui:menu_levelview_options-no-collision_title}}` |

Una condición que se omite toma su valor predeterminado: 3 vidas, velocidad `1.0`, checkpoints activados, sin bot, semilla `0`, colisiones activadas

Una partida iniciada así es una partida normal. Entra en las estadísticas como cualquier otra, [[10_statistics]]

## Interruptores para todo el inicio

Estos tres funcionan con cualquier pantalla y nunca cambian una configuración guardada:

| Argumento | Qué hace |
|---|---|
| `--autosave on`, `--autosave off` | activa o desactiva el autoguardado del editor en este inicio. La pestaña de configuración `{{ui:settings_game-editor_title}}` muestra el valor forzado y no deja cambiarlo |
| `--suppress-game-saves` | el modo anónimo durante todo el inicio. No se puede desactivar en el juego, [[4_settings#Modo anónimo]] |
| `--frame-stats` | escribe en el log un resumen de los tiempos de fotograma, con el tiempo de GPU y de CPU. Sirve para medir el rendimiento |
| `--frame-stats-windows` | mientras se juega un nivel, también escribe una línea cada {{v:performance.window-hop-seconds}} s de juego: el fotograma del nivel y la mediana del tiempo de CPU y de GPU. También activa `--frame-stats`. Sirve para comprobar [[17_performance-rating]] |

`--frame-stats` escribe una línea por pantalla cada 30 segundos, y también cada vez que cambia la ventana que está encima de la pantalla. Los primeros 3 segundos de una pantalla no se cuentan

## Combinaciones

| Comando | Resultado |
|---|---|
| nada o `--menu` | menú |
| `--editor` | el editor sin ningún nivel abierto |
| `--settings` | menú, con la configuración abierta en la pestaña en la que estuviste la última vez |
| `--settings graphics` | lo mismo, en la pestaña `{{ui:settings_graphics_title}}` |
| `--level X` | menú en la pantalla del nivel X, espera a `{{ui:menu_levelview_play-btn}}` |
| `--level X --game` | el nivel X, con una partida en curso |
| `--level X --editor` | el editor con el nivel X abierto |
| `--game` sin `--level` | menú y una advertencia |
| `--menu --editor` | menú y una advertencia |
| `--speed 2` sin `--game` | la condición se ignora, con una advertencia |
| `--editor --autosave off` | el editor, con el autoguardado desactivado solo en este inicio |
| `--autosave maybe` | se ignora con una advertencia, decide tu configuración |
| `--suppress-game-saves` | menú. Ninguno de los guardados propios del juego de este inicio llega al disco |
| `--level X --game --suppress-game-saves` | el nivel X, con una partida en curso, y no quedan estadísticas después |
| `--editor --suppress-game-saves` | el editor. Se escriben los guardados de niveles, el autoguardado y las copias de seguridad, la configuración y las estadísticas no |

## Ejemplos

En Windows, desde una terminal o un acceso directo:

```bash
"Bullet Hero.exe" --editor
"Bullet Hero.exe" --level 5f2b0e6a-1c3d-4b5e-8a9f-0d1e2f3a4b5c --game --lives 1 --speed 1.5
"Bullet Hero.exe" --level "C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero\levels\Volcano" --editor
```

En Steam, las opciones de lanzamiento del juego solo llevan los argumentos, sin el ejecutable: `--editor --autosave off`

## Android

Android no tiene línea de comandos. Los argumentos se pasan en el extra de texto `bh` del intent que inicia el juego, y se separan exactamente igual que una línea escrita. Desde un equipo se hace con `adb`:

```bash
adb shell "am start -S -n com.vertoker.BulletHero/com.unity3d.player.UnityPlayerGameActivity -e bh '--frame-stats --editor'"
```

- **Las comillas importan.** Todo el `am start` va entre comillas dobles, y el valor de `bh` entre comillas simples. Si no, el shell del dispositivo divide la línea: solo el primer argumento llega a `bh`, y el resto va a `am` como sus propios parámetros
- **`-S` primero detiene el juego abierto.** Los argumentos se leen una sola vez, al iniciar. Enviarlos a un juego que ya está abierto no cambia nada

iOS no tiene argumentos de inicio en absoluto
