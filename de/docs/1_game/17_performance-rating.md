---
title: Leistungsbewertung
date: 2026-10-15
tags: [player, level_author]
---

# Leistungsbewertung

Schon vor dem Spielen zeigt das Spiel, wie schwer ein Level für dein Gerät ist. Grün heißt, es läuft flüssig, Gelb heißt knapp, Rot heißt zu schwer, und die Bildrate wird einbrechen

Der Wert ist eine Zahl, bei der `{{v:performance.score-limit}}` genau der Zeit entspricht, die ein Frame bei deiner Ziel-Bildrate dauern darf. Die Stufe ergibt sich aus dem Wert:

| Stufe | Wert |
|---|---|
| `{{ui:level_performance_holds}}` | unter `{{v:performance.score-warning}}` |
| `{{ui:level_performance_tight}}` | von `{{v:performance.score-warning}}` bis `{{v:performance.score-limit}}` |
| `{{ui:level_performance_does-not-hold}}` | über `{{v:performance.score-limit}}` |
| `{{ui:level_performance_unknown}}` | das Level oder das Gerät wurde noch nicht gemessen |

Der Wert ist eine Vorhersage für den schwersten Moment des Levels, nicht für seinen Durchschnitt. Ein Level, das drei Minuten leicht ist und eine Sekunde hängt, bekommt den Wert dieser Sekunde

## Wo du ihn siehst

- im Level-Browser: ein farbiger Punkt auf jeder Level-Karte und die Gruppe `{{ui:root_level-filters_performance}}` in den Filtern
- auf der Level-Seite im Menü: die Stufe und der Wert
- im Level-Editor in den Metadaten des Levels: der Wert auf deinem Gerät und auf den Referenzgeräten, dazu die schwersten Stellen des Levels als Zeitmarken

## Zwei Hälften des Werts

**Die Hälfte des Levels** wird gemessen, wenn das Level im Editor gespeichert wird, und in seinen Metadaten abgelegt. Sie beschreibt, was das Level verlangt: wie viele Objekte leben, wie viel vom Bildschirm sie bedecken, wie viele Effekte und Post-Processing-Durchläufe laufen. Ein Level, das vor dieser Funktion gespeichert wurde, hat keinen solchen Eintrag und erscheint als `{{ui:level_performance_unknown}}`, bis es erneut gespeichert wird. Der Editor misst es beim Öffnen und behält das Ergebnis, bis du das Spiel schließt, ohne es in die Datei zu schreiben

**Die Hälfte des Geräts** sagt, wie schnell dein Gerät jede dieser Aufgaben erledigt. Bis du dein Gerät misst, nutzt das Spiel ein Referenzgerät deiner Plattform. Deine Einstellungen zählen auch: Render-Skalierung, Kantenglättung, Effekte und Post-Processing ändern den Wert ohne neue Messung

## Dein Gerät messen

1. Öffne im Hauptmenü `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}`
2. Drück `{{ui:settings_graphics-performance_measure}}`
3. Warte ein paar Minuten. Der Einstellungsbildschirm verschwindet, und das Spiel spielt Testlevel ab. Wechsle nicht zu einer anderen App

Danach zeigt der Abschnitt, was dein Gerät begrenzt (der Prozessor oder der Grafikchip), und welches `{{ui:settings_quick-setup_performance}}`-Preset er empfiehlt

War die Messung instabil (das Gerät wurde zu heiß, eine andere App war beschäftigt), ignoriert das Spiel sie und behält das Referenzgerät. Schließ andere Apps und miss erneut

## Wechsel auf ein anderes Gerät

Die Messung gehört dem Gerät, auf dem sie gemacht wurde. Die Profilübertragung ([[14_profile-transfer]]) und Cloud-Spielstände nehmen sie nicht mit, deshalb beginnt ein neues Gerät mit seinem Referenzgerät, bis du es erneut misst
