---
title: Level spielen
date: 2026-10-11
tags: [player]
---

# Level spielen

Wähle ein Level in der Levelliste, stelle die Bedingungen des Durchlaufs ein und starte es. Ein fremdes Level ist ein einfacher Ordner: kopiere ihn in den Levelordner und aktualisiere die Liste

## Hauptmenü

| Schaltfläche | Was sie tut |
|---|---|
| `{{ui:menu_main_levels-btn}}` | die Levelliste, siehe unten |
| `{{ui:menu_main_editor-btn}}` | der Leveleditor, [[2_editor/1_basics/index]] |
| `{{ui:menu_main_sandbox-btn}}` | eine Arena ohne Level und das Tutorial, [[13_sandbox]] |
| `{{ui:settings_common_title}}` | alle Einstellungen, [[4_settings]] |
| `{{ui:menu_main_story-btn}}` | funktioniert noch nicht |
| `{{ui:menu_main_multiplayer-btn}}` | funktioniert noch nicht |

## Die Levelliste

`{{ui:menu_main_levels-btn}}` im Hauptmenü öffnet die Liste der Levels. Levels kommen aus drei Quellen:

- `{{ui:root_level-source_local}}` - der Ordner `levels`, [[1_installation]]
- `{{ui:root_level-source_builtin}}` - die Levels, die mit dem Spiel kommen
- `Workshop` - nur in Steam-Builds. Hier stehen die Levels, die du abonniert hast. Abonnierte Ressourcensammlungen sind keine Levels: sie erscheinen in der Bibliothek des Editors, [[16_library-and-collections]]

Oben gibt es das Suchfeld, `{{ui:root_level-browser_sort}}`, `{{ui:root_level-browser_layout}}` (Raster oder Liste) und `{{ui:root_level-browser_filters}}`. Die Liste öffnet sich als Raster.
Sortieren kannst du nach `{{ui:root_level-browser_sort-relevance}}`, `{{ui:root_level-browser_sort-title}}`, `{{ui:root_level-browser_sort-duration}}`, `{{ui:root_level-browser_sort-progress}}` und `{{ui:root_level-browser_sort-recent}}`. Der Pfeil neben der Sortierschaltfläche (`{{ui:root_level-browser_reverse}}`) dreht die Reihenfolge um. `{{ui:root_level-browser_sort-relevance}}` hat keine Richtung

Die Suche schaut zuerst auf Levelnamen, dann auf Autoren, dann auf Tags

`{{ui:root_level-browser_filters}}` öffnet ein Fenster mit weiteren Filtern. Die Liste dahinter ändert sich, während du tippst und klickst:

- `{{ui:root_level-filters_ai}}` - `{{ui:root_level-filters_ai-yes}}`, `{{ui:root_level-filters_ai-no}}` und `{{ui:root_level-filters_ai-unspecified}}`
- `{{ui:root_level-filters_length}}` - kürzestes und längstes Level, dazu ob Levels mit unbekannter Länge angezeigt werden
- `{{ui:root_level-filters_progress}}` - `{{ui:root_level-filters_progress-unplayed}}`, `{{ui:root_level-filters_progress-started}}`, `{{ui:root_level-filters_progress-cleared}}`, `{{ui:root_level-filters_progress-bot}}`
- `{{ui:root_level-filters_recent}}` - die letzten 24 Stunden, 7 Tage oder 30 Tage
- `{{ui:root_level-filters_age}}` - die höchste Altersfreigabe, die angezeigt wird
- `{{ui:root_level-filters_other}}` - Levels mit Passwort ausblenden, Levels aus einer neueren Version des Spiels ausblenden
- `{{ui:root_level-filters_tags}}` - ein Tag einmal antippen, um ihn vorauszusetzen, zweimal, um ihn auszuschließen

`{{ui:root_level-filters_progress}}` und `{{ui:root_level-filters_recent}}` gibt es nur in der Liste des Hauptmenüs. Die Liste des Editors hat eigene Filter.
Die Schaltfläche zeigt, wie viele Filter aktiv sind, und `{{ui:root_level-browser_reset}}` schaltet alle aus. Filter bleiben gesetzt, bis du das Spiel schließt

Ein Level in den Ordner kopiert? Drücke `{{ui:root_level-browser_refresh}}`, und die Liste wird aktualisiert

