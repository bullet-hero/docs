---
title: Editoreinstellungen
date: 2026-10-11
tags: [level_author]
---

# Editoreinstellungen

Autospeichern, Raster, Auswahl, Gizmos und Presets für neue Levels. Autospeichern ist standardmäßig an und greift {{v:editor.autosave-delay}} Sekunden nach einer Änderung

## Spieleditor

Hier werden Autospeichern, Kamera, Auswahl und Dateiformate eingestellt

| Einstellung | Was sie tut | Standard |
|---|---|---|
| `{{ui:settings_game-editor_autosave}}` | schaltet das Autospeichern ein | an |
| `{{ui:settings_game-editor_autosave-rate}}` | wie viele Sekunden von einer ungespeicherten Änderung bis zum automatischen Speichern vergehen | {{v:editor.autosave-delay}} |
| `{{ui:settings_game-editor_max-autosave-files}}` | wie viele Kopien aufbewahrt werden. Ist die Grenze erreicht, wird die älteste gelöscht | {{v:editor.autosave-copies}} |

Der Timer läuft nur, solange es ungespeicherte Änderungen gibt

Ein automatisches Speichern tut zwei Dinge:
1. Es schreibt eine Kopie des Levels nach `<game folder>/backups/<level id>/`
2. Es speichert das Level selbst, so wie `Ctrl+S`

Eine Kopie enthält nur die Leveldatei. Wiederherstellen lässt sie sich auf zwei Wegen:
- in den Leveleinstellungen: `{{ui:settings_level-settings_dangerous-zone}}` → `{{ui:level_backups_open}}`
- von Hand: sie in den Levelordner kopieren, unter dem Namen `level.json` (oder `level.blob`)

