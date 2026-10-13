---
title: Was ein Level braucht
date: 2026-10-02
tags: [level_author]
---

# Was ein Level braucht

Das Minimum ist ein Song. Alles andere ist optional, und fast alles davon bringst du selbst mit

## Was ein Level nutzen kann

| Was | Details | Wo es liegt |
|---|---|---|
| Audio | mindestens ein Song, es können mehrere sein | im Levelordner |
| Bilder | wenn eine Form nicht reicht | im Levelordner |
| Schriftarten | `ttf`, `otf`, `ttc` | im Levelordner |
| Formen | 497 eingebaute und beliebige, die im `{{ui:hint_level_shape-editor_header}}` gezeichnet werden | im Spiel oder im Level eingebaut |
| Themes, Effekte, Prefabs | Daten, keine Dateien | in `level.json` |

Audio, Bilder und Schriftarten sind echte Dateien.
Nur sie machen den Ordner schwerer, brauchen vor dem Veröffentlichen einen Herkunftseintrag und können beim Verschieben verloren gehen

Ohne eigene Schriftart wird Text mit dem gezeichnet, was das System hat

**Das Spiel bringt überhaupt keine Texturen mit.** Eingebaute Formen sind Geometrie, keine Bilder. Sie haben keine Pixel, wiegen nichts, und es gibt nichts, woher man sie laden müsste

> [!tip] Empfehlung
> Greif immer zuerst zu einer Form statt zu einem Bild. Ein Bild ist eine Datei, die beim Verschieben verloren gehen kann, Speicher beim Laden und eine Zeile im Lizenzeintrag. Eine Form kostet nichts davon

## Das Gewicht des Ordners

Es gibt keine harte Grenze. Aber ein Level reist als Kopie, und wer es bekommt, sieht das Gewicht des Ordners

Ein Song von 4 Minuten wiegt in `ogg` 4-6 MB. Derselbe Song in `wav` sind etwa 40 MB

## Mehrere Quellen für eine Ressource

Eine Ressource kann eine Liste von Orten haben, von denen sie geholt wird: eine Datei neben dem Level, ein absoluter Pfad, ein direkter Link.
Das Spiel geht die Liste durch, bis etwas lädt

> [!tip] Empfehlung
> Nutze einen Link als Ergänzung zur Datei, nicht als Ersatz. Eine Website kann offline gehen, umziehen oder plötzlich etwas anderes ausliefern. Eine Datei im Ordner liegt dort, wo das Level liegt

## Rechte an den Dateien

Verlässt das Level deine Festplatte, braucht jede Datei darin eine Lizenz, die das erlaubt.
Das entscheiden die Ressourcen, die du ganz am Anfang auswählst

Mehr - [[2_editor/3_rights/index]]

Weiter: [[2_preparing-the-track]], [[3_images-and-fonts]]
