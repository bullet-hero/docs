---
title: Controls
date: 2026-09-24
tags: [player]
---

# Controls

Which devices you can play with, how to move and dash with them, and what can be rebound

## Devices

All controls are set in `Settings` → `Controls`, one group per device

| Device | Default mode | Move | Dash |
|---|---|---|---|
| `Keyboard & Mouse` | `Absolute` | hold the left button, the avatar follows the mouse | `Space`, `Shift`, the right mouse button or a double click (0.3 s) |
| `Touchscreen` | `Relative` | drag a finger anywhere on the screen | a second finger |
| `Gamepad` | `Direction` | either stick | the bottom face button or the right shoulder |
| `Motion Sensor` | `Direction` | tilt the device, `Max Tilt Angle` 20° | a tap anywhere on the screen |

The mouse alone is enough: the left button steers, `Dash Button` dashes. The keyboard is optional

Gamepad buttons are bound by position, not by symbol. A binding survives switching to a pad of another brand

## Steering modes

| Mode | What your input means |
|---|---|
| `Absolute` | a position. The cursor jumps there, the avatar chases it |
| `Relative` | a movement. The cursor adds it up, the avatar chases the cursor |
| `Direction` | a direction. There is no cursor at all |

Movement is instant in every mode: no acceleration and no slide

In the cursor modes the avatar chases the cursor at its own walking speed. So it lags behind a fast mouse.
A dash goes to the cursor. If the cursor is close, the dash is shorter and stops exactly on it

In `Direction` a stick pushed halfway gives half speed. A dash always goes its full length

On a touchscreen in `Absolute` the cursor sits above your finger (`Finger Offset Y`). That way the finger does not cover the avatar

The exact numbers - [[6_avatar]]

## Rebinding

- **Gameplay input** is in `Controls`: the mode, `Dash Keys`, `Dash Button`, `Dash Buttons`, sensitivity, dead zone, smoothing, inversion, the on-screen joystick and dash button. `Reset Controls` returns every device to this platform's defaults
- **Keyboard shortcuts** are in `Keybindings`. Almost all of them are the editor's. Outside the editor there are `Toggle Fullscreen` (`F11` by default) and the navigation keys. `Reset Keybindings` undoes every rebinding

While the game waits for a key, it says `Press a key for "..."`.
The rule then is `Tap or Escape cancels, Backspace unbinds`

The game stores only what you changed. If the developers improve a default later, it reaches you. The exception is a binding you changed yourself

The editor's shortcuts - [[3_speed-and-shortcuts]]

## Several devices at once

One device steers the avatar - the one you used last.
The switch happens by itself, on the same frame, with no menu

The game reads every active device every frame. An untouched gamepad reports zeroes, and that does not count as use

`Priority` decides who steers on the first frame and breaks ties. This matters, for example, on a laptop with a controller plugged in

A device can steer only when:

- it is ticked active
- the platform supports it
- it is connected right now

`Active now` at the top shows which one is steering

`Selection` set to `Manual` pins one device.
If it disappears, the game says `Selected control device (...) is unavailable - falling back` and uses another

> [!tip] Tip
> A control scheme seems to do nothing? It has usually lost on priority. Look at `Active now` first
