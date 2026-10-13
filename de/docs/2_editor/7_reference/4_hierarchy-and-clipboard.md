---
title: Hierarchie und Zwischenablage
date: 2026-10-02
tags: [level_author]
---

# Hierarchie und Zwischenablage

Die Hierarchie ist ein Baum der Objekte des aktuellen Frames nach Elternobjekt. Jede Zeitleiste hat ihren eigenen Puffer in der Zwischenablage, und die Befehlspalette findet jede Editoraktion per Name

## Hierarchie

Zeigt jedes Objekt, das im **aktuellen Frame** lebt, verschachtelt nach Elternobjekt

Ein Objekt ist hier nur sichtbar, solange der Abspielkopf in seiner Spanne steht. Die Liste ändert sich also, während du ziehst.
Eine leere Hierarchie heißt meist, dass der Abspielkopf hinter dem Ende des Inhalts steht

> [!info] Gut zu wissen
> **Ein Elternobjekt** gibt seine Transformation an seine Kinder weiter. Ebenen addieren sich entlang der Kette: die Zeichenreihenfolge eines Kindes ist seine eigene Ebene plus die Ebenen all seiner Vorfahren. Ein Wechsel des Elternobjekts verschiebt das Objekt also in der Zeichenreihenfolge. Er ändert auch seine Zufallswerte: der Zufall hängt an der resultierenden Ebene

> [!tip] Tipp
> Ein Rechtsklick auf eine Zeile öffnet ihre Aktionen. Auf einem Touchscreen öffnet Gedrückthalten dasselbe Menü

Gedrückthalten einer Zeile öffnet das Menü auch mit der Maus. Clips auf den Zeitleisten haben kein Menü per Gedrückthalten

Zieh eine Zeile auf eine andere, um das Objekt zu deren Kind zu machen. Lässt du es auf der leeren Fläche unter den Zeilen fallen, verliert es sein Elternobjekt. Ein Ablegen wird abgelehnt:
- auf das Objekt selbst oder auf das Elternobjekt, das es schon hat
- auf eines seiner eigenen Kinder
- wenn die Kette tiefer als 15 Stufen würde

Die Zeile `{{ui:editor_search-option_camera}}` ist unten an der Liste angeheftet. Eine darauf abgelegte Zeile macht das Objekt zum Kind der Kamera des Levels. In einer Prefab-Vorlage nimmt die Kamera keine Kinder an, die Wurzel der Vorlage aber schon

Mehr: [[3_how-the-editor-thinks|Wie der Editor funktioniert]]

## Mehrere Objekte auswählen

Ein Klick mit `Ctrl` fügt ein Objekt zur Auswahl hinzu oder entfernt es. Das funktioniert in der Hierarchie, auf den Zeitleisten und im Viewport gleich. `Ctrl` ist die einzige solche Taste: ein Klick mit `Shift` in der Hierarchie tut nichts, eine Bereichsauswahl gibt es nicht. Die Taste lässt sich neu belegen

Ein Klick mit `Ctrl` oder ein Rechteck, das mehr als ein Element erfasst, schaltet den **Mehrfachauswahlmodus** ein. Solange er an ist, hängt das, was ein einfacher Klick tut, von `{{ui:settings_game-editor-multi-select-requires_hold}}` ab - siehe [[14_editor-settings]]

Das Auswahlelement in der Werkzeugleiste zeigt `{{ui:editor_multi-select_status}}` oder `Ausgewählt (N)`. Es funktioniert, solange etwas ausgewählt ist:
- ein Druck hebt die ganze Auswahl auf
- ein Doppelklick oder ein Klick mit `Shift` schaltet stattdessen den Mehrfachauswahlmodus ein. Auf diese Weise eingeschaltet, ignoriert der Modus `{{ui:settings_game-editor-multi-select-requires_hold}}`, und jeder einfache Klick fügt hinzu. So baut ein Finger, der kein `Ctrl` hat, eine Auswahl auf

Dasselbe Element erscheint in Kontextmenüs, solange etwas ausgewählt ist. Dort hebt ein Druck die Auswahl auf

Der Modus schaltet sich von selbst aus, wenn nichts ausgewählt ist, und mit `Escape`, wenn gerade in kein Textfeld getippt wird

## Zwischenablage

Bringt eine Auswahl zwischen Levels und zwischen Geräten hin und her. Jede Zeitleiste hat ihren eigenen Puffer und ihre eigene Statuszeile

`{{ui:editor_clipboard-serialize_copy}}` schreibt alle Puffer als Text in die Zwischenablage des Systems.
`{{ui:editor_clipboard-deserialize_paste}}` liest den Text zurück in die Puffer - und **hört dort auf**

> [!info] Gut zu wissen
> Der Halt ist Absicht. Den Text lesen und einfügen sind zwei verschiedene Entscheidungen. Wo Inhalt eingefügt wird, hängt vom Abspielkopf und vom aktiven Kontext ab. Inhalt erscheint erst, wenn du ihn **in die Zeitleiste einfügst, die du gewählt hast**

Enthält die Zwischenablage des Systems fremden Text, meldet der Editor einen Fehler und stürzt nicht ab. Sie enthält, was du zuletzt irgendwo kopiert hast

Eine Aktion "alle Puffer auf einmal einfügen" gibt es nicht. Füge nach `{{ui:editor_clipboard-deserialize_paste}}` selbst in jede Zeitleiste ein

Eingefügte Keyframes landen am Abspielkopf. Für jeden Besitzer kommt sein frühester eingefügter Keyframe auf den Abspielkopf, gezählt innerhalb der Spanne dieses Besitzers. Ereignis-Keyframes verschieben sich um denselben Betrag, so bleiben eine Kamerafahrt und der Effekt, der dazugehörte, gleich weit auseinander

Ein Keyframe wird übersprungen, wenn er außerhalb der Zeitleiste seines Besitzers landen würde oder auf einem Frame, der auf seiner Spur schon belegt ist. Übersprungene Keyframes werden gezählt und in einer Meldung gemeldet

Ein erfolgreiches Kopieren oder Einfügen schreibt nichts in die Konsole. Gemeldet werden nur Probleme

Mehr: [[2_reuse|Wiederverwendung: Prefabs, Kopieren, Generatoren]]

## Befehlspalette

Findet jede Editoraktion per Name

Sie listet Befehle auf, keinen Inhalt. Es sind dieselben Aktionen, die die Werkzeugleiste und die Kontextmenüs ausführen

> [!tip] Tipp
> Die Inhaltssuche (`Ctrl+F`) ist ihr Zwilling. Sie durchsucht jedes Objekt des aktuellen Kontexts und jede Audiospur. Ressourcen sind nicht darin: jede wird über das Feld ausgewählt, das sie braucht

Mehr: [[3_speed-and-shortcuts|Tempo und Tastenkürzel]]
