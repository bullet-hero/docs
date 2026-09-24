---
title: Versioning and migrations
date: 2026-09-24
tags: [developer, level_author]
---

# Versioning and migrations

Which number versions what, how an older file is migrated and why a file from a newer build is refused

## Three versions and two impostors

| Label | What it versions | Where it lives |
|---|---|---|
| `gv` | the game client | the Unity project's `bundleVersion` |
| `sv` | the SDK as a library, semver over its public API | `SdkVersion.Value` |
| `mg` | the model format, one generation per domain | `[ModelGeneration]` on each root, `ModelGenerations.Current` |

The Settings screen shows them in this order, labelled: `gv 0.7.0, sv 0.7.0, mg 1`. Without the labels two equal numbers in a bug report cannot be told apart

Two more numbers look like "the version" and are not:
- `LevelMeta.LevelVersion` (key `vrs`) - the author's own version of the level, a string like `"1.0"`
- `BlobFormat.Generation` - the byte layout of `.blob`, see [[3_blob-format]]

## Generation: one integer per domain

A domain is a root that migrates as one unit. There are 20 of them: `Level`, `LevelMeta`, `UserSettings`, `Prefab`, `ThemeData`, `PublishProfile` and others, including the parts nested inside `Level` (`LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources`, `LevelHints`). Each writes its generation into the `g` key of its envelope

| Constant | Value | Meaning |
|---|---|---|
| `ModelGenerations.Invalid` | -1 | no generation at all |
| `ModelGenerations.Test` | 0 | the `Versions/V0` scaffold that exercises the migration path |
| `ModelGenerations.Release` | 1 | what the game writes today, every domain is at it |
| `ModelGenerations.Current` | the newest | what the interface and reports show |

**A generation is one number, not `major.minor`.** A change to the shape of a file either needs a migration or does not, there is no grade in between. **The numbers come from one global counter:** a domain that changes takes `ModelGenerations.Current + 1`, not the next free number for itself. That is what keeps the single `mg` in the version line meaningful

## Older migrates, newer is refused

Every model change is a generation bump: a shape change, an added member and a new enum variant alike. So a generation higher than the build knows is a shape it has provably never seen. Such a file is not read at all: no defaults, no skipped parts. `NewerGenerationException` carries `Domain`, `FileGeneration` and `BuildGeneration`, and the host asks the player to update

```
refused: 'Level' is at generation 2, newer than this build's 1 (domain Level, file 2, this SDK 1) - update the SDK
```

An older generation is migrated. A domain that changes shape gets:
1. a new generation from the global counter
2. a frozen snapshot of its old shape under `Versions/V<old>/`, a `[GenerateModel]` class with `[ModelGeneration(domain, <old>)]`
3. a `ModelMigration<TFrom, TTo>` under `Versions/V<old>/Migrations/`

```csharp
public class GameEventsV0ToV1 : ModelMigration<GameEventsV0, GameEvents>
{
    public override GameEvents Migrate(GameEventsV0 from) => new();
}
```

`VersionedTypeRegistry` finds snapshots and migrators by reflection and walks the chain up to today's shape. Every substitution a lossy read makes goes to `SerializationReport`, never into silence

## Refusing before reading

`LevelMeta.MinGeneration` (key `min_generation`) is the highest generation any domain of the level uses. It is computed at save by `LevelGenerations.Required()`, never typed by hand. A client compares it before opening `level.json`, so a level from the future is refused without reading megabytes of content. A file that makes no claim holds `-1`

> [!warning] Warning
> Until the SDK says otherwise, `sv` follows the game and 1.0.0 does not promise API stability. A major `sv` still says nothing about compatibility for code compiled against the DLL

The full design record is [VERSIONING.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Docs/VERSIONING.md) in the SDK repository