Mehr - [[4_not-losing-work#Autospeichern]]

`{{ui:settings_game-editor_camera-min-size}}` und `{{ui:settings_game-editor_camera-max-size}}` begrenzen, wie weit der Viewport des Editors hinein- und herauszoomen kann

`{{ui:settings_game-editor-multi-select-requires_hold}}` und `{{ui:settings_game-editor-pick-invisible_aabb}}` ändern, was ein Klick in den Viewport bedeutet.
Prüfe sie, wenn sich die Auswahl plötzlich anders verhält als gewohnt

`{{ui:settings_game-editor-level-serialize_mode}}` und `{{ui:settings_game-editor-resources-serialize_mode}}` legen das Standardformat für das Schreiben auf die Festplatte fest

`{{ui:settings_game-editor_publish-language}}` wählt die Sprache, in der Titel und Beschreibung eines Workshop-Eintrags zuerst veröffentlicht werden: `{{ui:enum_publish-language_english}}` (der Standard) oder `{{ui:enum_publish-language_system}}`, die Sprache des Geräts

Mehr - [[3_speed-and-shortcuts]]

## Raster

Das Raster des Viewports wird hinter dem Level gezeichnet und hilft dir beim Platzieren von Objekten

| Einstellung | Was sie tut | Standard |
|---|---|---|
| `{{ui:settings_game-editor_grid-active-default}}` | ob das Raster beim Öffnen des Editors an ist. Das ist nur der Anfangszustand | aus |
| `{{ui:settings_game-editor-grid_size}}` | die Seitenlänge einer Zelle in Welteinheiten | 1 |
| `{{ui:settings_game-editor-grid_opacity}}` | wie sichtbar die Linien sind, von 0 bis 1 | 0,25 |

Die Rasterschaltfläche in der Werkzeugleiste schaltet es ein und aus. Dieser Zustand wird zwischen Sitzungen nicht gespeichert

So sieht das Raster aus:
- Es hat keinen Rand. Die Zelle ändert sich beim Zoomen in Zehnerschritten, und das feinere Raster blendet sich allmählich ein
- Bräuchte eine Rasterstufe zu viele Linien, wird diese Stufe ausgeschaltet statt ausgedünnt
- Die Linienfarbe ist immer die Umkehrung des Kamerahintergrunds im aktuellen Frame, also bleibt das Raster sichtbar, wenn sich der Hintergrund ändert. Du stellst nur die Deckkraft ein

Mit eingeschaltetem Einrasten bleibt eine gezogene Position an einer halben Zelle hängen: an den Kreuzungen und an den Zellmitten. Dabei zählt das Raster, das du siehst. Mit ausgeschaltetem Raster rastet die Position in einem festen Schritt ein

## Auswahl

| Einstellung | Was sie tut | Standard |
|---|---|---|
| `{{ui:settings_game-editor-multi-select-requires_hold}}` | an: Im Mehrfachauswahlmodus fügt ein Klick nur hinzu, solange `Ctrl` gehalten wird, und ein einfacher Klick ersetzt die Auswahl. Aus: Solange der Modus an ist, fügt jeder Klick hinzu | an |
| `{{ui:settings_game-editor-preview-collider-on_select}}` | zeichnet die Hitbox jedes ausgewählten Objekts als durchscheinende Füllung | aus |
| `{{ui:settings_game-editor-pick-invisible_aabb}}` | ein Klick wählt ein Objekt über sein ganzes Rechteck aus, nicht über das, was es zeichnet | aus |
| `{{ui:settings_game-editor_selection-long-press-delay}}` | wie lange ein Halten dauert, bevor sich ein Menü öffnet, in Sekunden | 0,5 |
| `{{ui:settings_game-editor_selection-long-press-threshold}}` | wie weit sich der Cursor während des Haltens bewegen darf, bevor es zum Ziehen wird | 8 |
| `{{ui:settings_game-editor_selection-collider-opacity}}` | wie kräftig die Hitbox eines ausgewählten Objekts gezeichnet wird | 0,5 |
| `{{ui:settings_game-editor_selection-collider-opacity-view}}` | dasselbe für die Ansicht aller Hitboxen, schwächer, weil sich dort Hunderte davon überlagern | 0,25 |

Das Loslassen von `Ctrl` im Mehrfachauswahlmodus leert nichts und beendet den Modus nicht. Erst der nächste einfache Klick ersetzt die Auswahl. Mehr zum Modus - [[4_hierarchy-and-clipboard]]

Die Collider-Schaltfläche in der Werkzeugleiste zeigt die Hitboxen von allem im Bild, den Kreis des Spielers eingeschlossen. Dieser Zustand wird zwischen Sitzungen nicht gespeichert. Sind zu viele Hitboxen auf dem Bildschirm, schaltet sich die Ansicht mit einer Meldung selbst aus, statt nur einen Teil davon zu zeichnen

Ein Objekt ohne Collider zeichnet in keiner der beiden Ansichten eine Hitbox, ein inaktives Objekt ebenfalls nicht

Die Füllfarbe beider Ansichten ist `Einstellungen > Grafik > Nur-Collider-Modus > Füllfarbe`, geteilt mit dem Modus "Nur Collider" des Spiels ([[4_settings]]). Die beiden Deckkraftwerte oben bleiben eigene Einstellungen des Editors

## Gizmos

| Einstellung | Was sie tut | Standard |
|---|---|---|
| `{{ui:settings_game-editor_gizmos-scale}}` | wie groß die Ziehgriffe im Viewport sind, von 0,1 bis 10. Ein Griff in Mausgröße ist mit dem Finger schwer zu treffen | 1 |

Die Griffe behalten bei jedem Zoom dieselbe Größe auf dem Bildschirm

## KI-Agent

`{{ui:settings_game-editor_mcp_title}}` erlaubt einem KI-Client, der MCP spricht, das offene Level zu bearbeiten. Nur unter Windows, Linux und Mac: Smartphones und Tablets zeigen diesen Abschnitt nicht

| Einstellung | Was sie tut | Standard |
|---|---|---|
| `{{ui:settings_game-editor_mcp-enabled}}` | erlaubt einem Client die Verbindung. Nur dieser Computer kann sich verbinden, ein Client zur Zeit | aus |
| `{{ui:settings_game-editor_mcp-port}}` | der Port, auf dem der Editor lauscht. `0` wählt bei jedem Start einen freien, sonst von {{v:mcp.port-min}} bis {{v:mcp.port-max}}. Jede andere Zahl wird zurückgesetzt | 0 |
| `{{ui:settings_game-editor_mcp-follow-ai}}` | wohin der Abspielkopf geht, nachdem sich die KI einen Frame angesehen hat. Aus: zurück, wo du ihn gelassen hast. An: Er bleibt pausiert auf diesem Frame | an |
| `{{ui:settings_game-editor_mcp-reveal-edits}}` | wählt nach jeder Bearbeitung der KI aus und lokalisiert, was sie erstellt oder geändert hat. Nie, während du ziehst, tippst oder abspielst | an |
| `{{ui:settings_game-editor_mcp-operation-delay}}` | Sekunden, die der Editor zwischen zwei Operationen der KI wartet, von 0 bis {{v:mcp.operation-delay-max}}. `0` wendet jede sofort an. Abspielen, Pausieren und das Bewegen des Abspielkopfs werden nie verzögert, ebenso wenig alles, was die KI nur liest | {{v:mcp.operation-delay}} |

`{{ui:settings_game-editor_mcp-copy-config}}` kopiert die Konfiguration, die ein MCP-Client braucht, mit eingetragenem Pfad zum Server und zur Verbindungsdatei des Spiels

Die Zeile unter den Einstellungen sagt, was der Editor gerade tut: aus, lauscht auf einem Port, verbunden oder über das KI-Abzeichen im Editor gestoppt

Diese Einstellungen werden nur auf diesem Gerät gespeichert

Mehr - [[7_ai-assistant]]

## Ein Level erstellen

`{{ui:settings_editor-settings_level-presets}}` legen fest, womit ein neues Level beginnt: leer oder mit einem kleinen Grundgerüst.
Ohne Preset müsstest du dieses Gerüst jedes Mal von Hand bauen

> [!caution] Vorsicht
> `{{ui:settings_editor-settings_parameters}}` legen fest, was sich später nur umständlich ändern lässt: die Länge in Frames und die Framerate

> [!tip] Tipp
> Die Listen `{{ui:settings_editor-settings_quot-level-quot-file-format}}` und `{{ui:settings_editor-settings_quot-metadata-quot-file-format}}` wählen das Format, in dem das Level und seine Metadaten auf die Festplatte geschrieben werden. Beide lassen sich später in der `{{ui:settings_level-settings_dangerous-zone}}` des Levels ändern

Mehr - [[2_first-level]]

## Bibliothek

`{{ui:settings_editor-settings_library}}` ist der letzte Tab, nach `{{ui:settings_editor-settings_community}}`. Er enthält die Ressourcen, die du in mehreren Levels wiederverwendest: die Gerätebibliothek, deine eigenen Sammlungen und im Steam-Build die Sammlungen, die du im Steam Workshop abonniert hast

Die Spalte links wählt die Art: `{{ui:settings_level-settings_collections}}`, dann Prefabs, Themes, Formen und Effekte, dann Texturen, Schriftarten und Audio.
Hier erstellst und bearbeitest du Sammlungen, kopierst Einträge zwischen ihnen, importierst und exportierst sie und veröffentlichst im Steam-Build deine eigenen

Mehr - [[16_library-and-collections]]

## Fremde Werke verwenden

Jede externe Ressource in einem Level (Musik, Bilder, Schriftarten, Texte) muss eine von zwei Möglichkeiten erfüllen:
- eine Lizenz, die mindestens so frei ist wie `CC BY-NC`
- die eigene Erlaubnis des Rechteinhabers für eine öffentliche, nicht kommerzielle Verbreitung

> [!caution] Vorsicht
> Ein privates "klar, kein Problem" reicht nicht. Ein Level unter `CC BY-NC` wird öffentlich verbreitet. Die Erlaubnis muss genau das abdecken, nicht nur deine persönliche Nutzung

Ein Level, das auf deinem Gerät bleibt, wird nicht geprüft.
Die Regeln gelten in einem Moment: wenn das Level an einen Dienst übergeben wird

Die vollständigen Regeln, die Liste der akzeptierten Lizenzen, die Vorlage für eine Anfrage und wo man nach Ressourcen sucht:
- [[2_legal-resource-paths]]
- [[6_asking-permission]]
- [[3_where-to-get-resources]]
