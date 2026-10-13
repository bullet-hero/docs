---
title: "Farbe, Themes und Post-Processing"
date: 2026-10-02
tags: [level_author]
---

# Farbe, Themes und Post-Processing

Leite die Farbe der Inhalte über einen Theme-Verweis, feste Farben nur für wirklich Einzigartiges. Schalte Post-Processing am Höhepunkt ein und wieder aus, sonst verlieren Geschosse ihre Kanten

## Theme-Verweise und feste Farben

Eine Farbe lässt sich auf zwei Arten festlegen:
- **eine feste Farbe** - ein Wert, der direkt im Objekt eingetragen ist
- **ein Theme-Verweis** - "nimm den und den Slot des aktiven Themes". Welches Theme aktiv ist, legt eine Keyframe-Spur fest

Der Unterschied zeigt sich beim zweiten Durchgang. Mit Verweisen ist eine neue Palette eine einzige Änderung am Theme. Mit festen Farben ist es eine Änderung an jedem Objekt

Auch der Hintergrund nimmt seine Farbe aus dem Theme. Wie Slots und Theme-Keyframes funktionieren - [[6_themes]]

> [!caution] Vorsicht
> Prüfe den Kontrast in jedem Theme, nicht nur in dem, in dem du gearbeitet hast. Ein Level, das am Drop das Theme wechselt, muss in beiden lesbar bleiben. Dunkle Geschosse, die auf einem hellen Theme perfekt lesbar sind, verschwinden auf einem dunklen

## Post-Processing

Das Standardset von URP plus zwei Glitch-Effekte. Alles liegt auf Keyframes, also lässt sich jeder Parameter animieren

> [!caution] Vorsicht
> Das ist der schnellste Weg zu einem Level, das niemand spielen kann. Bloom am Anschlag macht jedes helle Objekt zu einem Fleck, und ein Geschoss verliert seine Kante. Chromatische Aberration zieht Kanten auseinander. Ein Glitch, der länger als ein Takt dauert, ist Störung, kein Stil. Bloom hat keinen Schwellenwert: Jedes Pixel leuchtet, also wird ein dunkler Hintergrund mit steigender Intensität grauer

Drei Regeln halten Post-Processing auf der Seite des Stils:
- schalte einen Effekt am Höhepunkt ein und wieder aus, lass ihn nicht als Kulisse stehen
- schalte keinen Effekt ein, der die Lesbarkeit der Geschosse verschlechtert, wo diesen Geschossen ausgewichen werden muss
- musstest du nach dem Einschalten eines Effekts die Augen zusammenkneifen? Schalte ihn aus. Der Spieler kneift nicht die Augen zusammen, er hört auf

## Kantenglättung

Kantenglättung ist die Einstellung des Spielers, nicht deine.
Ein Level, das nur in einem Modus richtig aussieht, sieht nicht bei allen richtig aus

| Modus | Was er tut |
|---|---|
| `{{ui:enum_anti-aliasing-type_msaa}}` | der Standard. Glättet genau die Kanten der Geometrie, und jede Form ist echte Geometrie |
| `{{ui:enum_anti-aliasing-type_fxaa}}` | kostet einen Durchgang über den Bildschirm, egal wie oft das Level über sich selbst zeichnet |
| `TAA`, `STP` | nicht angeboten: Sie ziehen Schlieren hinter schnellen Objekten her, und Schlieren hinter einem Geschoss macht das Level schwerer lesbar |

Weiter: [[1_readability-and-fairness|Lesbarkeit und Fairness]], [[1_level-budget|Levelbudget]]
