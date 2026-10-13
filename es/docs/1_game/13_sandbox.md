---
title: Sandbox y tutorial
date: 2026-10-02
tags: [player]
---

# Sandbox y tutorial

El sandbox es una arena del menú principal donde puedes mover el avatar, lanzarte cualquiera de los seis ataques y hacer el tutorial de seis pasos. No hace falta ningún nivel

En el primer inicio, el juego ofrece el tutorial una vez: `{{ui:menu_tutorial-offer_confirm}}` abre el sandbox en el tutorial, `{{ui:menu_tutorial-offer_cancel}}` cierra la oferta para siempre. El sandbox en sí sigue en el menú en cualquier caso

## El panel

El sandbox tiene un panel a la izquierda. Haz clic en su asa para contraer el panel, o arrastra el asa para hacerlo más ancho o más estrecho. El panel tiene cinco pestañas:

| Pestaña | Qué hace |
|---|---|
| `{{ui:sandbox_tab_home}}` | qué es el sandbox y qué hace cada pestaña |
| `{{ui:sandbox_tab_tutorial}}` | los pasos del tutorial y qué hacer ahora mismo |
| `{{ui:sandbox_tab_controls}}` | el modo del dispositivo con el que guías ahora mismo, el interruptor del sensor de movimiento y un acceso a toda la configuración de controles |
| `{{ui:sandbox_tab_attacks}}` | lanza cualquiera de los seis ataques a mano o deja que las oleadas lleguen solas |
| `{{ui:sandbox_tab_game}}` | las vidas, la velocidad de los ataques, el bot y la cámara libre |

`{{ui:settings_common_title}}` abre la configuración del juego encima del sandbox. `{{ui:sandbox_panel_exit}}` vuelve al menú principal

## Pausa

El botón de pausa está en la esquina superior derecha de la pantalla. `Esc` también abre la pausa en lugar de salir del sandbox. La pausa lo detiene todo, como en un nivel: el avatar, los ataques y el tutorial. La ventana de pausa tiene `{{ui:root_error_continue}}`, `{{ui:settings_common_title}}` y `{{ui:game_game-result_back-to-menu}}`

## Tutorial

Seis pasos, en orden:

1. `{{ui:sandbox_tutorial_move_title}}` - recorre más o menos el ancho de la pantalla
2. `{{ui:sandbox_tutorial_dash_title}}` - haz tres dashes
3. `{{ui:sandbox_tutorial_dodge_title}}` - aguanta 10 segundos bajo ráfagas ralentizadas sin recibir un impacto. Un impacto reinicia la cuenta
4. `{{ui:sandbox_tutorial_dash-through_title}}` - el anillo crece más allá de los bordes de la pantalla, así que la única salida es un dash a través de su borde. Tienes que pasar dos anillos: un anillo fallido no anula uno ya pasado. Nada te alcanza durante un dash
5. `{{ui:sandbox_tutorial_choose-mode_title}}` - prueba los modos de la pestaña `{{ui:sandbox_tab_controls}}` y pulsa `{{ui:sandbox_tutorial_confirm-mode}}`
6. `{{ui:sandbox_tutorial_done_title}}` - `{{ui:sandbox_tutorial_play-level}}` empieza el nivel del tutorial

Mientras se juega un paso en la arena, el panel se contrae y el paso se muestra como una pequeña tarjeta en la parte superior de la pantalla. Los toques atraviesan la tarjeta. El asa sigue abriendo el panel. En los pasos `{{ui:sandbox_tutorial_choose-mode_title}}` y `{{ui:sandbox_tutorial_done_title}}` el panel se abre solo, en la pestaña `{{ui:sandbox_tab_tutorial}}`

Un impacto o una muerte reinicia solo el paso en el que ocurrió, no todo el tutorial, y el paso se pone en rojo hasta que se supera. Los pasos superados están en verde

Hacer clic en un paso de la lista empieza ese paso, aunque ya esté superado. Después de superar un paso, el tutorial pasa al siguiente sin superar. El tutorial cuenta como completado solo cuando se superan todos los pasos, y es entonces cuando se escribe en las estadísticas. `{{ui:sandbox_tutorial_restart}}`, en la misma pestaña, lo reinicia en cualquier momento

> [!warning] Advertencia
> Con `{{ui:sandbox_game_immortal}}` en la pestaña `{{ui:sandbox_tab_game}}`, los impactos no se cuentan en absoluto, así que los pasos `{{ui:sandbox_tutorial_dodge_title}}` y `{{ui:sandbox_tutorial_dash-through_title}}` tampoco los ven. Deja unas cuantas vidas mientras haces el tutorial

## Controles

Los modos cambian para el dispositivo que está guiando ahora mismo y se guardan al instante. El sensor de movimiento no tiene el modo `{{ui:enum_control-mode_relative}}`. Qué significa cada modo - [[3_controls#Modos de control]]

## Ataques y juego

- `{{ui:sandbox_attacks_auto}}` lanza oleadas aleatorias con una separación de `{{ui:sandbox_attacks_gap}}`, como el fondo del menú principal
- `{{ui:sandbox_attacks_clear}}` quita todos los ataques de la pantalla
- `{{ui:sandbox_game_speed}}` ralentiza o acelera solo los ataques. El avatar siempre se mueve a su propia velocidad
- Vidas: `{{ui:sandbox_game_immortal}}`, 1, 3 o 5. Cuando se acaban, vuelven, y el sandbox no termina
- `{{ui:sandbox_game_bot}}` deja el avatar al mismo bot que juega en el fondo del menú principal
- `{{ui:sandbox_game_free-camera}}` permite mirar más allá de los bordes de la pantalla: mueve la vista con el botón central del ratón o con dos dedos, y haz zoom con la rueda o pellizcando. El marco azul muestra lo que ve la cámara del nivel, y `{{ui:sandbox_camera_back}}` devuelve la vista a él. Los controles, el dash y los ataques funcionan igual que sin ella
- Una muerte se desarrolla como en un nivel: los ataques se ralentizan y desaparecen, y el avatar aparece en el centro con todas las vidas
