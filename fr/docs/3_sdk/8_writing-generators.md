---
title: Écrire un générateur
date: 2026-10-02
tags: [developer]
---

# Écrire un générateur

Un générateur, c'est une classe sur une classe de base du SDK : BaseLevelGenerator, BaseContentGenerator ou BaseModifier. L'hôte construit lui-même le formulaire, l'estimation et l'annulation à partir du contrat

Un générateur crée du contenu de niveau à partir de quelques paramètres. L'auteur n'a pas à placer chaque objet à la main

Personne n'écrit d'interface pour un générateur, et aucune liste n'est modifiée

Ce que font les générateurs intégrés - [[8_generators]]

## Trois sortes

| Sorte | Crée | Classe de base | Point d'entrée |
|---|---|---|---|
| `Level` | un nouveau `Level` et un `LevelMeta` | `BaseLevelGenerator<TParams>` | `Create(parameters)` |
| `Content` | de nouveaux objets et ressources dans la portée active | `BaseContentGenerator<TParams>` | `Run(context, parameters)` |
| `Modifier` | des modifications d'objets qui existent déjà | `BaseModifier<TParams>` | `Run(context, parameters)` |

Content et Modifier partagent le point d'entrée. Ils diffèrent par l'intention et par `GeneratorRequirements`. Par défaut, un modificateur a besoin d'une sélection

Pour les générateurs qui créent des objets, il existe `BaseSpawnGenerator<TParams>`. Il crée chaque objet, lui donne un parent et le place dans le temps. Il ne reste à la classe concrète que les calculs de placement

## Pas de registre à tenir

`GeneratorRegistry` trouve tous les générateurs par réflexion au premier accès. Deux générateurs avec le même `NameKey` échouent à ce moment-là

Seule l'assembly du SDK lui-même est parcourue. Un nouveau générateur vit donc dans le dépôt du SDK et arrive sous forme de pull request. Plus - [[9_contributing-sdk]]

## Exemple

Une rangée d'objets, construite sur les mêmes classes que le `RadialGenerator` intégré :

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

`NameKey` a la forme d'une clé de localisation. L'hôte affiche le nom via sa propre table de chaînes

## Règles obligatoires

- **Ne modifie le niveau que via `GeneratorContext`** (`Create`, `Edit`, `Delete`, `SetValue` et d'autres). Il note chaque modification dans `GeneratorChangeLog`, et toute l'annulation repose dessus. Une modification directe du modèle compile et casse l'annulation sans bruit
- **Chaque champ est listé dans une section, chaque nombre a un `Range`.** L'ordre des champs obtenu par réflexion n'est pas garanti. Un nombre sans bornes ne donne à l'hôte rien sur quoi le limiter. Les plages sont vérifiées par un test
- **Les paramètres sont des champs publics modifiables et un constructeur sans paramètre.** Le formulaire s'y lie, et un préréglage les sérialise. Ne masque pas un champ hérité : tout est adressé par le nom du champ
- **L'estimation correspond à l'exécution.** L'hôte l'affiche avant l'exécution. Si l'exécution dépasse `LevelRules.MaxObjects`, l'hôte refuse
- **L'aléatoire vient de `context.CreateRandom()`,** pas de `System.Random`. La même graine donne le même niveau sur n'importe quelle plateforme
- **Donne comme parent `context.Parent` à ce que tu crées.** C'est ainsi que l'hôte rassemble toute l'exécution en un seul objet
- **Déclare `GeneratorRequirements.LevelScope`** si tu touches à `context.Game` ou `context.Audio`. Les deux valent `null` quand la portée active est un prefab
- **Redéfinis `IsDangerousTyped`** si une combinaison de paramètres supprime ou réécrit du contenu hors de la fenêtre que l'auteur regarde. L'hôte demande alors une confirmation

## Données externes

Le SDK n'a ni décodeur audio, ni FFT, ni chargeur d'images. Un générateur qui a besoin de ces données :
1. déclare `GeneratorRequirements.ExternalAnalysis`
2. implémente une interface de `External/` : `IWaveformInput`, `IBeatFramesInput`, `IPixelTextureInput` et d'autres

L'hôte remplit les données avant l'exécution. S'il n'a rien reçu, le générateur ne doit rien créer

Le contrat complet - [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md)
