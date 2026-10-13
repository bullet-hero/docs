---
title: Objekteigenschaften
date: 2026-10-12
tags: [level_author]
---

# Objekteigenschaften

Der Objekt-Inspector bearbeitet die Felder des ausgewählten Objekts, der Keyframe-Inspector die ausgewählten Keyframes, auf allen Spuren, die die Auswahl berührt, gleichzeitig

## Objekt-Inspector

Zeigt die Felder des ausgewählten Objekts. Jeder Typ hat die gemeinsamen Felder eines leeren Objekts. Form, Effekt, Text und Prefab fügen darunter ihre eigenen hinzu

`{{ui:field_common_active}}` schaltet das Rendering *und* die Kollision ab. Kinder erben es. Ein hier ausgeblendetes Objekt kann den Spieler nicht töten

> [!caution] Vorsicht
> `{{ui:editor_inspector_layer}}` wird relativ zum Elternobjekt gesetzt, nicht absolut. Daneben steht die globale Ebene, nur lesbar. Sie ist die, die der Renderer verwendet: deine Ebene plus die Ebenen aller Vorfahren

> [!tip] Tipp
> Bearbeitest du ein Feld an einem Objekt aus einem Prefab, wird eine **Überschreibung der Instanz** gespeichert. Das Kästchen daneben zeigt die Überschreibung und setzt sie zurück

Die Eltern-Schaltfläche zeigt, woran das Objekt hängt, `{{ui:editor_inspector-parent_btn}}` eingeschlossen. Sie öffnet das Fenster `{{ui:editor_picker_select-parent}}`: jedes Objekt des Kontexts, mit festen Optionen oben:
- im Level - `{{ui:editor_inspector-parent_btn}}` und `{{ui:editor_search-option_camera}}`. `{{ui:editor_search-option_camera}}` ist die Kamera des Levels, und ihr Kind bewegt sich mit ihr
- in einer Prefab-Vorlage - eine Zeile `{{ui:editor_search-option_prefab-root}}`. Sie bedeutet sowohl "kein Elternobjekt" als auch die Wurzel der Vorlage: dort ist das dasselbe. Die Kamera und der Spieler können in einer Vorlage keine Elternobjekte sein

Ein reserviertes Elternobjekt wird mit seiner ID angezeigt: `Kamera (-1)`, `Lokaler Spieler (-2)`, `Prefab-Wurzel (-3)`. Der KI-Assistent kann nur die Kamera (-1) und, in einer Vorlage, die Wurzel (-3) verwenden

Die Schaltfläche daneben wählt das Elternobjekt aus. Bei einem Objekt auf der obersten Ebene einer Vorlage wählt sie die Wurzel der Vorlage aus. Sie ist nicht verfügbar, wenn mehrere Objekte ausgewählt sind und wenn es nichts auszuwählen gibt: kein Elternobjekt, oder das Elternobjekt ist die Kamera oder der Spieler

Ein Tab des rechten Bereichs, der nichts zu zeigen hat, wird ausgeblendet. Wird der offene Tab leer, wechselt der Bereich zum ersten Tab, der etwas hat. Sind alle Tabs leer, steht im Bereich `{{ui:editor_right-panel_placeholder}}`

Mehr: [[3_how-the-editor-thinks|Wie der Editor funktioniert]]

## Keyframe-Inspector

Zeigt die ausgewählten Keyframes. **Jede Spur, die die Auswahl berührt, ist gleichzeitig sichtbar**, nicht nur die zuletzt angeklickte.
Eine Auswahl kann Keyframes von Position und Drehung enthalten, Keyframes verschiedener Objekte und Objekt-, Audio- und Ereignis-Keyframes zusammen

> [!tip] Tipp
> Die Auswahl `{{ui:enum_search-domain_ease}}` wirkt auf alle Spuren gleichzeitig und braucht **einen Rückgängig-Schritt**. Eine Auswahl aus Position und Drehung ändert sich in einer Operation, nicht in zwei

> [!info] Gut zu wissen
> Das Feld `{{ui:editor_frame-key-view_key-frame}}` ist gesperrt, wenn mehrere Keyframes ausgewählt sind. Auf einer Spur ist ein Frame eindeutig. Eine Zahl für alle Keyframes würde sie zu einem zusammenfallen lassen und den Rest stillschweigend löschen. Um mehrere Keyframes gleichzeitig zu verschieben, zieh sie auf der Zeitleiste

