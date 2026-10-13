---
title: Tempo und Tastenkürzel
date: 2026-10-02
tags: [level_author]
---

# Tempo und Tastenkürzel

Die Befehlspalette (Ctrl+Shift+P), die Inhaltssuche (Ctrl+F), die Ping-Schaltfläche und die Pfeiltasten auf einer Zeitleiste sparen am meisten Zeit. Jede Taste lässt sich neu belegen

## Die vier größten Zeitsparer

- **`{{ui:editor_search-title_command}}`** (`Ctrl+Shift+P`) - alles, was der Editor kann, nach Namen durchsuchbar. Schneller, als sich zu merken, in welchem Bereich eine Schaltfläche liegt
- **`Search Content`** (`Ctrl+F`) - springt per Name zu einem Objekt oder einer Audiospur. Der Abspielkopf geht mit
- **`{{ui:cmd_editor_ping}}`** - der Viewport rahmt die Auswahl ein, Zeitleiste und Hierarchie scrollen zu ihr, alles auf einmal. Erneutes Drücken springt zum nächsten Objekt einer Mehrfachauswahl
- **Pfeiltasten auf einer Zeitleiste** - sie bewegen sich nach Richtung, nicht nach Position in einer Liste. Du kannst ohne Maus zwischen benachbarten Keyframes wechseln

## Die Standardbelegung

Die Gruppen und Namen unten sind die, die `{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}` anzeigt

### Wiedergabe

| Taste | Name in den Einstellungen | Aktion |
|---|---|---|
| `Space` | `{{ui:settings_keybindings_editor_play_pause}}` | abspielen und pausieren |

### Bearbeiten

| Taste | Name in den Einstellungen | Aktion |
|---|---|---|
| `Ctrl+Z` | `{{ui:cmd_editor_undo}}` | rückgängig machen |
| `Ctrl+Y` oder `Ctrl+Shift+Z` | `{{ui:cmd_editor_redo}}` | wiederholen |
| `Ctrl+S` | `{{ui:settings_keybindings_editor_save}}` | speichern |
| `Ctrl+C` | `{{ui:cmd_editor_copy}}` | kopieren |
| `Ctrl+V` | `{{ui:cmd_editor_paste}}` | einfügen |
| `Ctrl+D` | `{{ui:cmd_editor_duplicate}}` | duplizieren |
| `Ctrl+G` | `{{ui:cmd_editor_pack-prefab}}` | ein Prefab aus der Auswahl erstellen |

### Auswahl

| Taste | Name in den Einstellungen | Aktion |
|---|---|---|
| `Del` | `{{ui:settings_keybindings_editor_delete}}` | die Auswahl löschen |
| `Ctrl` gehalten | `{{ui:settings_keybindings_editor_multi_select}}` | Mehrfachauswahl |
| `Ctrl+Shift+A` | `{{ui:settings_keybindings_editor_deselect}}` | jede Auswahl auf einmal aufheben: Objekte, Keyframes, Audio und Beat |
| `Ctrl+Shift+E` | `{{ui:cmd_editor_exit-prefab}}` | den Prefab-Modus verlassen und zum Level zurückkehren |

### Ansicht