Ein Schloss auf einer Karte bedeutet, dass das Level mit einem Passwort geschützt ist

Langes Drücken oder ein Rechtsklick auf eine Karte öffnet ein Menü: `{{ui:level_passphrase_open}}` und `{{ui:root_level-browser_delete}}`.
`{{ui:root_level-browser_delete}}` bei einem `Workshop`-Level beendet das Abo des Eintrags und löscht seine Dateien. Dafür muss Steam laufen: sonst lädt Steam das Level erneut herunter. Mitgelieferte Levels lassen sich nicht löschen

## Ein fremdes Level hinzufügen

Ein Level ist ein einfacher Ordner mit Dateien. Du kannst ihn in ein Archiv packen und einem Freund schicken

**Ein Ordner.** Kopiere den Levelordner nach `levels` und drücke `{{ui:root_level-browser_refresh}}`.
Kopiere den Levelordner selbst: den, in dem `level.json` (oder `level.blob`) und `metadata.json` liegen

**Ein Archiv.** Öffne den Editor und erstelle ein neues Level mit dem Generator `{{ui:gen_level_archive}}`.
Wähle dann die Datei mit der Schaltfläche `{{ui:editor_create-level_archive-choose}}`

| Datei | Ergebnis |
|---|---|
| `.zip`, `.tar.gz` | wird geöffnet |
| `.zip` mit eigenem Passwort, `.zip.gpg`, `.tar.gz.gpg` | wird nach `{{ui:editor_create-level_archive-protected}}` geöffnet |
| `.7z` | vorerst abgelehnt. Pack es als Zip neu |
| alles andere | abgelehnt, [[5_troubleshooting]] |

Ein umbenanntes Archiv öffnet sich trotzdem: das Spiel erkennt das Format an den Bytes der Datei.
Ein Archiv aus einer älteren Version des Spiels wird beim Import aktualisiert

Standardmäßig bekommt ein importiertes Level eine eigene ID. So überschreibt es kein Level, das schon auf dem Gerät liegt

Mehr - [[6_sharing-by-hand]]

## Der Levelbildschirm

Der Levelbildschirm zeigt das Cover, die Autoren, die Beschreibung und den Autor der Musik. Außerdem gibt es die Schaltflächen `{{ui:level_level-view_authors}}` und `{{ui:level_level-view_licenses}}`

Der Name des Autors und die Musikzeile öffnen einen eigenen Link, wenn die Metadaten des Levels einen enthalten

Die Altersfreigabe legt der Autor des Levels fest. Das Spiel prüft sie nicht

"Enthält KI-generierte Inhalte" erscheint, wenn der Autor angegeben hat, dass das Level, sein Cover oder eine seiner Ressourcen von einer KI erzeugt wurde. Auch das ist eine eigene Angabe des Autors. Fehlt diese Zeile, heißt das nicht "keine KI": der Autor hat vielleicht einfach nichts angegeben

Vor einem Durchlauf kannst du die Bedingungen wählen:

| Bedingung | Auswahl |
|---|---|
| `{{ui:menu_levelview_options-lifes_title}}` | `{{ui:menu_levelview_options-lifes_option-zen}}` (der Durchlauf endet nie), `{{ui:menu_levelview_options-lifes_option-one}}`, `{{ui:menu_levelview_options-lifes_option-three}}`, `{{ui:menu_levelview_options-lifes_option-custom}}` (ein Schieberegler bis 16) |
| `{{ui:field_common_speed}}` | `0.5`, `1.0`, `2.0`, `{{ui:menu_levelview_options-lifes_option-custom}}` (ein Schieberegler bis 2). Level und Musik ändern sich gemeinsam |
| `Checkpoints` | an oder aus, [[7_damage]] |
| `{{ui:menu_levelview_options-no-collision_title}}` | an oder aus. Der Avatar geht durch alles hindurch, [[7_damage]] |
| `{{ui:menu_levelview_options-bot}}` | `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}`, `{{ui:enum_bot-kind_warm}}`, [[9_bots]] |
| `{{ui:level_level-view_seed-value}}` | eine Zahl, `{{ui:level_level-view_seed-randomize}}`, `{{ui:level_level-view_seed-clear}}`. `0` - ein neuer Seed bei jedem Durchlauf, [[8_determinism]] |

`Spielen` startet den Durchlauf

