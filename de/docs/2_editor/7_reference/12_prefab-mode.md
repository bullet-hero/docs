---
title: Prefab-Modus
date: 2026-10-02
tags: [level_author]
---

# Prefab-Modus

Im Prefab-Modus bearbeitest du die Vorlage, und beim Speichern geht die Änderung an jede Platzierung. Hinein über "Prefab bearbeiten" im Inspector einer Platzierung, zurück zum Level mit Ctrl+Shift+E

## Prefab-Modus

> [!caution] Vorsicht
> Du bearbeitest die Vorlage, nicht eine einzelne Platzierung davon. Beim Speichern geht die Änderung an jede Platzierung, die auf diese Vorlage verweist

So funktioniert eine Platzierung:
- Sobald du eine Platzierung auf eine Vorlage zeigen lässt, bekommt sie echte Kopien ihrer Objekte mit dauerhaften IDs. Im Editor ist ein Kind eines Prefabs ein ganz gewöhnliches Objekt
- Die Leveldatei speichert nur die Platzierung: die Vorlage, die IDs der Kopien und die Überschreibungen. Die Kopien werden bei jedem Laden des Levels aus der Vorlage neu aufgebaut
- Eine Platzierung kann durch **Überschreibungen pro Instanz** von der Vorlage abweichen. Sie werden festgehalten, wenn du ein solches Objekt *außerhalb* des Prefab-Modus bearbeitest
- Bearbeitungen im Prefab-Modus halten keine Überschreibungen fest. Sie ändern die Vorlage selbst

> [!tip] Tipp
> Vorlagen öffnen sich übereinander. Eine Platzierung innerhalb einer Vorlage öffnet ihre eigene Vorlage, und `{{ui:editor_prefab-timeline_close}}` bringt dich zurück. Dieselbe Vorlage kann nicht zweimal gleichzeitig offen sein. Die Grenze der Verschachtelung liegt bei 8 Stufen

Mehr - [[2_reuse]]

## Betreten und Verlassen

Hinein geht es auf zwei Wegen:
- `{{ui:editor_inspector-prefab_edit}}` im Inspector einer Platzierung
- `{{ui:editor_level-prefab-item_edit}}` in der Zeile einer Vorlage in den Leveleinstellungen, Tab `Prefabs`. Das braucht keine Platzierung, öffnet also auch eine Vorlage, die nirgends platziert ist oder nur innerhalb einer anderen Vorlage

`{{ui:editor_context-menu_open-prefab}}` im Kontextmenü und in der Befehlspalette tut dasselbe für eine ausgewählte Platzierung oder für ein Objekt, das eine Platzierung mitgebracht hat. Das passende Objekt innerhalb der Vorlage wird sofort ausgewählt

Hinaus geht es auf zwei Wegen:
- `{{ui:editor_prefab-timeline_close}}` auf der Prefab-Zeitleiste verlässt eine Stufe, zurück zu der Vorlage, die diese geöffnet hat
- der Status in der Hauptwerkzeugleiste (`Bearbeitung '...'`) und `Ctrl+Shift+E` verlassen alle offenen Vorlagen auf einmal, zurück zum Level

Die Auswahl wird bei jedem Betreten und Verlassen geleert. Beim Zurückgehen um eine Stufe kommt wieder, was in dieser Vorlage ausgewählt war

Innerhalb einer Vorlage funktioniert das Auswählen wie im Level: Klick, `Ctrl`-Klick, Rechteck, Löschen, Kopieren und Einklappen. Ein Klick in den Viewport wählt dort nichts aus: Der Viewport zeigt weiter das Level, und eine Vorlage hat darin keine Live-Vorschau

## Innerhalb einer Vorlage

Jedes Objekt einer Vorlage hängt an ihrer **Wurzel**. Die Wurzel:
- umfasst die ganze Vorlage. Ihre Länge ist `{{ui:editor_prefab-mode-frame_length}}`, dieselbe Zahl im Inspector der Wurzel und im Tab `Prefab`
- kann nicht gelöscht werden und kein Elternobjekt bekommen
- hat schreibgeschützte Felder `{{ui:field_common_active}}` und `{{ui:editor_inspector_layer}}`. Diese gehören jeder Platzierung selbst

