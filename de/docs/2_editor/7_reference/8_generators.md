---
title: Generatoren
date: 2026-10-12
tags: [level_author]
---

# Generatoren

Ein Generator erstellt Inhalt und wendet ihn in einer Operation an, die sich in einem Schritt rückgängig machen lässt. Jeder Generator startet aus dem Fenster "Generatoren" in der Werkzeugleiste

## Generatoren

Das Formular eines Generators wird aus seinen eigenen Feldern aufgebaut. Eine eigene Oberfläche für jeden Generator gibt es nicht

> [!caution] Vorsicht
> Alles, was vorhandenen Inhalt überschreibt oder löscht, fragt vorher nach einer Bestätigung

> [!info] Gut zu wissen
> Es gibt zwei Familien. **Generatoren** (*gen_*) erstellen Inhalt: Geschosswellen, radiale Muster und einen Schriftcache. **Modifikatoren** (*mod_*) ändern, was schon da ist: Spannen einpassen, Keyframes quantisieren. Die Modifikatoren sind getrennt beschrieben - [[9_modifiers]]

Mehr - [[2_reuse]]

## Das Generatorenfenster

Inhaltsgeneratoren und Modifikatoren starten aus dem Fenster `{{ui:editor_generators_text}}` in der Werkzeugleiste. Sein Block `{{ui:editor_generators_base-parameters}}` ist allen Generatoren gemeinsam: `{{ui:editor_generators-start_frame}}`, `{{ui:editor_generators-end_frame}}`, `{{ui:editor_inspector_layer}}` und `{{ui:editor_generators_seed}}`. Sie gehören zum Fenster, nicht zu einem einzelnen Generator

Wie sich der Block verhält:
- Das Fenster öffnet sich mit einer Sekunde ab dem Abspielkopf und dem Seed auf 0. `{{ui:editor_generators-seed_random}}` würfelt einen neuen Seed
- Die Frames bleiben innerhalb der Zeitleiste, an der du arbeitest, von Frame 1 bis zu ihrem letzten Frame. Im Prefab-Modus ist das die Länge der Vorlage
- Eine Änderung von `{{ui:editor_generators-start_frame}}` schiebt `{{ui:editor_generators-end_frame}}` mit. Eine Änderung von `{{ui:editor_generators-end_frame}}` stoppt bei `{{ui:editor_generators-start_frame}}`. Die beiden kreuzen sich nie
- `{{ui:editor_inspector_layer}}` bleibt im erlaubten Bereich der Ebenen
- Jedes Frame-Feld hat eine Nadel, die es am Rand der Zeitleiste festhält. `{{ui:editor_generators-whole_level}}` setzt beide, und das Fenster reicht von Frame 1 bis zum letzten Frame. Die Felder bleiben bearbeitbar, und wer in ein Feld tippt, löst die Nadel an diesem Rand

`{{ui:editor_generators_group}}` und `{{ui:editor_generators-split_layers}}` sind standardmäßig an. Die Gruppe heißt wie der Generator. Beide betreffen nur Inhaltsgeneratoren: ein Modifikator erstellt nichts, also gibt es nichts zu gruppieren

Generierter Inhalt kommt nie unter das ausgewählte Objekt. Er landet auf der obersten Ebene des Kontexts oder in seiner eigenen Gruppe

Bevor du `{{ui:editor_generators_run}}` drückst, zeigt das Fenster, was ein Lauf hinzufügen wird. Die Schaltfläche ist nicht verfügbar, und statt der Schätzung steht der Grund da, wenn:
- der Generator das ganze Level braucht und du im Prefab-Modus bist. Das sind Beat-Blitz, Schriftcache, Kapazitätshinweis und Framerate umrechnen
- der Generator eine Auswahl braucht und nichts ausgewählt ist
- das Level nach dem Lauf mehr als 262 144 Objekte hätte
- ein Inhaltsgenerator nichts hinzufügen würde. Ein Modifikator wird deshalb nicht abgelehnt

Ein Generator, der externe Daten braucht (eine Audiospur, Beats, ein Bild), erstellt ohne sie nichts, und die Schätzung sagt das

`{{ui:editor_generators_run}}` schließt das Fenster. Der generierte Inhalt bleibt ausgewählt, im selben Rückgängig-Schritt

Das Fenster merkt sich beim Schließen und erneuten Öffnen, bei welchem Generator du warst und welche Parameter du eingegeben hast. `{{ui:editor_generators_reset}}` stellt die Standards wieder her

## Levels

Diese drei kann der KI-Assistent nicht ausführen. Er beginnt ein neues Level stattdessen mit seinem eigenen `level_create`

### Leeres Level

Leert das Level komplett. Alles Erstellte wird gelöscht.
Passt zum Neuanfang, nicht zum Bearbeiten

`Pin Screen Aspect` (standardmäßig an) setzt im ersten Frame einen Keyframe mit festem 16:9 auf die Spur `{{ui:editor_events-timeline_track_screen-limit}}`

Mehr - [[2_first-level]]

### Level aus Audiodatei

Beginnt ein Level mit einem Song.
Verbindet das Audio, passt die Länge des Levels an den Song an und setzt dich an den Anfang einer leeren Zeitleiste

`Pin Screen Aspect` (standardmäßig an) setzt im ersten Frame einen Keyframe mit festem 16:9 auf die Spur `{{ui:editor_events-timeline_track_screen-limit}}`

