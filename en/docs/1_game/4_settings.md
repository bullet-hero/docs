---
title: Settings
date: 2026-10-02
tags: [player]
---

# Settings

The most important settings are set on the first launch: the game opens a quick setup with language, volume, performance and effects by itself. A reset touches only settings, levels stay

## The tabs

| Tab | What it holds |
|---|---|
| `{{ui:settings_general_title}}` | the language - each named in itself, `Русский (ru)`. `System (en)` follows the device and shows which language it resolved to. Also how many level files load at once, the timeout for a file at a web address, `{{ui:settings_general-open_folder}}` |
| `{{ui:field_common_audio}}` | volume: `{{ui:settings_audio_volume}}`, `{{ui:settings_audio_game}}`, `{{ui:settings_audio_ui}}`, `{{ui:settings_audio_editor-ui}}`, `{{ui:settings_audio_editor-game}}` |
| `{{ui:settings_controls_title}}` | devices and the way of steering, [[3_controls]] |
| `{{ui:settings_keybindings_label}}` | hotkeys, mostly the editor's, [[3_speed-and-shortcuts]] |
| `{{ui:settings_graphics_title}}` | display, framerate, anti-aliasing, `{{ui:settings_graphics-colliders-mode_title}}`, textures, effects, post-processing |
| `{{ui:settings_interface_label}}` | the in-game interface, `{{ui:settings_interface_open-menu-on-lose}}`, `{{ui:settings_interface_menu-background}}`, `{{ui:settings_interface_levels-layout}}`, screen orientation, the statistics overlay |
| `{{ui:settings_game-editor_title}}` | the editor's own settings, including its own `{{ui:settings_interface_levels-layout}}` |
| `{{ui:settings_profile_tab}}` | your statistics, [[10_statistics]] |
| `{{ui:settings_other_title}}` | storage cleanup, folder access on Android, anonymous mode, `{{ui:settings_other_reset}}` |

`{{ui:settings_interface_menu-background}}` picks what is visible behind the main menu buttons: a live arena where a bot dodges attacks, a field of rotating shapes, or nothing

`{{ui:settings_interface_levels-layout}}` picks how the level selection opens - a `{{ui:enum_level-browser-layout_grid}}` of covers or a `{{ui:enum_level-browser-layout_list}}` of rows with descriptions. There are two of them: the one on the `{{ui:settings_interface_label}}` tab is for the menu (`{{ui:enum_level-browser-layout_grid}}` by default), the one on the `{{ui:settings_game-editor_title}}` tab is for the editor (`{{ui:enum_level-browser-layout_list}}` by default). The button next to the search field still switches the view until you leave that screen

## Quick Setup

`{{ui:settings_quick-setup_title}}`, a button on the `{{ui:settings_general_title}}` tab above `{{ui:settings_general-open_folder}}`, asks a few of the most important questions, one category per page. On the very first launch it opens by itself, before the tutorial offer.
Each answer has a line about what it does. Pages can be opened in any order, `{{ui:settings_quick-setup_next}}` only suggests the next one

| Page | Question | Answers | What it changes |
|---|---|---|---|
| `{{ui:settings_quick-setup_page-language}}` | `{{ui:settings_general_language}}` | `{{ui:settings_general_language_system}}` and every language of the game, each named in itself | the same as on the `{{ui:settings_general_title}}` tab |
| | `{{ui:settings_audio_volume}}` | a slider | the same as on the `{{ui:field_common_audio}}` tab |
| `{{ui:settings_graphics_title}}` | `{{ui:settings_quick-setup_performance}}` | `{{ui:settings_quick-setup_performance-minimum}}`, `{{ui:settings_quick-setup_performance-economy}}`, `{{ui:settings_quick-setup_performance-recommended}}`, `{{ui:settings_quick-setup_performance-max}}` | render scale (PC), anti-aliasing, texture size, the effects' framerate - but not the framerate cap: every answer runs at the screen's rate. `{{ui:settings_quick-setup_performance-minimum}}` also turns off particle effects and post-processing and limits images to 512 |
| | `{{ui:settings_quick-setup_comfort}}` | `{{ui:settings_quick-setup_comfort-full}}`, `{{ui:settings_quick-setup_comfort-soft}}`, `{{ui:settings_quick-setup_comfort-minimal}}` | every post-processing effect and the avatar's shatter. `{{ui:settings_quick-setup_comfort-soft}}` turns off glitches, grain, blur, lens distortion and colour fringing |
| `{{ui:settings_controls_title}}` | | `{{ui:settings_quick-setup_open-tutorial}}` | nothing here: the tutorial lets you try every control scheme and pick yours. It opens from the main menu or the sandbox |

