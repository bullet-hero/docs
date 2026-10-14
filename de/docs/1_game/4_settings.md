---
title: Einstellungen
date: 2026-10-14
tags: [player]
---

# Einstellungen

Die wichtigsten Einstellungen wählst du beim ersten Start in einer Schnelleinrichtung, die sich von selbst öffnet: Sprache, Lautstärke, Leistung, Effekte. Ein Reset lässt Levels unberührt

## Die Tabs

| Tab | Inhalt |
|---|---|
| `{{ui:settings_general_title}}` | die Sprache - jede in sich selbst benannt, `Русский (ru)`. `System (de)` folgt dem Gerät und zeigt, welche Sprache daraus wurde. Außerdem wie viele Leveldateien gleichzeitig laden, das Zeitlimit für eine Datei unter einer Webadresse, `{{ui:settings_general-open_folder}}` |
| `{{ui:field_common_audio}}` | Lautstärke: `{{ui:settings_audio_volume}}`, `{{ui:settings_audio_game}}`, `{{ui:settings_audio_ui}}`, `{{ui:settings_audio_editor-ui}}`, `{{ui:settings_audio_editor-game}}` |
| `{{ui:settings_controls_title}}` | Geräte und die Art der Steuerung, [[3_controls]] |
| `{{ui:settings_keybindings_label}}` | Tastenkürzel, vor allem die des Editors, [[3_speed-and-shortcuts]] |
| `{{ui:settings_graphics_title}}` | Anzeige, Framerate, Kantenglättung, `{{ui:settings_graphics-colliders-mode_title}}`, Texturen, Effekte, Post-Processing |
| `{{ui:settings_interface_label}}` | die Oberfläche im Spiel, `{{ui:settings_interface_open-menu-on-lose}}`, `{{ui:settings_interface_menu-background}}`, `{{ui:settings_interface_levels-layout}}`, Bildschirmausrichtung, das Statistik-Overlay |
| `{{ui:settings_game-editor_title}}` | die eigenen Einstellungen des Editors, darunter sein eigenes `{{ui:settings_interface_levels-layout}}` |
| `{{ui:settings_profile_tab}}` | deine Statistik, [[10_statistics]] |
| `{{ui:settings_other_title}}` | Speicherbereinigung, Profilübertragung und der Status von Steam Cloud ([[14_profile-transfer]]), Ordnerzugriff unter Android, anonymer Modus, `{{ui:settings_other_reset}}` |

`{{ui:settings_interface_menu-background}}` wählt, was hinter den Schaltflächen des Hauptmenüs zu sehen ist: eine Live-Arena, in der ein Bot Angriffen ausweicht, ein Feld rotierender Formen oder nichts

`{{ui:settings_interface_levels-layout}}` wählt, wie die Levelauswahl sich öffnet - als `{{ui:enum_level-browser-layout_grid}}` aus Covern oder als `{{ui:enum_level-browser-layout_list}}` aus Zeilen mit Beschreibungen. Davon gibt es zwei: die Einstellung auf dem Tab `{{ui:settings_interface_label}}` gilt für das Menü (standardmäßig `{{ui:enum_level-browser-layout_grid}}`), die auf dem Tab `{{ui:settings_game-editor_title}}` für den Editor (standardmäßig `{{ui:enum_level-browser-layout_list}}`). Die Schaltfläche neben dem Suchfeld wechselt die Ansicht trotzdem, bis du den Bildschirm verlässt

## Schnelleinrichtung

`{{ui:settings_quick-setup_title}}`, eine Schaltfläche auf dem Tab `{{ui:settings_general_title}}` über `{{ui:settings_general-open_folder}}`, stellt ein paar der wichtigsten Fragen, eine Kategorie pro Seite. Beim allerersten Start öffnet sie sich von selbst, noch vor dem Angebot des Tutorials.
Jede Antwort hat eine Zeile dazu, was sie bewirkt. Die Seiten lassen sich in beliebiger Reihenfolge öffnen, `{{ui:settings_quick-setup_next}}` schlägt die nächste nur vor

