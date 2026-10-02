---
title: Themes
date: 2026-10-02
tags: [level_author]
---

# Themes

A theme is a palette of 64 colours that objects refer to by slot number. Change the theme, and everything that refers to it changes with it

A colour of type `Theme` stores no colour of its own, only a slot number.
It takes whatever that slot holds in the theme active on the current frame

Why this beats hand-typed colours and how to keep a level readable under any theme - [[5_color-and-postprocessing]]

## What a theme holds

- **A name** - shown in lists and pickers
- **An id**, `ThemeId`. Theme keys refer to a theme by it, not by name
- **64 colours** on an 8 by 8 grid, each with transparency
- **A slot name** for each slot, optional. Until you name at least one slot, the file stores `null` instead of the list of names

A theme is data inside `level.json`, not a separate file in the level folder (see [[1_level-needs]]).
A level can hold any number of themes

The game assigns no role to a slot: the game's own `Balanced` theme simply groups its 64 colours by hue

## How a colour finds its value

In two steps:
1. The `Theme` track on the events timeline says which theme is active on this frame
2. A colour of type `Theme` names a slot from 0 to 63 in the active theme

Things that can refer to a theme include, for example, a shape's colour (each of its corners separately), a text's colour and the level background

**A slot's position is its identity.** Move a colour to another slot, and everything that referred to the old one is recoloured

## Switching themes over time

Between two theme keys the game smoothly blends the whole palette from one theme to the other.
The easing comes from the later key (see [[5_keyframes-and-easing]])

If there are no theme keys at all, every slot is white

> [!warning] Warning
> A new key gets `Linear`, so the palette drifts across the whole stretch from the previous theme key to this one. For the theme to switch exactly on the drop, set `Constant` on the key at the drop

> [!caution] Caution
> A theme key can outlive the theme itself. Delete a theme that keys still refer to, and all those frames turn white. The keys themselves stay. The editor asks again before deleting such a theme

## How to create and edit a theme

The `Themes` tab among the level's resources shows the level's themes. It has `{{ui:settings_level-settings_resources-themes-add}}` and `{{ui:settings_level-settings_resources-themes-import}}`.
Clicking a row opens the `{{ui:settings_level-settings_theme-editor}}`:
- `{{ui:field_common_name}}` of the theme
- `Theme Id` and `{{ui:settings_level-settings_theme-editor-regenerate-id}}`
- the 8 by 8 grid. Clicking a cell selects it, shows `Color:` with its number and loads the colour into the wheel below the grid
- `{{ui:editor_theme-editor_color-name}}` for the selected cell

The editor works on a copy. Nothing reaches the level until you save. The save itself is one undo step

## How to pick a slot

Switch a colour to `Theme` and open `{{ui:editor_select-theme_color}}`

The grid shows the palette as it is blended on the frame of the key being edited, not at the playhead.
Next to it are the two theme keys around that frame and what the selected slot holds in each. An unnamed slot is labelled `{{ui:editor_search_unnamed}}`

## How to share and import

- **The device library.** `{{ui:editor_level-theme-item_export}}` in a theme's row saves it to `resources/themes` - the device-wide shared library, where `resources` sits next to `levels` (see [[4_level-folder-and-backups]]). `{{ui:settings_level-settings_theme-library}}` shows it and marks what is already `{{ui:editor_theme-library-item_in-level}}`. `{{ui:editor_library_delete}}` removes a theme from the library. Importing copies the theme into the level, so the level never depends on your library. `{{ui:settings_level-settings_theme-library}}` also shows the themes from collections, with source chips - [[16_library-and-collections]]
- **The game's themes.** `{{ui:editor_search-title_theme}}` offers the themes that ship with the game next to the level's themes

Next: [[5_color-and-postprocessing|Colour, themes and post-processing]], [[1_readability-and-fairness|Readability and fairness]]
