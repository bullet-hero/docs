---
title: Blob-Format
date: 2026-10-01
tags: [developer]
---

# Blob-Format

Eine .blob-Datei enthält dieselben Daten wie .json in binärer Form: einen 24-Byte-Header, gefolgt von den Daten. Sie ist ein gleichwertiges Levelformat, kein Cache

Ein Level kann auch ausschließlich als `.blob` gespeichert sein

| Level `volcano`, 19.341 Objekte | Größe |
|---|---|
| `level.json` | 15,7 MB |
| `level.blob` | 5,1 MB, gelesen in 203 ms |

`.blob` verspricht keine Lesbarkeit. Es lässt sich weder mit bloßem Auge lesen noch per Diff vergleichen, deshalb ist es nirgends der Standard

Den Codec für jedes Modell erzeugt der Roslyn-Generator

## Header

| Offset | Größe | Feld | Wert |
|---|---|---|---|
| 0 | 4 | Magic | `uint` `0x4F424842`, Bytes `42 48 42 4F` (`BHBO`) |
| 4 | 2 | Codec-Generation | `ushort`, `BlobFormat.Generation` = 1 |
| 6 | 2 | Flags | `ushort`, Bit 0 `FlagHashed` = ein Hash ist vorhanden. Die übrigen Bits sind reserviert und müssen 0 sein |
| 8 | 8 | Datenlänge | `long` |
| 16 | 8 | Hash | `ulong`, xxHash64 der Daten mit der Codec-Generation als Seed |

Die Headerlänge `BlobFormat.HeaderLength` beträgt 24 Bytes, danach folgen die Daten

## Reihenfolge der Prüfungen

`BlobFormat.ReadHeader` prüft den Header in einer festen Reihenfolge. Bis der Header bestanden hat, wird nichts alloziert:
1. Magic
2. die Codec-Generation ist 1
3. keine unbekannten Flags
4. die angegebene Länge entspricht der tatsächlichen
5. der Hash stimmt, falls `FlagHashed` gesetzt ist

Jeder Fehlschlag ist eine `BlobFormatException` mit eigener Meldung. "Die Datei ist beschädigt" und "die Datei stammt aus einem neueren Build" verlangen vom Spieler Verschiedenes, deshalb werden sie nicht zu einem Fehler zusammengelegt

Der Hash ist absichtlich nicht kryptografisch. Er erkennt Beschädigungen, gegen Manipulation schützt die OpenPGP-Schicht. Mehr - [[4_archives]]

## Kodierung

- Little Endian, Zahlen fester Breite, kein Varint
- ein String ist eine Byteanzahl `int`, gefolgt von UTF-8
- `null` ist eine Länge von `-1`. So bleiben eine leere und eine fehlende Liste nach einem Hin-und-zurück verschieden
- ein polymorpher Wert beginnt mit einem Ein-Byte-Tag, `0xFF` ist für `null` reserviert. Das Tag ist `GetModelType()` des Modells, dieselbe Markierung, die JSON in `[tag, data]` schreibt
- eine aus einer Datei gelesene Anzahl wird in `BlobReader.ReadCount` geprüft, bevor irgendetwas dafür alloziert wird

## Hüllen und zwei Generationen

Jede Wurzel mit `[ModelGeneration]` schreibt ihre eigene Hülle: die Domäne als String, die Modellgeneration als `int`, die Länge des Inhalts, dann den Inhalt selbst. So liest ein Werkzeug die Generation einer Datei:

```csharp
var bytes = File.ReadAllBytes(path);
var reader = new BlobReader(bytes, BlobFormat.HeaderLength, bytes.Length - BlobFormat.HeaderLength);
var domain = reader.ReadString();
var generation = reader.ReadInt();
```

Hier gibt es zwei verschiedene Generationen:
- **die Codec-Generation** im Header beschreibt die Anordnung der Bytes. Ändert sie sich, wird jede alte `.blob` als Ganzes unlesbar: Es gibt nichts, worauf man zurückfallen könnte
- **die Modellgeneration** in jeder Hülle beschreibt die Form einer Domäne. Eine alte wird migriert, eine neue wird über `NewerGenerationException` abgelehnt. Mehr - [[5_versioning]]

Sie lassen sich nicht zu einer Zahl zusammenlegen. Die Modellgeneration liegt in der Hülle, und die Hülle findet nur, wer die Anordnung der Bytes schon kennt. Eine Modelländerung bewegt die Codec-Generation nie

## Den Header erweitern

Der Header hat keine freien Bytes und kein Feld mit eigener Länge. Er wächst auf zwei Wegen:
- **ein Flag.** 15 Bits sind frei. Ein alter Leser lehnt eine Datei mit einem unbekannten Flag ab, statt sie falsch zu lesen
- **eine neue Codec-Generation.** Eine neue Anordnung kann alles ändern, auch die Headerlänge. Ein neuerer Leser kann die alte Generation neben der neuen lesen

Hinter die Daten lässt sich nichts anhängen. Die angegebene Länge muss der tatsächlichen entsprechen, deshalb wird jeder zusätzliche Rest abgelehnt. Neue Leveldaten gehören in die Daten, über die Modellgeneration

> [!info] Gut zu wissen
> Inhalt, der nicht genau an seiner angegebenen Länge endet, gilt in beide Richtungen als Beschädigung. Manchmal besteht eine Wurzel jede Prüfung des Headers und lässt sich trotzdem nicht parsen. Dann wird sie anhand ihrer Länge übersprungen und behält ihre Standardwerte. Das Überspringen wird in `SerializationReport` festgehalten, nie stillschweigend
