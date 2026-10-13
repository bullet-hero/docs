---
title: Wie der Editor funktioniert
date: 2026-10-12
tags: [level_author]
---

# Wie der Editor funktioniert

Objekt, Frame, Spanne, Ebene, Elternobjekt, Keyframe - die sechs Ideen, auf denen der ganze Editor ruht

Sind diese sechs Ideen klar, erschließt sich der Rest des Editors von selbst:

| Idee | Kurz gesagt |
|---|---|
| Objekt | eine Form (was du siehst) und ein Collider (was trifft), zwei getrennte Felder |
| Frame | eine Zelle der Zeit, kein Zeitpunkt |
| Spanne | die Lebenszeit eines Objekts: ein Start und eine Dauer, das Ende nicht eingeschlossen |
| Ebene | Zeichenreihenfolge, addiert mit den Ebenen aller Elternobjekte |
| Elternobjekt | gibt seine Transformation, seinen Aktivzustand und seine Lebenszeit an seine Kinder weiter |
| Keyframe | der Wert eines Felds in einem Frame, zwischen den Keyframes bewegt das Spiel den Wert selbst |

Ein unbekanntes Wort - [[1_glossary]]

## Objekt

Ein Objekt ist das, was gezeichnet wird, und das, was trifft. Das sind zwei verschiedene Felder: eine Form (was du siehst) und ein Collider (was trifft).
Ein Strahl, der leuchtet, dich aber nie berührt, ist ein Objekt mit Form und ohne Collider. Eine unsichtbare Wand ist es umgekehrt

## Frame und Spanne

Ein Frame ist eine Zelle der Zeit, kein Zeitpunkt. Frame 30 nimmt einen Abschnitt ein, keinen Punkt.
Die Zeitleiste zählt ab eins. Ein Level mit 900 Frames enthält die Frames 1 bis 900. Die Zahl 901 ist die Endgrenze, kein Frame

Eine Spanne ist die Lebenszeit eines Objekts: ein Start und eine Dauer. Das Ende gehört nicht zur Spanne.
Zwei Objekte, die direkt hintereinander liegen, überschneiden sich also nicht in einem gemeinsamen Frame

Mehr - [[4_frames-and-time]]

## Ebene und Elternobjekt

Eine Ebene ist die Zeichenreihenfolge. Sie ist relativ: die Ebene eines Objekts wird mit den Ebenen aller seiner Elternobjekte addiert

Eine höhere Ebene wird weiter vorne gezeichnet. Von zwei Formen auf derselben resultierenden Ebene wird die neuere (die mit der höheren ID) dahinter gezeichnet. Die Form, die oben liegen muss, bekommt also eine höhere Ebene

> [!caution] Vorsicht
> Ziehst du ein Objekt unter ein anderes Elternobjekt, ändert sich seine Zeichenreihenfolge, auch wenn du die Zahl nie angefasst hast

Ein Elternobjekt gibt seine Transformation, seinen Aktivzustand und seine Lebenszeit an seine Kinder weiter.
Die Spanne eines Kinds muss innerhalb der Spanne seines Elternobjekts liegen

Der Editor schneidet nie ab, was du eingetragen hast. Er behält deinen Wert und berechnet den wirksamen Wert getrennt davon.
Deshalb lässt sich das Verkleinern eines Elternobjekts rückgängig machen: zieh es wieder breiter, und das Kind ist zurück

## Keyframe

Ein Keyframe ist der Wert eines Felds in einem Frame. Zwischen zwei Keyframes bewegt das Spiel den Wert selbst.
Jedes Feld hat seinen eigenen Satz Keyframes: Position, Drehung, Skalierung, Größe, Anker und Drehpunkt

> [!info] Gut zu wissen
> Ein Feld ohne Keyframes ist nicht kaputt, es nimmt den Standardwert. Es gibt keinen Grund, der Ordnung halber alles mit Keyframes zu versehen

Was ein Keyframe speichert und wie der Wert zwischen den Keyframes wandert - [[5_keyframes-and-easing]]

## Koordinaten

Positionen, Größen und Abstände werden in Welteinheiten angegeben. Der Punkt (0, 0) ist die Bildschirmmitte, solange die Kamera keine eigenen Keyframes hat. X wächst nach rechts, y wächst nach oben

Der Zoom der Kamera ist die Höhe des sichtbaren Bereichs in Einheiten, standardmäßig {{v:camera.default-height}}. Ein 16:9-Bildschirm zeigt also x von etwa -{{v:camera.default-half-width}} bis {{v:camera.default-half-width}} und y von -{{v:camera.default-half-height}} bis {{v:camera.default-half-height}}. Ein breiterer oder schmalerer Bildschirm ändert nur die Breite

Ein Positions-Keyframe ist relativ zum Elternobjekt. Er ist der Versatz des Drehpunkts des Objekts vom Ankerpunkt des Elternobjekts und dreht und skaliert sich mit dem Elternobjekt mit. Ein Objekt ohne Elternobjekt wird in Weltkoordinaten platziert. Ein Kind der Kamera bewegt sich mit der Kamera

- **Drehpunkt** - der Punkt im eigenen Rahmen des Objekts, den die Position platziert und um den Drehung und Skalierung wirken. Standardmäßig `(0.5, 0.5)`, die Mitte
- **Anker** - der Punkt im Rahmen des Elternobjekts, von dem aus die Position zählt, von `(0, 0)` (unten links) bis `(1, 1)` (oben rechts). Standardmäßig die Mitte. Zwei verschiedene Anker strecken das Kind mit dem Elternobjekt mit

Die Drehung erfolgt gegen den Uhrzeigersinn. Die Datei speichert sie in Radiant, und der KI-Assistent schreibt ebenfalls Radiant. Der Inspector zeigt standardmäßig Grad an, die Editoreinstellung `{{ui:settings_game-editor_interface-rotation-unit}}` schaltet auf Radiant um

Weiter: [[4_frames-and-time]], [[5_keyframes-and-easing]], [[1_readability-and-fairness]]
