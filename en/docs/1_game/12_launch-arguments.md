---
title: Launch arguments
date: 2026-10-02
tags: [advanced_player, developer]
---

# Launch arguments

Launch arguments open a screen, a level or a run straight away, and switches change a single launch of the game. They go after the executable: in a shortcut, a terminal or Steam's launch options

Without arguments the game opens the main menu

## Syntax

- every argument starts with two hyphens: `--editor`
- a value follows after a space or after `=`: `--speed 1.5` and `--speed=1.5` are the same
- the key's case does not matter: `--Editor` works too
- numbers use a dot whatever the system language: `1.5`, never `1,5`
- a value with spaces goes in double quotes: `--level "D:\My Levels\Volcano"`

**An argument the game cannot use never stops the launch.** It is dropped, a line about it goes to the log, and the game opens its usual screen. Where the log is - [[11_help#Logs]]

**Unknown arguments are ignored.** The game reads only its own arguments, the ones with two hyphens. Unity's own arguments with one hyphen, for example `-screen-width`, pass through untouched. Set resolution and fullscreen with them

## Screens

| Argument | What opens |
|---|---|
| `--menu` | the main menu, the same as no arguments |
| `--editor` | the level editor |
| `--game` | the level given in `--level`, and the run starts at once |
| `--settings` | the main menu with the settings screen on top of it |

At most one screen argument is passed. Two different ones cancel each other, and the menu opens with a warning in the log

`--settings` can name a tab: `general`, `audio`, `controls`, `keybindings`, `graphics`, `interface`, `game-editor`, `profile`, `other`. Without a name the settings open on the tab you were on last time. An unknown name is dropped, and the settings open anyway

The settings open once per launch. If you return to the menu later, they do not open again. What each tab holds - [[4_settings]]

## Choosing a level

`--level` names a level by its identifier (`LevelId`) or by the path to its folder. A title never works: titles repeat, get translated and get edited. A value that reads as an identifier is always taken as an identifier

The level is looked up among the ones the game already shows in its list. The game will not find a folder that is not in the list

| Together with | What happens |
|---|---|
| nothing | the menu opens on the level screen and waits for `{{ui:menu_levelview_play-btn}}` |
| `--editor` | the editor opens with this level |
| `--game` | the run starts at once |

A password is never passed as an argument. A protected level asks for it on screen and opens after the answer

## Run conditions

These conditions fill in the controls of the level screen, and the run starts as if you had pressed `{{ui:menu_levelview_play-btn}}`. They work only together with `--game`. Without it they are ignored, with a warning in the log

| Argument | Value | Control on the level screen |
|---|---|---|
| `--speed` | above `0` and up to `2`, rounded to `0.1` | `{{ui:field_common_speed}}` |
| `--lives` | from `0` to `16`, `0` is `{{ui:menu_levelview_options-lifes_option-zen}}` | `{{ui:menu_levelview_options-lifes_title}}` |
| `--seed` | `0` or a positive integer, `0` means a new seed for every run | `{{ui:level_level-view_seed-value}}` |
| `--bot` | `none`, `reflex`, `warm` | `{{ui:menu_levelview_options-bot}}` |
| `--checkpoints`, `--no-checkpoints` | - | `{{ui:menu_levelview_options-checkpoints_title}}` |
| `--no-collision` | - | `{{ui:menu_levelview_options-no-collision_title}}` |

A condition left out takes its default value: 3 lives, speed `1.0`, checkpoints on, no bot, seed `0`, collision on

A run started this way is an ordinary run. It goes into statistics like any other, [[10_statistics]]

## Switches for the whole launch

These three work with any screen and never change a saved setting:

| Argument | What it does |
|---|---|
| `--autosave on`, `--autosave off` | turns the editor's autosave on or off for this launch. The `{{ui:settings_game-editor_title}}` settings tab shows the forced value and does not let you change it |
| `--suppress-game-saves` | anonymous mode for the whole launch. It cannot be turned off in the game, [[4_settings#Anonymous mode]] |
| `--frame-stats` | writes a frame time summary to the log, with GPU and CPU time. Used for performance measurements |

`--frame-stats` writes a line per screen once every 30 seconds, and also every time the window on top of the screen changes. The first 3 seconds of a screen are not counted

## Combinations

| Command | Result |
|---|---|
| nothing or `--menu` | menu |
| `--editor` | the editor with no level open |
| `--settings` | menu, settings open on the tab you were on last time |
| `--settings graphics` | the same, on the `{{ui:settings_graphics_title}}` tab |
| `--level X` | menu on the screen of level X, waits for `{{ui:menu_levelview_play-btn}}` |
| `--level X --game` | level X, a run in progress |
| `--level X --editor` | the editor with level X open |
| `--game` without `--level` | menu and a warning |
| `--menu --editor` | menu and a warning |
| `--speed 2` without `--game` | the condition is ignored, with a warning |
| `--editor --autosave off` | the editor, autosave off for this launch only |
| `--autosave maybe` | ignored with a warning, your setting decides |
| `--suppress-game-saves` | menu. None of the game's own saves from this launch reach the disk |
| `--level X --game --suppress-game-saves` | level X, a run in progress, and no statistics are left after it |
| `--editor --suppress-game-saves` | the editor. Level saves, autosave and backups are written, settings and statistics are not |

## Examples

On Windows, from a terminal or a shortcut:

```bash
"Bullet Hero.exe" --editor
"Bullet Hero.exe" --level 5f2b0e6a-1c3d-4b5e-8a9f-0d1e2f3a4b5c --game --lives 1 --speed 1.5
"Bullet Hero.exe" --level "C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero\levels\Volcano" --editor
```

In Steam, the game's launch options take only the arguments, without the executable: `--editor --autosave off`

## Android

Android has no command line. The arguments are passed in the `bh` string extra of the intent that launches the game, and are split exactly like a typed line. From a computer this is done with `adb`:

```bash
adb shell "am start -S -n com.vertoker.BulletHero/com.unity3d.player.UnityPlayerGameActivity -e bh '--frame-stats --editor'"
```

- **The quotes matter.** The whole `am start` goes in double quotes, the `bh` value in single quotes. Otherwise the device's shell splits the line: only the first argument reaches `bh`, and the rest go to `am` as its own parameters
- **`-S` stops the running game first.** The arguments are read once, at launch. Sending them to a game that is already running changes nothing

iOS has no launch arguments at all
