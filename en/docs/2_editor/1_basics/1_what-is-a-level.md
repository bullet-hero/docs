---
title: What a level is
date: 2026-09-24
tags: [level_author]
---

# What a level is

A level is a folder of files, not a row in a database. What is inside it, why the format is open, and how you hand one to another person

A Bullet Hero level is a folder on disk. Not a row in a database and not an encrypted archive. A folder with ordinary files in it

At minimum there are two:
- `level.json` - the level itself: objects, keyframes, themes, resources, all the content
- `metadata.json` - the cover: name, description, authors, tags, duration

Next to them sits everything the level uses: the track, images, fonts. The developers ship no texture of their own, so everything you see in a level is a file that lives in that folder

> [!info] Worth knowing
> `metadata.json` is read separately from `level.json`, and that is for the catalogue: listing a thousand levels must not mean opening a thousand levels. The name and the description therefore live apart from the content

**You choose the file format.** Creating a level offers two:
- `Json` - plain text, openable in any editor and repairable by hand
- `Blob` - binary, dozens of times faster to load and a third of the size, unreadable by eye

> [!tip] Recommendation
> Build the level in `Json` and switch to `Blob` when it is finished. Json is the stable format to work in, because a level that stopped opening can still be read and fixed by hand. Blob is the fast format to play, and it is almost unrepairable - a single damaged byte fails its integrity check and there is nothing inside that a person can read

**The format is open.** The level data model is a separate MIT repository, [bullet-hero-sdk](https://github.com/vertoker/bullet-hero-sdk), so the levels stay readable independently of the game, a third-party tool can be written against them, and a defect in the format is visible from outside

**A level travels by copying.** Zip the folder, send it, unzip it, open it. Nothing is installed, nothing is registered, there is no import step. This works anywhere there is direct file access - on PC always, on mobile it depends on where the system lets you in

What follows from that in practice:
- do not rename files inside the folder by hand, resource references are stored by name
- a backup of a level is a copy of the folder, and nothing else is needed
- a level the editor will not open can still be read and repaired by eye, and the editor has a Raw tab for exactly that

> [!caution] Caution
> Do not edit `level.json` in a text editor while the level is open in the game. Saving from the editor overwrites those edits silently

Next: [[2_first-level|Your first level: the route]], [[4_level-folder-and-backups|The level folder and backups]]
