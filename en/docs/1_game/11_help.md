---
title: Getting help
date: 2026-09-25
tags: [player, level_author]
---

# Getting help

Where to report a bug or ask a question about the game and the editor, and what to put in a report so it can be reproduced

## Where to write

| Where | For what |
|---|---|
| [GitHub issues of the SDK](https://github.com/vertoker/bullet-hero-sdk/issues) | bugs in the game, the editor and the SDK. Public, anyone can read and add to a report |
| [Discord server](https://discord.gg/gkHQrp9NgS) | questions, help with a level, discussion before a report |
| [bullet-hero-docs](https://github.com/vertoker/bullet-hero-docs) | a mistake or an outdated fact on these pages, as an issue or a pull request, see [[5_contribute/index]] |

Before writing, check [[5_troubleshooting]]: a missing level, an "update required" message and a refused archive are covered there

## What to put in a bug report

A report the developers can reproduce gets fixed. One that says only "it crashed" usually does not, because nobody knows what to repeat

1. **The version line.** Click the version line on the settings screen, it copies itself. It reads `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>` (see [[4_settings]])
2. **The platform and the device:** the system, and on a phone its model
3. **The steps:** what you did, what you expected and what happened instead
4. **The level,** if the bug is tied to one: its folder zipped, or the archive you opened. For a protected level, say that it is protected
5. **The error report,** if an error window appeared: `Save Report` writes it to the `reports` folder, `Open Reports Folder` opens that folder (see [[1_installation]])

## Logs

The game writes a log while it runs. It helps when there was no error window at all

- **Windows:** `Player.log` in the game's data folder, `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` (Unity's standard location)
- **Android:** the log goes to logcat. With the device connected to a computer, `adb logcat -s Unity` prints it
- **Other systems:** not documented yet

> [!tip] Tip
> Attach files to the report instead of pasting them into the text. A log is long, and a pasted one is hard to read
