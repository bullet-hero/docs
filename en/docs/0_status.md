---
title: Current status
date: 2026-09-25
tags: [player, level_author, developer]
---

# Current status

Which products of Bullet Hero exist today, in which version, and what works in each of them

At the time of writing (2026-09-25) the state of the complex is:

| Product | Version | Status |
|---|---|---|
| Game | `gv 0.16.2` | post-alpha, builds for Windows and Android |
| Level editor | `gv 0.16.2`, part of the game | released with the game |
| SDK | `sv 0.16.2` | open under MIT |
| Server | none yet (`bv`) | planned, not built |
| Website | `fv 0.11.1` | working, closed |
| Documentation | no version | open, in English and Russian |

What each version number means is in [[5_versioning]]

## Game

- **Post-alpha.** The builds are unsigned, and a level made now may not load in a later version
- **On the [[download]] page:** a Windows `.exe` and an Android `.apk`. The other platforms and stores listed in [[1_game/index]] have no build there yet
- **What works:** the level browser, playing levels, level archives with passwords, bots, statistics and settings
- **What does not yet:** the `Story` and `Multiplayer` buttons are in the main menu, but neither mode is built
- **No accounts and no server:** everything the game remembers stays on your device

## Level editor

- **The same build as the game,** so its version is `gv`
- **Autosave** is on by default: it saves the level and keeps copies of it in the `backups` folder, outside the level folder (see [[4_not-losing-work#Autosave]])
- **Export** writes a level to a folder or an archive and can protect it with a password. Levels are shared by hand, see [[6_sharing-by-hand]]
- **The Afterbeat folder import** works on desktop and is not available on Android yet

## SDK

- **Version `sv 0.16.2`**, the current level format generation is `mg 1`
- **Open under MIT** at [github.com/vertoker/bullet-hero-sdk](https://github.com/vertoker/bullet-hero-sdk)
- **Not published on nuget.org.** It is built from the sources, see [[1_sdk-installation]]

## Server

- **There is no server,** official (OWS) or community (NOWS)
- **The protocol** between the game and a server has not been designed
- What is already decided is in [[4_server/index]]

## Website

- **Version `fv 0.11.1`**, the source is closed
- **What it shows:** the documentation, notes and the download page, in English and Russian
- **Level browsing, profiles and leaderboards** are planned and not built

## Documentation

- **Open** at [github.com/vertoker/bullet-hero-docs](https://github.com/vertoker/bullet-hero-docs), anyone can fix a text or add a translation
- **Two languages,** English and Russian. How to contribute is in [[5_contribute/index]]
