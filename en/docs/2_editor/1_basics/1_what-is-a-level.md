---
title: What a level is
date: 2026-10-01
tags: [level_author]
---

# What a level is

A level is an ordinary folder on disk: the level file, the metadata and everything it uses. Build it in Json and hand it over as a copy of the folder, nothing needs installing

## What is in the folder

The folder is not a row in a database and not an encrypted archive

There are two main files:
- `level.json` - the level itself: objects, keys, themes, resources
- `metadata.json` - the cover: name, description, authors, tags, duration

Next to them sits everything the level uses: the track, images, fonts.
The game ships no textures at all. Everything you see in a level is either a built-in shape or a file from this folder

The cover is a separate file, so that listing a thousand levels does not mean opening a thousand levels

The full list of files - [[4_level-folder-and-backups]]

## Json or Blob

You choose the file format when you create a level:

| Format | What it is |
|---|---|
| `Json` | plain text, opens in any editor and can be fixed by hand |
| `Blob` | a binary file, loads dozens of times faster and is a third of the size, unreadable by eye |

> [!tip] Recommendation
> Build the level in `Json` and convert it to `Blob` when it is finished. If the level stops opening, `Json` can be read and fixed by hand. `Blob` is almost unrepairable: a single damaged byte fails the integrity check

## How to hand a level over

A level travels by copying. Zip the folder, send it, unzip it, open it.
Nothing is installed, registered or imported

On PC this always works. On a phone - wherever the system lets you in

What follows from that:
- a backup of a level is a copy of the folder
- do not rename files inside the folder: resources are found by name
- a level the editor will not open can be read by eye or in the `Raw Data` tab

> [!caution] Caution
> Do not edit `level.json` in a text editor while the level is open in the game. Saving from the editor silently overwrites your edits

## The format is open

The level data model lives in a separate repository under the MIT licence - [bullet-hero/sdk](https://github.com/bullet-hero/sdk).
So a level can be read without the game, and you can write your own tool for the format. A defect in the format is visible from outside too

More about the format - [[3_sdk/index]]

Next: [[2_first-level]], [[4_level-folder-and-backups]]
