---
title: Bereiche
date: 2026-10-02
tags: [level_author]
---

# Bereiche

Hierarchie, Inspectors und Zeitleisten sind rund um den Viewport angedockt. Ein Klick auf den Griff am Rand eines Bereichs öffnet oder schließt ihn, Ziehen ändert seine Breite

## Drei Bereiche

Der Viewport sitzt in der Mitte, und drei Bereiche sind um ihn herum angedockt:
- der linke Bereich enthält die Hierarchie
- der rechte Bereich enthält die Inspectors
- der untere Bereich enthält die Zeitleisten

Ein Tab im rechten Bereich, der nichts anzuzeigen hat, ist ausgeblendet. Mehr - [[5_object-properties]]

## Griff des Bereichs

Jeder Bereich hat einen Griff an seinem Rand:
- ein Klick öffnet oder schließt den Bereich
- Ziehen ändert seine Größe. Eine Bewegung kann einen geschlossenen Bereich auf jede Breite herausziehen

Der Pfeil auf dem Griff zeigt den Zustand des Bereichs. Bei einem geschlossenen Bereich zeigt er in die eine Richtung, bei einem offenen ist er bei jeder Breite um eine halbe Drehung gewendet. Ein nur teilweise gedrehter Pfeil bedeutet, dass gerade gezogen wird

Ein Klick öffnet den Bereich mit einer Animation, die Tastenkürzel ebenso: `Ctrl+Left`, `Ctrl+Right` und `Ctrl+Down`. Mehr - [[3_speed-and-shortcuts]]

## Breite

Ein Bereich ist entweder geschlossen oder irgendwo zwischen seiner schmalsten und seiner breitesten Breite. Die schmalste Breite ist auch die gewöhnliche: so viel Platz braucht der Inhalt des Bereichs

| Bereich | Schmalste | Breiteste |
|---|---|---|
| links | 25 % des Bildschirms | 25 % des Bildschirms |
| rechts | 40 % des Bildschirms | 50 % des Bildschirms |
| unten | 35 % der Bildschirmhöhe | 70 % der Bildschirmhöhe |

Der linke Bereich öffnet und schließt sich nur. Der Rest des Editors ist an seiner Breite ausgerichtet

Lässt du ein Ziehen schmaler als die schmalste Breite los, geht der Bereich zu dem, was näher liegt: zur geschlossenen Position oder zur schmalsten Breite. Genau in der Mitte öffnet er sich. So schließt eine einzige Bewegung einen Bereich trotzdem

Ein Klick öffnet den Bereich in der Breite, in der du ihn zuletzt offen gelassen hast

> [!info] Gut zu wissen
> Eine gezogene Breite wird nicht gespeichert. Sie existiert nur in der aktuellen Sitzung, ein verbreiterter Bereich bleibt beim nächsten Mal also nicht breit

## Minimieren und von selbst öffnen

`{{ui:cmd_editor_toggle-minimize-panels}}` schließt alle offenen Bereiche und lässt nur den Viewport übrig. Erneutes Drücken öffnet die Bereiche, die offen waren. War keiner offen, öffnen sich alle drei

`{{ui:settings_game-editor_interface-auto-open-panel}}` (Einstellungen, Tab `{{ui:settings_game-editor_title}}`, `{{ui:settings_interface_label}}`) öffnet den rechten Bereich von selbst, wenn du etwas auswählst. Standardmäßig aus