Ein leerer Wert heißt, dass sich die ausgewählten Keyframes darin **unterscheiden**

Mehr: [[3_how-the-editor-thinks|Wie der Editor funktioniert]]

## Spanne

Legt fest, wann das Objekt existiert. Der Bereich ist halboffen: der Startframe gehört dazu, der Endframe nicht.
Ein Objekt, das bei 20 endet, und ein Objekt, das bei 20 beginnt, zeichnen nie beide auf diesem Frame

> [!info] Gut zu wissen
> **Die Spanne eines Kindes muss innerhalb der Spanne seines Elternobjekts liegen. Das wird beim Lesen aufgelöst und nie gespeichert.** Verkürzt du das Elternobjekt, werden die Kinder abgeschnitten, aber was hier steht, ändert sich nicht. Ziehst du es wieder auf, kehrt alles zurück. Ein Wurzelobjekt hinter dem Ende des Levels ist gültige Daten, es wird einfach nicht abgespielt

> [!info] Gut zu wissen
> **Anker** bedeuten "dieser Rand folgt dem Rand des Elternobjekts", und sie entscheiden, was abgespielt wird. Ein verankerter Rand sitzt auf dem Rand des Elternobjekts, ein verankertes Kind dehnt sich also mit einem wachsenden Elternobjekt mit. Seine Animation behält das gesetzte Timing

Die Länge einer Prefab-Platzierung kommt standardmäßig aus der Vorlage, lässt sich aber wie jede andere eintippen. Ein abweichender Wert speichert eine Überschreibung dieser Platzierung. Das Kästchen neben der Spanne zeigt sie und holt die Länge der Vorlage zurück

Die Wurzel einer Prefab-Vorlage hat keinen Spannenblock. An seiner Stelle steht eine Zeile `{{ui:editor_prefab-mode-frame_length}}`: die Länge der ganzen Vorlage, derselbe Wert wie `{{ui:editor_prefab-mode-frame_length}}` im Tab `{{ui:field_common_prefab}}`. `{{ui:field_common_active}}` und `{{ui:editor_inspector_layer}}` der Wurzel sind nur lesbar, und die Wurzel lässt sich weder löschen noch einem Elternobjekt unterordnen

Mehr: [[4_frames-and-time|Frames, Zeit und die Länge eines Levels]]

## Easing

Legt fest, wie der Wert vom vorigen Keyframe zu diesem gelangt

> [!info] Gut zu wissen
> Das Easing gehört zur **eingehenden** Seite eines Keyframes. Es legt die Strecke vom vorigen Keyframe zu diesem fest, und genau so liest es die Wiedergabe. Auf dem ersten Keyframe einer Spur hat das Easing deshalb keine Wirkung

> [!tip] Tipp
> Sind mehrere Keyframes ausgewählt, gilt die Wahl für alle gleichzeitig in **einem Rückgängig-Schritt**. Auch wenn die Keyframes auf verschiedenen Spuren liegen und zu verschiedenen Objekten gehören. Eine leere Wahl heißt, dass sich die ausgewählten Keyframes unterscheiden

Mehr: [[5_keyframes-and-easing]]

## Ebene

Legt die Zeichenreihenfolge **relativ zum Elternobjekt** fest, nicht absolut. Eine höhere resultierende Ebene zeichnet weiter vorn. Von zwei Formen auf derselben resultierenden Ebene zeichnet die neuere (die mit der höheren ID) dahinter

> [!caution] Vorsicht
> Der Renderer verwendet diese Zahl plus die Ebenen aller Vorfahren. Die Summe steht nur lesbar im Feld `{{ui:editor_inspector-global_layer}}` darunter. Dieselbe Ebene bedeutet unter verschiedenen Elternobjekten also Verschiedenes. Ein Wechsel des Elternobjekts ändert, wo das Objekt gezeichnet wird

> [!info] Gut zu wissen
> Die Ebene wirkt auch beim Zufall mit. Ein Zufallswert hängt an der resultierenden Ebene, ein Verschieben des Objekts in der Hierarchie ändert also die Zahlen, die es gewürfelt hat. Zwei Objekte mit derselben resultierenden Ebene UND demselben Startframe bekommen dieselben Zahlen

