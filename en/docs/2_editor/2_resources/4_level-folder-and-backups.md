---
title: The level folder and backups
date: 2026-09-24
tags: [level_author]
---

# The level folder and backups

What is in the folder, what not to touch by hand, and what autosave copies and a copy of the folder each keep

## What is in the folder

A level folder lives in `levels`, inside the game's own folder. Inside it:
- `level.json` - the level's content. It can be `level.blob` if you chose the binary format
- `metadata.json` - name, description, authors, tags. Can be `metadata.blob` as well
- `logo.png` or `logo.jpg` - the cover
- `resources` - the folder holding everything the level uses: the track, images, fonts

Next to `levels` sit the device-wide libraries: `themes`, `effects`, `shapes`, `prefabs`. Those are not part of any level. You export into them what you want to reuse elsewhere and import out of them

A level sent to another person carries everything it needs inside itself. The library does not travel with it

## What not to touch by hand

**The file format is decided by the extension, not by a field inside.** The game looks at what is on disk. Which is why changing the format in the editor does not merely write a new file, it deletes the old one - otherwise two would sit there and nothing could say which is real

> [!caution] Caution
> Do not rename files in `resources`. References to them are stored by name

Do not edit `level.json` in a text editor while the level is open in the game either. Saving from the editor overwrites those edits silently

Keep nothing in `resources` that the level does not use, because it travels with the folder

## Backups and recovery

**Autosave keeps copies of the level file.** Each autosave writes one to `backups/<level id>/` in the game's folder, outside `levels`, and `25` are kept. A copy holds the level alone, without metadata, track or images. How it works and how to restore a copy: [[4_not-losing-work#Autosave]]

**A complete snapshot is a copy of the folder.** The whole level is one folder, so a copy of it holds everything, resources included. Make one before every large rework and name them by date

**A level that stopped opening is not lost, as long as it is `Json`.** That file is text and can be read by eye, and the editor's Raw tab shows the entire saved file as a tree of fields. A `Blob` gives you neither - it is binary, and a damaged one is refused whole rather than read in part. What to know before editing in the Raw tab: [[4_not-losing-work#The Raw tab]]

Next: [[4_not-losing-work]], [[2_metadata-and-sharing]]
