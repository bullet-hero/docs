---
title: Validación
date: 2026-10-01
tags: [developer, level_author]
---

# Validación

La validación la llamas tú a través de ValidationFacade, no está integrada en el guardado ni en la carga. Las incidencias se dividen en Error, Warning y Advice, y ValidateAndFix corrige lo que puede

Dónde ejecutarla lo decide el juego. Al abrir un nivel en el editor se informa de los problemas, mientras que la reproducción se salta la comprobación. Así quien espera a la validación es el autor, y el jugador nunca

Un autor de niveles se encuentra con la validación al ofrecer un nivel a un servicio. Más - [[7_publish-profiles]]

## Cómo llamarla

`ValidationFacade` es el único punto de entrada. Quien llama no necesita saber cuántas pasadas existen:

```csharp
var facade = new ValidationFacade();
var report = facade.Validate(level);

if (report.HasErrors)
    Console.WriteLine(report);
```

| Método | Qué hace |
|---|---|
| `Validate(root, settings)` | comprueba cualquier raíz: `Level`, `LevelMeta`, `UserSettings`, un `Prefab` o un `EffectData` sueltos. La pasada del grafo solo se ejecuta para `Level` |
| `ValidateAndFix(root, analyzerSettings, fixerSettings)` | corrige lo que puede e informa de lo que queda |
| `ValidateForPublish(meta, profile, level, now, payload, settings)` | las tres pasadas a la vez, no corrige nada. `level` puede ser `null` para evaluar solo los metadatos |

`ValidationReport` contiene `RuleIssues` y `GraphIssues`:
- `IsValid` - no hay ninguna incidencia
- `HasErrors` - hay al menos una incidencia del grupo `Error`

## Gravedad

Cada regla pertenece a un `RuleGroup`:
- `Error` - el archivo no se puede jugar tal como está escrito
- `Warning` - se juega, pero no como se pretendía (contenido que nunca aparece, una referencia rota con alternativa). O la única corrección es destructiva
- `Advice` - la reproducción no cambia

## Tres pasadas

| Pasada | Qué pregunta | Sobre qué trabaja |
|---|---|---|
| `RuleAnalyzer` | si cada valor está en su rango, no es `null` y es un miembro conocido de la enumeración | cualquier raíz |
| `LevelGraphAnalyzer` | si los objetos concuerdan entre sí | solo `Level` |
| `PublishReadinessAnalyzer` | si el nivel se puede dar a desconocidos con el perfil indicado | `LevelMeta`, opcionalmente `Level` |

## Reglas

Un tipo entra en la comprobación con el marcador `[RuleContainer]`. Sus propiedades llevan atributos de reglas:
- `[RuleNotNull]`, `[RuleInRange]`, `[RuleMinValue]`, `[RuleEnumValid]`, `[RuleCollectionMaxCount]` y otros
- `[RuleEnumFlagsValid]` - para enumeraciones de indicadores
- `[RuleOptional]` - para un campo que puede faltar

Los propios límites son constantes de las tablas de `Rules/`: `FrameRules`, `ValueRules`, `LevelRules` y otras. Por ejemplo, `LevelRules.MaxObjects` vale 262 144

El recorrido de todos los contenedores de reglas lo genera `BH.SDK.Roslyn`, sin reflexión. En niveles grandes esto reduce su tiempo aproximadamente a la mitad

## Correcciones

Cada atributo de regla puede corregir su propio valor (`Fix`). `RuleFixer` aplica las correcciones en orden inverso a la traza: una corrección puede desplazar incidencias más profundas. `ValidateAndFix` repite la pasada hasta que el resultado deja de cambiar

La pasada del grafo se ejecuta después de las correcciones. Una corrección puede crear por sí misma un problema en el grafo, por ejemplo un id nuevo que coincide con uno existente

**Las incidencias del grafo nunca se corrigen:** `DuplicateObjectId`, `MissingParent`, `ParentCycle`, `PrefabRemapBroken`, `IdCounterNearExhaustion` y el resto. Cada corrección así es una decisión sobre el contenido (cuál de dos objetos conserva su id). Una suposición reescribiría el nivel

> [!caution] Precaución
> `ValidateAndFix` modifica el objeto que le pasas. Ejecútalo sobre una copia si necesitas el original, por ejemplo para mostrar al autor qué ha cambiado exactamente
