---
title: Komposition und Kamera
date: 2026-10-02
tags: [level_author]
---

# Komposition und Kamera

Halte Wichtiges vom Rand fern: Andere Bildschirme haben den Rand woanders, und eine Notch kann ein Geschoss verdecken. Kameraerschütterung taugt für einen Takt, schnelle Drehung und harter Zoom machen übel

## Jeder Bildschirm ist anders

Das Level entsteht auf einem 16:9-Monitor. Auf einem 20:9-Handy zeigt es mehr in der Breite und weniger in der Höhe, auf einem 4:3-Tablet umgekehrt.
Ein Objekt, das genau am Rand saß, landet entweder tief im Bild oder außerhalb davon

**Die Spur `{{ui:editor_events-timeline_track_screen-limit}}`** legt fest, wie der sichtbare Bereich begrenzt wird:
- gar nicht
- ein festes Seitenverhältnis
- ein Bereich von Seitenverhältnissen

Fest ist am berechenbarsten. Alle sehen genau das, was du gesehen hast, aber andere Bildschirme bekommen Balken an den Rändern.
Entscheide bewusst. "Gar nicht" ist auch eine Entscheidung, und sie bedeutet, dass du nicht weißt, was der Spieler sehen wird.
Ein neues leeres Level oder ein Level aus einer Audiodatei beginnt bereits mit einem Keyframe für festes 16:9 auf dem ersten Frame, außer du entfernst beim Erstellen den Haken bei `Pin Screen Aspect`

> [!caution] Vorsicht
> Die Oberfläche des Spiels weicht dem unsicheren Bereich des Bildschirms aus, der Levelinhalt nicht. Die Kamera rahmt das Level über den ganzen Bildschirm, deshalb kann eine Notch ein Geschoss verdecken. Halte wichtige Inhalte vom Rand fern

## Die Kamera ist ein Werkzeug

Die Kamera ist keine Kulisse. Sie hat Keyframe-Spuren: `{{ui:editor_dummy_text-15}}`, `{{ui:editor_dummy_text-16}}`, `{{ui:editor_dummy_text-17}}`, `{{ui:editor_dummy_text-18}}`, `{{ui:editor_dummy_text-19}}`

Eine Drehung um 15 Grad macht ein einfaches Muster schwer, ohne ein einziges neues Objekt.
Sie bricht jede Richtung, an die sich der Spieler gewöhnt hatte

Diese Macht wirkt auch gegen dich. Die Kamera kann ein Level unschaffbar machen, und du merkst es nicht, weil du weißt, wohin du schauen musst

> [!warning] Warnung
> Schnelle Drehung, ständige Erschütterung und harter Zoom machen ein Level körperlich unspielbar. Nicht wegen der Schwierigkeit, sondern weil es dem Spieler schlecht geht. Erschütterung taugt für einen Takt auf einem Drop und ist eine Minute lang unerträglich

## Ebenen

Die Zeichenreihenfolge ist relativ: Die Ebene eines Objekts wird mit den Ebenen aller seiner Elternobjekte addiert.
Ziehst du ein Objekt unter ein anderes Elternobjekt, ändert sich, was worüber gezeichnet wird. Selbst wenn die Ebenennummer nie angefasst wurde

Halte Deko und Gefahr in getrennten Ebenenbereichen. Dann verdeckt Deko nicht versehentlich ein Geschoss

## Lesbarkeit schlägt Schönheit

Ein Spieler, der ein Geschoss wegen der Deko nicht gesehen hat, ist dein Fehler, nicht seiner.
Wenn du wählen musst, streich die Deko

Weiter: [[2_mobile-devices|Mobile Geräte]], [[1_readability-and-fairness|Lesbarkeit und Fairness]]