The answer marked `{{ui:settings_quick-setup_default-badge}}` is what the game starts with on your device. A choice applies at once and is visible in the full settings.
If your settings match no answer, none is highlighted and a line says so - these are your own settings, and a press replaces them

## Folded sections

Long tabs are split into sections. What is changed often is open, fine tuning is folded: a section opens by its heading.
The button next to the tab's reset folds or unfolds all sections at once

On the `{{ui:settings_controls_title}}` tab only the device in your hands is open

## Reset

Each tab has its own reset.
`{{ui:settings_other_reset}}` in `{{ui:settings_other_title}}` resets all tabs at once

A reset touches only settings. Your levels stay

## The version line

The settings screen has a version line. A click on it copies it

It looks like this: `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`.
This is the line to quote in a bug report, [[11_help]]

## Graphics

**Anti-aliasing.** On PC the default is `{{ui:enum_anti-aliasing-type_msaa}}`. A phone starts with no anti-aliasing. Every shape in the game is real geometry, and `{{ui:enum_anti-aliasing-type_msaa}}` gives it clean edges without blurring on every platform

`{{ui:enum_anti-aliasing-type_fxaa}}` is for weak phones. It is one pass over the whole screen, and its cost is constant. The cost of `{{ui:enum_anti-aliasing-type_msaa}}` grows when many transparent shapes are drawn on top of each other

TAA is deliberately not offered. It leaves a trail behind fast bullets, and its jitter interferes with the glitch effects

**Framerate.** The target framerate is set manually, not through vertical sync. That way a level's timing is the same on a 60 Hz and a 144 Hz screen.
While `{{ui:settings_graphics_vsync}}` is on (PC only), the framerate cap does nothing

> [!tip] Recommendation
> On a weak device, lower the **render scale** below 1 first. It costs only sharpness, and the interface stays full size. PC only

More - [[2_mobile-devices]]

## Colliders Only Mode

A mode for practice, a folded section on the `{{ui:settings_graphics_title}}` tab. With `{{ui:settings_graphics-colliders-mode_active}}` on, a level in play draws every hitbox as a flat fill of one colour on a plain background, and nothing else.
Gone: the look of the shapes themselves, shapes with no collider, effects, texts, post-processing and the theme background.
Unchanged: the music, collision, the camera and its shake, checkpoints, the interface and statistics - a run in this mode counts like any other.
Your avatar is drawn as usual

The mode works only when playing levels. The editor, the sandbox and the menu background are drawn as usual

| Option | What it does |
|---|---|
| `{{ui:settings_graphics-colliders-mode_use-alpha}}` | on (the default) - fills are semi-transparent by the colour's alpha, and overlapping obstacles show darker. The alpha never drops below 0.15. Off - every fill is solid, and the colour's alpha is locked |
| `{{ui:settings_graphics-colliders-mode_color}}` | the fill colour, red with 0.6 alpha by default. The editor's collider view uses the same hue with its own opacity |
| `{{ui:settings_graphics-colliders-mode_background}}` | what is drawn behind the fills, dark grey by default - not black, so the edge of the camera frame is visible against the black bars around it |

Both colours are folded under their own caption: unfold the one you need to get its colour wheel

## Anonymous mode

Turned on in `{{ui:settings_other_title}}` → `{{ui:settings_other_suppress-game-saves}}`

While the mode is on, the game saves nothing of its own. `settings.json`, the global statistics and the level statistics stay on disk untouched.
A changed setting still works until the game is closed

Work with levels is saved as usual: saving, exporting, importing, copying and deleting.
The editor's autosave and backups work too, they have their own switch

The mode lasts until the game is closed and is not remembered anywhere

If you turn it off, the current settings are saved. Everything played during that time is discarded

> [!info] Worth knowing
> The mode also turns on by itself. The [[12_launch-arguments|launch argument]] `--suppress-game-saves` turns it on for the whole launch, and it cannot be turned off in the game. Settings or statistics from a newer version of the game turn it on too. Then the game asks at every launch whether to keep them or overwrite them with the defaults
