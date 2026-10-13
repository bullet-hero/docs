---
title: Levelbudget
date: 2026-10-01
tags: [level_author]
---

# Levelbudget

Ein Handy schafft bequem etwa 1000 Formen in einem Frame, ein schwacher PC 5000-10000. Overdraw kostet mehr als die Anzahl: Halbtransparentes über den ganzen Bildschirm, Ebene auf Ebene

## Wie viele Formen ein Gerät schafft

Es zählen **Formen**, die gleichzeitig in einem Frame leben. Die Zahlen sind ungefähr, aber die Größenordnung stimmt

| Gerät | Bequem | Grenze des Spielbaren |
|---|---|---|
| Handy | 1000 | 2000 |
| Schwacher PC | 5000-10000 | 20000-40000 |
| Durchschnittlicher PC (laut Steam-Umfrage) | 50000 | 100000 |

Teste auf dem schwächsten Gerät, das du erreichen kannst.
Auf deinem eigenen PC wird alles gut laufen, und das sagt nichts

## Text und Effekte

Auch Text und Effekte werden in Formen gezählt

**Text:** 2 bis 100 Formen pro Textobjekt. Die Kosten hängen von der Komplexität der Schriftart ab, von der Zahl der Zeichen, der Zahl der Stile und davon, ob der Text animiert ist

**Effekt:** 10 Formen für das Objekt selbst plus 0,1 Formen pro Partikel. Ein Effekt mit tausend Partikeln sind etwa 110 Formen

## Overdraw

**Teuer ist nicht die Anzahl, sondern der Overdraw.** Das ist, wenn derselbe Pixel immer wieder neu gemalt wird

Was daraus folgt:
- eine einzige halbtransparente Füllung über den ganzen Bildschirm kostet mehr als hundert Projektile
- Schichten halbtransparenter Dekoration übereinander sind das Teuerste, was du bauen kannst
- ruckelt das Level, such nach dem, was den ganzen Bildschirm bedeckt, statt Objekte zu zählen

> [!info] Gut zu wissen
> Auf einem durchschnittlichen Mobilchip verbringt eine Szene mit 1000 Objekten und 60- bis 70-facher Überlagerung 95-97 Prozent der GPU-Zeit mit dem Malen von Pixeln. Tausend kleine Formen über den ganzen Bildschirm sind billiger als zehn halbtransparente bildschirmfüllende Formen übereinander

## Deckend und halbtransparent

Eine Form hat die Wahl zwischen Zeichenwegen: `Auto`, `Opaque`, `Transparent`.
Der deckende Weg ist günstiger: die GPU verwirft verdeckte Pixel im Voraus

`Auto` entscheidet selbst, einmal beim Laden. Seine harte Bedingung ist, nie zu ändern, wie das Level aussieht.
Alles, was sich nicht als deckend beweisen lässt, wird halbtransparent

> [!warning] Warnung
> Stell den Weg nur von Hand ein, wenn du genau weißt, was du tust. Ein als deckend deklariertes Objekt, das nicht deckend ist, wird nicht schneller, sondern sieht falsch aus

## Kapazitätshinweis

Beim Speichern hält das Level fest, wie viele Objekte sein schwerster Frame gebraucht hat.
Das ist ein Hinweis für den Lader, keine Grenze. Ein Generator berechnet ihn neu

Weiter: [[2_mobile-devices|Mobile Geräte]], [[3_images-and-fonts|Bilder und Schriftarten]]
