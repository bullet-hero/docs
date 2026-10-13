---
title: Installation
date: 2026-10-02
tags: [developer, level_author]
---

# Installation

Das SDK ist das Paket BulletHero.SDK auf nuget.org oder ein Build aus dem Quellcode. Unity bindet es als Git-Submodul ein, und das Beispiel ConsoleSmoke prüft, ob deine Levels lesbar sind

Der Code des SDK liegt unter [github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk). Die Lizenz ist MIT

## .NET

Das Paket `BulletHero.SDK` ist auf nuget.org veröffentlicht: `dotnet add package BulletHero.SDK`. Die drei Abhängigkeiten kommen automatisch mit. So baust du es stattdessen aus dem Quellcode:

```bash
git clone https://github.com/bullet-hero/sdk.git
cd sdk
dotnet build -c Release BH.SDK.csproj   # bin~/Release/BH.SDK.dll and BH.SDK.xml
dotnet pack  -c Release BH.SDK.csproj   # bin~/Release/BulletHero.SDK.<version>.nupkg
```

Danach bindest du eines von beiden ein:
- das `.nupkg` aus einem lokalen Ordner: `dotnet add package BulletHero.SDK --source <folder>`. Die drei Abhängigkeiten kommen automatisch mit
- direkt die `BH.SDK.dll`. Dann fügst du die drei Pakete unten selbst hinzu: Ein Verweis auf eine DLL bringt ihre Abhängigkeiten nicht mit

Abhängigkeiten, alle aus NuGet:

| Paket | Version | Wofür |
|---|---|---|
| `Newtonsoft.Json` | 13.0.3 | JSON |
| `BouncyCastle.Cryptography` | 2.7.0 | OpenPGP für passwortgeschützte Levels |
| `SharpZipLib` | 1.4.2 | tar und zip (gzip kommt aus der BCL) |

### Details zum Build

- die Assembly ist `BH.SDK.dll`, ihre XML-Dokumentation liegt daneben
- das Ziel ist `netstandard2.1`, die Sprache C# 9. Das sind dieselben Werte wie im Unity-Projekt, daher bauen dieselben Quellen sowohl in Unity als auch ohne Unity
- die Ausgabeordner sind `bin~` und `obj~`. Die Tilde ist nötig, weil Unity Ordner nicht importiert, deren Name auf eine Tilde endet

## Unity

Das Spiel bindet das SDK als Git-Submodul ein:

```bash
git submodule init
git submodule add -f https://github.com/bullet-hero/sdk.git Assets/Plugins/BH.SDK
```

Entfernen geht mit `git rm -r -f Assets/Plugins/BH.SDK`

Was das Unity-Projekt selbst bereitstellen muss:
- `Newtonsoft.Json` über das Paket `com.unity.nuget.newtonsoft-json`
- `BouncyCastle.Cryptography` und `SharpZipLib` aus NuGet (das Spiel installiert sie mit NuGetForUnity)
- das Scripting Define `BHSDK_UNITY` in den Player Settings. Ohne es nimmt `UnityIntegration` den Zweig ohne Engine
- `BH.SDK.Roslyn.dll` im Wurzelordner des SDK. Unity wendet einen Analyzer nur auf die Assembly in seinem Ordner und auf die Assemblies an, die auf sie verweisen. An einen anderen Ort verschoben, analysiert er nichts

Im Wurzelordner des Repositorys liegt eine `package.json` mit dem Namen `com.vertoker.bullet-hero-sdk` und der Unity-Mindestversion `6000.0`. Deshalb kann auch der Package Manager das SDK per Git-URL hinzufügen. Dieser Weg wird nicht genutzt und ist hier nicht beschrieben

## Prüfen: das Beispiel ConsoleSmoke

`Samples~/ConsoleSmoke` ist eine Konsolenanwendung für `net8.0`. Sie verweist auf die gebaute `BH.SDK.dll`, genau wie ein Werkzeug eines Drittanbieters.
Die Anwendung liest einen Levelordner und gibt den Namen, die Anzahl der Objekte und die Generation aus. Danach schickt sie das Level einmal hin und zurück durch JSON und `.blob`

```bash
dotnet build -c Release Samples~/ConsoleSmoke/ConsoleSmoke.csproj
dotnet Samples~/ConsoleSmoke/bin~/Release/net8.0/ConsoleSmoke.dll <level folder>
```

| Exit-Code | Bedeutung |
|---|---|
| 0 | alles stimmt überein |
| 1 | falsche Argumente |
| 2 | `level.*` oder `metadata.*` nicht gefunden |
| 3 | ein Hin-und-zurück stimmt nicht überein |
| 4 | die Datei ist neuer als dieses SDK |

Die Ausgabe für das eingebaute Level `new-zero-demo` des Spiels (aufgenommen mit `sv 1.0.0`):

```
BH.SDK 1.0.0, model generation 1
name:       New zero demo
objects:    782
generation: 1 (Blob)
round trip Json: equal (1505078 bytes)
round trip Blob: equal (680706 bytes)
exit 0
```

Weiter - [[2_level-format]]

## Woraus das SDK besteht

| Teil | Was es ist | Braucht Unity |
|---|---|---|
| `BH.SDK` | der Kern: Modelle, Serialisierung, Versionen, Regeln, Validierung, Archive, Veröffentlichung, Generatoren | nein |
| `UnityIntegration` | eine dünne Schicht, in der jede Datei sowohl mit als auch ohne Unity kompiliert (`#if BHSDK_UNITY`), zum Beispiel der Logger `Cat` | nein: Außerhalb von Unity wird sie direkt in den Kern kompiliert |
| `UnityExtensions` | Umwandlungen in Unity-Typen, 2D-Transformationen, Bewegung des Avatars | ja, immer |
| `BH.SDK.Roslyn` | Analyzer und ein Quellgenerator. Für jedes Modell mit `[GenerateModel]` schreibt er `Equals`, das Kopieren, die Codecs für JSON und `.blob` und den Validierungsdurchlauf | läuft beim Kompilieren |

Eine Modelldatei enthält nur ihre Felder und Konstruktoren. Alles, was sich wiederholt, schreibt der Generator. So kann ein Feld in keinem der sieben generierten Rümpfe vergessen werden

## Warum eine eigene Bibliothek

- **Levels überleben das Spiel.** Ein Level ist ein Ordner mit Dateien in offenen Formaten (JSON, tar.gz, zip, OpenPGP). Auch der Code, der sie liest, ist offen. Ein Level bleibt lesbar, selbst wenn das Spiel, das es geschrieben hat, nicht mehr existiert
- **Austausch mit anderen Rhythmusspielen.** Das Format ist öffentlich beschrieben, daher lässt sich ein Konverter von oder zu einem anderen Spiel danach schreiben
- **Schnelle Korrekturen.** Ein Fehler im Format ist von außen sichtbar. Wer den Code liest, kann ihn melden oder eine Korrektur schicken
- **Werkzeuge von Drittanbietern.** Ein Konverter, ein Validator, ein Levelgenerator oder eine Mod arbeitet mit denselben Modellen wie das Spiel. Sie müssen nicht aus Dateien rekonstruiert werden
- **Server.** Der Kern baut ohne Unity als `netstandard2.1`. So führt ein Server dieselben Prüfungen über dieselben Modelle aus wie der Client
