---
title: Zeitleisten
date: 2026-10-02
tags: [level_author]
---

# Zeitleisten

Zeitleisten zeigen das Level über die Zeit: Objekte, die Keyframes des ausgewählten Objekts, die Vorlage eines Prefabs, Audio und Ereignisse. Das Beat-Raster hilft, alles davon auf die Musik zu legen

## Level-Zeitleiste

Zeigt alle Objekte des Levels über die Zeit. Jedes Objekt ist ein Clip. Die Zeile, in der ein Clip liegt, ist die **Ebene** des Objekts

Ein Clip ist eine halboffene **Spanne**. Ein Objekt auf den Frames 10-19 endet genau dort, wo ein Objekt beginnt, das bei Frame 20 startet. Die beiden zeichnen nie gleichzeitig auf einem gemeinsamen Frame

> [!info] Gut zu wissen
> Die Spanne eines Kindes muss innerhalb der Spanne seines Elternobjekts liegen. Das wird **beim Lesen aufgelöst und nie gespeichert**. Verkürzt du das Elternobjekt, werden die Kinder abgeschnitten, aber ihre Werte ändern sich nicht. Ziehst du es wieder auf, kehrt alles zurück. Ein Wurzelobjekt hinter dem Ende des Levels ist gültige Daten, es wird einfach nicht abgespielt

> [!tip] Tipp
> In der Schaltflächenleiste sitzen vier Werkzeuge: `{{ui:editor_timeline-tool-selection_tooltip}}` wählt aus und verschiebt, `Kanten` zieht an einem Rand, `Schere` schneidet den Clip unter dem Cursor, `Rechteckauswahl` fügt jeden Clip, den ein aufgezogenes Rechteck berührt, zur Auswahl hinzu. Das Menü öffnet sich per Rechtsklick auf eine *leere Stelle*. Ein Druck auf einen Clip beginnt das Ziehen

Eine Prefab-Platzierung und die Objekte, die sie mitbringt, werden in der Farbe des Prefabs gezeichnet

Wie die Werkzeuge eine Platzierung behandeln:
- Ihre Länge kommt standardmäßig aus der Vorlage. Eine abweichende Länge an einer Platzierung wird als Überschreibung nur dieser Platzierung gespeichert
- Ziehst du ihren Startrand mit `Kanten`, wandert die Stelle, ab der sie die Vorlage liest, mit. Das Bild darin bleibt also, wo es war
- `Schere` schneiden sie in zwei Platzierungen derselben Vorlage, und jede spielt ihren eigenen Teil. Die Vorlage selbst ändert sich nicht
- Die Objekte, die eine Platzierung mitgebracht hat, lassen sich nicht schneiden. Schneide die Platzierung selbst oder schneide diese Objekte im Prefab-Modus

Mehr: [[3_how-the-editor-thinks|Wie der Editor funktioniert]], [[4_composition-and-camera|Komposition und Kamera]]

## Lokale Zeitleiste

Zeigt die Keyframes des **ausgewählten Objekts**. Jede animierbare Eigenschaft hat ihre eigene Spur: Position, Drehung, Skalierung, Größe, Anker, Drehpunkt, Farbe, UV, Schriftgröße

Die Frames zählen hier **ab dem Beginn der Spanne des Objekts**. Verschiebst du das Objekt, wandert seine ganze Animation mit

> [!info] Gut zu wissen
> **Eine leere Spur ist gültige Daten**, keine Lücke. Eine Spur ohne Keyframes nimmt den Standardwert. Deshalb animiert ein neues Objekt nichts, bis du einen Keyframe setzt

Ein Wert wird nur zwischen benachbarten Keyframes übergeblendet. Die Spanne entscheidet, welche Frames existieren, aber nicht, wie die Werte übergehen

Bei einem Objekt aus einem Prefab wird eine Spur, die noch der Vorlage entspricht, in der Farbe des Prefabs gezeichnet. Füge auf ihr einen Keyframe hinzu, verschiebe oder bearbeite einen, und die Farbe verschwindet: die Spur enthält jetzt eine Überschreibung

Im Prefab-Modus ist diese Zeitleiste bei ausgewählter Wurzel der Vorlage so lang wie die ganze Vorlage

Mehr: [[3_how-the-editor-thinks|Wie der Editor funktioniert]]

## Prefab-Zeitleiste

Die eigene Zeitleiste des Prefab-Modus. Zeigt die Objekte der **Vorlage**

> [!info] Gut zu wissen
> Ihre Länge ist die eigene Länge der Vorlage, nicht die Spanne einer ihrer Platzierungen. Eine Vorlage wird wie ein kleines eigenständiges Level bearbeitet. Sie kann oft und zu verschiedenen Zeitpunkten platziert werden

