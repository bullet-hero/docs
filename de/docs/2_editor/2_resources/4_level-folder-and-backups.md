---
title: Der Levelordner und Sicherungen
date: 2026-10-11
tags: [level_author]
---

# Der Levelordner und Sicherungen

Ein Level liegt in einem eigenen Ordner in levels im Ordner des Spiels. Benenne die Dateien, die es nutzt, nicht um, und eine vollständige Sicherung ist eine Kopie des Levelordners

## Was im Ordner liegt

Der Levelordner liegt in `levels` im Ordner des Spiels. Wo der Ordner des Spiels liegt - [[1_installation]]

| Datei | Was es ist |
|---|---|
| `level.json` | der Inhalt des Levels. Im Binärformat - `level.blob` |
| `metadata.json` | Name, Beschreibung, Autoren, Tags. Im Binärformat - `metadata.blob` |
| `logo.png` oder `logo.jpg` | das Levelbild |
| der Song, Bilder, Schriftarten | alles andere, was das Level nutzt, direkt neben `level.json` |

Neben `levels` liegt `resources` mit den gerätweiten Bibliotheken: `themes`, `effects`, `shapes`, `prefabs`.
Sie gehören nicht zum Level. Was du wiederverwenden willst, exportierst du dorthin und importierst es von dort

Derselbe Ordner `resources` enthält `collections`, einen Ordner pro Sammlung. Mehr - [[16_library-and-collections]]

Ein Level, das du jemandem schickst, trägt alles, was es braucht, in sich. Die Bibliotheken reisen nicht mit

## Was du nicht von Hand anfassen solltest

> [!caution] Vorsicht
> Benenne die Dateien, die das Level nutzt, nicht um. Verweise darauf werden über den Namen gespeichert, eine umbenannte Datei ist also eine fehlende Datei

Bearbeite `level.json` nicht in einem Texteditor, während das Level im Spiel geöffnet ist. Speichern aus dem Editor überschreibt deine Änderungen stillschweigend

Leg nichts in den Levelordner, was das Level nicht nutzt. Es reist mit dem Ordner mit

Das Dateiformat ergibt sich aus der Endung, nicht aus einem Feld in der Datei. Ein Formatwechsel im Editor schreibt also eine neue Datei und löscht die alte.
Sonst lägen zwei Dateien auf der Festplatte, und niemand könnte sagen, welche die echte ist

## Wenn eine der beiden Dateien fehlt

Ein Ordner, der nur eine von `level.json` und `metadata.json` enthält, wird trotzdem in der Levelliste angezeigt. Die binären `level.blob` und `metadata.blob` zählen genauso

| Fehlt | Im Spiel | Im Editor |
|---|---|---|
| `level.json` | die Karte ist vollständig, aber das Level lässt sich nicht starten | wird aus der neuesten automatisch gespeicherten Kopie wiederhergestellt. Ohne Kopien wird ein leeres Level geschrieben |
| `metadata.json` | die Karte zeigt den Ordnernamen, und das Level lässt sich spielen | eine neue `metadata.json` wird mit dem Ordnernamen und Standardeinstellungen geschrieben |

Eine `metadata.json`, die das Spiel nicht lesen kann, zählt als fehlend. Der Editor verschiebt sie nach `metadata.json.bak`, bevor er die neue schreibt, es geht also nichts verloren

Der Editor fragt nach, bevor er irgendetwas schreibt. Ein eingebautes oder ein `Workshop`-Level wird nie an Ort und Stelle geändert: eines ohne `metadata.json` wird als Kopie angeboten, und eines ohne `level.json` lässt sich nicht öffnen

## Sicherungen und Wiederherstellung

**Eine vollständige Sicherung ist eine Kopie des Levelordners.** Sie enthält alles, Ressourcen eingeschlossen.
Mach vor jedem größeren Umbau eine Kopie und versieh sie mit dem Datum

**Das Autospeichern sichert nur die Leveldatei.** Keine Metadaten, keinen Song, keine Bilder.
Jedes automatische Speichern legt eine Kopie in `backups/<level id>/` im Ordner des Spiels ab, außerhalb von `levels`. `25` Kopien werden aufbewahrt. Wie man eine Kopie wiederherstellt - [[4_not-losing-work#Autospeichern]]

**Ein `Json`-Level, das sich nicht mehr öffnen lässt, ist nicht verloren.** Die Datei ist Text, du kannst sie also in jedem Texteditor öffnen und mit bloßem Auge reparieren. Das Spiel selbst öffnet kein Level, das nicht lädt, der Tab `{{ui:settings_level-settings_raw}}` hilft hier also nicht. Er zeigt das Modell eines Levels, das bereits geöffnet ist

Ein `Blob` lässt sich so nicht retten. Es ist binär, und eine beschädigte Datei wird als Ganzes abgelehnt, statt teilweise gelesen zu werden

Was du wissen solltest, bevor du im Tab `{{ui:settings_level-settings_raw}}` etwas bearbeitest - [[4_not-losing-work#Der Tab Raw]]

Weiter: [[4_not-losing-work]], [[2_metadata-and-sharing]]