Ein neues Objekt kommt unter das ausgewählte Objekt, wenn genau eines ausgewählt ist, die Wurzel eingeschlossen. Sonst kommt es auf die oberste Stufe der Vorlage, unter die Wurzel.
Es umfasst sein Elternobjekt und ist an beiden Enden verankert. Auf der obersten Stufe ist das die ganze Vorlage

Generatoren, die das ganze Level brauchen, sind hier nicht verfügbar. Ein Prefab aus einer Auswahl erstellen und eine Platzierung auflösen wird innerhalb einer Vorlage ebenfalls abgelehnt

## Prefab aus einer Auswahl erstellen

Macht aus den ausgewählten Objekten eine neue Vorlage und setzt eine Platzierung davon an ihre Stelle. Danach sieht das Level gleich aus und spielt sich gleich

Wo es zu finden ist:
- `{{ui:editor_context-menu_pack-prefab}}` im Menü einer Hierarchiezeile
- das Kontextmenü des Viewports
- `{{ui:cmd_editor_pack-prefab}}` in der Befehlspalette, `Ctrl+G`
- `{{ui:settings_level-settings_resources-prefabs-pack}}` in den Leveleinstellungen, Tab `Prefabs`

Es fragt nicht nach und ist ein Rückgängig-Schritt. Die neue Platzierung ist danach ausgewählt.
Ein Objekt gibt der Vorlage seinen eigenen Namen. Mehrere Objekte ergeben eine Vorlage namens `Prefab`. Umbenennen kannst du sie in den Leveleinstellungen, Tab `Prefabs`

Was abgelehnt wird:
- eine Platzierung oder ein Objekt, das eine Platzierung mitgebracht hat. Die Menüs bieten dafür stattdessen `{{ui:editor_context-menu_open-prefab}}` an
- eine Auswahl, die tiefer als 15 Stufen verschachtelt wäre. Nichts wird geschrieben, und die Meldung sagt das

## Platzierung auflösen

Löst eine Platzierung von ihrer Vorlage: Ihre Objekte werden gewöhnliche Levelobjekte und bleiben genau dort, wo sie sind

Wo es zu finden ist: `{{ui:editor_inspector-prefab_flatten}}` im Inspector der Platzierung, im Menü einer Hierarchiezeile und in der Befehlspalette

Es fragt immer vorher nach. Das Level sieht danach gleich aus, also würde ein versehentliches Auflösen sonst erst viel später auffallen, wenn eine Bearbeitung der Vorlage die Platzierung nicht mehr erreicht. Mehrere ausgewählte Platzierungen ergeben eine Bestätigung und einen Rückgängig-Schritt

Ein Objekt, das eine Platzierung mitgebracht hat, lässt sich nicht allein auflösen. Löse die Platzierung auf, zu der es gehört

## Verschachtelte Prefabs ebenfalls auflösen

Entscheidet, was mit den Prefabs innerhalb des aufgelösten passiert

**Aus** - nur die Platzierung, auf die du gezeigt hast, folgt ihrer Vorlage nicht mehr.
Ein darin platziertes Prefab bleibt eine Platzierung und behält seine Verbindung. Eine Bearbeitung dieser inneren Vorlage erreicht das Level weiterhin.
Das ist der Standard: Genau das meint "dieses Prefab entpacken" meistens. Der Schalter ist bei jedem Öffnen der Bestätigung aus

**An** - alles Verschachtelte wird ebenfalls aufgelöst.
Nach einem Druck ist nichts im Level mehr mit diesen inneren Vorlagen verbunden, in keiner Tiefe

In beiden Fällen bleiben die Vorlagen selbst im Level. Das ganze Auflösen ist ein Rückgängig-Schritt
