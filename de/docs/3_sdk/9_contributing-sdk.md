---
title: Zum SDK beitragen
date: 2026-10-02
tags: [developer]
---

# Zum SDK beitragen

Probleme mit dem SDK meldest du in den Issues des Repositorys bullet-hero/sdk, Codeänderungen schickst du dorthin als Pull Requests. Die Regeln für Mitwirkende liegen dort neben dem Code

Das Repository ist [bullet-hero/sdk](https://github.com/bullet-hero/sdk), der Standardzweig ist `master`

## Wo man meldet

| Worum es geht | Wohin |
|---|---|
| das SDK und sein Code | [bullet-hero/sdk/issues](https://github.com/bullet-hero/sdk/issues) |
| das Spiel: Fehler und Wünsche der Spieler | [bullet-hero/releases/issues](https://github.com/bullet-hero/releases/issues) |
| der Text der Dokumentation | [bullet-hero/docs](https://github.com/bullet-hero/docs) |

## Wo die Regeln stehen

Die Regeln für Mitwirkende liegen im SDK-Repository selbst, neben dem Code, den sie beschreiben:

| Datei | Was darin steht |
|---|---|
| [README.md](https://github.com/bullet-hero/sdk/blob/master/README.md) | Abhängigkeiten, Levelpakete, Bauen der DLL und des Pakets, das Prüfbeispiel |
| [CLAUDE.md](https://github.com/bullet-hero/sdk/blob/master/CLAUDE.md) | das Denkmodell, ein Ordnerverzeichnis und die Konventionen der ganzen Bibliothek |
| `CLAUDE.md` in jedem Ordner | die lokalen Regeln dieses Ordners, zum Beispiel [Serialization](https://github.com/bullet-hero/sdk/blob/master/Serialization/CLAUDE.md), [Validations](https://github.com/bullet-hero/sdk/blob/master/Validations/CLAUDE.md), [Publishing](https://github.com/bullet-hero/sdk/blob/master/Publishing/CLAUDE.md) |
| [Docs/VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) | Versionsachsen, Generationen, Migration und Ablehnung |
| [Docs/IDENTIFIERS.md](https://github.com/bullet-hero/sdk/blob/master/Docs/IDENTIFIERS.md) | wie das Modell Entitäten adressiert: Guid, int, Frame, Feldpfad |
| [[ugc-licensing-policy]] (auf dieser Website) | die Lizenzrichtlinie für Inhalte der Nutzer, wird gemeinsam mit `TrustedSourceCatalog` bearbeitet |
| [Versions/README.md](https://github.com/bullet-hero/sdk/blob/master/Versions/README.md) | wie man einen Schnappschuss und einen Migrator schreibt |
| [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md) | der Vertrag der Generatoren |
| [Roslyn/README.md](https://github.com/bullet-hero/sdk/blob/master/Roslyn/README.md) | die Analyzer und der Modellgenerator, wie man sie neu baut |
| [UnityIntegration/README.md](https://github.com/bullet-hero/sdk/blob/master/UnityIntegration/README.md) | der Vertrag der doppelten Kompilierung |
| [CHANGELOG.md](https://github.com/bullet-hero/sdk/blob/master/CHANGELOG.md) | Änderungen nach `sv`-Version, die neueste oben |

## Build und Tests

```bash
dotnet build -c Release BH.SDK.csproj
dotnet test Tests/BH.SDK.Tests.csproj
dotnet pack -c Release BH.SDK.csproj
```

- hier werden dieselben Quellen, die Unity kompiliert, ohne Unity gebaut. Eine Datei, die den Vertrag der Engine-Unabhängigkeit bricht, bricht diesen Build
- die Ausgabe landet in `bin~` und `obj~`
- der Pack-Befehl erzeugt nur ein `.nupkg`. Auf nuget.org veröffentlicht der Workflow `release` des Repositorys, wenn ein `sv`-Tag gepusht wird

> [!caution] Vorsicht
> Die Analyzer und der Modellgenerator werden als vorgebaute `BH.SDK.Roslyn.dll` im Wurzelordner des SDK ausgeliefert. Wenn du irgendetwas in `Roslyn/` änderst, baue sie neu und kopiere sie hinüber. Sonst läuft weiter der alte Generator, auch wenn die Quellen etwas anderes sagen

```bash
cd Roslyn
dotnet build BH.SDK.Roslyn.csproj -c Release
cp bin~/Release/BH.SDK.Roslyn.dll ../BH.SDK.Roslyn.dll
dotnet test Tests~/BH.SDK.Roslyn.Tests.csproj -c Release
```

Im Unity-Editor erledigt der Menüpunkt **Tools > BH.SDK.Roslyn > Build Analyzer** dasselbe

## Invarianten, die man vorher kennen sollte

- der Kern verweist auf keinen einzigen Typ aus `UnityEngine`. Code, der die Engine braucht, kommt nach `UnityExtensions/` oder nach `UnityIntegration/` hinter `#if BHSDK_UNITY` mit einem Zweig ohne Engine
- der Code arbeitet mit Dateien und mit Daten im Speicher gleich und nutzt nur die Asynchronität aus der BCL
- `netstandard2.1` und C# 9 sind das, womit das Unity-Projekt kompiliert. Sie werden nicht angehoben
- ein Modell ist eine `[GenerateModel] public sealed partial class`. Jedes serialisierte Feld nimmt seinen Schlüssel aus `Names.cs`
- jede Modelländerung ist eine neue Generation mit Schnappschuss und Migrator. Mehr - [[5_versioning]]
- die SDK-Version steht an drei Stellen: `SdkVersion.cs`, `package.json` und `<Version>` in `BH.SDK.csproj`. `SdkVersionAgreementTests` schlägt fehl, wenn sich eine davon allein bewegt hat
