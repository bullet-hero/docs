---
title: Lesbarkeit und Fairness
date: 2026-10-01
tags: [level_author]
---

# Lesbarkeit und Fairness

Der Spieler muss verstehen, woran er gestorben ist. Zeig eine Gefahr, bevor sie gefährlich wird, gib mindestens 12 Frames zum Reagieren und lass Gefahr stärker hervorstechen als Deko

Es gibt einen einzigen Test für Fairness: **Gibt der Spieler beim Sterben sich selbst die Schuld oder dem Level?**
Alles auf dieser Seite schiebt die Antwort in Richtung "sich selbst"

## Ankündigen

Eine Gefahr muss sichtbar sein, bevor sie gefährlich wird

Form und Collider sind zwei getrennte Felder desselben Objekts.
Eine Warnung ist deshalb einfach: Ein Strahl mit Form, aber ohne Collider leuchtet und trifft nicht. Eine halbe Sekunde später erscheint daneben ein zweiter, diesmal mit Collider

Umgekehrt geht es auch: Eine unsichtbare Wand ist ein Objekt ohne Form, aber mit echtem Collider

> [!caution] Vorsicht
> Eine unsichtbare Gefahr ist nur in einem Fall fair: Der Spieler weiß schon, dass sie da ist, weil das Level sie vorher gezeigt hat

## Reaktionszeit

Ein Mensch bemerkt eine Gefahr und reagiert im besten Fall in etwa 0.2-0.25 Sekunden.
Bei 60 Level-Frames pro Sekunde sind das 12-15 Frames

Eine Gefahr, die weniger als 12 Frames vor dem Kontakt erscheint (zum Beispiel 10), ist beim ersten Versuch nicht zu schaffen. Man kann sie nur auswendig lernen.
Wann das in Ordnung ist - [[3_difficulty-curve#Auswendiglernen]]

## Kontrast

Was gefährlich ist, muss sich stärker vom Hintergrund abheben als die Deko.
Der häufigste Fehler ist ein dunkles Geschoss auf dunklem Hintergrund, und zwar genau dann, wenn sich auch der Hintergrund ändert

> [!tip] Empfehlung
> Nimm sowohl die Farbe des Hintergrunds als auch die der Geschosse aus dem Theme. Dann hält eine einzige Änderung am Theme den Kontrast überall. Von Hand eingetippte Farben halten ihn nur bis zur ersten Änderung

## Eine Gefahr, ein Aussehen

Jede Art von Gefahr braucht ihr eigenes, wiedererkennbares Aussehen, und ihren eigenen Sound, wenn du Sound verwendest. Hat der Spieler einmal gelernt, dass so etwas trifft, muss alles, was genauso aussieht, auch treffen

Widersprich deinen eigenen Signalen nicht. Tötet an einer Stelle etwas, das wie Deko aussieht, vertraut der Spieler nichts mehr, was wie Deko aussieht

## Struktur schlägt Dichte

Ein Bildschirm voller Bewegung wirkt wie Rauschen, nicht wie Schwierigkeit.
Ein Spieler unterscheidet keine 40 Geschosse. Er unterscheidet eine Wand mit Loch, eine Welle, eine Spirale, einen Korridor

Acht Objekte mit Struktur sind schwerer und fairer als vierzig ohne

## Ein Level spielt sich immer gleich

Ein Level hat keine Bedingungen, Zähler oder Trigger, die auf den Spieler reagieren. Alles steht auf der Zeitleiste.
Auch der Zufall ändert sich nicht: Dieselbe Stelle liefert auf jedem Gerät dieselben Zahlen

Ein Level lässt sich deshalb nicht reaktiv machen. Es kann aber auch nicht versehentlich unfair werden, nur absichtlich

Zwischen zwei Durchläufen ändert sich nur, was der Spieler wählt: Leben, Wiedergabegeschwindigkeit und Checkpoints.
Mehr - [[3_difficulty-curve#Was der Spieler wählt]]

Weiter: [[3_difficulty-curve|Schwierigkeit und Kurve]], [[5_color-and-postprocessing|Farbe, Themes und Post-Processing]]
