---
title: Help and bug reports
date: 2026-10-02
tags: [player, level_author]
---

# Help and bug reports

Game bugs go to the releases issues, questions go to Discord. Attach the version string from the settings and the steps after which the bug appears

Check [[5_troubleshooting]] first. A missing level, "the game needs an update" and a rejected archive are covered there

## Where to write

| What | Where |
|---|---|
| a bug in the game or the editor, a request for the game | [bullet-hero/releases](https://github.com/bullet-hero/releases/issues) |
| a bug in the SDK or its code | [bullet-hero/sdk](https://github.com/bullet-hero/sdk/issues) |
| a mistake or an outdated fact in the docs | [bullet-hero/docs](https://github.com/bullet-hero/docs), [[community]] |
| a question, help with a level, a discussion | [Discord](https://discord.gg/gkHQrp9NgS) |

Messages on GitHub are public. Anyone can read them and add to them.
You can send an issue or a pull request to the docs

Not sure it is a bug? Ask in Discord first

All project links - [[links]]

## What to put in a bug report

A bug that can be reproduced gets fixed. "It crashed" usually cannot be fixed: nobody knows what to repeat

1. **The version string.** Click the version string on the settings screen and it is copied by itself. It looks like this: `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`, [[4_settings]]
2. **Platform and device:** the system, and for a phone, the model
3. **Steps:** what you did, what you expected and what happened
4. **The level,** if the bug is tied to it: its folder in an archive, or the archive you opened. If the level is protected, say so
5. **The error report,** if there was an error window. `{{ui:root_error_save}}` writes it to the `reports` folder, `{{ui:root_error_open-reports-folder}}` opens it, [[1_installation]]

> [!tip] Tip
> Attach files to the message instead of pasting them into the text. A log is long, and it is hard to read inside the text

## Logs

The game writes a log while it runs. It helps when there was no error window at all

- **Windows:** `Player.log` in the game's data folder, `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` (Unity's standard location)
- **Android:** the log goes to logcat. With the device connected to a computer, `adb logcat -s Unity` prints it
- **Other systems:** not described yet
