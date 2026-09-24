---
title: SDK
date: 2026-09-24
tags: [developer, level_author]
---

# SDK

The open data model of Bullet Hero levels and saves: what it is, why it lives apart from the game and where to start

**The SDK is the Bullet Hero level format written as a C# library.** It holds the models, JSON and binary serialization, versioning with migrations, validation rules, level archives, publishing profiles and generators. The game reads and writes every level through it, and any other program can do the same. The code is at [github.com/vertoker/bullet-hero-sdk](https://github.com/vertoker/bullet-hero-sdk) under the MIT license

## Why it is a separate library

- **Levels outlive the game.** A level is a folder of files in open formats (JSON, tar.gz, zip, OpenPGP), and the code that reads them is public. A level stays readable even when the game that wrote it is gone
- **Integration with other rhythm games.** Conversion to and from *Afterbeat* (formerly *Project Arrhythmia*) already lives in the SDK, see [[9_afterbeat-interop]]
- **Faster fixes.** A defect in the format can be seen from outside, so anyone who reads the code can report it or send a fix
- **Third-party tools.** A converter, a validator, a level generator or a mod works with the same models as the game, not with a reverse-engineered copy of them
- **Servers.** The core builds without Unity as `netstandard2.1`, so a server runs the same checks over the same models as the client

## What it is made of

| Part | What it is | Needs Unity |
|---|---|---|
| `BH.SDK` | the core: models, serialization, versions, rules, validation, archives, publishing, generators, Afterbeat interop | no |
| `UnityIntegration` | a thin layer where every file compiles both with and without Unity (`#if BHSDK_UNITY`), for example the `Cat` logger | no: outside Unity it is compiled into the core |
| `UnityExtensions` | conversion to Unity types, 2D transforms, avatar movement | yes, unconditionally |
| `BH.SDK.Roslyn` | analyzers and a source generator that write `Equals`, copying, the JSON and `.blob` codecs and the validation walk for every model marked `[GenerateModel]` | runs at compile time |

A model file holds only its members and constructors. Everything repetitive is written by the generator, so a member cannot be forgotten in one of the seven generated bodies

## Version

The SDK has its own version with the prefix `sv`, separate from the game's `gv` and from the model format generation `mg`. At the time of writing it is `sv 0.16.2`. The game's Settings screen shows all three on one line, for example `gv 0.7.0, sv 0.7.0, mg 1`

Until 1.0.0, `sv` moves together with the game and does not promise API stability. The details are on [[5_versioning]]

## Pages in this section

- [[1_sdk-installation]] - the NuGet package, the Unity package and the console sample
- [[2_level-format]] - the level folder, the files in it and the JSON layout
- [[3_blob-format]] - the byte layout of `.blob`
- [[4_archives]] - export modes, tar.gz and zip, password protection
- [[5_versioning]] - generations, migrations and the refusal of newer files
- [[6_validation]] - `ValidationFacade`, rules and fixers
- [[7_publish-profiles]] - a service's publishing policy as a data file
- [[8_writing-generators]] - how to write a generator
- [[9_afterbeat-interop]] - import and export of Afterbeat documents
- [[10_contributing-sdk]] - where the rules for contributors live and how to build the SDK