Die Pause bietet `{{ui:game_pause-window_continue-btn}}`, `{{ui:game_pause-window_restart-btn}}`, `{{ui:game_game-result_restart-checkpoint}}` (sobald ein Checkpoint erreicht ist), `{{ui:settings_common_title}}`, `{{ui:game_game-result_back-to-options}}` und `{{ui:game_game-result_back-to-menu}}`. `{{ui:game_game-result_back-to-options}}` führt zurück zum Levelbildschirm mit den Bedingungen, mit denen der Durchlauf gestartet wurde, oder zum Tab `Spielen` des Editors, wenn der Durchlauf dort gestartet wurde

## Das Ergebnisfenster

Das Fenster zeigt `Bestanden` oder `{{ui:game_game-result_lose}}` und drei Abschnitte: `Fortschritt`, `{{ui:game_game-result_section-damage}}` und `{{ui:game_game-result_section-conditions}}`

- Zeilen: `Abgeschlossen`, `{{ui:game_game-result_checkpoint}}`, `{{ui:field_common_time}}`, `{{ui:game_game-result_length}}`, `{{ui:game_game-result_hits}}`, `{{ui:game_game-result_lives-left}}`, `{{ui:game_game-result_streak}}`
- Bedingungen des Durchlaufs: `{{ui:field_common_speed}}`, `{{ui:menu_levelview_options-lifes_title}}`, `{{ui:menu_levelview_options-bot}}`, `{{ui:game_game-result_seed}}`, `Checkpoints`. Bei einem Durchlauf mit `{{ui:menu_levelview_options-no-collision_title}}` bekommt `{{ui:menu_levelview_options-lifes_title}}` den Zusatz `· Ohne Kollision`
- Schaltflächen: `{{ui:game_pause-window_restart-btn}}`, `{{ui:game_game-result_restart-checkpoint}}`, `{{ui:settings_common_title}}`, `{{ui:game_game-result_back-to-options}}`, `{{ui:game_game-result_back-to-menu}}`

Standardmäßig öffnet sich das Fenster bei einer Niederlage nicht. Stattdessen spult der Durchlauf zum letzten Checkpoint zurück.
Ändern lässt sich das unter `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_open-menu-on-lose}}`

## Rekorde

Der Levelbildschirm hat einen Rekordblock: `{{ui:menu_levelview_record-best}}`, `{{ui:menu_levelview_record-attempts}}` und `{{ui:menu_levelview_record-clears}}` (oder `{{ui:menu_levelview_record-none}}`)

Jede Kombination von Bedingungen hat ihren eigenen Rekord: Leben, Geschwindigkeit, Checkpoints, Kollisionen und der Bot. Der Block zeigt den Rekord für die gerade gewählten Bedingungen.
Versuche und Abschlüsse zählen bei jedem Durchlauf

Wie ein Rekord bestimmt wird - [[10_statistics]]

## Markierungen auf Karten

| Markierung | Bedeutung |
|---|---|
| `{{ui:root_level-entry_not-listed}}` | der Workshop-Ordner liegt auf der Festplatte, aber du hast ihn nicht abonniert. Nur sichtbar, wenn `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general_show-all-found-content}}` an ist |
| `{{ui:root_level-entry_unverified}}` | die Levelquelle hat nicht geantwortet |
| `{{ui:root_level-entry_newer-version}}`, `{{ui:root_level-entry_newer-file}}` | diese Version des Spiels öffnet das Level nicht, [[5_troubleshooting]] |
| `{{ui:root_level-entry_level-missing-badge}}` | im Ordner fehlt `level.json`, also lässt sich das Level nicht starten, [[4_level-folder-and-backups]] |
| `{{ui:root_level-entry_meta-missing-badge}}` | im Ordner fehlt eine lesbare `metadata.json`. Die Karte zeigt den Ordnernamen, und das Level lässt sich spielen, [[4_level-folder-and-backups]] |

## Ein Level löschen

Langes Drücken oder Rechtsklick auf eine Karte → `{{ui:root_level-browser_delete}}`. Das Spiel fragt vorher nach einer Bestätigung

Zusammen mit dem Level kannst du seine Statistik (`{{ui:root_level-delete_statistics}}`) und Sicherungen (`{{ui:root_level-delete_backups}}`) löschen

Zum Löschen eines geschützten Levels brauchst du kein Passwort