Mehr: [[3_how-the-editor-thinks|Wie der Editor funktioniert]]

## Form

Legt fest, was das Objekt **zeichnet**

> [!info] Gut zu wissen
> Eine Form ist echte Geometrie, kein Bild. Sie wird in ihren Rahmen eingepasst, und ihre lange Seite ist genau 1. Der Rahmen des Objekts ist also genau das, was auf dem Bildschirm zu sehen ist

> [!info] Gut zu wissen
> Das Spiel erzeugt rund 500 Formen entlang vier Achsen: Grundform, Sektor, Dicke und Umkehrung. Ein Level kann eigene hinzufügen. Ein leerer Wert ist gültig: ein Objekt ohne Bild, aber mit Hitbox ist eine unsichtbare Wand

Mehr: [[1_readability-and-fairness|Lesbarkeit und Fairness]]

## Collider

Legt fest, womit das Objekt **trifft**. Das ist eine eigene Wahl und hängt nicht davon ab, was das Objekt zeichnet

> [!info] Gut zu wissen
> Das eine wird absichtlich nicht aus dem anderen abgeleitet. Ein harmloser Warnstrahl, eine Hitbox, die einfacher als das Bild ist, und eine unsichtbare Wand sind gewöhnlicher Inhalt, keine Tricks

> [!tip] Tipp
> Beide Felder wählen aus denselben zwei Sammlungen. Eine Form, die das Level erstellt hat, funktioniert für beide

In den Anzeigemodi für Hitboxen zeichnet ein Objekt ohne Collider nichts, ebenso wenig ein inaktives Objekt. So unterscheidet sich Dekoration von Gefahr. Wie sie gezeichnet werden, legst du in [[14_editor-settings]] fest

Mehr: [[1_readability-and-fairness|Lesbarkeit und Fairness]]

## Shader-Typ

Legt fest, über welchen Pfad das Objekt gerendert wird

> [!caution] Vorsicht
> `{{ui:enum_shader-type_auto}}` entscheidet einmal, wenn das Level lädt. Die Regel ist streng: das Aussehen des Levels darf sich nicht ändern. Alles, was sich nicht als deckend beweisen lässt, wird transparent. Die Geometrie wird nicht betrachtet, nur Alpha

> [!tip] Tipp
> Das Label daneben zeigt, wozu `{{ui:enum_shader-type_auto}}` tatsächlich aufgelöst wurde. Es wird direkt aus den Renderdaten gelesen, nicht noch einmal berechnet. So kann das Label nicht von dem abweichen, was auf dem Bildschirm ist

Mehr: [[1_level-budget|Das Budget des Levels]]

## Aktuelle Werte

Zeigt, was die ausgewählten Objekte im aktuellen Frame **sind**, nicht was du in sie geschrieben hast. Jede Zahl wird aus der laufenden Simulation gelesen. Sie stimmt also mit dem überein, was im Viewport zu sehen ist

Das Quadrat am Ende einer Zeile ist der Keyframe-Zustand dieses Felds:
- blau - auf diesem Frame sitzt ein Keyframe. Ein Klick auf das Quadrat wählt ihn aus
- bernsteinfarben - der Frame liegt zwischen zwei Keyframes, der Wert wird interpoliert
- grau - die Spur hat Keyframes, aber der Frame liegt außerhalb davon. Der Wert wird gehalten
- hohl - die Spur ist leer, das Feld nimmt den Standardwert der Engine

Die Pfeile setzen den Abspielkopf auf den vorigen oder nächsten Keyframe dieser Spur

Eine UV-Zeile liest sich als zwei Paare: zuerst die Kachelung, dann der Versatz

Unter der Linie kommen die zusammengesetzten Werte: die summierte Ebene, die geerbte Aktivität und die Transformation mit berücksichtigten Elternobjekten. Kein Keyframe setzt sie, deshalb haben sie keine Anzeige

> [!info] Gut zu wissen
> Eine leere Keyframe-Spur ist gültige Daten, keine fehlenden Daten. Sie bedeutet, dass das Objekt für dieses Feld den Standardwert verwendet

> [!info] Gut zu wissen
> Im Prefab-Modus ist dieser Abschnitt ausgeblendet. Eine Vorlage spielt ihre eigenen Frames nicht ab, also gibt es auf einem Frame nichts zu zeigen
