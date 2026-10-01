---
title: Afterbeat interop
date: 2026-10-01
tags: [developer, level_author]
---

# Afterbeat interop

The SDK converts Afterbeat levels, metadata, themes and prefabs to the Bullet Hero format and back through the ABInterop class. Everything lost or approximated along the way goes into a report

*Afterbeat* (formerly *Project Arrhythmia*, by Vitamin Games) stores a level in four JSON documents, and `ABInterop` converts all four in both directions

| Document | Extension | Import | Export |
|---|---|---|---|
| level | `.vgd` | `ImportLevel(levelJson, metaJson, options)` | `ExportLevel(level, meta, options)` |
| metadata | `.vgm` | together with the level | together with the level |
| theme | `.vgt` | `ImportTheme(themeJson, report)` | `ExportTheme(theme, report)` |
| prefab | `.vgp` | `ImportPrefab(prefabJson, options, ...)` | `ExportPrefab(prefab, options, ...)` |

`ExportLevel` returns an `ExportedLevel` with `LevelJson`, `MetaJson` and `Report`

In the editor the import is wrapped in the `gen_level_afterbeat` generator. What it looks like for the author - [[3_afterbeat-import]]

## How it works

- **Text in, text out.** The interop layer reads no files and takes no paths. Where a document came from is up to the host
- **The host should search for files rather than rely on their names.** The Afterbeat level folder is poorly documented: `level.vgd`, `cover.jpg`, a song in `.ogg`, `.mp3` or `.wav`
- **Not through `SerializationService`.** A foreign document gets neither the `{"g", "v"}` envelope nor the converters of this format: both would corrupt it. The Afterbeat format has no version field at all
- **Unknown keys are kept.** Every Afterbeat model stores the keys it does not know (`[JsonExtensionData]`). A round trip does not remove them
- **Identifiers are derived, not generated.** Afterbeat names themes and prefabs with arbitrary strings, and `ABIdMap` hashes them into stable Guids. Importing a `.vgt` and then a `.vgd` that references it gives the same id both times
- **Every loss goes into the report.** `InteropReport` groups everything lost or approximated by reason. Each reason has a count of cases and the first place where it happened

`ABOptions` holds the decisions the conversion cannot make on its own: `Framerate` (60 by default), `ImportParallax`, `ImportPrefabs`, `LayerImport`, `OpacityHitThreshold` and others

## What changes along the way

| What | In Afterbeat | In Bullet Hero |
|---|---|---|
| time | seconds | frames at the level's rate |
| rotation | degrees, each key relative to the previous one | radians, absolute |
| camera zoom | half the visible height, 20 by default | `Zoom`, the whole visible height, that is twice as much |
| draw order | depth 0-60, lower is closer | `Layer` relative to the parent, higher is closer |
| damage | an object with opacity below 1 does not hurt | the object type sets the `ColliderId`, and opacity sets when that collider exists |
| parallax | a separate background subsystem | ordinary objects without a collider |

Themes carry over exactly in both directions. The 34 Afterbeat colors are the same slot layout as `ThemeData`, without alpha

The 21 themes the game ships are materialized in the level as ordinary themes

## Limitations

**Not imported:**
- triggers
- the screen gradient event track
- depth of field
- per-axis parent inheritance and parent time offsets
- prefab previews and prefab lead time

Player force and the hue track are marked in the report as deferred. They are waiting for work, not for a decision

**Not exported:**
- audio: an Afterbeat level is a single song file, with no list of tracks, offsets or effects
- geometry created in the level
- anchors
- per-corner colors
- per-character text effects
- random values
- beat segments after the first one
- checkpoint spaces other than World
- multiple post-processing effects
- overrides of individual prefab instances
- licenses, age rating and attribution: `.vgm` has no fields for them

What this means for the author - [[3_afterbeat-import]]

The full mapping - [Interop/AfterBeat/README.md](https://github.com/bullet-hero/sdk/blob/master/Interop/AfterBeat/README.md)
