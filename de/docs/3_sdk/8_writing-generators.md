---
title: Einen Generator schreiben
date: 2026-10-02
tags: [developer]
---

# Einen Generator schreiben

Ein Generator ist eine Klasse auf einer Basisklasse des SDK: BaseLevelGenerator, BaseContentGenerator oder BaseModifier. Formular, Schätzung und Rückgängig baut der Host selbst aus dem Vertrag

Ein Generator erzeugt Levelinhalt aus wenigen Parametern. Der Autor muss nicht jedes Objekt von Hand platzieren

Niemand schreibt eine Oberfläche für einen Generator, und keine Liste wird bearbeitet

Was die eingebauten Generatoren tun - [[8_generators]]

## Drei Arten

| Art | Erzeugt | Basisklasse | Einstiegspunkt |
|---|---|---|---|
| `Level` | ein neues `Level` und `LevelMeta` | `BaseLevelGenerator<TParams>` | `Create(parameters)` |
| `Content` | neue Objekte und Ressourcen im aktiven Bereich | `BaseContentGenerator<TParams>` | `Run(context, parameters)` |
| `Modifier` | Änderungen an Objekten, die schon existieren | `BaseModifier<TParams>` | `Run(context, parameters)` |

Content und Modifier teilen sich einen Einstiegspunkt. Sie unterscheiden sich in der Absicht und in `GeneratorRequirements`. Ein Modifikator braucht standardmäßig eine Auswahl

Für Generatoren, die Objekte erzeugen, gibt es `BaseSpawnGenerator<TParams>`. Er erzeugt jedes Objekt, hängt es an ein Elternobjekt und platziert es in der Zeit. Der konkreten Klasse bleibt nur die Mathematik der Platzierung

## Keine Registrierung

`GeneratorRegistry` findet beim ersten Zugriff alle Generatoren per Reflection. Zwei Generatoren mit demselben `NameKey` scheitern genau dort

Durchsucht wird nur die eigene Assembly des SDK. Deshalb lebt ein neuer Generator im SDK-Repository und kommt als Pull Request. Mehr - [[9_contributing-sdk]]

## Beispiel

Eine Reihe von Objekten, gebaut auf denselben Klassen wie der eingebaute `RadialGenerator`:

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

`NameKey` hat die Form eines Lokalisierungsschlüssels. Der Host zeigt den Namen über seine eigene String-Tabelle an

## Pflichtregeln

- **Ändere das Level nur über `GeneratorContext`** (`Create`, `Edit`, `Delete`, `SetValue` und weitere). Er hält jede Änderung in `GeneratorChangeLog` fest, und darauf ruht das ganze Rückgängigmachen. Eine direkte Änderung am Modell kompiliert und macht das Rückgängigmachen stillschweigend kaputt
- **Jedes Feld steht in einem Abschnitt, jede Zahl hat einen `Range`.** Die Reihenfolge der Felder aus Reflection ist nicht garantiert. Eine unbegrenzte Zahl gibt dem Host nichts, worauf er begrenzen kann. Die Bereiche werden von einem Test geprüft
- **Parameter sind öffentliche veränderbare Felder und ein parameterloser Konstruktor.** Das Formular bindet sich an sie, und ein Preset serialisiert sie. Verdecke kein geerbtes Feld: Alles wird über den Feldnamen adressiert
- **Die Schätzung entspricht dem Lauf.** Der Host zeigt sie vor dem Lauf an. Würde der Lauf `LevelRules.MaxObjects` überschreiten, lehnt der Host ab
- **Zufall kommt aus `context.CreateRandom()`,** nicht aus `System.Random`. Derselbe Seed ergibt auf jeder Plattform dasselbe Level
- **Hänge, was du erzeugst, an `context.Parent`.** So fasst der Host den ganzen Lauf in einem Objekt zusammen
- **Deklariere `GeneratorRequirements.LevelScope`,** wenn du `context.Game` oder `context.Audio` anfasst. Beide sind `null`, solange der aktive Bereich ein Prefab ist
- **Überschreibe `IsDangerousTyped`,** wenn eine Kombination von Parametern Inhalt außerhalb des Fensters löscht oder umschreibt, auf das der Autor gerade schaut. Dann fragt der Host nach einer Bestätigung

## Externe Daten

Das SDK hat keinen Audiodecoder, keine FFT und keinen Bildlader. Ein Generator, der solche Daten braucht:
1. deklariert `GeneratorRequirements.ExternalAnalysis`
2. implementiert ein Interface aus `External/`: `IWaveformInput`, `IBeatFramesInput`, `IPixelTextureInput` und weitere

Der Host füllt die Daten vor dem Lauf aus. Hat er nichts bekommen, muss der Generator nichts erzeugen

Der vollständige Vertrag - [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md)
