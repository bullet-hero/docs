---
title: Modifikatoren
date: 2026-10-12
tags: [level_author]
---

# Modifikatoren

Ein Modifikator ändert Vorhandenes im Level: er entfernt Inhalt, rechnet fps um, löst Prefabs auf, quantisiert Keyframes, passt Spannen ein und verschiebt sie. Ein Schritt macht einen Lauf rückgängig

## Inhalt entfernen

Entfernt Levelinhalt, der den angegebenen Bedingungen entspricht

> [!caution] Vorsicht
> Der Modifikator ändert Vorhandenes, statt hinzuzufügen. Zurückholen lässt sich alles nur mit einem Rückgängig-Schritt. Lies die Parameter, bevor du ihn ausführst

Er arbeitet auf dem Frame-Fenster aus dem Generatorenfenster. Im umgekehrten Modus entfernt er stattdessen, was keinen Frame mit dem Fenster teilt. Im umgekehrten Modus oder mit eingeschaltetem `{{ui:editor_generators-whole_level}}` kann er weit mehr entfernen, als auf dem Bildschirm zu sehen ist, deshalb fragt er vorher nach einer Bestätigung

Mehr - [[2_reuse]]

## Framerate umrechnen

Rechnet jede Frame-Nummer auf eine andere Framerate um.
Die Timings bleiben auf denselben Sekunden

> [!warning] Warnung
> Frames sind ganze Zahlen. Alles, was nicht glatt aufgeht, wird gerundet. Nach zwei Umrechnungen kehrt das Level also womöglich nicht zum Original zurück

Das Formular zeigt die aktuelle Framerate des Levels zur Orientierung, nur lesbar. Jede echte Änderung der Framerate fragt vorher nach einer Bestätigung. Der Modifikator braucht das ganze Level, deshalb ist er im Prefab-Modus nicht verfügbar

Mehr - [[4_frames-and-time]]

## Prefabs auflösen

Macht jede Prefab-Platzierung in diesem Kontext zu gewöhnlichen Objekten.
Die Verbindung zur Vorlage ist weg. Die Objekte bleiben genau, wo sie waren

> [!info] Gut zu wissen
> Das Level sieht aus wie vor dem Lauf: nichts wird gelöscht oder verschoben. Änderungen an einzelnen Platzierungen stehen schon in den Objekten selbst und gehen nicht verloren. Die Vorlagen bleiben im Level, außer du lässt sie löschen

## Keyframes quantisieren

Zieht Keyframes auf einen regelmäßigen Schritt.
So landet ungleichmäßige Handanimation auf dem Beat

Arbeitet auf der Auswahl und läuft ohne sie nicht

Das Raster kommt aus der ersten Quelle, die zutrifft:
1. `Use Beat Grid` ist an (der Standard) und das Level hat ein Beat-Raster. Die Linien sind die Beats seiner Segmente, jeder Beat in `Division` Teile geteilt. Eine Prefab-Vorlage hat kein Beat-Raster
2. `Use Bpm` ist an (der Standard). Eine Linie auf jedem Beat von `Bpm` bei der Framerate des Levels, in `Division` Teile geteilt
3. `Use Bpm` ist aus. Eine Linie alle `Step Frames` Frames, ab Frame 1

Jede Linie wird aus ihrer exakten Zeit gesetzt und erst dann auf einen Frame gerundet. So bleibt das Raster auf dem Beat, auch wo ein Beat keine ganze Zahl von Frames ist: 167 BPM bei 60 fps sind 21,56 Frames pro Beat

`Offset Frames` verschiebt jede Linie, `Mode` schickt einen Keyframe zwischen zwei Linien zur näheren, früheren oder späteren, `Tracks` wählt, welche Spuren einrasten. Die Labels des Formulars sind die Parameternamen selbst und werden nicht übersetzt

> [!warning] Warnung
> Ein Keyframe, dessen Linie schon von einem anderen Keyframe derselben Spur belegt ist, bleibt, wo er war. Grobes Quantisieren lässt also manche Keyframes neben dem Raster, statt sie zusammenzulegen. Ein Keyframe wird auch nie vor den Start seines Objekts verschoben

Mehr - [[2_rhythm-and-structure]], das Beat-Raster - [[3_timelines#Beat-Raster]]

## Spannen einpassen

Legt die Lebenszeiten der Kinder in die Lebenszeit ihres Elternobjekts.
Zwei Wege: die Kinder verkürzen oder die Elternobjekte dehnen.
Anker ändern sich bei keinem von beiden

> [!info] Gut zu wissen
> Ein Kind, das über sein Elternobjekt hinausreicht, ist gültige Daten. Es wird einfach abgeschnitten abgespielt. Einpassen ist eine Entscheidung über den Inhalt, keine Fehlerbehebung, deshalb läuft es nie von selbst

Mehr - [[4_frames-and-time]]

## Staffeln

Verschiebt die Auswahl in der Zeit.
Objekte, die zusammen begonnen haben, erscheinen nacheinander

Arbeitet auf der Auswahl und läuft ohne sie nicht

Mehr - [[2_reuse]]
