---
title: Controles
date: 2026-10-02
tags: [player]
---

# Controles

Puedes jugar con ratón, pantalla táctil, gamepad o sensor de movimiento. Con el ratón, mantener pulsado el botón izquierdo guía al avatar, y Space, Shift o el botón derecho hacen un dash

La entrada se reasigna en la configuración de controles, los botones del gamepad no

Para aprender los controles paso a paso o probar cada modo sin empezar un nivel - [[13_sandbox]]

## Dispositivos

Todos los controles se configuran en `{{ui:settings_common_title}}` → `{{ui:settings_controls_title}}`, un grupo por dispositivo

| Dispositivo | Modo predeterminado | Moverse | Dash |
|---|---|---|---|
| `{{ui:enum_control-device_keyboard-mouse}}` | `{{ui:enum_control-mode_absolute}}` | mantener pulsado el botón izquierdo, el avatar sigue al ratón | `Space`, `Shift`, el botón derecho del ratón o un doble clic (0.3 s) |
| `{{ui:enum_control-device_touchscreen}}` | `{{ui:enum_control-mode_relative}}` | arrastrar un dedo por cualquier parte de la pantalla | un segundo dedo |
| `{{ui:enum_control-device_gamepad}}` | `{{ui:field_common_direction}}` | cualquiera de los dos sticks | cualquier botón excepto `Start` y `Select` |
| `{{ui:enum_control-device_device-gyro}}` | `{{ui:field_common_direction}}` | inclinar el dispositivo respecto a la horizontal, velocidad máxima a 20° | un toque en cualquier parte de la pantalla |

Basta con el ratón: el botón izquierdo guía al avatar y `{{ui:settings_controls-keyboard-mouse_km-dash-button}}` hace el dash. El teclado es opcional

En el gamepad, `Start` pausa y reanuda. Los botones del gamepad no se reasignan: durante el juego cualquier botón excepto `Start` y `Select` hace un dash, también el botón frontal derecho. En el menú de pausa el botón frontal derecho funciona como "atrás", igual que en cualquier menú

## Modos de control

| Modo | Qué significa tu entrada |
|---|---|
| `{{ui:enum_control-mode_absolute}}` | una posición. El cursor salta allí y el avatar lo alcanza |
| `{{ui:enum_control-mode_relative}}` | un movimiento. El cursor lo acumula y el avatar alcanza al cursor |
| `{{ui:field_common_direction}}` | una dirección. No hay cursor en absoluto |

El movimiento es instantáneo en todos los modos: sin aceleración y sin deslizamiento

En los modos con cursor, el avatar alcanza al cursor a su propia velocidad al caminar. Por eso se queda atrás con un ratón rápido.
Un dash va hacia el cursor. Si el cursor está cerca, el dash es más corto y termina justo sobre él

Qué pasa cuando sueltas el botón de guiar o levantas el dedo lo decide una casilla - `{{ui:settings_controls-keyboard-mouse_km-cursor-return}}` para el ratón, `{{ui:settings_controls-touchscreen_touch-cursor-return}}` para la pantalla táctil:

- activada - el avatar se detiene donde está y el cursor vuelve a él. Es lo predeterminado en el ratón
- desactivada - el cursor se queda donde lo dejaste y el avatar camina hasta él. Solo el daño puede mover el cursor. Es lo predeterminado en la pantalla táctil

En el modo `{{ui:field_common_direction}}`, un stick inclinado a medias da la mitad de la velocidad. Un dash siempre recorre su longitud completa

En la pantalla táctil, en el modo `{{ui:enum_control-mode_absolute}}`, el cursor se coloca por encima del dedo (`{{ui:settings_controls-touchscreen_touch-finger-offset-y}}`). Así el dedo no tapa al avatar

Mientras un dedo guía al avatar, un segundo dedo hace un dash allí donde toque, también sobre un panel o un botón. La interfaz no recibe ese toque, así que un dash nunca pulsa nada por accidente

Los números exactos - [[6_avatar]]

## Sensor de movimiento

El sensor de movimiento no tiene calibración. El avatar se queda quieto cuando el teléfono está en horizontal, con la pantalla hacia arriba

- inclina el borde derecho hacia abajo y el avatar va a la derecha
- inclina el borde superior hacia abajo y va hacia arriba
- `{{ui:settings_controls-device_sensitivity}}` 1 da la velocidad máxima a 20°. Con 2 basta la mitad de inclinación

El sensor sigue a la pantalla: gira el teléfono a horizontal y de vuelta, y la derecha sigue siendo la derecha.
El sensor tiene dos modos, `{{ui:enum_control-mode_absolute}}` y `{{ui:field_common_direction}}`

## Reasignación

- **La entrada de juego** está en `{{ui:settings_controls_title}}`: el modo, `{{ui:settings_controls-keyboard-mouse_dash-keys}}`, `{{ui:settings_controls-keyboard-mouse_km-dash-button}}`, la sensibilidad, la zona muerta, la suavidad, la inversión, el joystick en pantalla y el botón de dash. `{{ui:settings_controls_reset}}` devuelve cada dispositivo a los valores predeterminados de esta plataforma
- **Los atajos de teclado** están en `{{ui:settings_keybindings_label}}`. Casi todos son para el editor. Fuera del editor están `{{ui:settings_keybindings_window_toggle_fullscreen}}` (`F11` por defecto), `{{ui:settings_keybindings_window_settings_save}}` (`Ctrl+S` mientras la configuración está abierta) y las teclas de navegación. `{{ui:settings_keybindings_reset}}` deshace todas las reasignaciones

Cuando el juego espera una tecla, muestra `Pulsa una tecla para "..."`.
Después rige la regla `{{ui:settings_escape-cancels_backspace}}`

Para las teclas, el juego guarda solo lo que reasignaste. Si más adelante mejora una asignación predeterminada, te llega, salvo que hayas cambiado esa asignación tú. La pestaña `{{ui:settings_controls_title}}` se guarda completa, así que los nuevos valores predeterminados de esa pestaña no te llegan

Los atajos del editor - [[3_speed-and-shortcuts]]

## Varios dispositivos a la vez

Un solo dispositivo guía al avatar: el último que usaste.
El cambio ocurre solo, en el mismo fotograma, sin ningún menú

El juego consulta todos los dispositivos activos en cada fotograma. Un gamepad que nadie toca envía ceros, y eso no cuenta como uso

En el primer fotograma todavía no se ha usado nada, así que decide la plataforma: el ratón en un PC, la pantalla táctil en un teléfono

El dash y la pausa funcionan desde cualquier dispositivo activo, sea cual sea el que guía. Un botón del gamepad hace un dash mientras guía el ratón. Un dash por sí solo no toma el control del movimiento

Un dispositivo puede guiar al avatar solo si:

- está marcado como activo
- la plataforma lo admite
- está conectado en este momento

`{{ui:settings_controls-active_now}}`, arriba, muestra cuál está guiando

> [!tip] Consejo
> ¿Un esquema de control parece no hacer nada? Normalmente se tocó otro dispositivo después. Mira primero `{{ui:settings_controls-active_now}}`
