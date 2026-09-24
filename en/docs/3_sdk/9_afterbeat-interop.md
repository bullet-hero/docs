---
title: Afterbeat interop
date: 2026-09-24
tags: [developer, level_author]
---

# Afterbeat interop

Converting Afterbeat levels, themes and prefabs to the Bullet Hero format and back, and what is lost on the way

*Afterbeat* (formerly *Project Arrhythmia*, by Vitamin Games) keeps a level in four JSON documents. The SDK converts all four in both directions through one class, `ABInterop`

| Document | Extension | Import | Export |
|---|---|---|---|
| level | `.vgd` | `ImportLevel(levelJson, metaJson, options)` | `ExportLevel(level, meta, options)` |
| metadata | `.vgm` | together with the level | together with the level |
| theme | `.vgt` | `ImportTheme(themeJson, report)` | `ExportTheme(theme, report)` |
| prefab | `.vgp` | `ImportPrefab(prefabJson, options, ...)` | `ExportPrefab(prefab, options, ...)` |

`ExportLevel` returns `ExportedLevel` with `LevelJson`, `MetaJson` and `Report`. In the editor the import is wrapped as the generator `gen_level_afterbeat`, and how it looks to an author is on [[3_afterbeat-import]]

## How it works

- **Text in, text out.** The interop layer reads no files and takes no paths: where a document came from is the host's business. The Afterbeat level folder is not documented well (`level.vgd`, `cover.jpg`, the song as `.ogg`, `.mp3` or `.wav`), so a host should look for the files instead of assuming their names
- **Not through `SerializationService`.** A foreign document gets no `{"g", "v"}` envelope and none of this format's converters, both would corrupt it. The Afterbeat format has no version field at all
- **Unknown keys survive.** Every Afterbeat model keeps keys it does not know (`[JsonExtensionData]`), so a round trip does not delete them
- **Ids are derived, not generated.** Afterbeat names themes and prefabs with arbitrary strings, and `ABIdMap` hashes them into stable Guids. Importing a `.vgt` and then a `.vgd` that references it gives the same id both times
- **Every loss is reported.** `InteropReport` groups everything lost or approximated by cause, with a count and the first place it happened

`ABOptions` holds the choices a conversion cannot make alone: `Framerate` (60 by default), `ImportParallax`, `ImportPrefabs`, `LayerImport`, `OpacityHitThreshold` and others

## What changes on the way

| Thing | In Afterbeat | In Bullet Hero |
|---|---|---|
| time | seconds | frames at the level's framerate |
| rotation | degrees, each key relative to the previous one | radians, absolute |
| camera zoom | half the visible height, 20 by default | `Zoom`, the whole visible height, so doubled |
| draw order | depth 0-60, smaller is in front | parent-relative `Layer`, higher is in front |
| damage | an object with opacity below 1 does not hurt | the object's type decides `ColliderId`, and opacity decides when that collider exists |
| parallax | a background subsystem | ordinary objects without a collider |

Themes cross exactly in both directions: the 34 Afterbeat colours are the same slot layout `ThemeData` uses, minus alpha. The 21 themes the game ships are materialized into the level as ordinary themes

## Limits

**Not imported:** triggers, the screen-gradient event track, depth of field, per-axis parent inheritance and parent time offsets, prefab preview images and lead times. Player force and the hue track are reported as deferred: they wait for work, not for a decision

**Not exported:** audio (an Afterbeat level is one song file, with no track list, offsets or effects), level-authored geometry, anchors, per-corner colours, per-character text effects, random values, beat segments after the first, checkpoint spaces other than World, several post-processing effects and per-instance prefab overrides

> [!caution] Caution
> Licensing, age rating and attribution are lost on export: `.vgm` has no fields for them. A level exported to Afterbeat carries no record of whose resources it uses, so keep that record yourself

The complete mapping is in [Interop/AfterBeat/README.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Interop/AfterBeat/README.md)
