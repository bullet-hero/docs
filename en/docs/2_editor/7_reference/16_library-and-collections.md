---
title: Library and collections
date: 2026-09-29
tags: [level_author]
---

# Library and collections

The Library tab, collections of reusable resources, where they come from, and how they get into a level and out of it

## What a collection is

**A collection** is a folder of reusable resources. It holds any of seven kinds:

| Kind | How it is stored |
|---|---|
| prefabs, themes, shapes, effects | data, one file per entry |
| textures, fonts, audio | media files |

A collection is not tied to a level. It sits on your device and serves every level you open

A level never refers to a collection. Importing always copies into the level, so a level stays a self-contained folder that plays anywhere

## Sources

The library lists resources from three sources. Each is a filter chip at the top of a list:

| Chip | What it is | Writable |
|---|---|---|
| `My library` | the device library: `resources/prefabs`, `themes`, `shapes`, `effects` | yes |
| `My collections` | your own collections, `resources/collections` | yes |
| `Workshop` | the collections you are subscribed to in Steam Workshop, read in place. Steam builds only | no |

A read-only collection is changed by copying its entries into a collection of your own

## The Library tab

`Library` is a tab on the editor's home screen, right after `Create Level`

A narrow column of buttons picks the kind:
- `Collections`
- `Prefabs`, `Themes`, `Shapes`, `Effects`
- `Textures`, `Fonts`, `Audio`

The list is to the right of that column

### Collections

- `New collection` creates an empty collection of your own
- `Import archive` adds a collection from a `.zip`, `.tar.gz` or `.tar` file. If that collection is already on the device, the game asks whether to replace it
- `Refresh` reads the folder again

Each row has `Open`. Your own collections also have `Delete`. It asks first and removes the collection with every file in it

### A collection's page

| Control | What it does |
|---|---|
| `Back` | returns to the list |
| `Save` | writes the changes. Nothing is written before it |
| `Export .zip`, `Export .tar.gz` | saves the collection as an archive |
| `Cover` | picks a png image as the cover |
| `Delete` | deletes the collection, after asking |

The fields are `Name`, `Description`, `Authors` (comma separated) and `License` (`Not stated` or one of the typical licences)

Below them are the contents, with `Remove` on each entry

A read-only collection says `Read only. Copy its entries into a collection of your own to change them`

In a Steam build the page of your own collection also has a publish section. More - [[17_publishing]]

### Prefabs, themes, shapes, effects

Each of these pages lists every entry from every source. The chips narrow the list

`Copy into` picks one of your own collections as the target. It is `Nowhere` by default. Once a target is picked, every row gets `Copy`

Entries you can change have `Delete`, and it asks first

### Textures, fonts, audio

These pages list the files of all collections. There is no personal library for files, so these kinds live in collections only.
Rows have `Copy` and `Remove`

### What a copy takes along

A copy takes everything the entry needs: a prefab's shapes, textures, fonts and nested prefabs, an effect's particle shape.
The credits of those resources go along too

## The Collections tab

`Collections` is a level settings tab, right after `Prefabs`. It has two modes at the top: `Import` and `Build a collection`

### Import

1. The tab lists the collections. Press `Open` on one
2. Tick the entries you want. `All` and `None` tick everything or nothing
3. The line `Selected: N, dependencies added: M` shows what will come in. Dependencies are added on their own
4. Press `Import`

The whole import is one undo step

Textures, fonts and audio always get new ids in the level. Their files are copied into the level folder under a unique name

### Build a collection

1. `Into` picks `A new collection` or one of your own. A new one takes its name from `Name`
2. Tick the level's resources, of any of the seven kinds
3. Press `Build`

A new collection takes the level's authors

A protected level cannot be turned into a collection. More - [[13_export-and-protection]]

## Pickers and search

Search and the resource pickers have a `Library` tier for prefabs, themes, shapes and effects. It lists every source.
The pickers are the shape, collider, effect and theme fields and `Place Prefab…`

Picking a library entry imports it into the level with its dependencies and assigns it. A conflict asks the same question as the Collections tab

The library browsers inside the level's resource tabs work the same way and show the source chips. More - [[11_level-resources]]

## Conflicts

An imported entry may already be in the level under the same id:
- the same content - nothing to do
- different content - the window `Already in the level` opens

The window lists every conflict with an `Import as a copy` toggle:

| Choice | Result |
|---|---|
| keep (toggle off) | the level's version stays and is used |
| `Import as a copy` | the collection's version is added under a new id. Whatever was imported with it points at the copy |

`Keep all` and `Copy all` set every toggle at once. `Import` applies the choices, `Cancel` imports nothing

No version wins silently. Every conflict with different content is decided in this window

## Credits

A level's resource records cover themes, effects, shapes and prefabs as well as textures, fonts and audio.
Importing copies the matching records into the level, so the credits arrive with the resource

More - [[4_resource-record]]

## On disk

Collections live in `resources/collections/<collection-guid>/` in the game's data folder. That is the same `resources` folder next to `levels` that holds the device library. More - [[4_level-folder-and-backups]]

| Path | What it holds |
|---|---|
| `collection.json` or `collection.blob` | the manifest: name, description, authors, licence, the texture, font and audio entries, and the credits of everything inside |
| `cover.png` | the cover, optional |
| `prefabs/`, `themes/`, `shapes/`, `effects/` | one `<guid>.json` or `<guid>.blob` per entry, the same files as in the device library |
| `media/` | texture, font and audio files |

A collection travels as an archive: `Export .zip` or `Export .tar.gz` on its page, `Import archive` in the list.
An archive that is not a collection is refused

Next: [[17_publishing]], [[2_reuse]], [[4_resource-record]]
