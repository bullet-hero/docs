---
title: The level folder and backups
date: 2026-09-24
tags: [level_author]
---

# The level folder and backups

What lies in a level folder, what not to touch by hand and how to make a backup

## What is in the folder

A level folder lives in `levels` inside the game's folder. Where the game's folder is - [[1_installation]]

| File | What it is |
|---|---|
| `level.json` | the level's content. In the binary format - `level.blob` |
| `metadata.json` | name, description, authors, tags. In the binary format - `metadata.blob` |
| `logo.png` or `logo.jpg` | the cover |
| `resources` | everything the level uses: the track, images, fonts |

Next to `levels` sit the device-wide libraries: `themes`, `effects`, `shapes`, `prefabs`.
They are not part of any level. You export into them what you want to reuse and import out of them

A level sent to another person carries everything it needs inside itself. The libraries do not travel with it

## What not to touch by hand

> [!caution] Caution
> Do not rename files in `resources`. References to them are stored by name, so a renamed file is a missing file

Do not edit `level.json` in a text editor while the level is open in the game. Saving from the editor overwrites your edits silently

Keep nothing in `resources` that the level does not use. It travels with the folder

The file format is decided by the extension, not by a field inside. So changing the format in the editor writes a new file and deletes the old one.
Otherwise two files would sit on disk, and nothing could say which one is real

## Backups and recovery

**A complete backup is a copy of the level folder.** It holds everything, resources included.
Make a copy before every large rework and name it by date

**Autosave keeps the level file only.** No metadata, track or images.
Each autosave puts a copy in `backups/<level id>/` in the game's folder, outside `levels`. `25` copies are kept. How to restore a copy - [[4_not-losing-work#Autosave]]

**A `Json` level that stopped opening is not lost.** The file is text and can be read by eye. The `Raw Data` tab shows the whole file as a tree of fields

A `Blob` cannot be saved that way. It is binary, and a damaged file is refused whole rather than read in part

What to know before editing in the `Raw Data` tab - [[4_not-losing-work#The Raw tab]]

Next: [[4_not-losing-work]], [[2_metadata-and-sharing]]
