---
title: Library and collections
date: 2026-10-02
tags: [level_author]
---

# Library and collections

Collections hold the resources you reuse across levels. A level never refers to a collection: importing copies the resource inside, and the level plays anywhere

## What a collection is

**A collection** is a folder of reusable resources. It can hold resources of seven kinds:

| Kind | How it is stored |
|---|---|
| prefabs, themes, shapes, effects | data, one file per entry |
| textures, fonts, audio | media files |

A collection is not tied to a level. It sits on your device and is available in any level you open

## Sources

The library shows resources from three sources. Each is a filter chip above the list:

| Chip | What it is | Can be changed |
|---|---|---|
| `{{ui:editor_library-source_library}}` | the device library: `resources/prefabs`, `themes`, `shapes`, `effects` | yes |
| `{{ui:editor_library-source_local}}` | your own collections, `resources/collections` | yes |
| `{{ui:editor_library-source_workshop}}` | the collections you are subscribed to in Steam Workshop, read in place. Steam builds only | no |

A read-only collection is changed like this: its entries are copied into a collection of your own

## The "Library" tab

`{{ui:settings_editor-settings_library}}` is the last tab on the editor's home screen, after `{{ui:settings_editor-settings_community}}`

A narrow column of buttons picks the kind:
- `{{ui:editor_library_kind-collections}}`
- `{{ui:editor_library_kind-prefabs}}`, `{{ui:editor_library_kind-themes}}`, `{{ui:editor_library_kind-shapes}}`, `{{ui:editor_library_kind-effects}}`
- `{{ui:editor_library_kind-textures}}`, `{{ui:editor_library_kind-fonts}}`, `{{ui:field_common_audio}}`

To the right of it, the page title (on the left) and its buttons (on the right) stand in one row. The list is below.
An empty list says so in its middle

On the pages of the seven kinds, from `{{ui:editor_library_kind-prefabs}}` to `{{ui:field_common_audio}}`, `{{ui:editor_library_copy-target}}` takes a separate full-width row under the title. The source chips stand in the row under it

A Library window (a collection's card, a texture's picture, the share window) closes with the cross in its corner. There is no `{{ui:editor_library_close}}` button

Every row is a button. Pressing it does the main thing for its kind:

| Kind | Pressing a row |
|---|---|
| collection | opens its page |
| theme, shape, effect | opens the editor |
| texture | shows the picture and its size |
| prefab, font, audio | nothing. An audio row has its own play button |

The small buttons on the right of a row are the other actions, and the bin icon deletes or removes

`{{ui:editor_library_open-folder}}` shows the folder of the current page in the system file manager. Available only on Windows, macOS and Linux

### Collections

`{{ui:editor_library_open-folder}}` and `{{ui:editor_library_refresh}}` stand to the right of the page title. `New collection` and `{{ui:editor_library_import-archive}}` are in a separate row under it, aligned right

- `New collection` creates an empty collection and opens its card
- `{{ui:editor_library_import-archive}}` adds a collection from a `.zip` or `.tar.gz` file or from a password-protected archive: a `.zip` with its own password, `.zip.gpg` or `.tar.gz.gpg`. If that collection is already on the device, the game asks whether to replace it

A password-protected archive opens the `{{ui:editor_library_passphrase-title}}` window: `{{ui:editor_library_passphrase-needed}}`. Enter the password and press `{{ui:editor_library_open}}`.
A wrong password shows `{{ui:editor_library_passphrase-wrong}}`
- `{{ui:editor_library_open-folder}}` opens `resources/collections`
- `{{ui:editor_library_refresh}}` reads the folders again

Your own collections have `{{ui:editor_library_edit}}` and the bin icon. The bin asks first and then deletes the collection with all its files

### A collection's card

`{{ui:editor_library_edit}}` opens a window with the collection's card:
- `{{ui:editor_library_field-name}}`, `{{ui:field_common_description}}`
- `{{ui:editor_library_field-authors}}`, comma separated
- `{{ui:editor_library_field-license}}`: `{{ui:editor_library_license-unspecified}}` or one of the typical licences
- `{{ui:editor_library_set-cover}}` picks a png image. The line next to it says whether there is a cover

`{{ui:editor_save_text}}` writes the card. `{{ui:editor_cancel_text}}`, the cross or a click outside the window discards the changes

### A collection's page

| Element | What it does |
|---|---|
| `{{ui:settings_common_back}}` | returns to the list |
| `{{ui:editor_library_edit}}` | opens the card. Only for your own collections |
| `{{ui:editor_share_share}}` | opens the share window: `{{ui:editor_share_archive}}` as `.zip` or `.tar.gz`, with or without a password, and in the Steam build also `{{ui:editor_share_steam}}` for a collection of your own |
| `{{ui:editor_library_open-folder}}` | opens the collection's own folder |
| `{{ui:editor_library_delete}}` | deletes the collection, asking first |

Below are the contents. A row opens the entry the same way its kind's page does, and the bin icon removes the entry from the collection

A read-only collection says `{{ui:editor_library_read-only}}`

More on `{{ui:editor_share_share}}` - [[17_publishing]]

### Prefabs, themes, shapes, effects

Each of these pages shows every entry from every source. The chips narrow the list

