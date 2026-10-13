---
title: Themes
date: 2026-10-02
tags: [level_author]
---

# Themes

Ein Theme ist eine Palette aus 64 Farben, auf die Objekte per Slotnummer verweisen. Änderst du das Theme, ändert sich alles mit, was darauf verweist

Eine Farbe vom Typ `Theme` speichert keine eigene Farbe, nur eine Slotnummer.
Sie nimmt das, was dieser Slot in dem Theme enthält, das auf dem aktuellen Frame aktiv ist

Warum das besser ist als von Hand eingetippte Farben und wie ein Level mit jedem Theme lesbar bleibt - [[5_color-and-postprocessing]]

## Was ein Theme enthält

- **Einen Namen** - wird in Listen und Auswahlfenstern angezeigt
- **Eine ID**, `ThemeId`. Theme-Keyframes verweisen über sie auf ein Theme, nicht über den Namen
- **64 Farben** in einem Raster von 8 mal 8, jede mit Transparenz
- **Einen Slotnamen** für jeden Slot, optional. Solange du keinen einzigen Slot benannt hast, speichert die Datei `null` statt der Namensliste

Ein Theme sind Daten in `level.json`, keine eigene Datei im Levelordner (siehe [[1_level-needs]]).
Ein Level kann beliebig viele Themes enthalten

Das Spiel weist einem Slot keine Rolle zu: Das spieleigene Theme `Balanced` gruppiert seine 64 Farben einfach nach Farbton

## Wie eine Farbe ihren Wert findet

In zwei Schritten:
1. Die Spur `Theme` auf der Ereignis-Zeitleiste sagt, welches Theme auf diesem Frame aktiv ist
2. Eine Farbe vom Typ `Theme` nennt einen Slot von 0 bis 63 im aktiven Theme

Auf ein Theme verweisen können zum Beispiel die Farbe einer Form (jede ihrer Ecken einzeln), die Farbe eines Texts und der Hintergrund des Levels

**Die Position eines Slots ist seine Identität.** Verschiebst du eine Farbe in einen anderen Slot, wird alles umgefärbt, was auf den alten verwiesen hat

## Themes über die Zeit wechseln

Zwischen zwei Theme-Keyframes blendet das Spiel die ganze Palette weich von einem Theme ins andere.
Das Easing kommt vom späteren Keyframe (siehe [[5_keyframes-and-easing]])

Gibt es überhaupt keine Theme-Keyframes, ist jeder Slot weiß

> [!warning] Warnung
> Ein neuer Keyframe bekommt `Linear`, deshalb gleitet die Palette über die ganze Strecke vom vorigen Theme-Keyframe bis zu diesem. Damit das Theme genau auf dem Drop wechselt, stell den Keyframe am Drop auf `Constant`

> [!caution] Vorsicht
> Ein Theme-Keyframe kann das Theme selbst überleben. Löschst du ein Theme, auf das noch Keyframes verweisen, werden all diese Frames weiß. Die Keyframes selbst bleiben. Vor dem Löschen eines solchen Themes fragt der Editor noch einmal nach

## Ein Theme erstellen und bearbeiten

Der Tab `Themes` unter den Ressourcen des Levels zeigt die Themes des Levels. Er hat `{{ui:settings_level-settings_resources-themes-add}}` und `{{ui:settings_level-settings_resources-themes-import}}`.
Ein Klick auf eine Zeile öffnet den `{{ui:settings_level-settings_theme-editor}}`:
- `{{ui:field_common_name}}` des Themes
- `Theme Id` und `{{ui:settings_level-settings_theme-editor-regenerate-id}}`
- das Raster von 8 mal 8. Ein Klick auf eine Zelle wählt sie aus, zeigt `Color:` mit ihrer Nummer und lädt die Farbe in das Farbrad unter dem Raster
- `{{ui:editor_theme-editor_color-name}}` für die ausgewählte Zelle

Der Editor arbeitet auf einer Kopie. Bis du speicherst, gelangt nichts ins Level. Das Speichern selbst ist ein einziger Rückgängig-Schritt

## Einen Slot auswählen

Stell eine Farbe auf `Theme` um und öffne `{{ui:editor_select-theme_color}}`

Das Raster zeigt die Palette so, wie sie auf dem Frame des bearbeiteten Keyframes gemischt ist, nicht am Abspielkopf.
Daneben stehen die beiden Theme-Keyframes um diesen Frame herum und was der ausgewählte Slot in jedem davon enthält. Ein unbenannter Slot ist mit `{{ui:editor_search_unnamed}}` beschriftet

## Teilen und importieren

- **Die Gerätebibliothek.** `{{ui:editor_level-theme-item_export}}` in der Zeile eines Themes speichert es in `resources/themes` - die gemeinsame Bibliothek des Geräts, wobei `resources` neben `levels` liegt (siehe [[4_level-folder-and-backups]]). `{{ui:settings_level-settings_theme-library}}` zeigt sie an und markiert, was bereits `{{ui:editor_theme-library-item_in-level}}` ist. `{{ui:editor_library_delete}}` entfernt ein Theme aus der Bibliothek. Beim Importieren wird das Theme ins Level kopiert, das Level hängt also nie von deiner Bibliothek ab. `{{ui:settings_level-settings_theme-library}}` zeigt auch die Themes aus Sammlungen, mit Quell-Chips - [[16_library-and-collections]]
- **Die Themes des Spiels.** `{{ui:editor_search-title_theme}}` bietet neben den Themes des Levels die Themes an, die mit dem Spiel ausgeliefert werden

Weiter: [[5_color-and-postprocessing|Farbe, Themes und Post-Processing]], [[1_readability-and-fairness|Lesbarkeit und Fairness]]
