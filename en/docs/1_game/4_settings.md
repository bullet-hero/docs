---
title: Settings
date: 2026-09-24
tags: [player]
---

# Settings

The settings tabs, and the three a player needs explained in full: controls, graphics and anonymous mode

## The tabs

| Tab | What it holds |
|---|---|
| `General` | language (empty follows the device), how many level files load at once, the timeout for a file at a web address, `Open Game Folder` |
| `Audio` | master, game, interface and editor volume |
| `Controls` | devices and steering, see below |
| `Keybindings` | keyboard shortcuts, mostly the editor's |
| `Graphics` | display, framerate, anti-aliasing, textures, effects, post-processing |
| `Interface` | the game HUD, `Open Menu on Lose`, `Menu Background`, screen orientation, the statistics overlay |
| `Game Editor` | the editor's own options |
| `Profile` | your statistics, see [[10_statistics]] |
| `Other` | storage cleanup, folder access on Android, anonymous mode, `Reset Settings To Default` |

Every tab has its own reset, and `Reset Settings To Default` in `Other` resets them all at once. It touches settings, never your levels

The version line on the settings screen copies itself on a click. It reads `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>` and is what to quote in a bug report

## Controls

Steering per device kind: keyboard and mouse, touchscreen, gamepad and device gyro. Several kinds can be active at once, and the **priority** list decides which one wins (this matters on a laptop with a controller plugged in)

The summary at the top shows what is active *right now*, so a scheme that seems to do nothing has usually lost on priority

More: [[3_controls]], [[3_speed-and-shortcuts|Speed and shortcuts]]

## Graphics

**Anti-aliasing.** `MSAA` is the default: every shape here is real geometry, and geometric edges are the one case multisampling resolves exactly, at full sharpness, on every platform. **`FXAA`** is for weaker phones: one full-screen pass however much the level overdraws, while `MSAA`'s cost grows with transparent overdraw. **TAA is deliberately not offered**: ghosting behind fast bullets hurts readability, and its jitter fights the glitch effects

**Framerate.** The target is applied manually rather than through vsync: a fixed framerate decouples simulation from display and keeps a level's timing identical on a 60 Hz and a 144 Hz screen. While `VSync` is on (desktop only), the framerate cap does nothing

> [!tip] Recommendation
> **Render scale** below 1 is the cheapest thing to give up when a device struggles: it costs sharpness and nothing else. The interface stays full size. Desktop only

More: [[2_mobile-devices|Mobile devices]]

## Anonymous mode

`Other`, `Suppress game saves (anonymous mode)`

While this is on, the game saves nothing of its own: `settings.json`, the global statistics and each level's statistics stay on disk untouched. A setting you change still works until the game is closed

Your level work is still saved as usual: saving, exporting, importing, copying and deleting levels, and the editor's autosave and backups, which have their own switch

It lasts until the game is closed and is never remembered. Turning it off saves your current settings and throws away everything played while it was on

> [!info] Worth knowing
> It also turns on by itself. The launch argument `--suppress-game-saves` turns it on for the whole launch, with no way to turn it off in the game. Settings or statistics saved by a newer version of the game turn it on too, and the game then asks at every launch whether to keep them or overwrite them with defaults
