---
title: FAQ
date: 2026-09-25
tags: [player, level_author]
---

# FAQ

Short answers to the questions newcomers ask first, with links to the details

## The game

### What is Bullet Hero?

A hybrid of a *rhythm game* and *bullet hell*. A level is music with shapes moving to it. You steer a small square, and it has to survive to the end of the track

The developers build an engine for the genre. So most levels are made by players in the built-in editor.
More - [[1_game/index]]

### Is it free?

Yes. The game has no purchases, no ads and no paid content.
More - [[1_licensing-basics]]

### Where can you get it?

Every build and store - [[download]]

The game is in alpha. The builds are unsigned

### Does the game need an account or the internet?

No. There are no accounts and no server, and the game sends nothing anywhere

The internet is needed only by one kind of level: one that loads a file from its author's web address.
More - [[1_installation]]

### Where are the levels stored?

In the `levels` folder inside the game's data folder. To open it: `Settings` → `General` → `Open Game Folder`.
More - [[1_installation]]

## Playing

### How do you play a level someone sent you?

Put the folder into `levels` and press `Scan again` in the level list.
An archive (`.zip`, `.tar.gz`) opens through the editor, with the `Level Archive` generator.
More - [[2_playing-levels]]

### The game says the level is from a newer version. What now?

Update the game. An old version does not open files from a newer one, so that it never reads them wrongly.
More - [[5_troubleshooting]]

### Can a forgotten level password be recovered?

No. The key is kept nowhere: not in the game, not in the file, not by the developers.
More - [[5_troubleshooting]]

### Can the game play a level by itself?

Yes, the `Bot` option on the level screen: `Reflex Bot v1` or `Warm Bot v1`. A bot has the same controls as you and can still lose.
More - [[9_bots]]

## Making levels

### How do you make a first level?

`Editor` in the main menu, then `Editor Settings`, then `Create Level`.
Copy a track into the level folder, set the tempo (bpm), place an object with two keyframes and playtest.
More - [[2_first-level]]

### Which music files work?

`ogg`, `mp3`, `wav`, `aiff` and the tracker modules. `flac` does not load

`ogg` is the best choice. It is 8 to 10 times smaller than `wav` and, unlike `mp3`, adds no silence to the start.
More - [[2_preparing-the-track]]

### Can I use any song?

On your own disk nothing is checked. The licence of the music matters when a level is offered to a service, and those services do not exist yet.
More - [[1_licensing-basics]]

### Can I bring levels over from Project Arrhythmia?

Yes. *Afterbeat* (formerly *Project Arrhythmia*) levels, themes and prefabs are imported and exported. The folder import is not available on Android yet.
More - [[3_afterbeat-import]]

### How do you share a level?

By hand, as a folder or an archive. There is no server to upload to yet.
More - [[6_sharing-by-hand]]

## The project

### Are there online leaderboards or a level catalogue?

Not yet. The official server and community servers are in development.
More - [[4_server/index]]

### Found a bug?

Report a bug in the game in [bullet-hero-releases](https://github.com/vertoker/bullet-hero-releases/issues). Bring questions to [Discord](https://discord.gg/gkHQrp9NgS).
Where to write and what to attach - [[11_help]]
