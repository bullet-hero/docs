---
title: Quick start
date: 2026-09-24
tags: [player, level_author]
---

# Quick start

Six steps from no game at all to your first level played and your first level built, each with a link to the full page

Every step below is the shortest route. The details, the exceptions and the other platforms are on the linked pages. Short answers to common questions are in [[6_faq]]

## 1. Get the game

The [[download]] page has a Windows `.exe` and an Android `.apk` you install by hand. Linux, macOS and iOS have no build there yet, see [[0_status]]. They are post-alpha and unsigned, and a level made now may not load in a later version. Where the game keeps your files and what updating does to them: [[1_installation]]

## 2. Launch it

The main menu has `Levels`, `Editor` and `Settings`. `Story` and `Multiplayer` are there too, but those modes are not built yet. On Android the game shows `Folder access` before the first file picker: it sees only the folder you pick

## 3. Play a first level

`Levels` opens the level browser: `My Levels` (the `levels` folder), `Built-in`, and `Workshop` in Steam builds. Pick a level, set the options on its screen and press `Play`. You steer a small square that has to survive until the track ends

> [!tip] Tip
> For a first run set `Lifes` to `Zen`: the run never ends, so you hear the whole track while you learn the controls

A level someone sent you is a folder: copy it into `levels` and press `Scan again`. An archive (`.zip`, `.tar.gz`) goes in through the editor, with the `Level Archive` generator. Both routes are in [[2_playing-levels]]

## 4. Learn the controls

| Device | Steer | Dash |
|---|---|---|
| mouse | hold the left button, the avatar follows the mouse | `Space`, `Shift` or the right button |
| touchscreen | drag anywhere | a second finger |
| gamepad | either stick | the bottom face button or the right shoulder |

Everything is rebound in `Settings`, `Controls`. If a device seems to do nothing, look at `Active now` there first. The full picture: [[3_controls]]

## 5. If something fails

- A copied level is not listed: the folder has to be the level folder itself, directly inside `levels`. Press `Scan again`
- The game says the level is from a newer version: update the game
- An error window: `Save Report` writes a report to the `reports` folder. Attach it when you report the problem

Every known case is in [[5_troubleshooting]]. Where to report a problem and what to attach: [[11_help]]

## 6. Build your first level

`Editor` in the main menu, then Editor Settings, then Create Level: a preset, a name, a duration. Copy an `ogg`, `mp3`, `wav` or `aiff` track into the level folder (`flac` does not load), set the bpm on the Beat panel, place an object with two keyframes on its position and playtest. A track of 1 to 2 minutes is enough for a start

Autosave is on by default: 60 seconds after an unsaved edit it writes a copy of the level to `backups` and saves the level itself. `Ctrl+S` saves at once. What autosave keeps and what it does not: [[4_not-losing-work#Autosave]]

The route step by step: [[2_first-level]]
