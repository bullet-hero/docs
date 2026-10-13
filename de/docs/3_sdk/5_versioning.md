---
title: Versionierung und Migrationen
date: 2026-10-02
tags: [developer, level_author]
---

# Versionierung und Migrationen

Es gibt drei Versionen: gv für das Spiel, sv für das SDK, mg für die Generation des Modellformats. Anhand von mg migriert das SDK eine alte Datei und lehnt eine mit neuerer Generation als der Build ab

## Drei Versionen

| Kürzel | Steht für | Was es versioniert | Wo es liegt |
|---|---|---|---|
| `gv` | `game version` | den Spielclient | `bundleVersion` des Unity-Projekts |
| `sv` | `sdk version` | das SDK als Bibliothek, Semver über die öffentliche API | `SdkVersion.Value` |
| `mg` | `model generation` | das Modellformat, eine Generation pro Domäne | `[ModelGeneration]` an jeder Wurzel, `ModelGenerations.Current` |

Die aktuellen Versionen sind `gv {{v:version.gv}}`, `sv {{v:version.sv}}`, `mg {{v:version.mg}}`

Die Nummern von `gv` und `sv` müssen einander nicht folgen, stimmen aber meistens überein.
Versionen werden gemeinsam erhöht, und ein gemeinsames Update trägt dieselbe Version

Was jeder Teil bedeutet:
- `gv`: Major ist ein globales Update (Geschichte, Mehrspieler), Minor sind gewöhnliche neue Funktionen, Patch ist ein Hotfix
- `sv`, sobald das SDK API-Stabilität verspricht: Major ist eine inkompatible API-Änderung (ein Typ entfernt, Signatur oder Bedeutung eines Members geändert), Minor ist eine Ergänzung, auf die niemand reagieren muss, Patch ist eine Korrektur, die keine Signaturen ändert

**`mg` ist wichtiger als die anderen.** Danach entscheidet das SDK, ob es eine Datei migriert oder ihr Lesen ablehnt

Der Einstellungsbildschirm zeigt alle drei in dieser Reihenfolge und mit Kürzeln: `gv {{v:version.gv}}, sv {{v:version.sv}}, mg {{v:version.mg}}`. Ohne die Kürzel lassen sich zwei gleiche Nummern in einem Fehlerbericht nicht auseinanderhalten

Eine Version mit `b` und einer Zahl am Ende, zum Beispiel `gv 1.1.0b1`, ist eine Beta: ein Build der nächsten Version zum Testen, meist in einem Beta-Zweig auf Steam. Das Release danach erscheint ohne den Buchstaben (`gv 1.1.0`). Eine von einer Beta gespeicherte Datei öffnet sich im vorherigen Release unter Umständen nicht

> [!warning] Warnung
> Bis das SDK etwas anderes sagt, folgt `sv` dem Spiel, und `sv 1.0.0` verspricht keine API-Stabilität. Eine Major-Version von `sv` sagt über die Kompatibilität von Code, der gegen die DLL gebaut ist, noch nichts aus

## Zahlen, die keine Versionen sind

Zwei weitere Zahlen sehen wie eine "Version" aus, sind aber keine:
- `LevelMeta.LevelVersion` (Schlüssel `vrs`) - die Version des Levels vom Autor, ein String wie `"1.0"`
- `BlobFormat.Generation` - die Anordnung der Bytes in `.blob`. Mehr - [[3_blob-format]]

## Generation: eine Ganzzahl pro Domäne

Eine Domäne ist eine Wurzel, die als ein Ganzes migriert. Es gibt 21 davon: `Level`, `LevelMeta`, `UserSettings`, `Prefab`, `ThemeData`, `PublishProfile` und weitere.
Dazu gehören auch die Teile innerhalb von `Level`: `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources`, `LevelHints`. Jede Domäne schreibt ihre Generation in den Schlüssel `g` ihrer Hülle

| Konstante | Wert | Bedeutung |
|---|---|---|
| `ModelGenerations.Invalid` | -1 | gar keine Generation |
| `ModelGenerations.Test` | 0 | das Gerüst `Versions/V0`, das den Migrationspfad durchspielt |
| `ModelGenerations.V1_AlphaRelease` | 1 | was `gv 1.0.0` ausgeliefert hat, die meisten Domänen sind noch darauf |
| `ModelGenerations.V2_SimplifyEntrance` | 2 | `UserSettings`, `LevelMeta`, `LevelStatistics`, `GameStatistics` und die neue `Collection` |
| `ModelGenerations.Current` | die neueste | was die Oberfläche und die Berichte anzeigen |

**Eine Generation ist eine Zahl, kein `major.minor`.** Eine Änderung an der Form einer Datei braucht entweder eine Migration oder nicht. Ein Dazwischen gibt es nicht

**Die Nummern kommen aus einem globalen Zähler.** Eine geänderte Domäne bekommt `ModelGenerations.Current + 1`, nicht ihre eigene nächste freie Nummer. Genau das hält das eine `mg` im Versionsstring aussagekräftig

## Das Neue wird abgelehnt

Jede Modelländerung ist eine neue Generation. Eine geänderte Form, ein hinzugefügtes Feld und ein neuer Enum-Wert zählen gleich.
Eine Generation, die höher ist, als der Build kennt, ist also eine Form, die er mit Sicherheit nie gesehen hat

Es gibt eine Ausnahme: ein völlig neues Modell, das kein bestehendes erwähnt, zum Beispiel Avatar-Skins in einer eigenen Datei. Das ist eine neue Domäne, aus der nichts migriert werden muss, daher wächst die Generation nicht. Wachsen muss die Generation des bestehenden Modells, das anfängt, darauf zu verweisen

Eine solche Datei wird überhaupt nicht gelesen: keine Standardwerte, keine übersprungenen Teile. `NewerGenerationException` trägt `Domain`, `FileGeneration` und `BuildGeneration`, und der Host bittet den Spieler, das Spiel zu aktualisieren

```
refused: 'Level' is at generation 2, newer than this build's 1 (domain Level, file 2, this SDK 1) - update the SDK
```

## Das Alte wird migriert

Eine Domäne, die ihre Form ändert, bekommt:
1. eine neue Generation aus dem globalen Zähler
2. einen eingefrorenen Schnappschuss der alten Form in `Versions/V<old>/`: eine Klasse mit `[GenerateModel]` und `[ModelGeneration(domain, <old>)]`
3. eine `ModelMigration<TFrom, TTo>` in `Versions/V<old>/Migrations/`

```csharp
public class GameEventsV0ToV1 : ModelMigration<GameEventsV0, GameEvents>
{
    public override GameEvents Migrate(GameEventsV0 from) => new();
}
```

`VersionedTypeRegistry` findet die Schnappschüsse und Migratoren per Reflection und geht die Kette bis zur heutigen Form entlang. Jede verlustbehaftete Ersetzung beim Lesen landet in `SerializationReport`, nicht im Schweigen

## Ablehnung vor dem Lesen

`LevelMeta.MinGeneration` (Schlüssel `min_generation`) ist die höchste Generation unter den Domänen des Levels. Sie wird beim Speichern über `LevelGenerations.Required()` berechnet und nie von Hand eingetragen

Der Client vergleicht sie, bevor er `level.json` öffnet. So wird ein Level aus der Zukunft abgelehnt, ohne Megabytes an Inhalt zu lesen. Eine Datei, die nichts angibt, speichert `-1`

Das vollständige Protokoll der Entscheidungen - [VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) im SDK-Repository
