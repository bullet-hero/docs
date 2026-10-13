---
title: Levelformat
date: 2026-10-02
tags: [developer, level_author]
---

# Levelformat

Ein Level ist ein Ordner: Inhalt in level.json oder level.blob, Metadaten in metadata.json oder metadata.blob, ein Cover und Mediendateien. Sicherungen, Rekorde und Einstellungen bleiben auf dem Gerät

## Der Levelordner

Jeder Dateiname in einem Levelordner ist in `FileNames` festgelegt:

| Datei | Modell | Was darin steht |
|---|---|---|
| `level.json` oder `level.blob` | `Level` | der Inhalt: Einstellungen, Objekte und Ereignisse, Audio, Ressourcen, Hilfen |
| `metadata.json` oder `metadata.blob` | `LevelMeta` | Titel, Beschreibung, Autoren, Lizenz, ein Eintrag für jede Ressource, ein Verweis auf das Cover |
| `logo.png` oder `logo.jpg` | - | das Cover |
| Musikstück, Bilder, Schriftarten | - | Mediendateien, auf die das Level verweist |

**Die Dateiendung ist das Format.** Sie steht nirgends innerhalb der Dateien. Der Leser schaut, welche Datei existiert: `level.json` oder `level.blob`

Level und Metadaten wählen ihr Format unabhängig voneinander. Das eingebaute Level `new-zero-demo` zum Beispiel hat `level.blob` neben `metadata.json`

**`metadata.json` ist absichtlich eine eigene Datei.** Ein Katalog zeigt tausend Levels aus tausend kleinen Metadatendateien an. Dafür wird kein einziges Level geöffnet

## Ressourcen

Eine Ressource wird über das Paar aus `uri` und `uri_type` (`ResourceUriType`) adressiert:

| Wert | Typ | Wo die Datei liegt |
|---|---|---|
| 1 | `LevelPath` | im Levelordner. Nur dieser Typ macht ein Level tragbar |
| 2 | `AbsolutePath` | an einem anderen Ort auf diesem Gerät |
| 3 | `DirectUrl` | wird über das Netzwerk heruntergeladen |
| 4 | `StreamingAssets` | wird mit dem Spiel ausgeliefert, nicht mit dem Level |

`AbsolutePath` entsteht, wenn ein Level um einen Song herum erstellt wird. Beim Export eines Archivs wird eine solche Datei hineinkopiert. Mehr - [[4_archives]]

Das Cover ist wie jede andere Ressource über `LevelMeta.LevelLogo` erreichbar. Ob es `logo.png` oder `logo.jpg` ist, entscheiden die Bytes der Datei selbst, nicht der Name des Ausgangsbilds

Der Urheberschaftseintrag des Covers ist ein `ResourceMeta` mit `resource_type` 9 (`LevelLogo`). Weder `resource_id` noch `resource_guid` ist darin ausgefüllt: Ein Level hat ein Cover, also ist der Typ die ganze Adresse

## KI-Angaben

`LevelMeta` und jedes `ResourceMeta` tragen `ai_generated` vom Typ `AiGeneration`:

| Wert | Name | Was es bedeutet |
|---|---|---|
| 0 | `NotSpecified` | nichts angegeben, unbekannt. Der Standardwert, ein fehlender Schlüssel wird ebenso gelesen |
| 1 | `No` | als ohne KI-Generierung erstellt angegeben |
| 2 | `Yes` | als KI-generiert angegeben |

In `LevelMeta` deckt es nur den eigenen Inhalt des Levels ab. Jede Ressource und das Cover machen ihre Angabe im eigenen Eintrag.
Ob ein Level KI-Inhalte enthält, wird nicht gespeichert: Das beantwortet `LevelMeta.ContainsAiContent()`, und nur `Yes` zählt

## Was nicht mit einem Level reist

Diese Dateien liegen neben dem Ordner `levels`, nie in einem Levelordner. Archivieren, Verschicken oder Löschen eines Levels berührt sie nicht:

| Ordner oder Datei | Was es ist | Warum es bleibt |
|---|---|---|
| `backups/` | automatische Sicherungen des Editors, ein Ordner pro Level-ID, `backup_level_<time>.<extension>` | eine Kopie im Ordner, den sie schützt, wird mit ihm zusammen gelöscht |
| `stats/` | Rekorde und Fortschritt nach `LevelId` und `statistics.json` | ein zugeschicktes Level käme bereits abgeschlossen an |
| `settings.json` | `UserSettings`, die Einstellungen des Spielers für das ganze Gerät | sie gehören dem Spieler, nicht dem Level |
| `resources/themes`, `effects`, `shapes`, `prefabs` | die gemeinsamen Bibliotheken des Geräts | alle Levels auf dem Gerät teilen sie |
| `reports/` | Diagnoseberichte | - |

