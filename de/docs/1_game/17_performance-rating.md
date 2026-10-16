---
title: Leistungsbewertung
date: 2026-10-17
tags: [player, level_author]
---

# Leistungsbewertung

Schon vor dem Spielen zeigt das Spiel, wie schwer ein Level für dein Gerät ist, als Anzeige aus fünf Balken: Je mehr Balken leuchten, desto leichter das Level. Grüne Balken heißen, es läuft flüssig, gelbe heißen knapp, rote heißen, die Bildrate wird einbrechen

Der Wert ist eine Zahl, bei der `{{v:performance.score-limit}}` genau der Zeit entspricht, die ein Frame bei deiner Ziel-Bildrate dauern darf. Die Stufe ergibt sich aus dem Wert:

| Balken | Stufe | Wert |
|---|---|---|
| 5 | `{{ui:level_performance_holds}}` | unter `{{v:performance.score-warning}}` |
| 4 | `{{ui:level_performance_tight}}` | von `{{v:performance.score-warning}}` bis `{{v:performance.score-limit}}` |
| 3 | `{{ui:level_performance_drops}}` | über `{{v:performance.score-limit}}`, bis `{{v:performance.score-heavy}}` |
| 2 | `{{ui:level_performance_severe-drops}}` | über `{{v:performance.score-heavy}}`, bis `{{v:performance.score-severe}}` |
| 1 | `{{ui:level_performance_does-not-hold}}` | über `{{v:performance.score-severe}}` |
| keine | `{{ui:level_performance_unknown}}` | das Level oder das Gerät wurde noch nicht gemessen |

Der Wert ist eine Vorhersage für den schwersten Moment des Levels, nicht für seinen Durchschnitt. Ein Level, das drei Minuten leicht ist und eine Sekunde hängt, bekommt den Wert dieser Sekunde

## Wo du ihn siehst

- im Level-Browser: die Anzeige auf jeder Level-Karte und die Gruppe `{{ui:root_level-filters_performance}}` in den Filtern
- auf der Level-Seite im Menü: die Anzeige, die Stufe und der Wert
- im Level-Editor in den Metadaten des Levels: der Wert auf deinem Gerät und auf den Referenzgeräten, dazu die schwersten Stellen des Levels als Zeitmarken

## Zwei Hälften des Werts

**Die Hälfte des Levels** wird im Editor in den Sekunden nach jedem Speichern gemessen, während du weiterarbeitest, und in seinen Metadaten abgelegt. Verlässt du den Editor vorher, behält die Datei die vorige Messung. Sie beschreibt, was das Level verlangt: wie viele Objekte leben, wie viel vom Bildschirm sie bedecken, wie viele Effekte und Post-Processing-Durchläufe laufen. Ein Level, das vor dieser Funktion gespeichert wurde, hat keinen solchen Eintrag und erscheint als `{{ui:level_performance_unknown}}`, bis es erneut gespeichert wird. Der Editor misst es beim Öffnen und behält das Ergebnis, bis du den Editor verlässt, ohne es in die Datei zu schreiben

**Die Hälfte des Geräts** sagt, wie schnell dein Gerät jede dieser Aufgaben erledigt. Bis du dein Gerät misst, nutzt das Spiel ein Referenzgerät deiner Plattform. Deine Einstellungen zählen auch: Render-Skalierung, Kantenglättung, Effekte und Post-Processing ändern den Wert ohne neue Messung

## Dein Gerät messen

1. Öffne im Hauptmenü `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}`
2. Drück `{{ui:settings_graphics-performance_measure}}`. Ein Fenster sagt, was der Messung hilft: andere Apps und Spiele schließen, ein Handy oder einen Laptop ans Ladegerät anschließen, das Gerät nicht berühren
3. Drück `{{ui:settings_graphics-performance_start}}` und warte bis zu {{v:performance.benchmark-max-seconds}} Sekunden. Der Einstellungsbildschirm verschwindet, und das Spiel spielt Testlevel ab und zeigt in den oberen Ecken, was es misst. Wechsle nicht zu einer anderen App

`{{ui:settings_graphics-performance_stop}}` bricht die Messung vorzeitig ab. Eine abgebrochene oder zu lange Messung speichert nichts, und das vorherige Ergebnis bleibt

Danach zeigt das Fenster das Ergebnis: die Anzeige des Demo-Levels auf deinem Gerät, was dein Gerät begrenzt (der Prozessor oder der Grafikchip), welches `{{ui:settings_quick-setup_performance}}`-Preset es empfiehlt und wie viele deiner Level in jede Stufe fallen. `{{ui:settings_graphics-performance_again}}` misst noch einmal

War die Messung unruhig (das Gerät wurde zu heiß, eine andere App war beschäftigt), nutzt das Spiel sie trotzdem, weil sie näher an deinem Gerät liegt als jedes Referenzgerät, und das Fenster weist darauf hin. Schließ andere Apps und miss erneut, um einen genaueren Wert zu bekommen

## Wechsel auf ein anderes Gerät

Die Messung gehört dem Gerät, auf dem sie gemacht wurde. Die Profilübertragung ([[14_profile-transfer]]) und Cloud-Spielstände nehmen sie nicht mit, deshalb beginnt ein neues Gerät mit seinem Referenzgerät, bis du es erneut misst
