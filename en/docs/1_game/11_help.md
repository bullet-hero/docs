---
title: Getting help
date: 2026-09-25
tags: [player, level_author]
---

# Getting help

Where to report a bug or ask a question, and what to write so the bug can be reproduced

Check [[5_troubleshooting]] first. A missing level, "update required" and a refused archive are covered there

## Where to write

| What | Where |
|---|---|
| a bug in the game or the editor, a request for the game | [bullet-hero/releases](https://github.com/bullet-hero/releases/issues) |
| a bug in the SDK or its code | [bullet-hero/sdk](https://github.com/bullet-hero/sdk/issues) |
| a mistake or an outdated fact in the docs | [bullet-hero/docs](https://github.com/bullet-hero/docs), [[5_contribute/index]] |
| a question, help with a level, discussion | [Discord](https://discord.gg/gkHQrp9NgS) |

Reports on GitHub are public. Anyone can read them and add to them.
The docs accept an issue or a pull request

Not sure it is a bug? Ask in Discord first

## What to put in a bug report

A bug the developers can reproduce gets fixed. "It crashed" usually does not: nobody knows what to repeat

1. **The version line.** Click the version line on the settings screen, it copies itself. It reads `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`, [[4_settings]]
2. **The platform and the device:** the system, and on a phone its model
3. **The steps:** what you did, what you expected and what happened
4. **The level,** if the bug is tied to one: its folder zipped, or the archive you opened. For a protected level, say that it is protected
5. **The error report,** if an error window appeared. `Save Report` writes it to the `reports` folder, `Open Reports Folder` opens that folder, [[1_installation]]

> [!tip] Tip
> Attach files to the report instead of pasting them into the text. A log is long, and a pasted one is hard to read

## Logs

The game writes a log while it runs. It helps when there was no error window at all

- **Windows:** `Player.log` in the game's data folder, `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` (Unity's standard location)
- **Android:** the log goes to logcat. With the device connected to a computer, `adb logcat -s Unity` prints it
- **Other systems:** not documented yet