## JSON-Schlüssel

JSON wird immer kompakt geschrieben, ohne Einrückung. Um es mit bloßem Auge zu lesen, formatierst du es in einem Texteditor

**Die Länge eines Schlüssels hängt davon ab, wie oft er in einem Level vorkommt:**
- ein Schlüssel, der einmal pro Datei vorkommt, wird in ganzen Wörtern in `snake_case` geschrieben: `level_id`, `min_generation`
- ein Schlüssel, der sich tausendfach wiederholt, wird auf wenige Buchstaben gekürzt: `objs`, `f`, `e`, `v`

Schlüssel machen 52 % der Bytes einer Leveldatei aus, deshalb ist das eine Regel und keine Geschmacksfrage. Alle Schlüssel sind in `Names.cs` deklariert

**Ein polymorpher Wert wird als `[tag, data]` geschrieben.** Ein einfacher String ist `[0,{"v":"Author"}]`, ein lokalisierter `[1,{"strs":[...]}]`

Hüllen für Bezeichner wie `ObjectId` werden als bloße Zahl oder bloßer String geschrieben

## Bezeichner

**Das Vorzeichen eines ganzzahligen Bezeichners hat eine Bedeutung.** `0` heißt immer "nicht gesetzt":

| Bezeichner | JSON-Schlüssel | Positiv | Negativ |
|---|---|---|---|
| `ObjectId` | `id`, und `pid` für das Elternobjekt | ein Objekt des Levels | ein Objekt des Spiels: `-1` die Kamera, `-2` der lokale Spieler, `-3` die Wurzel einer Prefab-Vorlage |
| Bezeichner von Ressourcen | `txid`, `fnid`, `auid`, `byid`, `ttid` | eine Ressource, die mit dem Spiel ausgeliefert wird | eine eigene Ressource des Levels |
| `AudioId` einer Audiospur | `aid` | eine Spur dieses Levels | nicht verwendet |

Ein `pid` gleich `0` heißt, dass das Objekt kein Elternobjekt hat. Zahlen unter `-3` existieren nur, während das Spiel läuft, und gelangen nie in eine Datei

**`Marker`, `Checkpoint` und `BeatSegment` haben keinen Bezeichner.** Ihre Adresse ist ein Zeitpunkt: Bei einem Marker und einem Checkpoint ist es der Frame `f`, bei einem Beat-Segment der erste Frame seiner Spanne `sp` (Segmente überlappen nicht). Wird ein solches Objekt verschoben, ändert sich seine Adresse

**Eine Prefab-Überschreibung nennt ein Feld per Nummer, nicht per JSON-Schlüssel.** Eine Platzierung hält ihre Überschreibungen in der Liste `mod`. Der `key` jeder Überschreibung enthält drei Zahlen:
- `id` - das Objekt innerhalb der Vorlage, nicht seine Kopie im Level
- `f` - die dauerhafte Nummer des Felds
- `i` - das Element eines Listenfelds oder `-1` für das ganze Feld

Die Nummer ist für immer an das Feld gebunden. Wird der JSON-Schlüssel dieses Felds umbenannt, brechen bereits in Levels gespeicherte Überschreibungen nicht

## Das äußere "g"

Jede Wurzel der Serialisierung steckt in einer Hülle mit zwei Schlüsseln:

```json
{"g":2,"v":{"level_id":"18df5f61-3aa4-4812-bf69-d357f2201bc3","vrs":"1.0", ... }}
```

`g` ist die Modellgeneration (`Names.Generation`), `v` sind die Daten

Hüllen sind verschachtelt. Innerhalb von `Level` haben `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources` und `LevelHints` jeweils ihre eigene Hülle. Wie Generationen funktionieren - [[5_versioning]]

> [!caution] Vorsicht
> `g` und `vrs` sind verschiedene Zahlen. `vrs` ist die Version des Levels vom Autor (`LevelMeta.LevelVersion`), mit dem Format hat sie nichts zu tun. Ändere `g` nicht von Hand: Eine Datei mit einem `g`, das höher ist, als der Build kennt, wird überhaupt nicht gelesen
