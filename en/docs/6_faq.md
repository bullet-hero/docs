---
title: FAQ
date: 2026-09-25
tags: [player, level_author]
---

# FAQ

Short answers to the questions newcomers ask first, each with a link to the page that has the details

## The game

### What is Bullet Hero?

A *rhythm* and *bullet hell* hybrid: a level is a piece of music with shapes moving to it, and you steer a small square that has to survive until the track ends. The developers build it as an engine for the genre, so most levels are made by players in the editor that ships with the game. More: [[1_game/index]]

### Is it free?

Yes. The game has no purchases, no ads and no paid content. More: [[1_licensing-basics]]

### Where can you get it?

On the [[download]] page. The builds are post-alpha and unsigned, and a level made now may not load in a later version. More: [[0_quick-start]]

### Does the game need an account or the internet?

No. There are no accounts and no server, and the game sends nothing anywhere. The one network request it can make is a level loading a file its author put behind a web address. More: [[1_installation]]

### Where are the levels stored?

In the `levels` folder inside the game's own data folder. On a desktop, `Settings`, `General`, `Open Game Folder` opens it. More: [[1_installation]]

## Playing

### How do you play a level someone sent you?

A folder goes into `levels`, then press `Scan again` in the browser. An archive (`.zip`, `.tar.gz`) goes in through the editor, with the `Level Archive` generator. More: [[2_playing-levels]]

### The game says the level is from a newer version. What now?

Update the game. A build refuses a file from a newer format rather than read it wrongly. More: [[5_troubleshooting]]

### Can a forgotten level password be recovered?

No. The key is kept nowhere: not in the game, not in the file, not by the developers. More: [[5_troubleshooting]]

### Can the game play a level by itself?

Yes, the `Bot` option on the level screen: `Reflex Bot v1` or `Warm Bot v1`. A bot has exactly your controls and can still lose. More: [[9_bots]]

## Making levels

### How do you make a first level?

`Editor` in the main menu, then Editor Settings, then Create Level. Copy a track into the level folder, set the bpm, place an object with two keyframes and playtest. More: [[2_first-level]]

### Which music files work?

`ogg`, `mp3`, `wav`, `aiff` and the tracker modules. `flac` does not load. Convert to `ogg`: it is 8 to 10 times smaller than `wav` and, unlike `mp3`, adds no silence to the start. More: [[2_preparing-the-track]]

### Can I use any song?

On your own disk nothing is checked. The licence of the music matters when a level is offered to a service, and those services do not exist yet. More: [[1_licensing-basics]]

### Can I bring levels over from Project Arrhythmia?

Yes. *Afterbeat* (formerly *Project Arrhythmia*) levels, themes and prefabs are imported and exported. The folder import is not available on Android yet. More: [[3_afterbeat-import]]

### How do you share a level?

By hand, as a folder or an archive: there is no server to upload to yet. More: [[6_sharing-by-hand]]

## The project

### Are there online leaderboards or a level catalogue?

Not yet. The official server and community servers are planned, and the protocol between them and the game has not been designed. More: [[4_server/index]]
