---
title: Controls
date: 2026-10-02
tags: [player]
---

# Controls

You can play with a mouse, a touchscreen, a gamepad or a motion sensor. With a mouse, holding the left button steers the avatar, and Space, Shift or the right button dash

Input is rebound in the controls settings, gamepad buttons are not

To learn the controls step by step or try every mode without starting a level - [[13_sandbox]]

## Devices

All controls are set in `{{ui:settings_common_title}}` → `{{ui:settings_controls_title}}`, one group per device

| Device | Default mode | Move | Dash |
|---|---|---|---|
| `{{ui:enum_control-device_keyboard-mouse}}` | `{{ui:enum_control-mode_absolute}}` | hold the left button, the avatar follows the mouse | `Space`, `Shift`, the right mouse button or a double click (0.3 s) |
| `{{ui:enum_control-device_touchscreen}}` | `{{ui:enum_control-mode_relative}}` | drag a finger anywhere on the screen | a second finger |
| `{{ui:enum_control-device_gamepad}}` | `{{ui:field_common_direction}}` | either stick | any button except `Start` and `Select` |
| `{{ui:enum_control-device_device-gyro}}` | `{{ui:field_common_direction}}` | tilt the device away from horizontal, full speed at 20° | a tap anywhere on the screen |

The mouse alone is enough: the left button steers the avatar, `{{ui:settings_controls-keyboard-mouse_km-dash-button}}` dashes. The keyboard is optional

On a gamepad `Start` pauses and resumes. Gamepad buttons are not rebound: in play any button except `Start` and `Select` dashes, including the right face button. In the pause menu the right face button works as "back", as in any menu

## Control modes

| Mode | What your input means |
|---|---|
| `{{ui:enum_control-mode_absolute}}` | a position. The cursor jumps there, the avatar catches up with it |
| `{{ui:enum_control-mode_relative}}` | a movement. The cursor accumulates it, the avatar catches up with the cursor |
| `{{ui:field_common_direction}}` | a direction. There is no cursor at all |

Movement is instant in every mode: no acceleration and no sliding

In the cursor modes the avatar catches up with the cursor at its own walking speed. So it lags behind a fast mouse.
A dash goes towards the cursor. If the cursor is close, the dash is shorter and ends exactly on it

What happens when you release the steering button or lift your finger is decided by one checkbox - `{{ui:settings_controls-keyboard-mouse_km-cursor-return}}` for the mouse, `{{ui:settings_controls-touchscreen_touch-cursor-return}}` for the touchscreen:

- on - the avatar stops where it is, the cursor returns to it. This is the mouse default
- off - the cursor stays where you left it, and the avatar walks to it. Only damage can move the cursor. This is the touchscreen default

In `{{ui:field_common_direction}}` mode a stick pushed halfway gives half speed. A dash always goes its full length

On a touchscreen in `{{ui:enum_control-mode_absolute}}` mode the cursor sits above your finger (`{{ui:settings_controls-touchscreen_touch-finger-offset-y}}`). That way the finger does not cover the avatar

While one finger steers the avatar, a second finger dashes wherever it lands - on a panel or on a button too. The interface does not receive that touch, so a dash never presses anything by accident

The exact numbers - [[6_avatar]]

## Motion sensor

The motion sensor has no calibration. The avatar stands still when the phone lies flat, screen up

- tilt the right edge down, and the avatar goes right
- tilt the top edge down, and it goes up
- `{{ui:settings_controls-device_sensitivity}}` 1 gives full speed at 20°. At 2 half the tilt is enough

The sensor follows the screen: turn the phone to landscape and back, and right stays right.
The sensor has two modes, `{{ui:enum_control-mode_absolute}}` and `{{ui:field_common_direction}}`

## Rebinding

- **Gameplay input** is in `{{ui:settings_controls_title}}`: the mode, `{{ui:settings_controls-keyboard-mouse_dash-keys}}`, `{{ui:settings_controls-keyboard-mouse_km-dash-button}}`, sensitivity, dead zone, smoothing, inversion, the on-screen joystick and dash button. `{{ui:settings_controls_reset}}` returns every device to this platform's defaults
- **Hotkeys** are in `{{ui:settings_keybindings_label}}`. Almost all of them are for the editor. Outside the editor there are `{{ui:settings_keybindings_window_toggle_fullscreen}}` (`F11` by default), `{{ui:settings_keybindings_window_settings_save}}` (`Ctrl+S` while the settings are open) and the navigation keys. `{{ui:settings_keybindings_reset}}` undoes every rebinding

When the game waits for a key, it shows `Press a key for "..."`.
Then the rule is `{{ui:settings_escape-cancels_backspace}}`

For keys the game stores only what you rebound. If a default binding gets better later, it reaches you, unless you changed that binding yourself. The `{{ui:settings_controls_title}}` tab is stored in full, so new defaults for it do not reach you

The editor's hotkeys - [[3_speed-and-shortcuts]]

## Several devices at once

One device steers the avatar - the one you used last.
The switch happens by itself, on the same frame, with no menu at all

The game polls every active device every frame. An untouched gamepad sends zeroes, and that does not count as use

On the first frame nothing has been used yet, so the platform decides: the mouse on a computer, the touchscreen on a phone

Dash and pause work from any active device, whichever one is steering. A gamepad button dashes while the mouse steers. A dash alone does not take over steering

A device can steer the avatar only if:

- it is marked active
- the platform supports it
- it is connected right now

`{{ui:settings_controls-active_now}}` at the top shows which one is steering

> [!tip] Tip
> A control scheme seems to do nothing? Usually another device was touched after it. Look at `{{ui:settings_controls-active_now}}` first
