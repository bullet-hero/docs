---
title: Controls
date: 2026-09-24
tags: [player]
---

# Controls

Which devices you can play with, how to move and dash with them, and what can be rebound

To learn the controls step by step or try every mode without starting a level - [[13_sandbox]]

## Devices

All controls are set in `Settings` → `Controls`, one group per device

| Device | Default mode | Move | Dash |
|---|---|---|---|
| `Keyboard & Mouse` | `Absolute` | hold the left button, the avatar follows the mouse | `Space`, `Shift`, the right mouse button or a double click (0.3 s) |
| `Touchscreen` | `Relative` | drag a finger anywhere on the screen | a second finger |
| `Gamepad` | `Direction` | either stick | any button except `Start` and `Select` |
| `Motion Sensor` | `Direction` | tilt the device away from lying flat, full speed at 20° | a tap anywhere on the screen |

The mouse alone is enough: the left button steers, `Dash Button` dashes. The keyboard is optional

On a gamepad `Start` pauses and resumes. The gamepad's buttons are not rebound: in play every button except `Start` and `Select` dashes, including the right face button. In the pause menu the right face button goes back, as in any menu

## Steering modes

| Mode | What your input means |
|---|---|
| `Absolute` | a position. The cursor jumps there, the avatar chases it |
| `Relative` | a movement. The cursor adds it up, the avatar chases the cursor |
| `Direction` | a direction. There is no cursor at all |

Movement is instant in every mode: no acceleration and no slide

In the cursor modes the avatar chases the cursor at its own walking speed. So it lags behind a fast mouse.
A dash goes to the cursor. If the cursor is close, the dash is shorter and stops exactly on it

Let go of the steering button or lift your finger, and what happens is up to one checkbox - `Stop On Release` for the mouse, `Stop On Lift` for a touchscreen:

- on - the avatar stops where it is, the cursor comes back onto it. The mouse default
- off - the cursor stays where you left it, the avatar walks on to it. Only a hit moves the cursor. The touchscreen default

In `Direction` a stick pushed halfway gives half speed. A dash always goes its full length

On a touchscreen in `Absolute` the cursor sits above your finger (`Finger Offset Y`). That way the finger does not cover the avatar

While one finger steers, a second finger dashes wherever it lands - on a panel or a button too. The interface ignores that touch, so a dash never presses anything by accident

The exact numbers - [[6_avatar]]

## Motion sensor

The motion sensor has no calibration. The avatar stands still when the phone lies flat, screen up

- tilt the right edge down, and the avatar goes right
- tilt the top edge down, and it goes up
- `Sensitivity` 1 reaches full speed at 20°. At 2 half the tilt is enough

It follows the screen: turn the phone to landscape and back, and right stays right.
The sensor has two modes, `Absolute` and `Direction`

## Rebinding

- **Gameplay input** is in `Controls`: the mode, `Dash Keys`, `Dash Button`, sensitivity, dead zone, smoothing, inversion, the on-screen joystick and dash button. `Reset Controls` returns every device to this platform's defaults
- **Keyboard shortcuts** are in `Keybindings`. Almost all of them are the editor's. Outside the editor there are `Toggle Fullscreen` (`F11` by default) and the navigation keys. `Reset Keybindings` undoes every rebinding

While the game waits for a key, it says `Press a key for "..."`.
The rule then is `Tap or Escape cancels, Backspace unbinds`

For keybindings the game stores only what you rebound. If a default binding is improved later, it reaches you, unless you changed that binding yourself. The `Controls` tab is stored in full, so a later change of its defaults does not reach you

The editor's shortcuts - [[3_speed-and-shortcuts]]

## Several devices at once

One device steers the avatar - the one you used last.
The switch happens by itself, on the same frame, with no menu

The game reads every active device every frame. An untouched gamepad reports zeroes, and that does not count as use

On the first frame nothing has been used yet, so the platform decides: the mouse on a computer, the touchscreen on a phone

A dash and a pause work from every active device, whichever one steers. A gamepad button dashes while the mouse steers. A dash alone does not take over steering

A device can steer only when:

- it is ticked active
- the platform supports it
- it is connected right now

`Active now` at the top shows which one is steering

> [!tip] Tip
> A control scheme seems to do nothing? Usually another device was touched after it. Look at `Active now` first
