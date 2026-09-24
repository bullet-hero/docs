---
title: Controls
date: 2026-09-24
tags: [player]
---

# Controls

Four kinds of device, three steering modes, how the game picks the device that steers, and what can be rebound

## Devices and their defaults

Everything below is in `Settings`, `Controls`, one group per device:

| Device | Default mode | Dash by default |
|---|---|---|
| `Keyboard & Mouse` | `Absolute`: the avatar follows the mouse while the left button is held | `Space` or `Shift`, the right mouse button, or a double click (0.3 s) |
| `Touchscreen` | `Relative`: dragging anywhere moves the cursor by the drag | a second finger |
| `Gamepad` | `Direction`: either stick is the direction | the bottom face button or the right shoulder |
| `Motion Sensor` | `Direction`: the tilt is the direction, `Max Tilt Angle` 20° | a tap anywhere on the screen |

The mouse alone is a complete controller: the hold button steers and `Dash Button` dashes, so the keyboard is optional. Gamepad buttons are bound by position (the bottom face button), not by symbol, so a binding survives switching pad brands

## Steering modes

| Mode | What your input means |
|---|---|
| `Absolute` | a position. The cursor jumps there and the avatar chases it |
| `Relative` | a movement. The cursor adds it up and the avatar chases the cursor |
| `Direction` | a direction. There is no cursor at all |

In the two cursor modes the avatar chases the point at its own walking speed, so it lags behind a fast mouse. A dash goes to the cursor and a short one stops exactly on it. In `Direction` a stick pushed halfway walks at half speed and a dash always goes its full length. Movement is instant in every mode: no acceleration, no slide. The numbers are on the [[6_avatar]] page

On a touchscreen in `Absolute` the cursor sits above your finger (`Finger Offset Y`) so the finger does not cover the avatar

## Several devices at once

Every active device is read every frame, and exactly one of them steers. `Priority` decides who steers on the first frame and breaks ties. After that, the device you used last takes over the moment it reports real input, with no menu: an untouched gamepad reporting zeroes never counts as used

A device can steer only when all three hold: it is ticked active, this platform supports it, and it is physically present right now. `Active now` at the top shows which one is steering. `Selection` set to `Manual` pins one device. When the pinned one disappears, the game says `Selected control device (...) is unavailable - falling back` and uses another

> [!tip] Tip
> A control scheme that seems to do nothing has usually lost the priority race. Look at `Active now` first

## Rebinding

- **Gameplay input** lives in `Controls`: the mode, `Dash Keys`, `Dash Button`, `Dash Buttons`, sensitivity, dead zone, smoothing, inversion and the on-screen joystick and dash button. `Reset Controls` returns every device to this platform's defaults
- **Keyboard shortcuts** live in `Keybindings`. Almost all of them are the editor's. Outside it there are `Toggle Fullscreen` (`F11` by default) and the navigation keys. While the game waits with `Press a key for "..."`, the rule is `Tap or Escape cancels, Backspace unbinds`. `Reset Keybindings` undoes every rebinding

Only what you changed is stored. A default the developers improve later reaches you unless you had moved that binding yourself

More: [[4_settings]], [[3_speed-and-shortcuts]] for the editor's shortcuts
