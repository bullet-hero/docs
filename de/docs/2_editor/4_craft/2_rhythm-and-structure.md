---
title: Rhythmus und Struktur
date: 2026-10-02
tags: [level_author]
---

# Rhythmus und Struktur

Lege zuerst das Beat-Raster an: das Tempo, dann den Versatz, dann die Beats pro Takt. Setz den Höhepunkt des Levels auf den Höhepunkt des Songs und gönn dem Spieler in den Breaks eine Pause

Ein Rhythmusspiel beruht auf einem Gefühl: Der Spieler bewegt sich nicht zur Musik, er spielt sie

## Das Beat-Raster

Das Beat-Raster ist für dich, nicht für das Spiel. Die Wiedergabe liest es nicht.
Du platzierst damit Inhalte auf der Musik, und Generatoren arbeiten auf denselben Beats

Das Raster besteht aus Segmenten. **Ein Segment ist ein Abschnitt mit konstantem Tempo**, und es kann mehrere geben.
Zwischen den Segmenten darf es Lücken geben: ein Intro ohne Drums, ein Break, das Ende nach der letzten Note

Lege nur die Abschnitte an, die Inhalt tragen werden. Ein Intro braucht meistens nichts

## Das Tempo finden

1. Finde das Tempo
2. Dann den Versatz
3. Dann die Beats pro Takt

Du kennst das Tempo nicht? Tippe es im Fenster `{{ui:editor_beat-window_title}}` (`Shift+T`) zum Song mit.
Runde auf eine ganze Zahl und stimme den Rest mit dem Versatz fein ab

Ein Song ist fast immer in einem ganzzahligen Tempo geschrieben. Ein Wert mit Nachkommastellen bedeutet meistens, dass der Versatz falsch ist, nicht das Tempo

## Klang in Bewegung

**Verteile die Instrumente auf verschiedene Arten von Inhalt:**
- die Kick - unter das, was vom Spieler eine Aktion verlangt
- Nebenschläge - unter Bewegung, die keine Aktion verlangt
- lange Pads und Atmosphäre - unter den Hintergrund und die Kamera

Dann klingt das Level räumlich, statt mit allem gleichzeitig auf einen Beat zu schlagen

**Die Größe einer Bewegung trägt die Stärke eines Klangs.** Eine kleine Bewegung ist ein schwacher Schlag, eine große ein starker.
Ein großer Effekt auf einer schwachen Note wirkt wie ein Synchronisationsfehler, selbst wenn die Frames exakt stimmen

**Die Form einer Bewegung trägt die Betonung.** Eine scharfe Drehung betont eine starke Note, ein weicher Bogen eine schwache

**Im 4/4-Takt ordnen sich die Beats nach Gewicht als 1, 3, 2, 4.** Eine Aktion auf dem ersten Beat ist am intuitivsten.
Synkopen geben Groove. Häufige oder inkonsequente Synkopen sorgen aber dafür, dass der Spieler nicht mehr weiß, wo er ist

**Eine ungewöhnliche Taktart wird in Gruppen aufgeteilt, die der Spieler zählen kann.** Im 7/4-Takt sind Gruppen von 4+4+2+2+2 leichter zu verfolgen als 4+4+4+2

## Struktur

Abschnitte sind das, woran sich ein Spieler erinnert.
Ein Level ohne sie ist vier Minuten lang dasselbe, selbst wenn alle fünf Sekunden etwas Neues passiert

**Wiederholung lehrt.** Ein Muster, das zurückkehrt, wird schneller erkannt und gelernt. Zu viel davon langweilt aber, und ein etabliertes Muster ohne Grund zu brechen, wirkt wie Nachlässigkeit, nicht wie Abwechslung

> [!tip] Empfehlung
> Setze Marker auf die Struktur des Songs, bevor du das erste Objekt platzierst: Intro, Strophe, Refrain, Break, Drop, Outro. Sie erscheinen auf jeder Zeitleiste und kosten nichts

> [!caution] Vorsicht
> Der Höhepunkt des Levels muss auf dem Höhepunkt des Songs liegen, und Pausen sind Pflicht. Ein Break ist die Stelle, an der der Spieler durchatmet. Ein Level ohne Pausen erschöpft die Leute, bevor es schwierig wird

Auch das Ende will durchdacht sein: entweder ein letzter Höhepunkt oder ein ruhiges Ausklingen. Ein Level sollte nicht einfach abbrechen

## Warum Segmente und keine Keyframes

Das Beat-Raster ist eine Liste von Abschnitten, keine Spur aus Keyframes.
Eine Keyframe-Spur kann keine Abwesenheit ausdrücken: Ihr letzter Keyframe würde bis zum Ende des Levels reichen. Segmente brauchen aber Lücken zwischen sich

Weiter: [[4_frames-and-time|Frames, Zeit und die Länge eines Levels]], [[3_difficulty-curve|Schwierigkeit und Kurve]]
