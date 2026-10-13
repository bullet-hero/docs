---
title: Validierung
date: 2026-10-01
tags: [developer, level_author]
---

# Validierung

Die Validierung rufst du selbst über ValidationFacade auf, sie steckt nicht im Speichern und Laden. Befunde teilen sich in Error, Warning und Advice, und ValidateAndFix repariert, was möglich ist

Wo sie läuft, entscheidet das Spiel. Beim Öffnen eines Levels im Editor werden Probleme gemeldet, beim Abspielen wird die Prüfung übersprungen. So wartet der Autor auf die Validierung, der Spieler nie

Ein Levelautor begegnet der Validierung, wenn er ein Level einem Dienst anbietet. Mehr - [[7_publish-profiles]]

## Wie man sie aufruft

`ValidationFacade` ist der einzige Einstiegspunkt. Der Aufrufer muss nicht wissen, wie viele Durchläufe es gibt:

```csharp
var facade = new ValidationFacade();
var report = facade.Validate(level);

if (report.HasErrors)
    Console.WriteLine(report);
```

| Methode | Was sie tut |
|---|---|
| `Validate(root, settings)` | prüft jede Wurzel: `Level`, `LevelMeta`, `UserSettings`, ein eigenständiges `Prefab` oder `EffectData`. Der Graphdurchlauf läuft nur für `Level` |
| `ValidateAndFix(root, analyzerSettings, fixerSettings)` | repariert, was möglich ist, und meldet den Rest |
| `ValidateForPublish(meta, profile, level, now, payload, settings)` | alle drei Durchläufe auf einmal, repariert nichts. `level` kann `null` sein, um nur die Metadaten zu bewerten |

`ValidationReport` enthält `RuleIssues` und `GraphIssues`:
- `IsValid` - es gibt überhaupt keine Befunde
- `HasErrors` - es gibt mindestens einen Befund in der Gruppe `Error`

## Schweregrad

Jede Regel gehört zu einer `RuleGroup`:
- `Error` - die Datei lässt sich so, wie sie geschrieben ist, nicht spielen
- `Warning` - sie läuft, aber nicht wie beabsichtigt (Inhalt, der nie erscheint, ein kaputter Verweis mit Ersatzwert). Oder die einzige Reparatur ist destruktiv
- `Advice` - das Abspielen ändert sich nicht

## Drei Durchläufe

| Durchlauf | Was er fragt | Worauf er arbeitet |
|---|---|---|
| `RuleAnalyzer` | ob jeder Wert in seinem Bereich liegt, nicht `null` ist, ein bekannter Enum-Wert ist | jede Wurzel |
| `LevelGraphAnalyzer` | ob die Objekte zueinander passen | nur `Level` |
| `PublishReadinessAnalyzer` | ob das Level unter dem gegebenen Profil an Fremde gehen kann | `LevelMeta`, optional `Level` |

## Regeln

Ein Typ wird über die Markierung `[RuleContainer]` in die Prüfung aufgenommen. Seine Eigenschaften tragen Regelattribute:
- `[RuleNotNull]`, `[RuleInRange]`, `[RuleMinValue]`, `[RuleEnumValid]`, `[RuleCollectionMaxCount]` und weitere
- `[RuleEnumFlagsValid]` - für Flag-Enums
- `[RuleOptional]` - für ein Feld, das fehlen darf

Die Grenzen selbst sind Konstanten in den Tabellen unter `Rules/`: `FrameRules`, `ValueRules`, `LevelRules` und weitere. Zum Beispiel ist `LevelRules.MaxObjects` 262.144

Den Durchlauf über alle Regelcontainer erzeugt `BH.SDK.Roslyn`, ohne Reflection. Bei großen Levels halbiert das seine Laufzeit ungefähr

## Reparaturen

Jedes Regelattribut kann seinen eigenen Wert reparieren (`Fix`).
`RuleFixer` wendet Reparaturen in umgekehrter Trace-Reihenfolge an: Eine Reparatur kann tiefer liegende Befunde verschieben. `ValidateAndFix` wiederholt den Durchlauf, bis sich das Ergebnis nicht mehr ändert

Der Graphdurchlauf läuft nach den Reparaturen. Eine Reparatur kann selbst ein Problem im Graphen erzeugen, zum Beispiel eine neue ID, die mit einer bestehenden übereinstimmt

**Graphbefunde werden nie repariert:** `DuplicateObjectId`, `MissingParent`, `ParentCycle`, `PrefabRemapBroken`, `IdCounterNearExhaustion` und die übrigen. Jede solche Reparatur ist eine Entscheidung über den Inhalt (welches von zwei Objekten seine ID behält). Eine Vermutung würde das Level umschreiben

> [!caution] Vorsicht
> `ValidateAndFix` verändert das übergebene Objekt. Lass es auf einer Kopie laufen, wenn du das Original brauchst, zum Beispiel um dem Autor zu zeigen, was sich genau geändert hat
