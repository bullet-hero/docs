---
title: Damit keine Arbeit verloren geht
date: 2026-10-02
tags: [level_author]
---

# Damit keine Arbeit verloren geht

Deine Arbeit schützen Autospeichern, Rückgängig und eine Kopie des Levelordners. Nur die Kopie ist ein vollständiger Stand. Formatwechsel und Löschen lassen sich nicht rückgängig machen

Jede Sicherung deckt ab, was die anderen nicht abdecken. Autospeichern und Rückgängig ersetzen keine Kopie des Ordners, denn das ganze Level ist ein einziger Ordner

## Die Gewohnheit

> [!tip] Empfehlung
> `Ctrl+S` nach jedem fertigen Abschnitt. Eine Kopie des Levelordners vor jedem Umbau. Die Prüfung im Tab `{{ui:settings_level-settings_rules}}`, bevor du das Level als fertig betrachtest

## Autospeichern

Autospeichern ist standardmäßig an. Es funktioniert so:
1. Eine ungespeicherte Änderung entsteht - ein Countdown von `60` Sekunden beginnt
2. Das Spiel schreibt eine Kopie des Levels nach `backups/<level id>/` im Ordner des Spiels, außerhalb von `levels`
3. Dann speichert es das Level selbst, so wie `Ctrl+S` es tun würde

Ein Editor, der ohne Änderungen geöffnet wurde, schreibt nichts.
Alles, was seit dem letzten Speichern geändert wurde, von dir oder automatisch, existiert nur im Arbeitsspeicher

`25` Kopien werden aufbewahrt, die älteste wird zuerst gelöscht.
Eine Kopie enthält nur die Leveldatei, ohne Metadaten, Song oder Bilder. Sie übersteht das Löschen des Levels, außer du setzt den Haken bei `{{ui:root_level-delete_backups}}`.
Eine Kopie eines geschützten Levels ist mit dem eigenen Passwort dieses Levels verschlüsselt

Der Schalter, das Intervall und die Anzahl der Kopien werden unter `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` eingestellt

**Wiederherstellen:** Leveleinstellungen, Tab `{{ui:settings_level-settings_dangerous-zone}}`, `{{ui:level_backups_open}}`. Die Kopien gehen von der neuesten zur ältesten, jede nach dem Moment benannt, in dem sie entstand.
Die aktuelle Datei wird zuerst selbst nach `backups` kopiert, also lässt sich auch eine Wiederherstellung zurücknehmen

Du kannst auch von Hand wiederherstellen: Kopiere die Sicherung als `level.json` (oder `level.blob`) in den Levelordner

## Ungespeicherte Änderungen

Eine Aktion, die das offene Level ersetzen oder verlassen würde, fragt zuerst, was mit ungespeicherten Änderungen geschehen soll:
- ein anderes Level aus der Levelliste öffnen, auch ein Level kopieren und die Kopie öffnen
- ein Level erstellen
- `{{ui:settings_level-settings_quit}}` aus den Editoreinstellungen und aus den Leveleinstellungen
- `{{ui:level_backups_open}}`
- in `{{ui:settings_level-settings_dangerous-zone}}`: das Level kopieren und die Kopie öffnen, das Dateiformat ändern, ein Passwort setzen

Der Dialog hat drei Antworten:
- `{{ui:editor_save_text}}` - speichert das Level und setzt die Aktion fort
- `{{ui:editor_unsaved-changes_discard}}` - die rote Schaltfläche, die einzige Antwort, bei der Änderungen verloren gehen
- `{{ui:editor_cancel_text}}` - tut nichts

Auch Spielen aus den Leveleinstellungen fragt nach, aber mit zwei Antworten: `{{ui:editor_unsaved-changes_save-play}}` und `{{ui:editor_cancel_text}}`. Verwerfen geht hier nicht, denn bei der Rückkehr aus dem Spiel wird das Level erneut von der Festplatte gelesen.
Ist nichts ungespeichert, erscheint der Dialog nicht

## Was Rückgängig abdeckt

Rückgängig deckt Änderungen am Level ab, und nur diese. Jede Änderung an Objekten, Keyframes, Ressourcen, Themes, Prefabs und Einstellungen läuft durch einen einzigen Operationspuffer

Was das Level nicht ändert, wird nicht rückgängig gemacht:
- das gewählte Gizmo, das Zeitleisten-Werkzeug, ob Einrasten und Raster an sind
- die Anordnung der Bereiche, der offene Tab, die Position des Abspielkopfs
- die Zwischenablagen
- ein neu erzeugter Sitzungs-Seed. Neu laden des Levels wählt ihn erneut
- **das Speichern**. Rückgängig setzt das Level im Arbeitsspeicher zurück, nicht die Datei auf der Festplatte

## Was gar nicht rückgängig zu machen ist

Zwei Aktionen schreiben direkt auf die Festplatte:
- **Das Dateiformat des Levels ändern.** Wird das Level als `Blob` geschrieben, wird das vorherige `Json` gelöscht. Und ein `Blob` lässt sich nicht mit bloßem Auge lesen oder reparieren
- **Ein Level löschen.** Deshalb ist es in `{{ui:settings_level-settings_dangerous-zone}}` versteckt

## Der Tab Raw

Der Tab `{{ui:settings_level-settings_raw}}` zeigt die ganze gespeicherte Datei als Baum aus Feldern. Er prüft nichts: keine Regeln, keine Grenzen

Er ist der letzte Ausweg. Alle Änderungen einer Sitzung werden als eine Operation angewendet, und sie lässt sich rückgängig machen

> [!caution] Vorsicht
> Nichts hat geprüft, was du im Tab `{{ui:settings_level-settings_raw}}` geschrieben hast. Halte eine Kopie des Levelordners bereit. Mehr - [[4_level-folder-and-backups#Sicherungen und Wiederherstellung]]

## Regeln

Die Prüfung, die sich lohnt, ist der Tab `{{ui:settings_level-settings_rules}}`. Er zeigt, was die Validierung gefunden hat: kaputte Verweise, doppelte IDs, Zyklen von Elternobjekten, zu tief verschachtelte Prefabs, überlappende Beat-Segmente

Manche Befunde kann das Spiel beheben: einzeln oder alle auf einmal mit der Schaltfläche `{{ui:settings_level-settings_rules-fix-all}}`.
Die Korrekturen werden mit der Schaltfläche `{{ui:editor_save_text}}` übernommen, als eine Operation, die sich rückgängig machen lässt. `{{ui:settings_level-settings_raw-discard}}` verwirft sie.
Befunde im Graphen haben keine Korrektur

Die Spanne eines Kindes, die über die seines Elternobjekts hinausläuft, ist kein Fehler. Das sind normale Daten, und sie verhalten sich wie vorgesehen.
Um Lebensdauern einzupassen, führe den Modifikator `{{ui:mod_span_fit}}` aus

Weiter: [[4_level-folder-and-backups|Der Levelordner und Sicherungen]], [[1_order-of-work|Die Reihenfolge der Arbeit]]
