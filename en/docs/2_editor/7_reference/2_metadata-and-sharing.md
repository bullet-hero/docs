---
title: Metadata and sharing a level
date: 2026-09-24
tags: [level_author]
---

# Metadata and sharing a level

The level's own cover - name, authors, age rating, content warnings - and how a level reaches another person

> [!caution] Caution
> The official server and the site do not exist yet. They arrive at release. Until then a level reaches another person as a folder, which is described at the end

The level's cover lives in its own file, read separately from the level itself so a catalogue can list a thousand levels without opening one of them

**Identity.** The level carries a stable id that survives renames and folder moves - that is what scores and comments hang on, not the name. There is also your own version number, which you bump when you edit. It is unrelated to the format's version

**Name and description** are localisable, and they work differently from the game's own interface text. A level's strings have no keys at all: you write the text per language, inline, and it travels inside the level

**The logo** is a file beside the level, `logo.png` or `logo.jpg`

**Authors** is who made the level - the mapping, the design. It is separate from the authors of its assets, who are credited per resource in their own records

> [!caution] Caution
> Confusing the two is how a musician ends up uncredited

**The age rating** is one number, the minimum age, so it shows directly as "12+" and two ratings compare as plain numbers

> [!info] Worth knowing
> It is deliberately one scale rather than separate ESRB, PEGI and RARS fields. User levels are not submitted to any rating board, so a per-board value would be a guess three times over. `Unrated` is zero and means nothing was declared, not that the content is safe

> [!caution] Caution
> The rating is the only warning the card carries. In a game built around drops and glitch effects, flashing is not an edge case, so if the level flashes or gets loud, say it in the description. That line is the whole warning a player gets

**Sharing a level today.** Zip the folder, send it, the other person unzips it into their own `levels` folder and opens it. Nothing is installed, nothing is registered, there is no import step

> [!warning] Warning
> Every file in `resources` travels with it, used or not. Clean it out before sending

**Sharing a level later.** The official server, the site and Steam Workshop. That is when [[1_licensing-basics|the licensing section]] stops being background reading and becomes a gate

Next: [[4_resource-record|A resource's record]], [[4_level-folder-and-backups|The level folder and backups]]
