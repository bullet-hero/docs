---
title: "Wiederverwendung: Prefabs, Kopieren, Generatoren"
date: 2026-10-02
tags: [level_author]
---

# Wiederverwendung: Prefabs, Kopieren, Generatoren

Objekte, die du später alle auf einmal ändern musst, werden ein Prefab, egal wie viele es sind. Inhalt, der sich durch eine Regel beschreiben lässt, wird ein Generator. Sonst einfach kopieren

Ein Generator lohnt sich schon bei acht Objekten: Ein Generatorlauf ist eine einzige Operation zum Rückgängigmachen.
Acht von Hand platzierte Objekte sind acht Gelegenheiten, bei einem danebenzuliegen

## Kopieren

Für eine Form, die du ein paar Mal wiederholen musst und die nicht mehr mit dem Original verbunden sein soll

Es gibt fünf Zwischenablagen, eine pro Zeitleiste. Auf einer Zeitleiste kopierte Clips lassen sich auf einer anderen nicht über Keyframes einfügen

Kopieren und Einfügen werden unterschiedlich geleitet:
- **Einfügen** geht immer in die Zeitleiste, die du gerade ansiehst
- **Kopieren** nimmt das, was ausgewählt ist. Die offene Zeitleiste gewinnt, wenn sie eine eigene Auswahl hat. Sonst wird die Auswahl kopiert, wo auch immer sie ist, also wird ein Objekt, das bei offener lokaler Zeitleiste ausgewählt ist, trotzdem kopiert

Duplizieren (`Ctrl+D`) schreibt in keine Zwischenablage. Was du vorher kopiert hast, geht nicht verloren

Duplizieren und Einfügen behandeln das Elternobjekt unterschiedlich:
- **Ein Duplikat** behält das Elternobjekt. Die Kopie steht in der Hierarchie neben dem Original
- **Beim Einfügen** fällt das Elternobjekt weg, und die eingefügten Objekte landen ganz oben in der Hierarchie. Die Ausnahme ist ein Elternobjekt `{{ui:editor_search-option_camera}}` oder `{{ui:editor_search-option_local-player}}`: Im Levelbereich übersteht es das Einfügen

Beide suchen eine freie Ebene nur auf den Frames, auf denen das jeweilige kopierte Objekt landet. Ein Einfügen auf eine leere Strecke der Zeitleiste behält die Ebenen der Objekte bei

Der Name einer Kopie wird neu nummeriert. Ein Ende aus `_` und Ziffern ist die ID des Objekts, also wird `Shape_12` zu `Shape_` mit einer neuen ID. Ein Name ohne ein solches Ende bekommt keines, und ein Ende, das nicht nur aus Ziffern besteht (`Wave_2b`), bleibt, wie es ist. Audiospuren werden genauso umbenannt

Im Prefab-Modus kopierte Objekte werden wieder in die Vorlage eingefügt, nicht ins Level

> [!caution] Vorsicht
> Die Zwischenablagen werden geleert, wenn ein Level geladen wird. Alle IDs und Frames darin gehören zu dem Level, das offen war

## Prefabs

Für etwas, das du oft brauchst und überall auf einmal ändern willst

Ein Prefab ist eine Vorlage plus ihre Platzierungen. Gibst du einer Platzierung eine Vorlage, bekommt die Platzierung echte Kopien ihrer Objekte mit dauerhaften IDs. Die Leveldatei speichert nur die Platzierung selbst: die Vorlage, die IDs der Kopien und deine Überschreibungen. Die Kopien werden bei jedem Laden des Levels aus der Vorlage neu aufgebaut

Eine Änderung an der Vorlage überträgt sich auf jede Platzierung, die auf sie verweist.
Eine Änderung an einer Kopie in einer Platzierung (außerhalb der Vorlagenbearbeitung) wird als Überschreibung nur dieser Instanz gespeichert.
Überschreibungen überstehen spätere Änderungen an der Vorlage. Deshalb taugt ein Prefab auch für Varianten, nicht nur für Klone

Prefabs lassen sich ineinander verschachteln. Eine verschachtelte Vorlage lässt sich aus einer anderen heraus bearbeiten: Vorlagen öffnen sich übereinander und schließen sich in umgekehrter Reihenfolge

### Ein Prefab aus einer Auswahl

Wähle Objekte aus und drück `Ctrl+G` (`{{ui:cmd_editor_pack-prefab}}`). Dieselbe Aktion gibt es auch:
- in der Befehlspalette
- im Kontextmenü des Viewports, solange etwas ausgewählt ist
- im Menü einer Hierarchiezeile, als `{{ui:editor_context-menu_pack-prefab}}`
- in den Leveleinstellungen, Tab `{{ui:editor_library_kind-prefabs}}`, `{{ui:settings_level-settings_resources-prefabs-pack}}`

Die ausgewählten Objekte wandern in eine neue Vorlage, eine Platzierung davon nimmt ihren Platz ein, und diese Platzierung wird ausgewählt. Das ist eine einzige Operation zum Rückgängigmachen.
Ein einzelnes Objekt gibt der Vorlage ihren Namen. Mehrere Objekte ergeben eine Vorlage namens `Prefab`

Eine Platzierung und ein Objekt, das zu ihr gehört, lassen sich nicht noch einmal packen. Ihre Menüs bieten stattdessen `{{ui:editor_context-menu_open-prefab}}` an, und ihre Vorlage öffnet sich.
Im Prefab-Modus ist Packen nicht verfügbar

## Generatoren und Modifikatoren

**Generatoren** erzeugen Inhalt nach einer Regel: eine Spirale, ein Raster, ein Fraktal, eine Welle, einen Kugelregen, einen Fächer aus Strahlen. Du legst ein Frame-Fenster, eine Ebene und einen Seed fest und bekommst Objekte. Die Schätzung des Ergebnisses ist sichtbar, bevor du irgendetwas drückst

**Modifikatoren** arbeiten genauso, aber mit dem, was schon da ist: Sie passen Spannen ein, ziehen sie auseinander, quantisieren Keyframes, rechnen die Framerate um, löschen Inhalt in einem Fenster

## Zwischen Levels: die Gerätebibliotheken

Alles oben Beschriebene wirkt innerhalb eines Levels. Nur die Gerätebibliotheken und Sammlungen werden von Level zu Level mitgenommen

Themes, Effekte, Formen und Prefabs werden aus einem Level exportiert und in ein anderes importiert.
Die Bibliotheken liegen neben dem Levelordner, also trägt ein Level, das du verschickst, seine eigene Kopie

Eine Sammlung enthält Ressourcen jeder der sieben Arten, auch Texturen, Schriftarten und Audio, und reist als Archiv oder über den Steam Workshop. Mehr - [[16_library-and-collections]]

Weiter: [[3_speed-and-shortcuts|Tempo und Tastenkürzel]], [[4_level-folder-and-backups|Der Levelordner und Sicherungen]]
