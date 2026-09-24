---
title: Level format
date: 2026-09-24
tags: [developer, level_author]
---

# Level format

What a level folder holds, which files travel with it and which stay on the device, and how the JSON inside is laid out

## The level folder

A level is a folder. Every file name in it is fixed in `FileNames`:

| File | Model | What is in it |
|---|---|---|
| `level.json` or `level.blob` | `Level` | the content: settings, objects and events, audio, resources, hints |
| `metadata.json` or `metadata.blob` | `LevelMeta` | name, description, authors, license, a record per resource, the cover reference |
| `logo.png` or `logo.jpg` | - | the cover |
| the track, images, fonts | - | the media files the level references |

**The extension is the format.** It is stored nowhere inside the files. A reader checks which file exists: `level.json` or `level.blob`

The level and the metadata choose their formats independently. For example, the built-in level `new-zero-demo` keeps `level.blob` next to `metadata.json`

**`metadata.json` is a separate file on purpose.** A catalogue lists a thousand levels by reading a thousand small metadata files. Not a single level is opened

## Resources

A resource is addressed by a `uri` and a `uri_type` (`ResourceUriType`):

| Value | Type | Where the file is |
|---|---|---|
| 1 | `LevelPath` | inside the level folder. Only this type makes a level portable |
| 2 | `AbsolutePath` | somewhere else on this device |
| 3 | `DirectUrl` | downloaded over the network |
| 4 | `StreamingAssets` | shipped with the game, not with the level |

`AbsolutePath` is what you get when a level is created around a song. Exporting an archive copies such a file inside. More - [[4_archives]]

The cover is reached through `LevelMeta.LevelLogo` like any other resource. `logo.png` or `logo.jpg` is decided by the file's own bytes, not by the name of the source image

## What does not travel with a level

These files live next to the `levels` folder, never inside a level folder. Zipping, sharing or deleting a level leaves them alone:

| Folder or file | What it is | Why it stays |
|---|---|---|
| `backups/` | editor autosaves, one folder per level id, `backup_level_<timestamp>.<ext>` | a backup inside the folder it protects is deleted together with it |
| `stats/` | records and progress per `LevelId`, plus `statistics.json` | a shared level would arrive already won |
| `settings.json` | `UserSettings`, device-wide player options | they belong to the player, not to a level |
| `resources/themes`, `effects`, `shapes`, `prefabs` | device-wide shared libraries | they are shared between all levels on the device |
| `reports/` | diagnostic reports | - |

## JSON keys

JSON is always written compact, without indentation. To read it by eye, format it in a text editor

**The length of a key depends on how often it appears in a level:**
- a key that appears once per file is written in full `snake_case`: `level_id`, `min_generation`
- a key that repeats thousands of times is shortened to a few letters: `objs`, `f`, `e`, `v`

Keys take 52% of the bytes of a level file, which is why this is a rule and not a matter of taste. Every key is declared in `Names.cs`

**A polymorphic value is written as `[tag, payload]`.** A plain string is `[0,{"v":"Author"}]`, a localized one is `[1,{"strs":[...]}]`

Id wrappers such as `ObjectId` are written as a bare number or string

## The outer "g"

Every serialization root is wrapped in an envelope with two keys:

```json
{"g":1,"v":{"level_id":"18df5f61-3aa4-4812-bf69-d357f2201bc3","vrs":"1.0", ... }}
```

`g` is the generation of the model (`Names.Generation`), `v` is the payload

Envelopes nest. Inside `Level`, each of `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources` and `LevelHints` carries its own. How generations work - [[5_versioning]]

> [!caution] Caution
> `g` and `vrs` are different numbers. `vrs` is the author's version of the level (`LevelMeta.LevelVersion`), and it has nothing to do with the format. Do not change `g` by hand: a file with a `g` higher than the build knows is refused whole
