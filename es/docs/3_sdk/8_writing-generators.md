---
title: Cómo escribir un generador
date: 2026-10-02
tags: [developer]
---

# Cómo escribir un generador

Un generador es una clase sobre una clase base del SDK: BaseLevelGenerator, BaseContentGenerator o BaseModifier. El host construye por sí mismo el formulario, la estimación y la acción de deshacer a partir del contrato

Un generador crea contenido del nivel a partir de unos pocos parámetros. El autor no tiene que colocar cada objeto a mano

Nadie escribe una interfaz para un generador, y no se edita ninguna lista

Qué hacen los generadores integrados - [[8_generators]]

## Tres tipos

| Tipo | Crea | Clase base | Punto de entrada |
|---|---|---|---|
| `Level` | un `Level` y un `LevelMeta` nuevos | `BaseLevelGenerator<TParams>` | `Create(parameters)` |
| `Content` | objetos y recursos nuevos en el ámbito activo | `BaseContentGenerator<TParams>` | `Run(context, parameters)` |
| `Modifier` | cambios en objetos que ya existen | `BaseModifier<TParams>` | `Run(context, parameters)` |

Content y Modifier comparten punto de entrada. Se diferencian en la intención y en `GeneratorRequirements`. Un modificador necesita una selección de forma predeterminada

Para los generadores que crean objetos existe `BaseSpawnGenerator<TParams>`. Crea cada objeto, le asigna el padre y lo coloca en el tiempo. A la clase concreta solo le queda la matemática de la colocación

## Sin registro

`GeneratorRegistry` encuentra todos los generadores mediante reflexión en el primer acceso. Dos generadores con el mismo `NameKey` fallan ahí mismo

Solo se analiza el propio ensamblado del SDK. Por eso un generador nuevo vive en el repositorio del SDK y llega como pull request. Más - [[9_contributing-sdk]]

## Ejemplo

Una fila de objetos, construida sobre las mismas clases que el `RadialGenerator` integrado:

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

`NameKey` tiene la forma de una clave de localización. El host muestra el nombre mediante su propia tabla de cadenas

## Reglas obligatorias

- **Cambia el nivel solo a través de `GeneratorContext`** (`Create`, `Edit`, `Delete`, `SetValue` y otros). Registra cada cambio en `GeneratorChangeLog`, y toda la función de deshacer se apoya en eso. Un cambio directo del modelo compila y rompe la función de deshacer sin avisar
- **Cada campo figura en una sección, cada número tiene un `Range`.** El orden de los campos que da la reflexión no está garantizado. Un número sin límites no le da al host nada a lo que limitarlo. Los rangos los comprueba un test
- **Los parámetros son campos públicos mutables y un constructor sin parámetros.** El formulario se enlaza a ellos y un preset los serializa. No ocultes un campo heredado: todo se direcciona por el nombre del campo
- **La estimación coincide con la ejecución.** El host la muestra antes de la ejecución. Si la ejecución superara `LevelRules.MaxObjects`, el host la rechaza
- **La aleatoriedad sale de `context.CreateRandom()`,** no de `System.Random`. La misma semilla da el mismo nivel en cualquier plataforma
- **Haz que `context.Parent` sea el padre de lo que crees.** Así el host reúne toda la ejecución en un solo objeto
- **Declara `GeneratorRequirements.LevelScope`** si tocas `context.Game` o `context.Audio`. Ambos son `null` mientras el ámbito activo es un prefab
- **Sobrescribe `IsDangerousTyped`** si una combinación de parámetros elimina o reescribe contenido fuera de la ventana que el autor está mirando. Entonces el host pide confirmación

## Datos externos

El SDK no tiene decodificador de audio, ni FFT, ni cargador de imágenes. Un generador que necesita esos datos:
1. declara `GeneratorRequirements.ExternalAnalysis`
2. implementa una interfaz de `External/`: `IWaveformInput`, `IBeatFramesInput`, `IPixelTextureInput` y otras

El host rellena los datos antes de la ejecución. Si no recibió nada, el generador no debe crear nada

El contrato completo - [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md)
