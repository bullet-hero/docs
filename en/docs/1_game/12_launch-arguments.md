---
title: Launch arguments
date: 2026-09-25
tags: [advanced_player, developer]
---

# Launch arguments

Command-line arguments that open a screen, a level or a run at once, and switches that change one launch of the game

Launch arguments tell the game what to open when it starts. They are written after the executable: in a shortcut, in a terminal or in Steam's launch options. Without them the game opens the main menu

## Syntax

- every argument starts with two hyphens: `--editor`
- a value follows after a space or after `=`: `--speed 1.5` and `--speed=1.5` are the same
- the case of a key does not matter: `--Editor` works too
- numbers use a dot whatever the system language: `1.5`, never `1,5`
- a value with spaces goes in double quotes: `--level "D:\My Levels\Volcano"`

**An argument the game cannot use never stops the launch.** It is dropped, a line about it goes to the log, and the game opens its usual screen. Where the log is - [[11_help#Logs]]

**Unknown arguments are ignored.** The game reads only its own arguments, the ones with two hyphens. Unity's own single-hyphen arguments such as `-screen-width` pass through untouched. Use them for the resolution and fullscreen

## Screens

| Argument | What opens |
|---|---|
| `--menu` | the main menu, the same as no argument |
| `--editor` | the level editor |
| `--game` | the level named by `--level`, and the run starts at once |
| `--settings` | the main menu with the settings screen open over it |

Pass at most one screen argument. Two different ones cancel each other, and the menu opens with a warning in the log

`--settings` can name a tab: `general`, `audio`, `controls`, `keybindings`, `graphics`, `interface`, `game-editor`, `profile`, `other`. Without a name the settings open on the tab you left last. A name the game does not know is dropped, and the settings still open

The settings open once per launch. Coming back to the menu later does not open them again. What each tab holds - [[4_settings]]

## Picking a level

`--level` names a level by its id (`LevelId`) or by the path to its folder. A title never works: titles repeat, get translated and get edited. A value that reads as an id is always taken as an id

The game looks for the level among the levels it lists anyway. A folder it does not list is not found

| Together with | What happens |
|---|---|
| nothing | the menu opens on the level's screen and waits for `Play` |
| `--editor` | the editor opens with the level |
| `--game` | the run starts at once |

A password is never an argument. A protected level asks for it on screen and opens once you answer

## Run options

These options fill in the controls of the level screen, then the run starts as if you pressed `Play`. They work only together with `--game`. Without it they are ignored, with a warning in the log

| Argument | Value | Control on the level screen |
|---|---|---|
| `--speed` | above `0` and up to `2`, rounded to `0.1` | `Speed` |
| `--lives` | `0` to `16`, `0` is `Zen` | `Lifes` |
| `--seed` | `0` or a positive whole number, `0` is a fresh seed every run | `Player Seed` |
| `--bot` | `none`, `reflex`, `warm` | `Bot` |
| `--checkpoints`, `--no-checkpoints` | - | `Checkpoints` |

An option left out takes its default: 3 lives, speed `1.0`, checkpoints on, no bot, seed `0`

A run started this way is an ordinary run. It counts in your statistics like any other, [[10_statistics]]

## Switches for the whole launch

These three work with any screen and never change a saved setting:

| Argument | What it does |
|---|---|
| `--autosave on`, `--autosave off` | turns the editor's autosave on or off for this launch. The `Game Editor` settings tab shows the forced value and does not let you change it |
| `--suppress-game-saves` | anonymous mode for the whole launch. It cannot be turned off in the game, [[4_settings#Anonymous mode]] |
| `--frame-stats` | writes a frame-time summary to the log, with GPU and CPU time. It is meant for measuring performance |

`--frame-stats` writes a line per screen every 30 seconds, and also whenever the window on top of the screen changes. The first 3 seconds of a screen are not counted

## Combinations

| Command | Result |
|---|---|
| nothing, or `--menu` | the menu |
| `--editor` | the editor, no level open |
| `--settings` | the menu, the settings open on the tab left last |
| `--settings graphics` | the same, on the `Graphics` tab |
| `--level X` | the menu, on level X's screen, waiting for `Play` |
| `--level X --game` | level X, playing |
| `--level X --editor` | the editor with level X open |
| `--game` without `--level` | the menu and a warning |
| `--menu --editor` | the menu and a warning |
| `--speed 2` without `--game` | the option is ignored, with a warning |
| `--editor --autosave off` | the editor, autosave off for this launch only |
| `--autosave maybe` | ignored with a warning, your setting decides |
| `--suppress-game-saves` | the menu. Nothing the game saves of its own reaches the disk during this launch |
| `--level X --game --suppress-game-saves` | level X, playing, and the run leaves no statistics behind |
| `--editor --suppress-game-saves` | the editor. Level saves, autosave and backups still write, settings and statistics do not |

## Examples

On Windows, from a terminal or a shortcut:

```bash
"Bullet Hero.exe" --editor
"Bullet Hero.exe" --level 5f2b0e6a-1c3d-4b5e-8a9f-0d1e2f3a4b5c --game --lives 1 --speed 1.5
"Bullet Hero.exe" --level "C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero\levels\Volcano" --editor
```

In Steam, write only the arguments into the game's launch options, without the executable: `--editor --autosave off`

## Android

Android has no command line. The arguments ride in the `bh` string extra of the intent that starts the game, and are split exactly like a typed line. From a computer this is done with `adb`:

```bash
adb shell "am start -S -n com.vertoker.BulletHero/com.unity3d.player.UnityPlayerGameActivity -e bh '--frame-stats --editor'"
```

- **Quotes matter.** The whole `am start` goes in double quotes, the value of `bh` in single quotes. Otherwise the device's shell splits the line: `bh` receives only the first argument, and the rest reach `am` as its own options
- **`-S` stops a running game first.** The arguments are read once, at launch. Sending them to a game that is already running changes nothing

iOS has no launch arguments at all
