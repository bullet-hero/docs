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
| `General` | language (empty follows the device), how many level files load at once, the network timeout for a file behind a web address, `Open Game Folder` |
| `Audio` | master, game, interface and editor volume |
| `Controls` | devices and steering, see below and [[3_controls]] |
| `Keybindings` | keyboard shortcuts, mostly the editor's |
| `Graphics` | display, framerate, anti-aliasing, textures, effects, post-processing |
| `Interface` | the game HUD, `Open Menu on Lose`, `Menu Background`, screen orientation, the statistics overlay |
| `Game Editor` | the editor's own options |
| `Profile` | your statistics, see [[10_statistics]] |
| `Other` | storage cleanup, folder access on Android, anonymous mode, `Reset Settings To Default` |

Every tab has its own reset. `Reset Settings To Default` in `Other` resets every tab at once. It touches settings only: your levels are files on disk and are not affected

The version line on the settings screen copies itself on a click. It reads `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>` and is what to quote in a bug report

## Controls

How you steer the player, per device kind - keyboard and mouse, touchscreen, gamepad and device gyro

> [!info] Worth knowing
> Several kinds can be active at once and the **priority** list decides which one wins when two are, which matters on a laptop with a controller plugged in

> [!tip] Tip
> The summary at the top shows what is active *right now*, so a control scheme that seems to do nothing is usually one that lost the priority race

More: [[3_controls]], [[3_speed-and-shortcuts|Speed and shortcuts]]

## Graphics

**Anti-aliasing.** `MSAA` is the default because every shape in this game is real geometry, so every edge that aliases is a real geometric edge - the one case multisampling resolves exactly, at full sharpness, on every platform. **`FXAA`** is the alternative for weaker phones: it costs one full-screen pass no matter how much the level overdraws, while `MSAA`'s cost grows with transparent overdraw. **TAA is deliberately not offered** - ghosting behind fast bullets is a readability problem in this genre, and its jitter fights the glitch effects

**Framerate.** The target is applied manually rather than through vsync. Fixed framerate decouples simulation from display, which is what keeps a level's timing identical on a 60 Hz and a 144 Hz screen. While `VSync` is on (desktop only), the framerate cap does nothing

> [!tip] Recommendation
> **Render scale** below 1 is the cheapest thing to give up when a device struggles: it costs sharpness and nothing else. The interface is drawn at full size either way. The setting is desktop only

More: [[2_mobile-devices|Mobile devices]]

## Anonymous mode

`Other`, `Suppress game saves (anonymous mode)`

While this is on, the game saves nothing of its own: `settings.json`, the global statistics and each level's statistics stay on disk exactly as they are. A setting you change still works until the game is closed

Your level work is still saved as usual - saving, exporting, importing, copying and deleting levels, and the editor's autosave and backups, which have their own switch

It lasts until the game is closed and is never remembered. Turning it off saves your current settings and throws away everything played while it was on

> [!info] Worth knowing
> It also turns on by itself. The launch argument `--suppress-game-saves` turns it on for the whole launch, and nothing in the game can turn it off. Settings or statistics saved by a newer version of the game turn it on too, and then the game asks at every launch whether to keep them or overwrite them with defaults
