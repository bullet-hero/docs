---
title: Themes
date: 2026-09-25
tags: [level_author]
---

# Themes

A theme is a palette of 64 colours that objects point at by slot number. How slots, references and theme keys work, and how to make, share and import a theme

A theme is a named palette of 64 slots. A colour set to `Theme` stores no colour of its own, only a slot number, and takes whatever that slot holds in the theme active on the current frame. Change the theme and everything pointing at it changes with it. Why that beats literal colours, and how to keep a level readable under every theme, is in [[5_color-and-postprocessing]]

## What a theme holds

- **A name**, shown in the lists and pickers
- **An id**, a `ThemeId`. Theme keys point at a theme by this id, not by its name
- **64 colours** on an 8 by 8 grid, each with transparency
- **A name per slot**, optional. Until you name a slot, the list of names is not written to the file at all

A theme is data inside `level.json`, not a file in `resources` (see [[1_level-needs]]). A level can hold any number of them. The 8 by 8 layout mirrors the one in *Afterbeat*, and nothing in the game gives a slot a fixed role: the game's own `Balanced` theme simply groups its 64 colours by hue

## How a colour finds its value

It takes two steps:
1. The Theme track on the Events timeline says which theme is active on this frame
2. A colour of type `Theme` names a slot from 0 to 63 in whatever theme that is

Themeable colours include a shape's colour (each of its corners separately), a text's colour and the level background. **A slot's position is its identity.** Moving a colour to another slot restyles everything that pointed at the old one

## Switching themes over time

Between two theme keys the game blends the whole palette from one theme to the other, using the easing of the later key (see [[5_keyframes-and-easing]]). With no theme keys at all every slot is white

> [!warning] Warning
> A new key gets `Linear`, so the palette drifts across the whole stretch from the previous theme key to this one. For a switch exactly on the drop, set `Constant` on the key at the drop

> [!caution] Caution
> A theme key can outlive its theme. Delete a theme that keys still point at, and every one of those frames turns white. The keys themselves stay, and the editor asks before deleting a theme something still references

## Making and editing a theme

The Themes tab among the level's resources lists the level's themes and has `Create` and `Import`. A row opens the `Theme Editor`:
- `Name` of the theme
- `Theme Id` and `Regenerate Id`
- the 8 by 8 grid. Clicking a cell selects it, shows `Color:` with its number and loads the colour into the wheel below
- `Slot name` for the selected cell

The editor works on a copy. Nothing reaches the level until you save, and the save is one undo step

**Picking a slot.** Switch a colour to `Theme` and open `Select Theme Color`. The grid shows the palette as it is blended on the frame of the key you are editing, not at the playhead. Beside it are the two theme keys around that frame and what the selected slot holds in each. An unnamed slot reads `(unnamed)`

## Sharing and importing

- **The device library.** A row's `Export` saves the theme into `themes`, the device-wide library next to `levels` (see [[4_level-folder-and-backups]]). `Theme Library` lists it, marks what is already `In Level`, and `Delete` removes it from the library. Importing copies the theme into the level, so the level never depends on your library
- **The game's own themes.** `Select Theme` offers the themes that ship with the game next to the level's own
- **Afterbeat.** `Import .vgt` turns an *Afterbeat* theme file into a level theme, and importing the same file again updates it rather than making a copy. `Export .vgt` writes every theme of the level into a folder you pick, one file each, and drops transparency, since *Afterbeat* theme colours carry none. Both buttons are hidden on Android, iOS and WebGL (see [[3_afterbeat-import]])

Next: [[5_color-and-postprocessing|Colour, themes and post-processing]], [[1_readability-and-fairness|Readability and fairness]]
