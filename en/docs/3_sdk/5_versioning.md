---
title: Versioning and migrations
date: 2026-10-02
tags: [developer, level_author]
---

# Versioning and migrations

There are three versions: gv for the game, sv for the SDK, mg for the generation of the model format. By mg the SDK migrates an old file and refuses to read one with a generation newer than the build

## Three versions

| Label | Stands for | What it versions | Where it lives |
|---|---|---|---|
| `gv` | `game version` | the game client | the Unity project's `bundleVersion` |
| `sv` | `sdk version` | the SDK as a library, semver over the public API | `SdkVersion.Value` |
| `mg` | `model generation` | the model format, one generation per domain | `[ModelGeneration]` on every root, `ModelGenerations.Current` |

The current versions are `gv {{v:version.gv}}`, `sv {{v:version.sv}}`, `mg {{v:version.mg}}`

The `gv` and `sv` numbers do not have to follow each other, but in most cases they match.
Versions are bumped together, and a shared update carries the same version

What each part means:
- `gv`: major is a global update (story, multiplayer), minor is ordinary new features, patch is a hotfix
- `sv`, once the SDK starts promising API stability: major is a breaking API change (a type removed, a member's signature or meaning changed), minor is an addition nobody has to react to, patch is a fix that changes no signatures

**`mg` matters more than the others.** By it the SDK decides whether to migrate a file or refuse to read it

The settings screen shows all three in this order and with labels: `gv {{v:version.gv}}, sv {{v:version.sv}}, mg {{v:version.mg}}`. Without the labels two identical numbers in a bug report cannot be told apart

A version with `b` and a number at the end, for example `gv 1.1.0b1`, is a beta: a build of the next version for testing, usually on a Steam beta branch. The release after it comes out without the letter (`gv 1.1.0`). A file saved by a beta may not open in the previous release

> [!warning] Warning
> Until the SDK says otherwise, `sv` follows the game, and `sv 1.0.0` promises no API stability. A major `sv` says nothing about compatibility yet for code built against the DLL

## Numbers that are not versions

Two more numbers look like a "version" but are not one:
- `LevelMeta.LevelVersion` (key `vrs`) - the author's version of the level, a string such as `"1.0"`
- `BlobFormat.Generation` - the byte layout of `.blob`. More - [[3_blob-format]]

## Generation: one integer per domain

A domain is a root that migrates as a single whole. There are 21 of them: `Level`, `LevelMeta`, `UserSettings`, `Prefab`, `ThemeData`, `PublishProfile` and others.
This includes the parts inside `Level`: `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources`, `LevelHints`. Each domain writes its generation into the `g` key of its envelope

| Constant | Value | Meaning |
|---|---|---|
| `ModelGenerations.Invalid` | -1 | no generation at all |
| `ModelGenerations.Test` | 0 | the `Versions/V0` scaffold that exercises the migration path |
| `ModelGenerations.V1_AlphaRelease` | 1 | what `gv 1.0.0` shipped, most domains are still on it |
| `ModelGenerations.V2_SimplifyEntrance` | 2 | `UserSettings`, `LevelMeta`, `LevelStatistics`, `GameStatistics` and the new `Collection` |
| `ModelGenerations.Current` | the newest | what the interface and reports show |

**A generation is one number, not `major.minor`.** A change to the shape of a file either needs a migration or it does not. There is no degree in between

**Numbers come from one global counter.** A domain that changed gets `ModelGenerations.Current + 1`, not the next free number of its own. That is exactly what keeps the single `mg` in the version string meaningful

## The new is refused

Every model change is a new generation. A change of shape, an added field and a new enum value count the same.
So a generation higher than the build knows is a shape it has certainly never seen

There is one exception: a completely new model that no existing one mentions, for example avatar skins in a separate file. It is a new domain with nothing to migrate from, so the generation does not grow. What grows is the generation of the existing model that starts referencing it

Such a file is not read at all: no default values, no skipped parts. `NewerGenerationException` carries `Domain`, `FileGeneration` and `BuildGeneration`, and the host asks the player to update

```
refused: 'Level' is at generation 2, newer than this build's 1 (domain Level, file 2, this SDK 1) - update the SDK
```

## The old migrates

A domain that changes shape gets:
1. a new generation from the global counter
2. a frozen snapshot of the old shape in `Versions/V<old>/`: a class with `[GenerateModel]` and `[ModelGeneration(domain, <old>)]`
3. a `ModelMigration<TFrom, TTo>` in `Versions/V<old>/Migrations/`

```csharp
public class GameEventsV0ToV1 : ModelMigration<GameEventsV0, GameEvents>
{
    public override GameEvents Migrate(GameEventsV0 from) => new();
}
```

`VersionedTypeRegistry` finds the snapshots and migrators through reflection and walks the chain up to today's shape. Every lossy substitution during reading goes into `SerializationReport`, not into silence

## Refusal before reading

`LevelMeta.MinGeneration` (key `min_generation`) is the highest generation among the level's domains. It is computed on save through `LevelGenerations.Required()` and never entered by hand

The client compares it before opening `level.json`. So a level from the future is refused without reading megabytes of content. A file that declares nothing stores `-1`

The full record of decisions - [VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) in the SDK repository
