---
title: Installation
date: 2026-09-24
tags: [developer, level_author]
---

# Installation

How to connect the SDK to a .NET project or a Unity project, and how to check that it reads your levels

## .NET: the BulletHero.SDK package

The package is called `BulletHero.SDK`, it targets `netstandard2.1` and is compiled with C# 9. Both numbers are what the Unity project compiles with, so the same sources build inside and outside Unity. The assembly is `BH.SDK.dll`, and its XML documentation ships beside it

Dependencies, all from NuGet:

| Package | Version | What for |
|---|---|---|
| `Newtonsoft.Json` | 13.0.3 | JSON |
| `BouncyCastle.Cryptography` | 2.7.0 | OpenPGP for password-protected levels |
| `SharpZipLib` | 1.4.2 | tar and zip (gzip comes from the BCL) |

> [!warning] Warning
> At the time of writing (2026-09-24) the package is not published on nuget.org. Build it from the sources with the commands below

```bash
git clone https://github.com/vertoker/bullet-hero-sdk.git
cd bullet-hero-sdk
dotnet build -c Release BH.SDK.csproj   # bin~/Release/BH.SDK.dll and BH.SDK.xml
dotnet pack  -c Release BH.SDK.csproj   # bin~/Release/BulletHero.SDK.<version>.nupkg
```

The output folders are `bin~` and `obj~`, with a tilde, because Unity does not import folders whose name ends in one. After that you have two options:
- add the `.nupkg` from a local folder: `dotnet add package BulletHero.SDK --source <folder>`, and the three dependencies arrive with it
- reference `BH.SDK.dll` directly and add the three packages above yourself, since a reference to a DLL does not bring its dependencies along

## Unity

The repository root carries a `package.json` with the name `com.vertoker.bullet-hero-sdk` and a minimum Unity version of `6000.0`. The game connects the SDK as a git submodule:

```bash
git submodule init
git submodule add -f https://github.com/vertoker/bullet-hero-sdk.git Assets/Plugins/BulletHeroSDK
```

Removal is `git rm -r -f Assets/Plugins/BulletHeroSDK`. Because `package.json` sits in the root, the Package Manager can also add the repository by its git URL, but the developers do not use or describe that route

What the Unity project has to provide itself:
- `Newtonsoft.Json` through the `com.unity.nuget.newtonsoft-json` package
- `BouncyCastle.Cryptography` and `SharpZipLib` from NuGet (the game installs them with NuGetForUnity)
- the scripting define `BHSDK_UNITY` in Player Settings, otherwise `UnityIntegration` takes its engine-free branch
- `BH.SDK.Roslyn.dll` left in the SDK root. Unity applies an analyzer only to the assembly whose folder contains it and to the assemblies that reference it, so moved elsewhere it analyzes nothing

## Checking: the ConsoleSmoke sample

`Samples~/ConsoleSmoke` is a `net8.0` console application that references the built `BH.SDK.dll`, exactly as a third-party tool would. It reads a level folder, prints the name, the object count and the generation, and round-trips the level through JSON and `.blob`

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

The output on the game's built-in level `new-zero-demo` (recorded with SDK 0.15.0):

```
BH.SDK 0.15.0, model generation 1
name:       New zero demo
objects:    782
generation: 1 (Blob)
round trip Json: equal (1505132 bytes)
round trip Blob: equal (680751 bytes)
exit 0
```

Next: [[2_level-format]]