`{{ui:editor_library_copy-target}}` picks one of your own collections. By default it is `{{ui:editor_library_copy-target-none}}`. Once a target is picked, every row from somewhere else gets `{{ui:editor_library_copy-to}}`

A theme, shape or effect opens in the same editor as in the level settings. `{{ui:editor_save_text}}` writes the change where the entry lives: into `{{ui:editor_library-source_library}}` or into your collection.
An entry from the Workshop opens read only, and `{{ui:editor_save_text}}` is off. To change it, copy it into a collection of your own

`{{ui:editor_library_new-entry}}` makes a new theme, shape or effect in the editor. The entry is saved into the target collection, or into `{{ui:editor_library-source_library}}` if no target is picked. Prefabs are made in a level, and they have no `{{ui:editor_library_new-entry}}`

Entries you can change have the bin icon, and it asks first

Every row has `{{ui:editor_share_share}}`. The button packs the entry with everything it needs (for example, a prefab's shapes, textures and nested prefabs) into a `.zip` or `.tar.gz`, with or without a password, as a collection of one entry. The recipient imports that file through `{{ui:editor_library_import-archive}}`, like any collection

`{{ui:editor_library_open-folder}}` opens the device library folder for that kind, for example `resources/themes`

### Textures, fonts, audio

These pages show the files of all collections. There is no personal library for files, so these kinds live only in collections

- a texture row shows the picture
- an audio row has a play button. One track plays at a time, and it stops when you leave the page
- a font row has no preview

`{{ui:editor_library_add-file}}` puts a file from the device into the target collection, so without a target the button is off. A texture is png or jpg, a font ttf or otf, audio mp3, wav or ogg.
If the collection already has a file with the same bytes, nothing is added, and the game says so

Rows have `{{ui:editor_library_copy-to}}` and the bin icon

### What a copy takes along

A copy takes everything the entry needs: a prefab's shapes, textures, fonts and nested prefabs, an effect's particle shape.
The authorship information of those resources goes along with them too

## The "Collections" tab

`{{ui:editor_library_kind-collections}}` is a level settings tab, right after `{{ui:editor_library_kind-prefabs}}`. At the top there are two modes: `Import` and `{{ui:editor_collections_mode-build}}`

### Import

1. The tab shows a list of collections. Press the one you need
2. Tick the entries you need. `{{ui:editor_collections_select-all}}` and `{{ui:editor_collections_select-none}}` tick everything or clear all ticks
3. The line `Selected: N, dependencies added: M` shows what will come into the level. Dependencies are added on their own
4. Press `Import`

The whole import is one undo step

Textures, fonts and audio get new ids in the level, and their files are copied into the level folder under a unique name.
A file the level already has byte for byte is not copied a second time: the import takes the level's own texture, font or track

### Build a collection

1. `{{ui:editor_collections_target}}` picks `A new collection` or one of yours. A new one takes its name from the `{{ui:editor_library_field-name}}` field
2. Tick the level's resources, of any of the seven kinds
3. Press `{{ui:editor_collections_build}}`

A new collection gets the level's authors

A collection cannot be built from a protected level. More - [[13_export-and-protection]]

## Resource picking and search

Search and the resource picking windows have a `{{ui:settings_editor-settings_library}}` tier for prefabs, themes, shapes and effects. It shows all sources.
The picking windows are the shape, collider, effect and theme fields and `{{ui:cmd_editor_place-prefab}}`

Picking an entry from the library imports it into the level with its dependencies and assigns it. A conflict asks the same question as on the "Collections" tab

The library browsers inside the level's resource tabs work the same way and show the source chips. More - [[11_level-resources]]

## Conflicts

An imported entry may already be in the level with the same id:
- the same content - nothing needs to be done
- different content - the `{{ui:editor_resource-conflict_title}}` window opens

The window lists every conflict, each with an `{{ui:editor_resource-conflict_copy}}` toggle:

| Choice | Result |
|---|---|
| keep (toggle off) | the level's version stays and is used |
| `{{ui:editor_resource-conflict_copy}}` | the collection's version is added under a new id. Everything imported together with it refers to the copy |

`{{ui:editor_resource-conflict_all-keep}}` and `{{ui:editor_resource-conflict_all-copy}}` set all toggles at once. `Import` applies the choice, `{{ui:editor_cancel_text}}` imports nothing

No version wins silently. Every conflict with different content is decided in this window

## Authorship

The records about a level's resources cover themes, effects, shapes and prefabs as well as textures, fonts and audio.
Importing copies the needed records into the level, so authorship arrives together with the resource

More - [[4_resource-record]]

## On disk

Collections live in `resources/collections/<collection-guid>/` in the game's data folder. This is the same `resources` folder next to `levels` where the device library lives. More - [[4_level-folder-and-backups]]

| Path | What it holds |
|---|---|
| `collection.json` or `collection.blob` | the manifest: name, description, authors, licence, the texture, font and audio entries and the authorship information of everything inside |
| `cover.png` | the cover, optional |
| `prefabs/`, `themes/`, `shapes/`, `effects/` | one `<guid>.json` or `<guid>.blob` per entry, the same files as in the device library |
| `media/` | texture, font and audio files |

A collection is passed on as an archive: `{{ui:editor_share_share}}` on its page, `{{ui:editor_library_import-archive}}` in the list.
An archive that is not a collection is rejected

Next: [[17_publishing]], [[2_reuse]], [[4_resource-record]]