| Taste | Name in den Einstellungen | Aktion |
|---|---|---|
| `Ctrl+F` | `Search Content` | Inhalt durchsuchen |
| `Ctrl+Shift+P` | `{{ui:editor_search-title_command}}` | einen Befehl ausführen |
| `Ctrl+Left` | `{{ui:settings_keybindings_editor_panel_left}}` | den linken Bereich ein- oder ausblenden |
| `Ctrl+Right` | `{{ui:settings_keybindings_editor_panel_right}}` | den rechten Bereich ein- oder ausblenden |
| `Ctrl+Down` | `{{ui:settings_keybindings_editor_panel_bottom}}` | den unteren Bereich ein- oder ausblenden |
| `Ctrl+Up` | `{{ui:settings_keybindings_editor_viewport_tools}}` | die Werkzeuggruppen über dem Viewport ein- oder ausblenden |
| `` ` `` gehalten | `{{ui:settings_keybindings_editor_preview}}` | Vorschau: Die Oberfläche des Editors ist ausgeblendet, solange die Taste gedrückt ist |

### Zeitleiste

| Taste | Name in den Einstellungen | Aktion |
|---|---|---|
| `Z` | `{{ui:settings_keybindings_editor_expansion_cycle}}` | Einklappen durchschalten: jeder Teilbaum, nur die gewählten Arten, nichts |
| `X` | `{{ui:settings_keybindings_editor_tool_snap}}` | Einrasten ein- oder ausschalten |
| `C` | `{{ui:settings_keybindings_editor_tool_selection}}` | das Auswahlwerkzeug |
| `V` | `{{ui:settings_keybindings_editor_tool_marquee}}` | das Werkzeug für die Rechteckauswahl |
| `B` | `{{ui:settings_keybindings_editor_tool_scissors}}` | das Scherenwerkzeug |
| `N` | `{{ui:settings_keybindings_editor_tool_edges}}` | das Ränder-Werkzeug |
| `Ctrl+E` | `{{ui:settings_keybindings_editor_fold}}` | die ausgewählten Objekte auf der Zeitleiste einklappen |
| `Q` | `{{ui:settings_keybindings_editor_tab_timeline_level}}` | die Level-Zeitleiste öffnen |
| `W` | `{{ui:settings_keybindings_editor_tab_timeline_local}}` | die lokale Zeitleiste öffnen |
| `E` | `{{ui:settings_keybindings_editor_tab_timeline_audio}}` | die Audio-Zeitleiste öffnen |
| `R` | `{{ui:settings_keybindings_editor_tab_timeline_events}}` | die Ereignis-Zeitleiste öffnen |
| `T` | `{{ui:settings_keybindings_editor_tab_timeline_prefab}}` | die Prefab-Zeitleiste öffnen |
| `Shift+T` | `{{ui:settings_keybindings_editor_beat_window}}` | das Fenster des Beat-Rasters, in dem das Tempo eingetippt wird. `{{ui:settings_keybindings_editor_beat_tap}}` selbst hat keine Standardtaste, belege bei Bedarf eine |
| `Ctrl` gehalten mit dem Mausrad | `{{ui:settings_keybindings_timeline_pan_modifier}}` | schwenken |
| `Shift` gehalten mit dem Mausrad | `{{ui:settings_keybindings_timeline_zoom_modifier}}` | zoomen |

`Z X C V B N` folgen der Werkzeugleiste der Zeitleiste von links nach rechts, `Q W E R T` der Tab-Leiste. Eine Zeitleiste mit weniger Werkzeugen lässt sie von rechts weg: Die lokale Zeitleiste hat nur `Z X C V`. Ein Buchstabe, für den die offene Zeitleiste kein Werkzeug hat, tut nichts

### Gizmos

| Taste | Name in den Einstellungen | Aktion |
|---|---|---|
| `1` | `{{ui:settings_keybindings_editor_gizmo_none}}` | Auswahl |
| `2` | `{{ui:settings_keybindings_editor_gizmo_position}}` | Position |
| `3` | `{{ui:settings_keybindings_editor_gizmo_rotation}}` | Drehung |
| `4` | `{{ui:settings_keybindings_editor_gizmo_scale}}` | Skalierung |
| `5` | `{{ui:settings_keybindings_editor_gizmo_size}}` | Größe |
| `6` | `{{ui:settings_keybindings_editor_gizmo_anchors}}` | Anker |
| `7` | `{{ui:settings_keybindings_editor_gizmo_pivot}}` | Drehpunkt |
| `0` | `{{ui:settings_keybindings_editor_gizmo_hidden}}` | ausgeblendet: Die Auswahl bleibt, aber weder Griffe noch Rahmen werden gezeichnet |

### Fenster

| Taste | Name in den Einstellungen | Aktion |
|---|---|---|
| `F11` | `{{ui:settings_keybindings_window_toggle_fullscreen}}` | Vollbild ein- oder ausschalten. Funktioniert auf jedem Bildschirm, nur auf dem Desktop |
| `Ctrl+S` | `{{ui:settings_keybindings_window_settings_save}}` | die Einstellungen sofort auf die Festplatte schreiben, solange die Einstellungen offen sind. Im Editor speichert `Ctrl+S` stattdessen das Level |

### Navigation

| Taste | Name in den Einstellungen | Aktion |
|---|---|---|
| `Up` | `{{ui:settings_keybindings_nav_up}}` | nach oben auf der Fläche, in die du zuletzt geklickt hast |
| `Down` | `{{ui:settings_keybindings_nav_down}}` | nach unten auf der Fläche, in die du zuletzt geklickt hast |
| `Left` | `{{ui:settings_keybindings_nav_left}}` | nach links auf der Fläche, in die du zuletzt geklickt hast |
| `Right` | `{{ui:settings_keybindings_nav_right}}` | nach rechts auf der Fläche, in die du zuletzt geklickt hast |

Einzelne Tasten wie die Gizmo-Ziffern, die Buchstaben der Zeitleiste und `Space` tun nichts, während du in ein Textfeld tippst. Eine `2` in einem Frame-Feld wechselt das Gizmo nicht

## Pfeiltasten auf einer Zeitleiste

Ein Pfeil wählt das nächstgelegene Element in dieser Richtung auf dem Bildschirm. Derselbe Tastendruck findet bei jedem Zoom dasselbe Element

- Bei einer Mehrfachauswahl startet ein Pfeil bei dem Element, das in der gedrückten Richtung am weitesten vorn liegt. Er springt nie zurück in den Block, den du ausgewählt hast
- Ein Pfeilschritt ersetzt immer die Auswahl. Er fügt nie etwas hinzu
- Die Zeitleiste scrollt nur so weit, wie nötig ist, um das neue Element zu zeigen. Ein Klick auf die Anzeige des Abspielkopfs zentriert die Ansicht weiterhin
- Solange der Testspieler an ist, steuern die Pfeile ihn, nicht die Zeitleiste. Die Hierarchie und der Tab `{{ui:settings_level-settings_raw}}` behalten ihre Pfeile, sobald du hineinklickst

## Das Level sehen

**Vorschau.** Halte `` ` `` gedrückt, um die Oberfläche des Editors auszublenden und nur das Level zu sehen. Es ist ein Halten, kein Umschalten: Lässt du die Taste los, ist alles wieder da. Das Level, die Letterbox-Balken, der Spieler und die Kameragrenzen bleiben sichtbar.
Es gibt dafür weder eine Schaltfläche noch eine Einstellung. Die Taste lässt sich als `{{ui:settings_keybindings_editor_preview}}` neu belegen

