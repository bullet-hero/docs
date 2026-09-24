---
title: Metadata and sharing a level
date: 2026-09-24
tags: [level_author]
---

# Metadata and sharing a level

The level's own cover - name, authors, age rating, content warnings - and how a level reaches another person

> [!warning] Warning
> The official server and the site do not exist yet. They arrive at release. Until then a level is shared as a folder, described at the end of the page

## The metadata file

The level's cover lives in its own file. It is read without the level itself.
That way a catalogue can list a thousand levels without opening one of them

## Identity

The level carries a stable id. It survives renames and folder moves.
Scores and comments are tied to it, not to the name

There is also your own version number for the level. Bump it when you edit. It is unrelated to the format's version

## Name, description and logo

**Name and description** can be translated into several languages. They have no keys: you write the text for each language inline.
The text is stored inside the level. That is how it differs from the game's own interface text

**The logo** is a file beside the level, `logo.png` or `logo.jpg`

## Authors

**Authors** are the people who made the level: the mapping, the design.
Asset authors are credited separately, in each resource's own record

> [!caution] Caution
> Confuse the two lists and the musician ends up uncredited

## Age rating

**The age rating** is one number, the minimum age. It shows as "12+". Two ratings compare as plain numbers

`Unrated` is zero. It means nothing was declared, not that the content is safe

> [!info] Worth knowing
> There is one scale, with no separate ESRB, PEGI and RARS fields. User levels are not submitted to any rating board, so a value per board would be a guess

> [!caution] Caution
> The rating is the only warning on the card. If the level flashes or gets loud, say so in the description. In a game of drops and glitch effects flashing is common, and that line is the whole warning a player gets

## Sharing a level today

1. Zip the level folder and send it
2. The other person unzips it into their own `levels` folder
3. The level opens. Nothing is installed or imported

> [!warning] Warning
> Every file in `resources` travels with the folder, used or not. Clean it out before sending

## Sharing a level later

The official server, the site and publishing to Steam Workshop are planned

Steam builds already read Workshop: they list and play the levels you subscribed to. More - [[2_playing-levels]].
The game cannot publish a level there yet

Once publishing arrives, [[1_licensing-basics|the licensing section]] becomes required reading

Next: [[4_resource-record|A resource's record]], [[4_level-folder-and-backups|The level folder and backups]]
