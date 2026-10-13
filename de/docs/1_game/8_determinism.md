---
title: Determinismus
date: 2026-10-02
tags: [advanced_player]
---

# Determinismus

Ein Level mit demselben Seed läuft auf jedem Gerät und bei jeder Framerate gleich. Sein Zufall wird aus dem Seed berechnet, und deine Aktionen beeinflussen das Level nicht

## Ein Level ist eine Funktion der Zeit

Ein Level ist auf einer Zeitleiste aufgebaut. Jedes Objekt lebt in einer Spanne von Frames und bewegt sich entlang von Keyframes

Das Level liest deine Aktionen nicht. Deshalb sieht Frame 1200 gleich aus, ob du lebst, tot bist, gerade dashst oder ein Bot für dich spielt

Der Einfluss geht nur in eine Richtung. Ein Level kann die Größe des Avatars ändern, ihn verlangsamen, ihm die Steuerung nehmen oder Kollisionen ausschalten. Einen Rückkanal vom Avatar zum Level gibt es nicht

Trigger gibt es nicht. Sie werden für künftige Versionen diskutiert, aber entschieden ist nichts

Ein Level läuft in Echtzeit. Die Framerate legt nur fest, wie oft der Bildschirm neu gezeichnet wird.
Derselbe Durchlauf läuft bei 30 und bei 144 Frames pro Sekunde gleich

## Der Seed

Der Seed wird von der ersten Stelle genommen, an der er gesetzt ist:

1. `{{ui:level_level-view_seed-value}}` auf dem Levelbildschirm (`{{ui:level_level-view_seed-randomize}}` wählt einen neuen, `{{ui:level_level-view_seed-clear}}` entfernt ihn)
2. der eigene Seed des Levels, vom Autor gesetzt
3. ein neuer Seed für diesen Durchlauf

`0` bedeutet "nicht gesetzt". Ein gewöhnliches Level nimmt also bei jedem Laden einen neuen Seed

Das Ergebnisfenster zeigt den Seed des Durchlaufs, und der Rekord speichert ihn. So lässt sich ein glücklicher Durchlauf wiederholen

## Wie der Zufall funktioniert

Ein Zufallswert in einem Level kommt nicht aus einem Generator, der sich seinen Zustand merkt. Er wird aus seiner Adresse berechnet:

`Hash(seed, keyframe frame, layer, start frame, track, channel)`

Dieselbe Adresse ergibt immer dieselbe Zahl. Auf jedem Gerät und in jeder Rechenreihenfolge.
Jeder Teil der Adresse ist etwas, das der Autor bearbeitet. Deshalb wiederholt derselbe Aufbau denselben Durchlauf

## Was das bringt

- **Der Warm-Bot** plant vor dem Start eine Route durch das ganze Level. Das geht, weil genau das Level läuft, für das er geplant hat
- **Der Reflex-Bot** baut Frames vor dem aktuellen und weicht nach ihnen aus
- **Das Zurückspulen zu einem Checkpoint** baut den nötigen Frame neu, statt etwas rückgängig zu machen
- **Der Editor** baut jeden Frame von Grund auf, deshalb ist das Ziehen über die Zeitleiste sofort
- **Rekorde und Statistik** bedeuten auf jedem Gerät dasselbe

## Bekannte Grenzen

Die Seite des Levels ist deterministisch. Die Seite des Avatars hat bekannte Mängel, die noch nicht behoben sind:

- zwei Hindernisse treffen den Avatar im selben Frame. Welches davon die Richtung des Rückstoßes bestimmt, kann sich zwischen Durchläufen unterscheiden
- die Uhr des Avatars wird beim Start des Levels nicht zurückgesetzt. Ein Dash kann einen Frame länger oder kürzer dauern, je nachdem, wie lange das Level zum Laden gebraucht hat

Dieselben Bot-Durchläufe auf einem Build stimmten bei der Messung bis zur letzten Stelle überein. Diese Mängel greifen also nicht in jedem Level.
Ihretwegen ist ein Durchlauf in der Praxis reproduzierbar, aber nicht garantiert
