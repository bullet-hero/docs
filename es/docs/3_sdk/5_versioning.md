---
title: Versiones y migraciones
date: 2026-10-02
tags: [developer, level_author]
---

# Versiones y migraciones

Hay tres versiones: gv para el juego, sv para el SDK y mg para la generación del formato de modelos. Según mg, el SDK migra un archivo antiguo y se niega a leer uno con una generación más reciente que la compilación

## Tres versiones

| Etiqueta | Significa | Qué versiona | Dónde vive |
|---|---|---|---|
| `gv` | `game version` | el cliente del juego | `bundleVersion` del proyecto de Unity |
| `sv` | `sdk version` | el SDK como biblioteca, semver sobre la API pública | `SdkVersion.Value` |
| `mg` | `model generation` | el formato de modelos, una generación por dominio | `[ModelGeneration]` en cada raíz, `ModelGenerations.Current` |

Las versiones actuales son `gv {{v:version.gv}}`, `sv {{v:version.sv}}`, `mg {{v:version.mg}}`

Los números de `gv` y `sv` no tienen por qué seguirse, pero en la mayoría de los casos coinciden. Las versiones se suben juntas, y una actualización común lleva la misma versión

Qué significa cada parte:
- `gv`: major es una actualización global (historia, multijugador), minor son nuevas funciones normales, patch es una corrección urgente (hotfix)
- `sv`, cuando el SDK empiece a prometer estabilidad de la API: major es un cambio incompatible de la API (se elimina un tipo, cambia la firma o el significado de un miembro), minor es una adición a la que nadie tiene que reaccionar, patch es una corrección que no cambia firmas

**`mg` importa más que las demás.** Con este número el SDK decide si migra un archivo o se niega a leerlo

La pantalla de configuración muestra las tres en este orden y con etiquetas: `gv {{v:version.gv}}, sv {{v:version.sv}}, mg {{v:version.mg}}`. Sin las etiquetas, dos números iguales en un informe de errores no se pueden distinguir

Una versión con `b` y un número al final, por ejemplo `gv 1.1.0b1`, es una beta: una compilación de la siguiente versión para pruebas, normalmente en una rama beta de Steam. La versión estable que la sigue sale sin la letra (`gv 1.1.0`). Un archivo guardado por una beta puede no abrirse en la versión estable anterior

> [!warning] Advertencia
> Hasta que el SDK diga lo contrario, `sv` sigue al juego, y `sv 1.0.0` no promete estabilidad de la API. Un cambio de major en `sv` todavía no dice nada sobre la compatibilidad del código compilado contra la DLL

## Números que no son versiones

Otros dos números parecen una "versión", pero no lo son:
- `LevelMeta.LevelVersion` (clave `vrs`) - la versión del nivel que pone el autor, una cadena como `"1.0"`
- `BlobFormat.Generation` - la disposición de bytes de `.blob`. Más - [[3_blob-format]]

## Generación: un entero por dominio

Un dominio es una raíz que migra como un todo. Hay 21: `Level`, `LevelMeta`, `UserSettings`, `Prefab`, `ThemeData`, `PublishProfile` y otros. Esto incluye las partes dentro de `Level`: `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources`, `LevelHints`. Cada dominio escribe su generación en la clave `g` de su sobre

| Constante | Valor | Significado |
|---|---|---|
| `ModelGenerations.Invalid` | -1 | no hay ninguna generación |
| `ModelGenerations.Test` | 0 | el andamiaje `Versions/V0` que pone a prueba la ruta de migración |
| `ModelGenerations.V1_AlphaRelease` | 1 | lo que trajo `gv 1.0.0`, la mayoría de los dominios siguen en ella |
| `ModelGenerations.V2_SimplifyEntrance` | 2 | `UserSettings`, `LevelMeta`, `LevelStatistics`, `GameStatistics` y el nuevo `Collection` |
| `ModelGenerations.Current` | la más reciente | lo que muestran la interfaz y los informes |

**Una generación es un número, no `major.minor`.** Un cambio en la forma de un archivo necesita una migración o no la necesita. No hay grados intermedios

**Los números salen de un único contador global.** Un dominio que cambió recibe `ModelGenerations.Current + 1`, no su propio siguiente número libre. Eso es justo lo que mantiene el sentido del único `mg` de la cadena de versiones

## Lo nuevo se rechaza

Cada cambio del modelo es una nueva generación. Un cambio de forma, un campo añadido y un nuevo valor de enumeración cuentan igual. Así que una generación mayor que la que conoce la compilación es una forma que la compilación seguro que nunca ha visto

Hay una excepción: un modelo completamente nuevo al que no menciona ninguno de los existentes, por ejemplo las skins del avatar en un archivo aparte. Es un dominio nuevo sin nada desde lo que migrar, así que la generación no crece. Lo que crece es la generación del modelo existente que empieza a hacer referencia a él

Un archivo así no se lee en absoluto: ni valores predeterminados ni partes omitidas. `NewerGenerationException` lleva `Domain`, `FileGeneration` y `BuildGeneration`, y el host pide al jugador que actualice

```
refused: 'Level' is at generation 2, newer than this build's 1 (domain Level, file 2, this SDK 1) - update the SDK
```

## Lo antiguo se migra

Un dominio que cambia de forma recibe:
1. una nueva generación del contador global
2. una instantánea congelada de la forma antigua en `Versions/V<old>/`: una clase con `[GenerateModel]` y `[ModelGeneration(domain, <old>)]`
3. un `ModelMigration<TFrom, TTo>` en `Versions/V<old>/Migrations/`

```csharp
public class GameEventsV0ToV1 : ModelMigration<GameEventsV0, GameEvents>
{
    public override GameEvents Migrate(GameEventsV0 from) => new();
}
```

`VersionedTypeRegistry` encuentra las instantáneas y los migradores mediante reflexión y recorre la cadena hasta la forma actual. Cada sustitución con pérdida durante la lectura va a `SerializationReport`, no al silencio

## Rechazo antes de leer

`LevelMeta.MinGeneration` (clave `min_generation`) es la generación más alta entre los dominios del nivel. Se calcula al guardar mediante `LevelGenerations.Required()` y nunca se introduce a mano

El cliente la compara antes de abrir `level.json`. Así un nivel del futuro se rechaza sin leer megabytes de contenido. Un archivo que no declara nada guarda `-1`

El registro completo de decisiones - [VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) en el repositorio del SDK
