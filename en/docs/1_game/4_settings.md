---
title: Settings
date: 2026-09-24
tags: [player]
---

# Settings

Quick Setup, what each settings tab holds, how to reset them, and how graphics and anonymous mode work

## The tabs

| Tab | What it holds |
|---|---|
| `General` | language (empty follows the device), how many level files load at once, the timeout for a file at a web address, `Open Game Folder` |
| `Audio` | volume: `Master Audio`, `Game`, `User Interface`, `Editor Interface`, `Editor Playback` |
| `Controls` | devices and steering, [[3_controls]] |
| `Keybindings` | keyboard shortcuts, mostly the editor's, [[3_speed-and-shortcuts]] |
| `Graphics` | display, framerate, anti-aliasing, textures, effects, post-processing |
| `Interface` | the game HUD, `Open Menu on Lose`, `Menu Background`, screen orientation, the statistics overlay |
| `Game Editor` | the editor's own options |
| `Profile` | your statistics, [[10_statistics]] |
| `Other` | storage cleanup, folder access on Android, anonymous mode, `Reset Settings To Default` |

`Menu Background` picks what is drawn behind the main menu buttons: a live arena where a bot dodges attacks, a field of rotating shapes, or nothing

## Quick Setup

`Quick Setup` in the main menu holds the few choices that matter most, on one screen. It also opens by itself on the very first launch, before the tutorial offer

| Row | Options | What it changes |
|---|---|---|
| `Performance` | `Economy`, `Recommended`, `Maximum` | framerate cap, render scale (desktop), anti-aliasing, texture size, the effects' own framerate |
| `Effects` | `Full`, `Soft`, `Minimal` | post-processing and the avatar's shatter. `Soft` turns off the glitches, grain, blur, lens distortion and colour fringing |
| `Controls` | desktop: `Mouse`, `Mouse drag`, `Keyboard`. Phone: `Swipe`, `Finger`, `Joystick`, `Tilt` | how the main device steers. `Tilt` appears only on a phone with a motion sensor |
| `Hand` | left or right | phone only: which side the on-screen controls take |
| `Language`, `Master Audio` | | the same as in `General` and `Audio` |

`Recommended` and `Full` are what the game starts with on your device. Every choice applies at once and shows up in the full settings.
When your settings match no option, no button is lit - they are your own, and a press replaces them

## Folded sections

Long tabs are split into sections. What you change often is open, the fine tuning is folded: open a section by its caption.
The button next to the tab's reset folds or unfolds every section at once

In `Controls` only the device you are holding is open

## Resetting

Every tab has its own reset.
`Reset Settings To Default` in `Other` resets all tabs at once

A reset touches only settings. Your levels stay

## The version line

The settings screen has a version line. A click copies it

It reads `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`.
This is the line to quote in a bug report, [[11_help]]

## Graphics

**Anti-aliasing.** `MSAA` is the default on a desktop. A phone starts with no anti-aliasing. Every shape in the game is real geometry, and `MSAA` gives it clean edges without blur on every platform

`FXAA` is for weaker phones. It is one pass over the whole screen, and its cost is constant. The cost of `MSAA` grows when many transparent shapes are drawn on top of each other

TAA is deliberately not offered. It leaves ghosting behind fast bullets, and its jitter fights the glitch effects

**Framerate.** The target framerate is applied manually, not through vsync. That keeps a level's timing identical on a 60 Hz and a 144 Hz screen.
While `VSync` is on (desktop only), the framerate cap does nothing

> [!tip] Recommendation
> On a weak device, lower the **render scale** below 1 first. It costs only sharpness, and the interface stays full size. Desktop only

More - [[2_mobile-devices]]

## Anonymous mode

Turned on in `Other` → `Suppress game saves (anonymous mode)`

While it is on, the game saves nothing of its own. `settings.json`, the global statistics and each level's statistics stay on disk untouched.
A setting you change still works until the game is closed

Your level work is saved as usual: saving, exporting, importing, copying and deleting.
The editor's autosave and backups work too, they have their own switch

The mode lasts until the game is closed and is never remembered

Turning it off saves your current settings. Everything played while it was on is thrown away

> [!info] Worth knowing
> The mode also turns on by itself. The [[12_launch-arguments|launch argument]] `--suppress-game-saves` turns it on for the whole launch, and it cannot be turned off in the game. Settings or statistics from a newer version of the game turn it on too. The game then asks at every launch whether to keep them or overwrite them with defaults