Mehr - [[2_preparing-the-track]]

### Levelarchiv importieren

Baut ein Level aus einem Archiv, das dieses Spiel erstellt hat.
Formate: `.tar.gz` und `.zip`. Beide dürfen passwortgeschützt sein

Der Dateityp wird am Inhalt erkannt, nicht am Namen. Ein umbenanntes Archiv öffnet sich trotzdem.
Das Spiel erkennt `7z`, liest es aber noch nicht und lehnt es ab

> [!tip] Tipp
> Ein Archiv aus einem alten Build öffnet sich ohne Vorbereitung. Das Spiel wandelt es beim Import selbst in das aktuelle Format um

> [!warning] Warnung
> Standardmäßig bekommt ein importiertes Level eine neue ID. So überschreibt es kein Level, das schon auf diesem Gerät ist. Entferne dieses Häkchen nur, um ein Level wiederherzustellen, das früher auf diesem Gerät war

## Geschosse

Mehr zu allen Geschossgeneratoren - [[1_readability-and-fairness]]

> [!caution] Vorsicht
> Der `Collider` eines Geschossgenerators ist standardmäßig leer. Seine Geschosse zeichnen ein Quadrat und können dem Spieler nicht schaden, bis du einen Collider wählst, zum Beispiel dieselbe Form wie bei `Shape`. Die anderen Generatoren, die Formen platzieren, Geometrie und Audio-Wellenform, haben dasselbe Feld mit demselben Standard

### Geschosswelle

Eine Reihe von Geschossen, die sich zusammen bewegen.
Das Grundmuster, und mit ihm fängt man an. Seine Parameter wiederholen sich in den anderen Geschossgeneratoren

### Geschossspirale

Geschosse fliegen entlang eines rotierenden Strahls hinaus. Das Ergebnis ist die klassische Spiralwand

### Geschossregen

Geschosse fallen über eine festgelegte Zeit auf eine Fläche.
Dichte und Streuung sind einstellbar.
Wohin jedes Geschoss fällt, kommt aus dem `{{ui:editor_generators_seed}}` des Fensters, nicht aus dem Seed des Levels. Derselbe Seed wiederholt einen Lauf genau, und ein anderer Seed ergibt eine andere Verteilung. Der KI-Assistent übergibt seinen eigenen Seed, `0`, wenn er keinen anderen angibt, zwei Läufe, die sich unterscheiden sollen, brauchen also zwei Seeds

### Zielsuchende Geschosse

Geschosse biegen zu der Stelle ab, an der der Spieler erwartet wird.
Die Bahn wird vorab berechnet, nicht während des Spiels. Deshalb ist das Ergebnis auf jedem Gerät gleich

### Laserschwenk

Ein Strahl zieht über das Feld.
Die Warnung und die schädliche Phase sind verschiedene Objekte. So lässt sich die Warnung zeigen, und sie tötet nicht.
Der Warnstrahl kollidiert nie. Der feuernde Strahl schadet nur mit gewähltem `Collider`

## Geometrie

Mehr zu allen Geometriegeneratoren - [[2_reuse]]

### Polygon

Platziert Formen auf den Ecken oder Kanten eines regelmäßigen Polygons

### Radial

Platziert Kopien im Kreis. Die Grundlage der meisten symmetrischen Muster

### Spirale

Platziert Kopien entlang einer Spirale. Radius und Winkel wachsen zusammen

### Raster

Füllt ein Rechteck in gleichen Abständen mit Kopien einer Form

### Fraktal

Wiederholt eine Form in sich selbst, jedes Mal kleiner.
Die Anzahl der Objekte wächst exponentiell mit der Tiefe. Erhöhe die Tiefe Schritt für Schritt

## Audio und Effekte

### Audio-Wellenform

Baut Objekte aus der Form einer Audiospur. Das Level folgt sichtbar dem, was zu hören ist

Mehr - [[2_reuse]]

### Beat-Blitz

Setzt einen Blitz auf jeden Beat.
Die Beats kommen aus der Beat-Karte des Levels. Gibt es keine Karte, aus den Markern.
Es blitzt also genau das, was du auf dem Raster siehst

Mehr - [[2_rhythm-and-structure]]

## Ressourcen und Hilfsmittel

### Texturobjekte

Macht aus einem Bild Objekte, eines pro Zelle.
Das Bild wird zu Levelinhalt und wird wie alles andere animiert

Mehr - [[3_images-and-fonts]]

### Schriftcache

Sammelt jedes Zeichen, das die Texte des Levels verwenden, und backt sie vorab.
Dann wird kein Zeichen erst in dem Moment vorbereitet, in dem es zum ersten Mal erscheint

> [!tip] Empfehlung
> Führ ihn aus, wenn der Text fertig ist. Ein später hinzugefügtes Zeichen ohne neues Backen verursacht beim ersten Erscheinen ein Ruckeln

Mehr - [[3_images-and-fonts]]

### Kapazitätshinweis

Speichert die empfohlenen Grenzen des Levels: wie viele Objekte und Effekte es gleichzeitig braucht

> [!info] Gut zu wissen
> Auf das, was angezeigt wird, wirkt er sich nicht aus. Das Spiel reserviert für diese Grenzen vorab Puffer. Sonst würden die Puffer mitten im Level wachsen, und das würde ein Ruckeln verursachen

Mehr - [[1_level-budget]]
