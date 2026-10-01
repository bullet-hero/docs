---
title: Level format
date: 2026-10-01
tags: [developer, level_author]
---

# Level format

A level is a folder: content in level.json or level.blob, metadata in metadata.json or metadata.blob, a cover and media files. Backups, records and player settings stay on the device

## The level folder

Every file name in a level folder is fixed in `FileNames`:

| File | Model | What is inside |
|---|---|---|
| `level.json` or `level.blob` | `Level` | the content: settings, objects and events, audio, resources, hints |
| `metadata.json` or `metadata.blob` | `LevelMeta` | title, description, authors, license, a record for every resource, a reference to the cover |
| `logo.png` or `logo.jpg` | - | the cover |
| track, images, fonts | - | media files the level references |

**The extension is the format.** It is not written anywhere inside the files. The reader looks at which file exists: `level.json` or `level.blob`

The level and the metadata choose their format independently. For example, the built-in level `new-zero-demo` keeps `level.blob` next to `metadata.json`

**`metadata.json` is a separate file on purpose.** A catalog shows a thousand levels from a thousand small metadata files. Not a single level is opened for that

## Resources

A resource is addressed by a pair of `uri` and `uri_type` (`ResourceUriType`):

| Value | Type | Where the file is |
|---|---|---|
| 1 | `LevelPath` | inside the level folder. Only this type makes a level portable |
| 2 | `AbsolutePath` | somewhere else on this device |
| 3 | `DirectUrl` | downloaded over the network |
| 4 | `StreamingAssets` | ships with the game, not with the level |

`AbsolutePath` appears when a level is created around a song. Exporting an archive copies such a file inside. More - [[4_archives]]

The cover is available through `LevelMeta.LevelLogo`, like any other resource. Whether it is `logo.png` or `logo.jpg` is decided by the bytes of the file itself, not by the name of the source image

The authorship record of the cover is a `ResourceMeta` with `resource_type` 9 (`LevelLogo`). Neither `resource_id` nor `resource_guid` is filled in it: a level has one cover, so the type is the whole address

## AI declarations

`LevelMeta` and every `ResourceMeta` carry `ai_generated` of type `AiGeneration`:

| Value | Name | What it means |
|---|---|---|
| 0 | `NotSpecified` | nothing declared, unknown. The default value, and a missing key reads as this |
| 1 | `No` | declared as made without AI generation |
| 2 | `Yes` | declared as AI-generated |

In `LevelMeta` it covers only the level's own content. Every resource and the cover declare themselves in their own records.
Whether a level contains AI content is not stored: `LevelMeta.ContainsAiContent()` answers that, and only `Yes` counts

## What does not travel with a level

These files lie next to the `levels` folder, never inside a level folder. Archiving, sending or deleting a level does not touch them:

| Folder or file | What it is | Why it stays |
|---|---|---|
| `backups/` | editor autosaves, a folder per level id, `backup_level_<time>.<extension>` | a copy inside the folder it protects is deleted together with it |
| `stats/` | records and progress by `LevelId` and `statistics.json` | a level someone sent would arrive already completed |
| `settings.json` | `UserSettings`, the player's settings for the whole device | they belong to the player, not to the level |
| `resources/themes`, `effects`, `shapes`, `prefabs` | the device's shared libraries | they are shared by all levels on the device |
| `reports/` | diagnostic reports | - |

## JSON keys

JSON is always written compact, without indentation. To read it by eye, format it in a text editor

**The length of a key depends on how many times it occurs in a level:**
- a key that occurs once per file is written in full words in `snake_case`: `level_id`, `min_generation`
- a key that repeats thousands of times is shortened to a few letters: `objs`, `f`, `e`, `v`

Keys take up 52% of the bytes of a level file, so this is a rule, not a matter of taste. All keys are declared in `Names.cs`

**A polymorphic value is written as `[tag, data]`.** A plain string is `[0,{"v":"Author"}]`, a localized one is `[1,{"strs":[...]}]`

Identifier wrappers such as `ObjectId` are written as a bare number or string

## Identifiers

**The sign of an integer identifier has a meaning.** `0` always means "not set":

| Identifier | JSON key | Positive | Negative |
|---|---|---|---|
| `ObjectId` | `id`, and `pid` for the parent | a level object | a game object: `-1` the camera, `-2` the local player, `-3` the root of a prefab template |
| resource identifiers | `txid`, `fnid`, `auid`, `byid`, `ttid` | a resource that ships with the game | the level's own resource |
| `AudioId` of an audio track | `aid` | a track of this level | not used |

A `pid` equal to `0` means the object has no parent. Numbers below `-3` exist only while the game runs and never reach a file

**`Marker`, `Checkpoint` and `BeatSegment` have no identifier.** Their address is a place in time: for a marker and a checkpoint it is the frame `f`, for a beat segment it is the first frame of its span `sp` (segments do not overlap). If such an object is moved, its address changes

**A prefab override names a field by number, not by JSON key.** A placement keeps its overrides in the `mod` list. The `key` of each override holds three numbers:
- `id` - the object inside the template, not its copy in the level
- `f` - the permanent number of the field
- `i` - the element of a list field, or `-1` for the whole field

The number is bound to the field forever. Renaming the JSON key of that field does not break overrides already saved in levels

## The outer "g"

Every serialization root is wrapped in an envelope with two keys:

```json
{"g":1,"v":{"level_id":"18df5f61-3aa4-4812-bf69-d357f2201bc3","vrs":"1.0", ... }}
```

`g` is the model generation (`Names.Generation`), `v` is the data

Envelopes nest. Inside `Level`, `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources` and `LevelHints` each have their own envelope. How generations work - [[5_versioning]]

> [!caution] Caution
> `g` and `vrs` are different numbers. `vrs` is the author's version of the level (`LevelMeta.LevelVersion`), it has nothing to do with the format. Do not change `g` by hand: a file with a `g` higher than the build knows is not read at all
