---
title: Contributing to the SDK
date: 2026-10-01
tags: [developer]
---

# Contributing to the SDK

Report SDK problems in the issues of the bullet-hero/sdk repository, and send code changes there as pull requests. The contributor rules live in the same repository, next to the code

The repository is [bullet-hero/sdk](https://github.com/bullet-hero/sdk), the default branch is `master`

## Where to report

| What about | Where |
|---|---|
| the SDK and its code | [bullet-hero/sdk/issues](https://github.com/bullet-hero/sdk/issues) |
| the game: players' bugs and requests | [bullet-hero/releases/issues](https://github.com/bullet-hero/releases/issues) |
| the documentation text | [bullet-hero/docs](https://github.com/bullet-hero/docs) |

## Where the rules are

The contributor rules live in the SDK repository itself, next to the code they describe:

| File | What is in it |
|---|---|
| [README.md](https://github.com/bullet-hero/sdk/blob/master/README.md) | dependencies, level packages, building the DLL and the package, the check sample |
| [CLAUDE.md](https://github.com/bullet-hero/sdk/blob/master/CLAUDE.md) | the mental model, a folder index and the conventions of the whole library |
| `CLAUDE.md` in every folder | the local rules of that folder, for example [Serialization](https://github.com/bullet-hero/sdk/blob/master/Serialization/CLAUDE.md), [Validations](https://github.com/bullet-hero/sdk/blob/master/Validations/CLAUDE.md), [Publishing](https://github.com/bullet-hero/sdk/blob/master/Publishing/CLAUDE.md) |
| [Docs/VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) | version axes, generations, migration and refusal |
| [Docs/IDENTIFIERS.md](https://github.com/bullet-hero/sdk/blob/master/Docs/IDENTIFIERS.md) | how the model addresses entities: Guid, int, frame, field path |
| [[ugc-licensing-policy]] (on this site) | the licensing policy for user content, edited together with `TrustedSourceCatalog` |
| [Versions/README.md](https://github.com/bullet-hero/sdk/blob/master/Versions/README.md) | how to write a snapshot and a migrator |
| [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md) | the generator contract |
| [Roslyn/README.md](https://github.com/bullet-hero/sdk/blob/master/Roslyn/README.md) | the analyzers and the model generator, how to rebuild them |
| [UnityIntegration/README.md](https://github.com/bullet-hero/sdk/blob/master/UnityIntegration/README.md) | the dual-compilation contract |
| [CHANGELOG.md](https://github.com/bullet-hero/sdk/blob/master/CHANGELOG.md) | changes by `sv` version, with an `[Unreleased]` section on top |

## Build and tests

```bash
dotnet build -c Release BH.SDK.csproj
dotnet test Tests/BH.SDK.Tests.csproj
dotnet pack -c Release BH.SDK.csproj
```

- here the same sources that Unity compiles are built without Unity. A file that breaks the engine-independence contract breaks this build
- the output goes to `bin~` and `obj~`
- the pack command only creates a `.nupkg`. Nothing is pushed to nuget.org from the repository

> [!caution] Caution
> The analyzers and the model generator ship as a prebuilt `BH.SDK.Roslyn.dll` in the SDK root. After editing anything in `Roslyn/`, rebuild it and copy it over. Otherwise the old generator keeps running, even though the sources say otherwise

```bash
cd Roslyn
dotnet build BH.SDK.Roslyn.csproj -c Release
cp bin~/Release/BH.SDK.Roslyn.dll ../BH.SDK.Roslyn.dll
dotnet test Tests~/BH.SDK.Roslyn.Tests.csproj -c Release
```

Inside the Unity editor the menu item **Tools > BH.SDK.Roslyn > Build Analyzer** does the same

## Invariants worth knowing in advance

- the core does not reference a single `UnityEngine` type. Code that needs the engine goes into `UnityExtensions/` or into `UnityIntegration/` behind `#if BHSDK_UNITY` with an engine-free branch
- the code works the same with files and with in-memory data and uses only the asynchrony from the BCL
- `netstandard2.1` and C# 9 are what the Unity project compiles with. They are not raised
- a model is a `[GenerateModel] public sealed partial class`. Every serialized field takes its key from `Names.cs`
- any model change is a new generation with a snapshot and a migrator. More - [[5_versioning]]
- the SDK version lives in three places: `SdkVersion.cs`, `package.json` and `<Version>` in `BH.SDK.csproj`. `SdkVersionAgreementTests` fails if one of them moved alone