Eine Zeile ist die **Wurzel** der Vorlage, und sie reicht über die Länge der ganzen Vorlage. Jedes andere Objekt der Vorlage hängt an ihr:
- die Wurzelzeile lässt sich auswählen. Der Inspector und die lokale Zeitleiste zeigen dann die Wurzel
- sie lässt sich nicht ziehen, dehnen oder schneiden
- sie klappt ein wie jedes Elternobjekt. Eine eingeklappte Wurzel blendet auf dieser Zeitleiste die ganze Vorlage aus

> [!warning] Warnung
> Die Auswahl wird nicht mit dem Rest des Editors geteilt. Es gibt keine Live-Vorschau einer bestimmten Platzierung. Änderungen betreffen die Vorlage und gehen auf jede Platzierung über, die auf sie verweist

Mehr: [[2_reuse|Wiederverwendung: Prefabs, Kopieren, Generatoren]]

## Audio-Zeitleiste

Zeigt die Audiospuren des Levels mit ihrer Wellenform. So lässt sich Inhalt leicht an dem ausrichten, was du hörst

> [!tip] Tipp
> `{{ui:editor_inspector-audio-span_fit}}` im Inspector passt die Spur an die echte Länge des Clips an. Die Schaltfläche ist nicht verfügbar, wenn es keinen Clip gibt oder die Geschwindigkeit 0 ist: eine eingefrorene Spur hat keine Länge
> `{{ui:editor_inspector-audio-span_fit-level}}` verlängert auch das Level, bis der ganze Clip hineinpasst. Beide Schaltflächen fragen vorher nach einer Bestätigung

> [!caution] Vorsicht
> Der Regler `{{ui:editor_inspector-audio_volume}}` im Inspector ist der Fader der Spur. Die per Keyframes gesetzte Lautstärke ist eine eigene Spur Volume auf der lokalen Zeitleiste. Beim Abspielen werden beide multipliziert

Mehr: [[2_preparing-the-track|Den Song vorbereiten]]

## Ereignis-Zeitleiste

Zeigt die Keyframes des Levels, die zu keinem Objekt gehören:
- Position, Drehung, Zoom, Drehpunkt und Erschütterung der Kamera
- Marker und Checkpoints
- die Bildschirmgrenze
- Hintergrund und Theme
- jeden Post-Processing-Effekt
- Sichtbarkeit, Steuerung, Kollision, Größe und Geschwindigkeit des Spielers

> [!info] Gut zu wissen
> Die Spur **Beat** ist hier die Ausnahme. Ihre Elemente haben eine Spanne, und sie ist die einzige Spur, auf die `Kanten` und `Schere` wirken

> [!tip] Tipp
> Eine Farbe kann statt eines festen Werts auf das Theme des Levels verweisen. Dann färbt eine Änderung des Themes alles, was darauf verweist, auf einmal um

Mehr: [[4_composition-and-camera|Komposition und Kamera]], [[6_themes]]

## Beat-Raster

Hilft, Inhalt auf die Musik zu legen. Generatoren arbeiten mit denselben Beats, die du siehst

Es sind Metadaten für das Erstellen, keine Mechanik. **Beim Abspielen wird das Raster nicht gelesen**

Das Raster ist eine Liste von **Segmenten**. Jedes hat ein konstantes Tempo: BPM, Phasenversatz, Beats pro Takt.
Segmente überlappen sich nicht. Die Lücken zwischen ihnen werden gebraucht: ein Intro ohne Schlagzeug, ein Break, das Ende nach dem Song. Eine einzige Tempospur könnte das nicht ausdrücken

> [!tip] Tipp
> `TAP` zeichnet Tippen am Abspielkopf auf. `{{ui:editor_beat-tap_commit}}` macht daraus ein Segment vom ersten bis zum letzten Tippen. Beats werden immer ab dem Beginn des Segments gezählt und summieren sich nicht auf, deshalb liegt der Fehler unter einem halben Frame

Mehr: [[2_rhythm-and-structure|Rhythmus und Struktur]]

## Beat-Segment

Ein Abschnitt mit konstantem Tempo: BPM, Phasenversatz in Bruchteilen von Frames, Beats pro Takt, ein Name und eine Farbe

Es wird genau ein Segment angezeigt, auch wenn mehrere ausgewählt sind. Jedes Feld außer dem Namen ist für ein Segment eindeutig. Sie gemeinsam zu bearbeiten, würde die Segmente ineinanderfallen lassen

> [!caution] Vorsicht
> Ein Segment wird über seinen Startframe erkannt. Deshalb **ändert ein Verschieben seine Identität**. Wähle das Segment nach dem Verschieben an seinem neuen Start erneut aus

> [!tip] Tipp
> Tippen richtet hier die Phase des ausgewählten Segments neu aus, statt ein neues zu erstellen. BPM und Versatz ändern sich in einem Rückgängig-Schritt

Mehr: [[2_rhythm-and-structure|Rhythmus und Struktur]]
