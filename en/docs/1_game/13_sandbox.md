---
title: Sandbox and tutorial
date: 2026-09-28
tags: [player]
---

# Sandbox and tutorial

An arena where you steer freely, throw attacks at yourself and learn the controls step by step

`Sandbox` is on the main menu. On the first launch the game offers the tutorial once: `Start` opens the sandbox on its tutorial, `Not now` closes the offer for good. The sandbox itself stays on the menu either way.

## The panel

The sandbox has one panel on the left. Tap its handle to fold it away, or drag the handle to make the panel wider or narrower. The panel has five tabs:

| Tab | What it does |
|---|---|
| `Sandbox` | what the sandbox is and what each tab does |
| `Tutorial` | the tutorial steps and what to do right now |
| `Controls` | the mode of the device you are steering with, the motion sensor switch and a link to all control settings |
| `Attacks` | fires any of the six attacks by hand, or lets waves come on their own |
| `Game` | lives, attack speed, the bot and the free camera |

`Settings` opens the game settings over the sandbox. `Exit` goes back to the main menu.

## Pause

The pause button is in the top right corner of the screen. `Esc` opens the pause as well rather than leaving the sandbox. The pause stops everything, as in a level: the avatar, the attacks and the tutorial. The pause window has `Continue`, `Settings` and `Back to Menu`

## Tutorial

Six steps, in this order:

1. `Move` - travel about one screen width
2. `Dash` - dash three times
3. `Dodge` - hold out 10 seconds under slowed volleys without a hit. A hit starts the count again
4. `Through the ring` - the ring grows past the edges of the screen, so the only way out is a dash through its rim. During a dash nothing hits you
5. `Control mode` - try the modes on the `Controls` tab and press `Keep this mode`
6. `Done` - `Play the tutorial level` starts the tutorial level

While a step is played in the arena, the panel folds away and the step shows as a small card at the top of the screen. Touches go straight through the card. The handle still opens the panel. On `Control mode` and `Done` the panel opens by itself on the `Tutorial` tab

A hit or a death restarts only the step it happened in, never the whole tutorial, and the step turns red until it is passed. Passed steps are green.

Pressing a step in the list plays that step, a passed one too. Once a step is passed, the tutorial moves on to the next one not yet passed. The tutorial counts as finished only once every step is passed - that is also when it is written to the statistics. `Start the tutorial` on the same tab runs it again at any time.

> [!warning] Warning
> With `Immortal` on the `Game` tab, hits are not counted at all, so the `Dodge` and `Through the ring` steps cannot see them either. Keep some lives while you go through the tutorial

## Controls

The modes change the device that is steering right now, and the change is saved at once. The motion sensor has no `Relative` mode. What each mode means - [[3_controls#Steering modes]]

## Attacks and the game

- `Waves on their own` fires random waves with `Pause between waves` between them, like the menu background
- `Clear` removes every attack on screen
- `Attack speed` slows or speeds up the attacks only. The avatar always moves at its own speed
- Lives are `Immortal`, 1, 3 or 5. When they run out they come back, the sandbox never ends
- `Bot plays` hands the avatar to the same bot the menu background uses
- `Free camera` lets you look past the edges of the screen: pan with the middle mouse button or two fingers, zoom with the wheel or a pinch. A blue frame shows what the level camera sees, and `Back to the camera` returns the view to it. Steering, dashing and the attacks work exactly as without it
- A death plays out as in a level: the attacks slow down and disappear, and the avatar comes back in the centre with its lives refilled
