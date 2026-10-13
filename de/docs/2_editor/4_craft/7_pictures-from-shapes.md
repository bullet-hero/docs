---
title: Bilder aus Formen
date: 2026-10-13
tags: [level_author]
---

# Bilder aus Formen

Bau ein Bild aus eingebauten Formen, eigene nur, wo keine passt. Leg Licht und Schatten über eine Grundform, mach Wiederholungen zu Prefabs und vergleiche mit dem Original über dem Level

## Zuerst eingebaute Formen

Eine eingebaute Form ist echte Geometrie mit sauberen Kanten, und sie wiederzuverwenden kostet nichts.
Kreis und Quadrat lassen sich auf jede Größe strecken: Ein gestrecktes, gedrehtes Quadrat ist jeder Balken, jede Linie und jeder Stab, ein gestreckter Kreis ist eine Ellipse

Zeichne eine eigene Form im Formeditor nur dort, wo keine eingebaute passt: ein Mantel, eine Hand, ein Segel.
Gib ihr nur ihre echten Ecken, mit geraden Kanten dazwischen. Ein Dutzend Ecken liest sich besser als hundert, die jedem Pixel nachgezogen sind

> [!tip] Empfehlung
> Details sind der Preis für saubere Kanten. Ein ausgefranster Umriss oder eine sichtbare Naht schadet einem Bild mehr als eine verlorene Kerbe

## Eine Grundform, Details obendrauf

Licht und Schatten sind eigene Formen, die auf einer Grundform liegen und an ihrem Rand beschnitten sind.
Zwei Formen, die sich nur Kante an Kante berühren, lassen dazwischen eine dünne Naht aus Hintergrund, und die sieht man

Ein Teil, den ein anderer verdeckt, läuft unter ihm weiter. Ein Hals reicht ein wenig unter den Mantel und den Kopf, ein Bein unter den Saum.
Dann treffen sich die Teile auch dann noch, wenn sich einer von ihnen bewegt

## Wiederholungen sind Prefabs

Alles, was mehr als einmal vorkommt, ist ein Prefab: ein Auge, ein Fenster, ein Blütenblatt.
Bau eines, mach es zum Prefab, platziere die übrigen und ändere an jeder Kopie nur, was abweicht: Position, Größe, Farben. Jede solche Änderung ist eine Überschreibung dieser Kopie

Eine Änderung an der Vorlage erreicht dann jede Kopie, und das Level bleibt klein

## Ebenen

Gib jedem Objekt seine eigene Ebene. Zwei Objekte auf derselben Ebene zur selben Zeit werden in einer Reihenfolge gezeichnet, die du nicht gewählt hast.
Halte die Grundform unter ihren Details und die Details unter dem, was darüber liegt

## Mit dem Original vergleichen

Importiere das Originalbild als Textur und leg es auf ein Rechteck genau in seiner Größe, über alles andere.
Zum Vergleichen schaltest du das Rechteck ein. Für die restliche Arbeit schaltest du es aus, statt es transparent zu machen: Ein ausgeschaltetes Objekt zeichnet überhaupt nichts

Prüfe das Bild als Ganzes, dann vergrößert, Teil für Teil: die Kanten, die Stellen, wo Teile aufeinandertreffen, die Schatten

Weiter: [[2_reuse]], [[4_composition-and-camera]]