| Seite | Frage | Antworten | Was sich ändert |
|---|---|---|---|
| `{{ui:settings_quick-setup_page-language}}` | `{{ui:settings_general_language}}` | `{{ui:settings_general_language_system}}` und jede Sprache des Spiels, jede in sich selbst benannt | dasselbe wie auf dem Tab `{{ui:settings_general_title}}` |
| | `{{ui:settings_audio_volume}}` | ein Schieberegler | dasselbe wie auf dem Tab `{{ui:field_common_audio}}` |
| `{{ui:settings_graphics_title}}` | `{{ui:settings_quick-setup_performance}}` | `{{ui:settings_quick-setup_performance-minimum}}`, `{{ui:settings_quick-setup_performance-economy}}`, `{{ui:settings_quick-setup_performance-recommended}}`, `{{ui:settings_quick-setup_performance-max}}` | Renderskalierung (PC), Kantenglättung, Texturgröße, die Framerate der Effekte - aber nicht die Framerate-Grenze: jede Antwort läuft mit der Rate des Bildschirms. `{{ui:settings_quick-setup_performance-minimum}}` schaltet außerdem Partikeleffekte und Post-Processing aus und begrenzt Bilder auf 512 |
| | `{{ui:settings_quick-setup_comfort}}` | `{{ui:settings_quick-setup_comfort-full}}`, `{{ui:settings_quick-setup_comfort-soft}}`, `{{ui:settings_quick-setup_comfort-minimal}}` | jeden Post-Processing-Effekt und das Zerspringen des Avatars. `{{ui:settings_quick-setup_comfort-soft}}` schaltet Glitches, Körnung, Unschärfe, Linsenverzerrung und Farbsäume aus |
| `{{ui:settings_controls_title}}` | | `{{ui:settings_quick-setup_open-tutorial}}` | hier nichts: im Tutorial probierst du jedes Steuerungsschema aus und wählst deins. Es öffnet sich aus dem Hauptmenü oder der Sandbox |

Die mit `{{ui:settings_quick-setup_default-badge}}` markierte Antwort ist das, womit das Spiel auf deinem Gerät startet. Eine Auswahl gilt sofort und ist in den vollständigen Einstellungen sichtbar.
Passen deine Einstellungen zu keiner Antwort, ist keine hervorgehoben, und eine Zeile sagt das - das sind deine eigenen Einstellungen, und ein Klick ersetzt sie

## Eingeklappte Abschnitte

Lange Tabs sind in Abschnitte geteilt. Was oft geändert wird, ist offen, die Feinabstimmung ist eingeklappt: ein Abschnitt öffnet sich über seine Überschrift.
Die Schaltfläche neben dem Zurücksetzen des Tabs klappt alle Abschnitte auf einmal ein oder auf

Auf dem Tab `{{ui:settings_controls_title}}` ist nur das Gerät offen, das du gerade in der Hand hast

## Zurücksetzen

Jeder Tab hat sein eigenes Zurücksetzen.
`{{ui:settings_other_reset}}` unter `{{ui:settings_other_title}}` setzt alle Tabs auf einmal zurück

Ein Zurücksetzen betrifft nur Einstellungen. Deine Levels bleiben

## Die Versionszeile

Der Einstellungsbildschirm hat eine Versionszeile. Ein Klick darauf kopiert sie

Sie sieht so aus: `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`.
Genau diese Zeile gehört in einen Fehlerbericht, [[11_help]]

## Grafik

**Kantenglättung.** Am PC ist der Standard `{{ui:enum_anti-aliasing-type_msaa}}`. Ein Handy startet ohne Kantenglättung. Jede Form im Spiel ist echte Geometrie, und `{{ui:enum_anti-aliasing-type_msaa}}` gibt ihr auf jeder Plattform saubere Kanten ohne Unschärfe

`{{ui:enum_anti-aliasing-type_fxaa}}` ist für schwache Handys. Es ist ein Durchgang über den ganzen Bildschirm, und seine Kosten sind konstant. Die Kosten von `{{ui:enum_anti-aliasing-type_msaa}}` steigen, wenn viele transparente Formen übereinander gezeichnet werden

