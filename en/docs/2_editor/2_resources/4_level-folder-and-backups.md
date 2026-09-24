---
title: The level folder and backups
date: 2026-09-24
tags: [level_author]
---

# The level folder and backups

What is in the folder, what not to touch by hand, and why a copy of the folder is the only backup there is

A level folder lives in `levels`, inside the game's own folder. Inside it:
- `level.json` - the level's content. It can be `level.blob` if you chose the binary format
- `metadata.json` - name, description, authors, tags. Can be `metadata.blob` as well
- `logo.png` or `logo.jpg` - the cover
- `resources` - the folder holding everything the level uses: the track, images, fonts

Next to `levels` sit the device-wide libraries: `themes`, `effects`, `shapes`, `prefabs`. Those are not part of any level. You export into them what you want to reuse elsewhere and import out of them

> [!info] Worth knowing
> A level sent to another person carries everything it needs inside itself. The library does not travel with it

**The file format is decided by the extension, not by a field inside.** The game looks at what is on disk. Which is why changing the format in the editor does not merely write a new file, it deletes the old one - otherwise two would sit there and nothing could say which is real

> [!caution] Caution
> Do not rename files in `resources`. References to them are stored by name

> [!caution] Caution
> Do not edit `level.json` in a text editor while the level is open in the game. Saving from the editor overwrites those edits silently

> [!tip] Recommendation
> Keep nothing in `resources` that the level does not use. It travels with the folder

**A backup is a copy of the folder.** The whole level is one folder, so a copy of it is a complete snapshot. No other method is needed

> [!tip] Recommendation
> Make a copy before every large rework and name them by date

**A level that stopped opening is not lost, as long as it is `Json`.** That file is text and can be read by eye, and the editor's Raw tab shows the entire saved file as a tree of fields. A `Blob` gives you neither - it is binary, and a damaged one is refused whole rather than read in part

> [!caution] Caution
> The Raw tab validates nothing. It is the one surface through which deliberately broken data reaches a level, which is what it exists for. Edit there with a copy of the folder beside you

Next: [[4_not-losing-work|Not losing your work]], [[2_metadata-and-sharing|Metadata and sharing a level]]
