---
title: Controls
date: 2026-10-01
tags: [player]
---

# Controls

You can play with a mouse, a touchscreen, a gamepad or a motion sensor. With a mouse, holding the left button steers the avatar, and Space, Shift or the right button dash

Input is rebound in the controls settings, gamepad buttons are not

To learn the controls step by step or try every mode without starting a level - [[13_sandbox]]

## Devices

All controls are set in `Settings` → `Controls`, one group per device

| Device | Default mode | Move | Dash |
|---|---|---|---|
| `Keyboard & Mouse` | `Absolute` | hold the left button, the avatar follows the mouse | `Space`, `Shift`, the right mouse button or a double click (0.3 s) |
| `Touchscreen` | `Relative` | drag a finger anywhere on the screen | a second finger |
| `Gamepad` | `Direction` | either stick | any button except `Start` and `Select` |
| `Motion Sensor` | `Direction` | tilt the device away from horizontal, full speed at 20° | a tap anywhere on the screen |

The mouse alone is enough: the left button steers the avatar, `Dash Button` dashes. The keyboard is optional

On a gamepad `Start` pauses and resumes. Gamepad buttons are not rebound: in play any button except `Start` and `Select` dashes, including the right face button. In the pause menu the right face button works as "back", as in any menu

## Control modes

| Mode | What your input means |
|---|---|
| `Absolute` | a position. The cursor jumps there, the avatar catches up with it |
| `Relative` | a movement. The cursor accumulates it, the avatar catches up with the cursor |
| `Direction` | a direction. There is no cursor at all |

Movement is instant in every mode: no acceleration and no sliding

In the cursor modes the avatar catches up with the cursor at its own walking speed. So it lags behind a fast mouse.
A dash goes towards the cursor. If the cursor is close, the dash is shorter and ends exactly on it

What happens when you release the steering button or lift your finger is decided by one checkbox - `Stop On Release` for the mouse, `Stop On Lift` for the touchscreen:

- on - the avatar stops where it is, the cursor returns to it. This is the mouse default
- off - the cursor stays where you left it, and the avatar walks to it. Only damage can move the cursor. This is the touchscreen default

In `Direction` mode a stick pushed halfway gives half speed. A dash always goes its full length

On a touchscreen in `Absolute` mode the cursor sits above your finger (`Finger Offset Y`). That way the finger does not cover the avatar

While one finger steers the avatar, a second finger dashes wherever it lands - on a panel or on a button too. The interface does not receive that touch, so a dash never presses anything by accident

The exact numbers - [[6_avatar]]

## Motion sensor

The motion sensor has no calibration. The avatar stands still when the phone lies flat, screen up

- tilt the right edge down, and the avatar goes right
- tilt the top edge down, and it goes up
- `Sensitivity` 1 gives full speed at 20°. At 2 half the tilt is enough

The sensor follows the screen: turn the phone to landscape and back, and right stays right.
The sensor has two modes, `Absolute` and `Direction`

## Rebinding

- **Gameplay input** is in `Controls`: the mode, `Dash Keys`, `Dash Button`, sensitivity, dead zone, smoothing, inversion, the on-screen joystick and dash button. `Reset Controls` returns every device to this platform's defaults
- **Hotkeys** are in `Keybindings`. Almost all of them are for the editor. Outside the editor there are `Toggle Fullscreen` (`F11` by default) and the navigation keys. `Reset Keybindings` undoes every rebinding

When the game waits for a key, it shows `Press a key for "..."`.
Then the rule is `Tap or Escape cancels, Backspace unbinds`

For keys the game stores only what you rebound. If a default binding gets better later, it reaches you, unless you changed that binding yourself. The `Controls` tab is stored in full, so new defaults for it do not reach you

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

`Active now` at the top shows which one is steering

> [!tip] Tip
> A control scheme seems to do nothing? Usually another device was touched after it. Look at `Active now` first
