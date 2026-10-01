---
title: Installation
date: 2026-10-01
tags: [developer, level_author]
---

# Installation

There is no package on nuget.org yet: the SDK is built from source into the BulletHero.SDK package. Unity takes it as a git submodule, and the ConsoleSmoke sample checks that your levels read

The SDK code is at [github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk). The license is MIT

## .NET

The `BulletHero.SDK` package is not published on nuget.org yet. Build it from source:

```bash
git clone https://github.com/bullet-hero/sdk.git
cd sdk
dotnet build -c Release BH.SDK.csproj   # bin~/Release/BH.SDK.dll and BH.SDK.xml
dotnet pack  -c Release BH.SDK.csproj   # bin~/Release/BulletHero.SDK.<version>.nupkg
```

Then connect one of the two:
- the `.nupkg` from a local folder: `dotnet add package BulletHero.SDK --source <folder>`. The three dependencies arrive with it
- `BH.SDK.dll` directly. Then add the three packages below yourself: a reference to a DLL does not bring its dependencies along

Dependencies, all from NuGet:

| Package | Version | What for |
|---|---|---|
| `Newtonsoft.Json` | 13.0.3 | JSON |
| `BouncyCastle.Cryptography` | 2.7.0 | OpenPGP for password-protected levels |
| `SharpZipLib` | 1.4.2 | tar and zip (gzip comes from the BCL) |

### Build details

- the assembly is `BH.SDK.dll`, and its XML documentation lies beside it
- the target is `netstandard2.1`, the language is C# 9. These are the same numbers as the Unity project's, so the same sources build both inside Unity and without it
- the output folders are `bin~` and `obj~`. The tilde is needed because Unity does not import folders whose name ends in one

## Unity

The game connects the SDK as a git submodule:

```bash
git submodule init
git submodule add -f https://github.com/bullet-hero/sdk.git Assets/Plugins/BH.SDK
```

Removal is `git rm -r -f Assets/Plugins/BH.SDK`

What the Unity project has to provide itself:
- `Newtonsoft.Json` through the `com.unity.nuget.newtonsoft-json` package
- `BouncyCastle.Cryptography` and `SharpZipLib` from NuGet (the game installs them with NuGetForUnity)
- the scripting define `BHSDK_UNITY` in Player Settings. Without it `UnityIntegration` takes the engine-free branch
- `BH.SDK.Roslyn.dll` in the SDK root. Unity applies an analyzer only to the assembly in its folder and to the assemblies that reference it. Moved elsewhere, it analyzes nothing

The repository root holds a `package.json` with the name `com.vertoker.bullet-hero-sdk` and a minimum Unity version of `6000.0`. So the Package Manager can also add the SDK by git URL. That route is not used and is not described here

## Checking: the ConsoleSmoke sample

`Samples~/ConsoleSmoke` is a `net8.0` console application. It references the built `BH.SDK.dll`, exactly as a third-party tool would.
The application reads a level folder and prints the name, the object count and the generation. Then it round-trips the level through JSON and `.blob`

```bash
dotnet build -c Release Samples~/ConsoleSmoke/ConsoleSmoke.csproj
dotnet Samples~/ConsoleSmoke/bin~/Release/net8.0/ConsoleSmoke.dll <level folder>
```

| Exit code | Meaning |
|---|---|
| 0 | everything matched |
| 1 | wrong arguments |
| 2 | `level.*` or `metadata.*` not found |
| 3 | a round trip did not match |
| 4 | the file is newer than this SDK |

The output on the game's built-in level `new-zero-demo` (recorded with `sv 1.0.0`):

```
BH.SDK 1.0.0, model generation 1
name:       New zero demo
objects:    782
generation: 1 (Blob)
round trip Json: equal (1505078 bytes)
round trip Blob: equal (680706 bytes)
exit 0
```

Next - [[2_level-format]]

## What the SDK is made of

| Part | What it is | Needs Unity |
|---|---|---|
| `BH.SDK` | the core: models, serialization, versions, rules, validation, archives, publishing, generators, Afterbeat interop | no |
| `UnityIntegration` | a thin layer where every file compiles both with and without Unity (`#if BHSDK_UNITY`), for example the `Cat` logger | no: outside Unity it is compiled straight into the core |
| `UnityExtensions` | conversions to Unity types, 2D transforms, avatar movement | yes, always |
| `BH.SDK.Roslyn` | analyzers and a source generator. For every model with `[GenerateModel]` it writes `Equals`, copying, the JSON and `.blob` codecs and the validation walk | runs at compile time |

A model file holds only its fields and constructors. Everything repetitive is written by the generator. So a field cannot be forgotten in one of the seven generated bodies

## Why a separate library

- **Levels outlive the game.** A level is a folder of files in open formats (JSON, tar.gz, zip, OpenPGP). The code that reads them is open too. A level stays readable even when the game that wrote it is gone
- **Interop with other rhythm games.** Conversion to and from *Afterbeat* (formerly *Project Arrhythmia*) is already in the SDK. More - [[9_afterbeat-interop]]
- **Fast fixes.** A defect in the format is visible from outside. Anyone who reads the code can report it or send a fix
- **Third-party tools.** A converter, a validator, a level generator or a mod works with the same models as the game. There is no need to reconstruct them from files
- **Servers.** The core builds without Unity as `netstandard2.1`. So a server runs the same checks over the same models as the client
