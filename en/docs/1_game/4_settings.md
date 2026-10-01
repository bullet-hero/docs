---
title: Settings
date: 2026-10-01
tags: [player]
---

# Settings

The most important settings are set on the first launch: the game opens a quick setup with language, volume, performance and effects by itself. A reset touches only settings, levels stay

## The tabs

| Tab | What it holds |
|---|---|
| `General` | the language - each named in itself, `Русский (ru)`. `System (en)` follows the device and shows which language it resolved to. Also how many level files load at once, the timeout for a file at a web address, `Open Game Folder` |
| `Audio` | volume: `Master Audio`, `Game`, `User Interface`, `Editor Interface`, `Editor Playback` |
| `Controls` | devices and the way of steering, [[3_controls]] |
| `Keybindings` | hotkeys, mostly the editor's, [[3_speed-and-shortcuts]] |
| `Graphics` | display, framerate, anti-aliasing, `Colliders Only Mode`, textures, effects, post-processing |
| `Interface` | the in-game interface, `Open Menu on Lose`, `Menu Background`, `Levels View`, screen orientation, the statistics overlay |
| `Game Editor` | the editor's own settings, including its own `Levels View` |
| `Profile` | your statistics, [[10_statistics]] |
| `Other` | storage cleanup, folder access on Android, anonymous mode, `Reset Settings To Default` |

`Menu Background` picks what is visible behind the main menu buttons: a live arena where a bot dodges attacks, a field of rotating shapes, or nothing

`Levels View` picks how the level selection opens - a `Grid` of covers or a `List` of rows with descriptions. There are two of them: the one on the `Interface` tab is for the menu (`Grid` by default), the one on the `Game Editor` tab is for the editor (`List` by default). The button next to the search field still switches the view until you leave that screen

## Quick Setup

`Quick Setup`, a button on the `General` tab above `Open Game Folder`, asks a few of the most important questions, one category per page. On the very first launch it opens by itself, before the tutorial offer.
Each answer has a line about what it does. Pages can be opened in any order, `Next` only suggests the next one

| Page | Question | Answers | What it changes |
|---|---|---|---|
| `Language and sound` | `Language` | `System` and every language of the game, each named in itself | the same as on the `General` tab |
| | `Master Audio` | a slider | the same as on the `Audio` tab |
| `Graphics` | `Performance` | `Minimum`, `Economy`, `Recommended`, `Maximum` | render scale (PC), anti-aliasing, texture size, the effects' framerate - but not the framerate cap: every answer runs at the screen's rate. `Minimum` also turns off particle effects and post-processing and limits images to 512 |
| | `Effects` | `Full`, `Soft`, `Off` | every post-processing effect and the avatar's shatter. `Soft` turns off glitches, grain, blur, lens distortion and colour fringing |
| `Controls` | | `Open the tutorial` | nothing here: the tutorial lets you try every control scheme and pick yours. It opens from the main menu or the sandbox |

The answer marked `Default` is what the game starts with on your device. A choice applies at once and is visible in the full settings.
If your settings match no answer, none is highlighted and a line says so - these are your own settings, and a press replaces them

## Folded sections

Long tabs are split into sections. What is changed often is open, fine tuning is folded: a section opens by its heading.
The button next to the tab's reset folds or unfolds all sections at once

On the `Controls` tab only the device in your hands is open

## Reset

Each tab has its own reset.
`Reset Settings To Default` in `Other` resets all tabs at once

A reset touches only settings. Your levels stay

## The version line

The settings screen has a version line. A click on it copies it

It looks like this: `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`.
This is the line to quote in a bug report, [[11_help]]

## Graphics

**Anti-aliasing.** On PC the default is `MSAA`. A phone starts with no anti-aliasing. Every shape in the game is real geometry, and `MSAA` gives it clean edges without blurring on every platform

`FXAA` is for weak phones. It is one pass over the whole screen, and its cost is constant. The cost of `MSAA` grows when many transparent shapes are drawn on top of each other

TAA is deliberately not offered. It leaves a trail behind fast bullets, and its jitter interferes with the glitch effects

**Framerate.** The target framerate is set manually, not through vertical sync. That way a level's timing is the same on a 60 Hz and a 144 Hz screen.
While `VSync` is on (PC only), the framerate cap does nothing

> [!tip] Recommendation
> On a weak device, lower the **render scale** below 1 first. It costs only sharpness, and the interface stays full size. PC only

More - [[2_mobile-devices]]

## Colliders Only Mode

A mode for practice, a folded section on the `Graphics` tab. With `Enable Mode` on, a level in play draws every hitbox as a flat fill of one colour on a plain background, and nothing else.
Gone: the look of the shapes themselves, shapes with no collider, effects, texts, post-processing and the theme background.
Unchanged: the music, collision, the camera and its shake, checkpoints, the interface and statistics - a run in this mode counts like any other.
Your avatar is drawn as usual

The mode works only when playing levels. The editor, the sandbox and the menu background are drawn as usual

| Option | What it does |
|---|---|
| `Use Transparency` | on (the default) - fills are semi-transparent by the colour's alpha, and overlapping obstacles show darker. The alpha never drops below 0.15. Off - every fill is solid, and the colour's alpha is locked |
| `Fill Color` | the fill colour, red with 0.6 alpha by default. The editor's collider view uses the same hue with its own opacity |
| `Background Color` | what is drawn behind the fills, dark grey by default - not black, so the edge of the camera frame is visible against the black bars around it |

Both colours are folded under their own caption: unfold the one you need to get its colour wheel

## Anonymous mode

Turned on in `Other` → `Suppress game saves (anonymous mode)`

While the mode is on, the game saves nothing of its own. `settings.json`, the global statistics and the level statistics stay on disk untouched.
A changed setting still works until the game is closed

Work with levels is saved as usual: saving, exporting, importing, copying and deleting.
The editor's autosave and backups work too, they have their own switch

The mode lasts until the game is closed and is not remembered anywhere

If you turn it off, the current settings are saved. Everything played during that time is discarded

> [!info] Worth knowing
> The mode also turns on by itself. The [[12_launch-arguments|launch argument]] `--suppress-game-saves` turns it on for the whole launch, and it cannot be turned off in the game. Settings or statistics from a newer version of the game turn it on too. Then the game asks at every launch whether to keep them or overwrite them with the defaults
