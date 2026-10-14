---
title: Skins
date: 2026-10-15
tags: [player, advanced_player]
---

# Skins

The avatar's body is a grid of cells, and a skin decides what each cell draws: a shape and one of the skin's colours. A skin can also switch off the eyes, the hands, the shadow and the effects. Build one under `{{ui:menu_main_avatar-btn}}` in the main menu from ready shapes, a palette and a grid editor, or write the file by hand

A skin changes only the look. The hitbox, the speed and the hitbox ring stay the same for every skin

## The Avatar Hub

`{{ui:menu_main_avatar-btn}}` in the main menu opens a screen of its own. Your avatar walks on the left and the panel takes the right half. `{{ui:menu_avatar_bot}}` at the bottom left hands the avatar to you, so you can try the skin in motion, and the `{{ui:menu_avatar_damage}}` slider beside it shows how the skin loses cells as health falls. The bar on top of the panel jumps to each section:

| Section | What it does |
|---|---|
| `{{ui:menu_avatar_tab-shapes}}` | ready shapes, drawn with the eyes and hands they come with. A click puts the shape on your skin and keeps your colours. The round and polygon shapes come with eyes, the patterned ones without. The first card is the classic avatar's cube. The classic avatar itself, colours and all, is worn from `{{ui:menu_avatar_tab-skins}}` |
| `{{ui:menu_avatar_tab-colors}}` | the body colours and the eyes. Pick a target, then a colour. The hands, the trails and the dash tint follow your colours by themselves |
| `{{ui:menu_avatar_elements}}` | each button turns a part of the avatar on or off |
| `{{ui:menu_avatar_editor}}` | the grid itself: its size, the pieces in its cells, each piece's shape, colour, rotation, mirror and scale, and shapes of your own |

`{{ui:menu_avatar_randomize}}` at the top right gives your skin a random shape and colours. It is off while the classic avatar is worn. `{{ui:menu_avatar_tab-skins}}` next to it lists your skin files: a click on one wears it, and the buttons export, delete, import and duplicate. `{{ui:menu_avatar_create}}` makes a new skin from a random shape in random colours. A file the game cannot read can still be deleted from there

Every change is saved at once. The first change made on the classic avatar creates a new skin file, and from then on you wear that file

### The editor

1. `{{ui:menu_avatar_paint}}` puts the selected piece into a cell, `{{ui:menu_avatar_erase}}` empties it. Drag across the grid to do several cells at once
2. `{{ui:menu_avatar_pieces}}` lists what the cells can draw. `+` copies the selected piece, `-` removes it and its cells take the first piece
3. The selected piece takes a built-in shape or one of the skin's own. `{{ui:menu_avatar_new-mesh}}` draws a new one: place points, then connect three of them into a triangle
4. `{{ui:menu_avatar_columns}}` and `{{ui:menu_avatar_rows}}` resize the grid. Cells are square, so a grid taller than it is wide makes a tall body
5. `{{ui:menu_avatar_rotate-left}}` and `{{ui:menu_avatar_rotate-right}}` turn the whole skin a quarter: the grid and every piece with it

The top of a skin is its front: the avatar turns so that it points where it moves

A change that breaks the body - too few cells, or cells in two pieces - is not saved. The reason is shown under the grid until you fix it

## Where skins are kept

In the `skins` folder inside the data folder ([[1_installation]]). One skin is one `.json` file. `selection.json` next to them remembers which skin you wear

- on a computer `{{ui:menu_avatar_open-folder}}` opens the folder
- on a phone use `{{ui:menu_avatar_import}}` and `{{ui:menu_avatar_export}}`: they open the system file picker

Skins travel with a profile transfer and with Steam Cloud - [[14_profile-transfer]]

## The file

This is an exported skin, shortened:

```json
{"g":3,"v":{
  "id":"9b2f0d64-1c3a-4e8b-8f21-6a0c5d7e9f13",
  "name":"Hex knight",
  "size":1.0,
  "columns":5,"rows":5,
  "mask":60651675406,
  "cells":[0,0,0,0,1,1,1,0,0,1,2,1,0,0,1,1,1,0,0,0,0],
  "parts":[
    {"shape":"00000000-0000-0000-0000-000000016000","color":0},
    {"shape":"00000000-0000-0000-0000-000000001000","color":1,"scale":0.9},
    {"shape":"4d1f6c2a-7b3e-4f10-9a55-2c8e01b7d001","color":2,"rotation":90.0,"mirror":true}
  ],
  "colors":[[0,{"r":0.51,"g":0.76,"b":0.96,"a":1.0}],[0,{"r":0.2,"g":0.4,"b":0.9,"a":1.0}],[0,{"r":1.0,"g":1.0,"b":1.0,"a":1.0}]],
  "meshes":[{"id":"4d1f6c2a-7b3e-4f10-9a55-2c8e01b7d001","vts":[[0,{"x":-0.5,"y":-0.5}],[0,{"x":0.5,"y":-0.5}],[0,{"x":0.0,"y":0.5}]],"idxs":[0,1,2]}],
  "elements":125
}}
```

`g` is the file format's generation, `v` holds the skin. The easiest start is to export a skin and edit the copy

| Key | What it is |
|---|---|
| `id` | who the skin is: a GUID of its own. The game names the file after it, but finds a skin by this key, so the file name does not matter |
| `name` | the name shown in the list |
| `size` | how large the body is drawn, from `{{v:skin.size-min}}` to `{{v:skin.size-max}}` of the classic one. The hitbox does not change |
| `columns`, `rows` | the grid's width and height, from `{{v:skin.grid-min}}` to `{{v:skin.grid-max}}`. Cells are square: the longer side spans the body |
| `mask` | which cells are filled, as one 64-bit number: the cell in column `x` and row `y` is bit `y * 8 + x`, row 0 at the bottom. The row is always 8 bits wide, whatever `columns` says |
| `cells` | the part each filled cell draws, an index into `parts`, in the order of the bits from the lowest. Leave it empty and every cell draws part 0 |
| `parts` | what a cell draws: `shape` (the id of a built-in shape, or the `id` of one of the skin's `meshes`), `color` (an index into `colors`), `rotation` (degrees), `mirror` and `scale` (from `{{v:skin.part-scale-min}}` to `{{v:skin.part-scale-max}}` of the cell) |
| `colors` | the body colours, from 1 to `{{v:skin.colors-max}}`. A colour is `[0,{"r":…,"g":…,"b":…,"a":…}]`, each channel from 0 to 1 |
| `meshes` | up to `{{v:skin.meshes-max}}` shapes of the skin's own: an `id` (any GUID that is not a built-in shape's), points `vts` inside the box from -0.5 to 0.5 and triangles `idxs`, three points each |
| `elements` | which parts of the avatar are drawn, as the sum of: eyes 1, hands 2, shadow 4, trail 8, dash trail 16, hit burst 32, dash tint 64. 127 draws everything, a new skin starts at 125: everything but the hands. The grid is always drawn |
| `eyes`, `hands`, `shadow`, `move_effect`, `dash_effect`, `damage_effect`, `dash_body` | the colours of the rest of the avatar, in the same form as `colors`. A part switched off in `elements` keeps its colour |

A key you leave out keeps the classic avatar's value. A built-in shape's id is easiest to copy from an exported skin: the patterned presets under `{{ui:menu_avatar_tab-shapes}}` use only built-in shapes. A file you write by hand may leave `id` out - `{{ui:menu_avatar_import}}` gives it one

## What a skin must follow

- `columns` and `rows` are `{{v:skin.grid-min}}` to `{{v:skin.grid-max}}`, and `mask` fills no cell outside them
- at least `{{v:skin.filled-min}}` cells are filled, and all of them touch each other by an edge: the body is one piece
- `cells` is empty or holds exactly one part for every filled cell
- at most `{{v:skin.parts-max}}` parts, and every part's shape and colour exist
- the body and the shadow are drawn with an opacity of at least `{{v:skin.body-alpha-min}}`

A skin that breaks a rule is shown greyed out in `{{ui:menu_avatar_tab-skins}}` with the reason, and cannot be worn. So is a second file with the same `id`. If the worn skin breaks, the classic avatar is drawn and your choice is kept. A skin written by a newer version of the game says `{{ui:menu_avatar_newer}}`

## Health

Health is shown by the filled cells only. Lost cells stay as dark ghosts, from the edge towards the centre, and the last cell holds while any health is left. With fewer filled cells each one is worth more health - [[7_damage]]
