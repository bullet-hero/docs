---
title: Versioning and migrations
date: 2026-09-24
tags: [developer, level_author]
---

# Versioning and migrations

Which number versions what, how an older file is migrated and why a file from a newer build is refused

## Three versions

| Label | Stands for | What it versions | Where it lives |
|---|---|---|---|
| `gv` | `game version` | the game client | the Unity project's `bundleVersion` |
| `sv` | `sdk version` | the SDK as a library, semver over its public API | `SdkVersion.Value` |
| `mg` | `model generation` | the model format, one generation per domain | `[ModelGeneration]` on each root, `ModelGenerations.Current` |

Current versions - `gv 0.16.2`, `sv 0.16.2`, `mg 1`

The `gv` and `sv` numbers do not have to follow each other, but in most cases they match.
Versions are bumped together, and a shared update carries the same version

What each part means:
- `gv`: major is a global update (story, multiplayer), minor is ordinary features, patch is a hotfix
- `sv`, once the SDK promises API stability: major is a breaking API change (a type removed, a signature or a member's meaning changed), minor is an addition nothing has to react to, patch is a fix that moves no signature

**`mg` matters more than the others.** It is what the SDK uses to decide whether to migrate a file or refuse to read it

The Settings screen shows all three in this order, labelled: `gv 0.16.2, sv 0.16.2, mg 1`. Without the labels two equal numbers in a bug report cannot be told apart

> [!warning] Warning
> Until the SDK says otherwise, `sv` follows the game and 1.0.0 does not promise API stability. A major `sv` still says nothing about compatibility for code compiled against the DLL

## Numbers that are not versions

Two more numbers look like "the version" and are not:
- `LevelMeta.LevelVersion` (key `vrs`) - the author's version of the level, a string like `"1.0"`
- `BlobFormat.Generation` - the byte layout of `.blob`. More - [[3_blob-format]]

## Generation: one integer per domain

A domain is a root that migrates as one unit. There are 20 of them: `Level`, `LevelMeta`, `UserSettings`, `Prefab`, `ThemeData`, `PublishProfile` and others.
They include the parts nested inside `Level`: `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources`, `LevelHints`. Each domain writes its generation into the `g` key of its envelope

| Constant | Value | Meaning |
|---|---|---|
| `ModelGenerations.Invalid` | -1 | no generation at all |
| `ModelGenerations.Test` | 0 | the `Versions/V0` scaffold that exercises the migration path |
| `ModelGenerations.Release` | 1 | what the game writes today, every domain is at it |
| `ModelGenerations.Current` | the newest | what the interface and reports show |

**A generation is one number, not `major.minor`.** A change to the shape of a file either needs a migration or does not. There is no grade in between

**The numbers come from one global counter.** A domain that changes takes `ModelGenerations.Current + 1`, not the next free number for itself. That is what keeps the single `mg` in the version line meaningful

## Newer is refused

Every model change is a new generation. A shape change, an added member and a new enum variant count alike.
So a generation higher than the build knows is a shape it has provably never seen

Such a file is not read at all: no defaults, no skipped parts. `NewerGenerationException` carries `Domain`, `FileGeneration` and `BuildGeneration`, and the host asks the player to update

```
refused: 'Level' is at generation 2, newer than this build's 1 (domain Level, file 2, this SDK 1) - update the SDK
```

## Older migrates

A domain that changes shape gets:
1. a new generation from the global counter
2. a frozen snapshot of its old shape under `Versions/V<old>/`: a `[GenerateModel]` class with `[ModelGeneration(domain, <old>)]`
3. a `ModelMigration<TFrom, TTo>` under `Versions/V<old>/Migrations/`

```csharp
public class GameEventsV0ToV1 : ModelMigration<GameEventsV0, GameEvents>
{
    public override GameEvents Migrate(GameEventsV0 from) => new();
}
```

`VersionedTypeRegistry` finds snapshots and migrators by reflection and walks the chain up to today's shape. Every substitution a lossy read makes goes to `SerializationReport`, never into silence

## Refusing before reading

`LevelMeta.MinGeneration` (key `min_generation`) is the highest generation any domain of the level uses. It is computed at save by `LevelGenerations.Required()` and never typed by hand

A client compares it before opening `level.json`. So a level from the future is refused without reading megabytes of content. A file that makes no claim holds `-1`

The full design record is [VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) in the SDK repository
