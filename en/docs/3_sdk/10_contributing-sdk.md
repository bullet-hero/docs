---
title: Contributing to the SDK
date: 2026-09-24
tags: [developer]
---

# Contributing to the SDK

Where the SDK's rules for contributors are written down, and how to build, test and pack it

The SDK is a separate repository, [vertoker/bullet-hero-sdk](https://github.com/vertoker/bullet-hero-sdk), with the default branch `master`. Changes arrive as pull requests. The rules for contributors live in the repository itself, next to the code they describe, and this page only points at them

## Where the rules are

| File | What it holds |
|---|---|
| [README.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/README.md) | dependencies, level packages, building the DLL and the package, the smoke sample |
| [CLAUDE.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/CLAUDE.md) | the mental model, the index of folders and the conventions of the whole library |
| `CLAUDE.md` in each folder | the local rules of that folder, for example [Serialization](https://github.com/vertoker/bullet-hero-sdk/blob/master/Serialization/CLAUDE.md), [Validations](https://github.com/vertoker/bullet-hero-sdk/blob/master/Validations/CLAUDE.md), [Publishing](https://github.com/vertoker/bullet-hero-sdk/blob/master/Publishing/CLAUDE.md) |
| [Docs/VERSIONING.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Docs/VERSIONING.md) | the version axes, generations, migration and refusal |
| [Docs/IDENTIFIERS.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Docs/IDENTIFIERS.md) | how a model addresses things: Guid, int, frame, field path |
| [Docs/UGC-LICENSING-POLICY.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Docs/UGC-LICENSING-POLICY.md) | the licensing policy for user content, edited together with `TrustedSourceCatalog` |
| [Versions/README.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Versions/README.md) | how to write a snapshot and a migrator |
| [Generators/README.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Generators/README.md) | the generator contract |
| [Roslyn/README.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/Roslyn/README.md) | the analyzers and the model generator, how to rebuild them |
| [UnityIntegration/README.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/UnityIntegration/README.md) | the dual-compilation contract |
| [CHANGELOG.md](https://github.com/vertoker/bullet-hero-sdk/blob/master/CHANGELOG.md) | changes by `sv` version, with an `[Unreleased]` section on top |

## Invariants worth knowing first

- the core references no `UnityEngine` type. Code that needs the engine goes to `UnityExtensions/`, or to `UnityIntegration/` behind `#if BHSDK_UNITY` with an engine-free branch
- code works on files and on in-memory data alike, and uses only BCL async
- `netstandard2.1` and C# 9 are what the Unity project compiles with, they are not raised
- a model is a `[GenerateModel] public sealed partial class`, and every serialized member takes its key from `Names.cs`
- any change to the model is a generation bump with a snapshot and a migrator, see [[5_versioning]]
- the SDK version lives in three places: `SdkVersion.cs`, `package.json` and `<Version>` in `BH.SDK.csproj`. `SdkVersionAgreementTests` fails when one moves alone

## Building and testing

```bash
dotnet build -c Release BH.SDK.csproj
dotnet test Tests/BH.SDK.Tests.csproj
dotnet pack -c Release BH.SDK.csproj
```

The same sources that Unity compiles build here without Unity, so a file that breaks the engine-free contract fails this build. Output goes to `bin~` and `obj~`. The packing command only produces a `.nupkg`, nothing is pushed to nuget.org from the repository

> [!caution] Caution
> The analyzers and the model generator ship as a prebuilt `BH.SDK.Roslyn.dll` in the SDK root. After editing anything under `Roslyn/`, rebuild and copy it, otherwise the old generator keeps running while the sources say otherwise

```bash
cd Roslyn
dotnet build BH.SDK.Roslyn.csproj -c Release
cp bin~/Release/BH.SDK.Roslyn.dll ../BH.SDK.Roslyn.dll
dotnet test Tests~/BH.SDK.Roslyn.Tests.csproj -c Release
```

Inside the Unity Editor the same is done by the menu item **Tools > BH.SDK.Roslyn > Build Analyzer**
