---
title: Writing a generator
date: 2026-10-02
tags: [developer]
---

# Writing a generator

A generator is one class on an SDK base class: BaseLevelGenerator, BaseContentGenerator or BaseModifier. The host builds the form, the estimate and the undo itself from the contract

A generator creates level content from a few parameters. The author does not have to place every object by hand

Nobody writes an interface for a generator, and no list is edited

What the built-in generators do - [[8_generators]]

## Three kinds

| Kind | Creates | Base class | Entry point |
|---|---|---|---|
| `Level` | a new `Level` and `LevelMeta` | `BaseLevelGenerator<TParams>` | `Create(parameters)` |
| `Content` | new objects and resources in the active scope | `BaseContentGenerator<TParams>` | `Run(context, parameters)` |
| `Modifier` | edits to objects that already exist | `BaseModifier<TParams>` | `Run(context, parameters)` |

Content and Modifier share an entry point. They differ in intent and in `GeneratorRequirements`. A modifier needs a selection by default

For generators that create objects there is `BaseSpawnGenerator<TParams>`. It creates every object, parents it and places it in time. The concrete class is left with only the placement math

## No registry

`GeneratorRegistry` finds all generators through reflection on first access. Two generators with the same `NameKey` fail right there

Only the SDK's own assembly is scanned. So a new generator lives in the SDK repository and arrives as a pull request. More - [[9_contributing-sdk]]

## Example

A row of objects, built on the same classes as the built-in `RadialGenerator`:

```csharp
using BH.SDK.Generators;
using BH.SDK.Generators.Spawn;
using BH.SDK.Rules;

public class RowGenerator : BaseSpawnGenerator<RowGenerator.Parameters>
{
    public override string NameKey => "gen_geometry_row";

    public override GeneratorHints Hints { get; } = new GeneratorHints.Builder()
        .Section(GeneratorSections.Main, SpawnParameters.MainFields)
        .Section(GeneratorSections.Main, nameof(Parameters.Count), nameof(Parameters.Spacing))
        .Section(GeneratorSections.Additional, SpawnParameters.AdditionalFields)
        .Section(GeneratorSections.Additional, nameof(Parameters.StartX), nameof(Parameters.Y))
        .Range(nameof(Parameters.Count), 1, 256)
        .Range(nameof(Parameters.Spacing), 0f, ValueRules.MaxPos)
        .Range(nameof(Parameters.StartX), ValueRules.MinPos, ValueRules.MaxPos)
        .Range(nameof(Parameters.Y), ValueRules.MinPos, ValueRules.MaxPos)
        .Range(nameof(SpawnParameters.Size), ValueRules.MinSca, ValueRules.MaxSca)
        .Build();

    protected override void Generate(GeneratorContext context, Parameters parameters)
    {
        for (var i = 0; i < parameters.Count; i++)
        {
            var obj = Spawn(context, parameters, $"row_{i}", context.Span);
            AddPosition(obj, parameters.StartX + i * parameters.Spacing, parameters.Y, obj.Span.StartFrame);
        }
    }

    // Spawn adds a size key and a color key, AddPosition adds the third
    protected override GeneratorCost EstimateTyped(GeneratorContext context, Parameters parameters)
        => new GeneratorCost(parameters.Count, parameters.Count * 3);

    public class Parameters : SpawnParameters
    {
        public int Count = 8;
        public float Spacing = 2f;
        public float StartX;
        public float Y;
    }
}
```

`NameKey` has the shape of a localization key. The host shows the name through its own string table

## Required rules

- **Change the level only through `GeneratorContext`** (`Create`, `Edit`, `Delete`, `SetValue` and others). It records every change in `GeneratorChangeLog`, and all of undo rests on that. A direct model change compiles and silently breaks undo
- **Every field is listed in a section, every number has a `Range`.** Field order from reflection is not guaranteed. An unbounded number gives the host nothing to clamp to. The ranges are checked by a test
- **Parameters are public mutable fields and a parameterless constructor.** The form binds to them, and a preset serializes them. Do not hide an inherited field: everything is addressed by field name
- **The estimate matches the run.** The host shows it before the run. If the run would exceed `LevelRules.MaxObjects`, the host refuses
- **Randomness comes from `context.CreateRandom()`,** not from `System.Random`. The same seed gives the same level on any platform
- **Parent what you create to `context.Parent`.** That is how the host gathers the whole run into one object
- **Declare `GeneratorRequirements.LevelScope`** if you touch `context.Game` or `context.Audio`. Both are `null` while the active scope is a prefab
- **Override `IsDangerousTyped`** if a combination of parameters deletes or rewrites content outside the window the author is looking at. Then the host asks for confirmation

## External data

The SDK has no audio decoder, no FFT and no image loader. A generator that needs such data:
1. declares `GeneratorRequirements.ExternalAnalysis`
2. implements an interface from `External/`: `IWaveformInput`, `IBeatFramesInput`, `IPixelTextureInput` and others

The host fills in the data before the run. If it was given nothing, the generator must create nothing

The full contract - [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md)
