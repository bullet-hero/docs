---
title: Was ein Level ist
date: 2026-10-02
tags: [level_author]
---

# Was ein Level ist

Ein Level ist ein gewöhnlicher Ordner auf der Festplatte: die Leveldatei, die Metadaten und alles, was es nutzt. Bau es in Json und gib es als Kopie des Ordners weiter, installiert wird nichts

## Was im Ordner liegt

Der Ordner ist keine Zeile in einer Datenbank und kein verschlüsseltes Archiv

Es gibt zwei Hauptdateien:
- `level.json` - das Level selbst: Objekte, Keyframes, Themes, Ressourcen
- `metadata.json` - der Steckbrief: Name, Beschreibung, Autoren, Tags, Dauer

Daneben liegt alles, was das Level nutzt: der Song, Bilder, Schriftarten.
Das Spiel bringt überhaupt keine Texturen mit. Alles, was du in einem Level siehst, ist entweder eine eingebaute Form oder eine Datei aus diesem Ordner

Der Steckbrief ist eine eigene Datei, damit eine Liste von tausend Levels nicht bedeutet, tausend Levels zu öffnen

Die vollständige Liste der Dateien - [[4_level-folder-and-backups]]

## Json oder Blob

Das Dateiformat wählst du beim Erstellen eines Levels:

| Format | Was es ist |
|---|---|
| `Json` | reiner Text, lässt sich in jedem Editor öffnen und von Hand reparieren |
| `Blob` | eine Binärdatei, lädt Dutzende Male schneller und ist ein Drittel so groß, mit bloßem Auge nicht lesbar |

> [!tip] Empfehlung
> Bau das Level in `Json` und wandle es in `Blob` um, wenn es fertig ist. Öffnet sich das Level nicht mehr, lässt sich `Json` lesen und von Hand reparieren. `Blob` ist kaum zu retten: ein einziges beschädigtes Byte lässt die Integritätsprüfung scheitern

## Wie man ein Level weitergibt

Ein Level reist als Kopie. Ordner zippen, verschicken, entpacken, öffnen.
Nichts wird installiert, registriert oder importiert

Am PC funktioniert das immer. Auf dem Handy überall dort, wo das System dich hineinlässt

Was daraus folgt:
- eine Sicherung eines Levels ist eine Kopie des Ordners
- benenne Dateien im Ordner nicht um: Ressourcen werden über den Namen gefunden
- ein `Json`-Level, das der Editor nicht öffnet, lässt sich trotzdem mit bloßem Auge lesen. Der Tab `{{ui:settings_level-settings_raw}}` zeigt nur ein Level, das bereits geöffnet ist

> [!caution] Vorsicht
> Bearbeite `level.json` nicht in einem Texteditor, während das Level im Spiel geöffnet ist. Speichern aus dem Editor überschreibt deine Änderungen stillschweigend

## Das Format ist offen

Das Datenmodell der Level liegt in einem eigenen Repository unter der MIT-Lizenz - [bullet-hero/sdk](https://github.com/bullet-hero/sdk).
Ein Level lässt sich also ohne das Spiel lesen, und du kannst dein eigenes Werkzeug für das Format schreiben. Ein Fehler im Format ist auch von außen sichtbar

Mehr zum Format - [[3_sdk/index]]

Weiter: [[2_first-level]], [[4_level-folder-and-backups]]
