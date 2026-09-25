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

## Identifiers

**The sign of an integer id carries meaning.** `0` always means unset:

| Id | JSON key | Positive | Negative |
|---|---|---|---|
| `ObjectId` | `id`, and `pid` for the parent | an object of the level | an object of the game: `-1` the camera, `-2` the local player, `-3` the root of a prefab template |
| resource ids | `txid`, `fnid`, `auid`, `byid`, `ttid` | a resource shipped with the game | a resource of the level itself |
| `AudioId` of an audio track | `aid` | a track of this level | never used |

A `pid` of `0` means the object has no parent. Numbers below `-3` exist only while the game runs and never appear in a file

**`Marker`, `Checkpoint` and `BeatSegment` carry no id.** They are addressed by their place in time: a marker and a checkpoint by their frame `f`, a beat segment by the first frame of its span `sp` (segments never overlap). Moving one of them changes its address

**A prefab override names its field by a number, not by a JSON key.** A placement keeps its overrides in the list `mod`. The `key` of each override holds three numbers:
- `id` - the object inside the template, not its copy in the level
- `f` - the field's fixed number
- `i` - the element of a list field, or `-1` for the whole field

The number belongs to the field for good. Renaming the field's JSON key does not break the overrides already saved in levels

## The outer "g"

Every serialization root is wrapped in an envelope with two keys:

```json
{"g":1,"v":{"level_id":"18df5f61-3aa4-4812-bf69-d357f2201bc3","vrs":"1.0", ... }}
```

`g` is the generation of the model (`Names.Generation`), `v` is the payload

Envelopes nest. Inside `Level`, each of `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources` and `LevelHints` carries its own. How generations work - [[5_versioning]]

> [!caution] Caution
> `g` and `vrs` are different numbers. `vrs` is the author's version of the level (`LevelMeta.LevelVersion`), and it has nothing to do with the format. Do not change `g` by hand: a file with a `g` higher than the build knows is refused whole
