---
title: What a level is
date: 2026-09-24
tags: [level_author]
---

# What a level is

A level is a folder of files. What is inside it, which format to keep it in and how to hand a level to another person

## What is in the folder

A Bullet Hero level is an ordinary folder on disk. Not a row in a database and not an encrypted archive

There are two main files:
- `level.json` - the level itself: objects, keyframes, themes, resources
- `metadata.json` - the cover: name, description, authors, tags, duration

Next to them sits everything the level uses: the track, images, fonts.
The developers ship no textures at all. Everything you see in a level is either a built-in shape or a file from that folder

The cover is a separate file, so that listing a thousand levels does not mean opening a thousand levels

The full list of files - [[4_level-folder-and-backups]]

## Json or Blob

You choose the file format when you create a level:

| Format | What it is |
|---|---|
| `Json` | plain text, opens in any editor and can be fixed by hand |
| `Blob` | a binary file, dozens of times faster to load and a third of the size, unreadable by eye |

> [!tip] Recommendation
> Build the level in `Json` and switch it to `Blob` when it is finished. If the level stops opening, `Json` can be read and fixed by hand. `Blob` is almost unrepairable: a single damaged byte fails its integrity check

## How to hand a level over

A level travels by copying. Zip the folder, send it, unzip it, open it.
Nothing is installed, registered or imported

On PC this always works. On a phone - wherever the system lets you in

What follows from that:
- a backup of a level is a copy of the folder
- do not rename files inside the folder: resources are found by name
- a level the editor will not open can still be read by eye or in the `Raw Data` tab

> [!caution] Caution
> Do not edit `level.json` in a text editor while the level is open in the game. Saving from the editor overwrites your edits silently

## The format is open

The level data model lives in a separate repository under the MIT licence - [bullet-hero/sdk](https://github.com/bullet-hero/sdk).
So a level can be read without the game, and anyone can write their own tool for the format. A defect in the format is visible from outside too

More about the format - [[3_sdk/index]]

Next: [[2_first-level]], [[4_level-folder-and-backups]]
