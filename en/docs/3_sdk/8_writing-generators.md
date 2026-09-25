---
title: Writing a generator
date: 2026-09-24
tags: [developer]
---

# Writing a generator

How a generator is built from the SDK base classes and what it has to respect to work in the editor

A generator produces level content from a few parameters. The author does not have to place every object by hand

Adding a generator means adding one class. The host builds its form, its estimate and its undo from the contract. Nobody writes UI for it, and no list is edited

What the built-in generators do - [[8_generators]]

## Three kinds

| Kind | Produces | Base class | Entry point |
|---|---|---|---|
| `Level` | a new `Level` and `LevelMeta` | `BaseLevelGenerator<TParams>` | `Create(parameters)` |
| `Content` | new objects and resources in the active scope | `BaseContentGenerator<TParams>` | `Run(context, parameters)` |
| `Modifier` | edits to objects that already exist | `BaseModifier<TParams>` | `Run(context, parameters)` |

Content and Modifier share one entry point. They differ in intent and in `GeneratorRequirements`. A modifier requires a selection by default

For generators that spawn objects there is `BaseSpawnGenerator<TParams>`. It creates each object, parents it and places it in time. The concrete class is left with only the placement math

## No registry

`GeneratorRegistry` finds every generator by reflection when it is first touched. Two generators with the same `NameKey` fail right there

Only the SDK's own assembly is scanned. So a new generator lives in the SDK repository and arrives as a pull request. More - [[10_contributing-sdk]]

## An example

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

    // Spawn adds a size key and a colour key, AddPosition adds the third
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

`NameKey` is shaped as a localization key. The host shows the name through its string table

## Rules that are not optional

- **Change the level only through `GeneratorContext`** (`Create`, `Edit`, `Delete`, `SetValue` and others). It records every change in a `GeneratorChangeLog`, which is the whole of undo. Touching the model directly compiles and silently breaks undo
- **Every field is listed in a section, and every number has a `Range`.** Field order from reflection is not guaranteed. A host has nothing to clamp an unbounded number against. A test enforces the ranges
- **Parameters are public mutable fields with a parameterless constructor.** A form binds to them and a preset serializes them. Do not shadow an inherited field: everything is keyed by field name
- **The estimate matches the run.** A host shows it before running. If the run would go past `LevelRules.MaxObjects`, the host refuses it
- **Randomness comes from `context.CreateRandom()`,** not `System.Random`. The same seed gives the same level on every runtime
- **Parent what you create to `context.Parent`.** That is how the host groups a whole run into one object
- **Declare `GeneratorRequirements.LevelScope`** if you touch `context.Game` or `context.Audio`. Both are `null` while a prefab is the active scope
- **Override `IsDangerousTyped`** when a parameter combination deletes or rewrites content outside the window the author is looking at. The host then asks for confirmation

## External data

The SDK has no audio decoder, FFT or image loader. A generator that needs such data:
1. declares `GeneratorRequirements.ExternalAnalysis`
2. implements an interface from `External/`: `IWaveformInput`, `IBeatFramesInput`, `IPixelTextureInput` and others

The host fills the data in before the run. Handed nothing, the generator must produce nothing

The full contract is [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md)
