---
title: Effekte
date: 2026-10-01
tags: [level_author]
---

# Effekte

Ein Effekt sind VFX-Graph-Partikel mit Parametern in Modulen: wie viele Partikel, woher sie kommen, wie sie sich bewegen, Farbe und Größe. Bearbeitet werden sie im Inspector oder im Effekteditor

## Effekt-Inspector

Zeigt die Parameter eines `VFX Graph`-Effekts in Gruppen: Konfiguration, Kern, Kräfte, Form, Winkel, Skalierung und Farbe. Alle Gruppen sind gleichzeitig sichtbar

> [!info] Gut zu wissen
> Effekte bekommen ihren **Seed genauso wie alles andere**: aus den Zahlen, die du bearbeitest, nicht aus dem Zustand eines Generators. Deshalb läuft das Level auf jedem Gerät identisch ab

> [!tip] Tipp
> Farben können statt eines festen Werts auf das Theme des Levels verweisen. Verlaufstypen öffnen den gemeinsamen Verlaufseditor

Mehr: [[1_level-budget|Das Budget des Levels]]

## Kern - wie viele Partikel und wie lange

Legt fest, wie viele Partikel existieren, wie lange sie leben und womit sie gezeichnet werden. Das ist alles, was vor der ersten Kraft gilt. Die andere Hälfte sind die [[6_effects#Kräfte - was ein Partikel bewegt|Kräfte]]

`Partikelanzahl` ist der wichtigste Kostenregler. Es ist genau die Zahl, die der Kapazitätshinweis des Levels zählt

Ein Emitter kostet ungefähr seine Anzahl mal seine Lebensdauer. `Lebensdauergrenzen` zu verdoppeln kostet so viel wie die Anzahl zu verdoppeln

`Form` ist die Silhouette jedes Partikels, aus demselben Satz, den gewöhnliche Objekte verwenden. `Textur` ist das Bild darauf. Beide Felder dürfen leer sein. Ein Partikel ohne Textur ist der günstige Normalfall

> [!warning] Warnung
> Die Anzahl ist auf 1024 begrenzt. Das ist die Kapazität des Graphen selbst. Ein VFX-Graph verarbeitet in jedem Frame seine ganze KAPAZITÄT, nicht nur die lebenden Partikel. Ein System kostet also so viel, wie es angefordert hat, auch wenn es weniger braucht

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt jedes Feld in einem Rückgängig-Schritt auf seinen Standard zurück

Mehr: [[1_level-budget|Was sich ein Level leisten kann]]

## Konfiguration - wann der Emitter verstummt

Legt fest, wann der Emitter aufhört, Partikel zu erzeugen. Ist das aus, erzeugt er sie, solange das Objekt lebt. Das ist der Normalfall: der Ausstoß endet zusammen mit dem Objekt

`Stopp-Frame` zählt ab dem Beginn der eigenen Spanne des OBJEKTS, nicht ab der Level-Zeitleiste. Ein Effekt am Ende eines Levels kann also dreihundert seiner eigenen Frames später verstummen

Schon lebende Partikel leben ihr Leben zu Ende. Der Ausstoß wird abgeschnitten, und das Bild blendet sanft aus

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt beide Felder in einem Rückgängig-Schritt auf ihre Standards zurück

Mehr: [[1_level-budget|Was sich ein Level leisten kann]]

## Winkel - Drehung der Partikel

Legt fest, wie ein Partikel über sein Leben gedreht wird. Es gibt fünf Varianten:
- `Wert` - ein fester Winkel
- die zwei `Kurven`-Varianten lesen eine Kurve
- die zwei `Zufällig`-Varianten ziehen für jedes Partikel einen Wert zwischen A und B

Welche Zeilen es gibt, hängt von der Wahl ab. Die zwei Kurvenvarianten unterscheiden sich darin, WONACH die Kurve gelesen wird:
- `Kurven über Lebensdauer` - nach der Lebensdauer des Partikels
- `Kurven nach Tempo` - nach der Geschwindigkeit des Partikels, über das Geschwindigkeitsfenster darunter

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt die ganze Gruppe auf ihre Standards zurück, `Typ` eingeschlossen. Die eingestellte Kurve oder das Zufallspaar geht verloren

Mehr: [[1_readability-and-fairness|Lesbarkeit]]

## Farbe - Farbe der Partikel

Legt fest, wie ein Partikel über sein Leben gefärbt wird. Sechs Varianten: dieselben fünf wie bei [[6_effects#Winkel - Drehung der Partikel|Winkel]] und [[6_effects#Skalierung - Größe der Partikel|Skalierung]], nur mit Verläufen statt Kurven, plus `Zufälliger Verlauf`:
- `Verlauf über Lebensdauer` liest den Verlauf nach der Lebensdauer des Partikels
- `Verlauf nach Tempo` liest ihn nach der Geschwindigkeit des Partikels
- `Zufälliger Verlauf` nimmt pro Partikel eine Farbe aus dem Verlauf, statt an ihm entlangzuwandern
- die zwei `Zufällig`-Varianten unten ziehen eine Farbe zwischen zwei Farben

> [!tip] Tipp
> Eine Farbe kann hier wie überall im Level ein Verweis auf das Theme sein. So folgt der Effekt einem Level, das unterwegs seine Palette wechselt

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt die ganze Gruppe auf ihre Standards zurück, `Typ` eingeschlossen. Der eingestellte Verlauf oder das Farbpaar geht verloren

Mehr: [[5_color-and-postprocessing|Farbe und Themes]]

## Skalierung - Größe der Partikel

Legt die Größe eines Partikels über sein Leben fest. Dieselben fünf Varianten wie bei [[6_effects#Winkel - Drehung der Partikel|Winkel]]: eine feste Größe, eine Kurve oder ein Bereich pro Partikel

Hier gibt es zwei Kurven, weil die Größe zwei Achsen hat. `Curve X` und `Curve Y` werden unabhängig gelesen. Ein Partikel kann sich gleichzeitig strecken und stauchen

> [!warning] Warnung
> Die Zeile unter den Kurven wird WIEDERVERWENDET. Bei `Wert` und den zwei `Zufällig`-Varianten ist sie die Größe selbst. Bei `Kurven nach Tempo` ist sie das Geschwindigkeitsfenster. Die Beschriftung daneben und ihre Hilfe sagen, was die Zeile gerade ist

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt die ganze Gruppe auf ihre Standards zurück, `Typ` eingeschlossen. Beide Kurven und das Zufallspaar gehen verloren

Mehr: [[1_readability-and-fairness|Lesbarkeit]]

## Form - woher die Partikel kommen

Legt das Spawnvolumen fest: ein Punkt, ein Ring, ein Rechteck, eine Strecke, ein Kegel oder ein Torus. Es entscheidet nur, wo ein Partikel STARTET. Was danach mit ihm passiert, sind die [[6_effects#Kräfte - was ein Partikel bewegt|Kräfte]]

Ein Wechsel von `Typ` ändert die Felder darunter. Die Zeilen werden wiederverwendet: die erste ist je nach Auswahl der Radius eines Kreises, der obere Radius eines Kegels oder der kleine Radius eines Torus

`Bogen` ist, wie viel vom Rand genutzt wird, in Radiant, gegen den Uhrzeigersinn ab der +X-Achse. Weniger als eine volle Umdrehung ergibt einen Fächer

> [!tip] Tipp
> `Öffnung` macht aus einem statischen Ring einen bewegten. Es entscheidet, wo auf dem Rand das nächste Partikel landet: zufällig, im Kreis in eine Richtung, hin und zurück oder entlang einer Sinuskurve. `Schleife` ist der klassische rotierende Emitter

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt die ganze Gruppe auf ihre Standards zurück, `Typ` eingeschlossen. Die eingestellte Form mit ihren Radien und ihrer Öffnung geht verloren

Mehr: [[4_composition-and-camera|Komposition]]

## Kräfte - was ein Partikel bewegt

Legt alles fest, was ein Partikel nach dem Spawnen bewegt. Die [[6_effects#Form - woher die Partikel kommen|Form]] entscheidet, wo es startet, und diese Gruppe, wohin es fliegt

Die Felder gibt es in zwei Arten. Sie zu verwechseln ist der übliche Fehler:
- die `Start`-Paare werden EINMAL gezogen, wenn ein Partikel entsteht, zwischen ihrem Minimum und Maximum. Zieh ein Paar auseinander, und ein gleichmäßiger Ausstoß wird zum Fächer
- alles andere wirkt FORTLAUFEND über das ganze Leben des Partikels

Felder der zweiten Art:
- `Lineare Geschwindigkeit` ist Wind, kein Stoß
- `Lineare Kraft` ist eine Beschleunigung, sie summiert sich also auf
- `Orbitalgeschwindigkeit` dreht Partikel um das Zentrum, nicht um sich selbst

> [!tip] Tipp
> `Bewegungstempo` multipliziert das ganze Ergebnis. So lässt sich ein fertiger Effekt verlangsamen oder beschleunigen, ohne die anderen Felder anzufassen

> [!info] Gut zu wissen
> Das **Zurücksetzen** neben dieser Schaltfläche setzt alle elf Felder in einem Rückgängig-Schritt auf ihre Standards zurück

Mehr: [[4_composition-and-camera|Komposition]]

## Effekteditor

Baut einen Partikeleffekt und zeigt ihn auf der Leinwand

> [!info] Gut zu wissen
> Die Parametergruppen sind dieselben wie im Effekt-Inspector. Hier werden sie als **Entwurf** bearbeitet: nichts erreicht das Level, bis du speicherst

> [!tip] Tipp
> Speichere den Effekt in der gemeinsamen Bibliothek des Geräts, um ihn in anderen Levels zu verwenden

Mehr: [[1_level-budget|Das Budget des Levels]]