TAA wird absichtlich nicht angeboten. Es hinterlässt eine Spur hinter schnellen Geschossen, und sein Jitter stört die Glitch-Effekte

**Framerate.** Die Ziel-Framerate wird von Hand gesetzt, nicht über vertikale Synchronisation. So ist das Timing eines Levels auf einem 60-Hz- und einem 144-Hz-Bildschirm gleich.
Solange `{{ui:settings_graphics_vsync}}` an ist (nur PC), hat die Framerate-Grenze keine Wirkung

> [!tip] Empfehlung
> Auf einem schwachen Gerät senkst du am besten zuerst die **Renderskalierung** unter 1. Sie kostet nur Schärfe, und die Oberfläche bleibt in voller Größe. Nur PC

Mehr - [[2_mobile-devices]]

## Nur-Collider-Modus

Ein Modus zum Üben, ein eingeklappter Abschnitt auf dem Tab `{{ui:settings_graphics_title}}`. Mit `{{ui:settings_graphics-colliders-mode_active}}` zeichnet ein laufendes Level jede Hitbox als flache Fläche in einer Farbe auf schlichtem Hintergrund, und sonst nichts.
Weg sind: das Aussehen der Formen selbst, Formen ohne Collider, Effekte, Texte, Post-Processing und der Hintergrund des Themes.
Unverändert bleiben: die Musik, die Kollision, die Kamera und ihre Erschütterung, Checkpoints, die Oberfläche und die Statistik - ein Durchlauf in diesem Modus zählt wie jeder andere.
Dein Avatar wird wie gewohnt gezeichnet

Der Modus wirkt nur beim Spielen von Levels. Editor, Sandbox und Menühintergrund werden wie gewohnt gezeichnet

| Option | Was sie tut |
|---|---|
| `{{ui:settings_graphics-colliders-mode_use-alpha}}` | an (Standard) - die Flächen sind je nach Alpha der Farbe halbtransparent, und überlappende Hindernisse wirken dunkler. Das Alpha fällt nie unter 0,15. Aus - jede Fläche ist deckend, und das Alpha der Farbe ist gesperrt |
| `{{ui:settings_graphics-colliders-mode_color}}` | die Füllfarbe, standardmäßig Rot mit Alpha 0,6. Die Collider-Ansicht des Editors nutzt denselben Farbton mit eigener Deckkraft |
| `{{ui:settings_graphics-colliders-mode_background}}` | was hinter den Flächen gezeichnet wird, standardmäßig Dunkelgrau - nicht Schwarz, damit der Rand des Kamerabilds vor den schwarzen Balken drumherum sichtbar bleibt |

Beide Farben sind unter einer eigenen Beschriftung eingeklappt: klappe die benötigte auf, um ihr Farbrad zu sehen

## Anonymer Modus

Wird unter `{{ui:settings_other_title}}` → `{{ui:settings_other_suppress-game-saves}}` eingeschaltet

Solange der Modus an ist, speichert das Spiel nichts Eigenes. `settings.json`, die globale Statistik und die Levelstatistik bleiben unangetastet auf der Festplatte.
Eine geänderte Einstellung wirkt trotzdem, bis das Spiel geschlossen wird

Die Arbeit mit Levels wird wie gewohnt gespeichert: Speichern, Exportieren, Importieren, Kopieren und Löschen.
Das Autospeichern und die Sicherungen des Editors laufen ebenfalls, sie haben einen eigenen Schalter

Der Modus gilt, bis das Spiel geschlossen wird, und wird nirgends gespeichert

Schaltest du ihn aus, werden die aktuellen Einstellungen gespeichert. Alles, was in dieser Zeit gespielt wurde, wird verworfen

> [!info] Gut zu wissen
> Der Modus schaltet sich auch von selbst ein. Das [[12_launch-arguments|Startargument]] `--suppress-game-saves` schaltet ihn für den ganzen Start ein, und im Spiel lässt er sich dann nicht ausschalten. Einstellungen oder Statistik aus einer neueren Version des Spiels schalten ihn ebenfalls ein. Dann fragt das Spiel bei jedem Start, ob sie behalten oder mit den Standardwerten überschrieben werden sollen