**Das Raster im Viewport** wird mit seiner Schaltfläche in der Werkzeugleiste oder dem Befehl `{{ui:cmd_editor_viewport-grid}}` umgeschaltet. Es startet ausgeschaltet. Das lässt sich unter `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_grid-active-default}}` ändern, und ob du es eingeschaltet hast, wird zwischen Sitzungen nicht gespeichert

**Der Gizmo-Magnet** lässt das, was ein Gizmo zieht, am Raster einrasten. Er ist standardmäßig an und hängt nicht vom Gizmo-Modus ab. Umgeschaltet wird er mit seiner Schaltfläche in der Werkzeugleiste und dem Befehl `{{ui:cmd_editor_gizmo-magnet}}`

**Pausiert ist der normale Zustand zum Anschauen.** Raster, Collider, Bot-Overlay, Gizmo-Griffe und Auswahlrahmen werden alle weiter gezeichnet, während die Wiedergabe pausiert ist. Wer einen Gizmo-Griff packt, pausiert die Wiedergabe

## Neu belegen

Jede Taste lässt sich neu belegen: `{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`

Gespeichert werden nur die Tasten, die du geändert hast. Der Rest kommt aus der Standardbelegung.
Eine verbesserte Standardbelegung erreicht dich also, wenn du diese Taste nicht angefasst hast.
`{{ui:settings_keybindings_reset}}` entfernt einfach deine Änderungen, und alle Tasten kehren zur Standardbelegung zurück

> [!tip] Tipp
> Tastenbeschriftungen sind nicht fest in die Oberfläche eingebaut. Nach einer Neubelegung zeigen die Befehlspalette und jedes Kontextmenü sofort die neue Taste

## Gedrückte und gehaltene Tasten

Eine gedrückte Taste löst nur aus, wenn ihre Modifikatortasten genau übereinstimmen.
`Ctrl+Shift+P` löst nicht zusätzlich als `Ctrl+P` aus, und ein einzelnes `T` löst nicht aus, während `Ctrl` gehalten wird

Eine gehaltene Taste löst aus, wenn ihre Modifikatortasten unter den gehaltenen sind. Sie verfeinert eine Geste, die schon läuft

> [!info] Gut zu wissen
> Deshalb können sich zwei gehaltene Tasten absichtlich einen Knopf teilen. Mehrfachauswahl und Schwenken der Zeitleiste liegen beide auf `Ctrl` und kommen sich nicht in die Quere

Weiter: [[1_order-of-work|Die Reihenfolge der Arbeit]], [[2_reuse|Wiederverwendung: Prefabs, Kopieren, Generatoren]]
