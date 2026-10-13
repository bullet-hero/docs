---
title: Fehlerbehebung
date: 2026-10-03
tags: [player]
---

# Fehlerbehebung

Ein von Hand kopiertes Level erscheint nach einem neuen Scan. Ein Level aus einer neueren Version braucht ein Update, ein .7z-Archiv muss in Zip umgepackt werden. Ein vergessenes Passwort ist verloren

Dein Problem ist nicht dabei? Wo du es meldest - [[11_help]]

## Ein Level fehlt in der Liste

- **Von Hand kopiert.** Der Levelordner muss direkt in `levels` liegen, [[1_installation]]. Drücke nach dem Kopieren `{{ui:root_level-browser_refresh}}`
- **Ein Workshop-Eintrag.** Der Steam-Build zeigt nur deine Abos. `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general_show-all-found-content}}` fügt die auf der Festplatte gefundenen Ordner hinzu. Sie sind mit `{{ui:root_level-entry_not-listed}}` markiert
- **Gar nichts wird angezeigt.** Der Levelordner ist vielleicht nicht erreichbar. In diesem Zustand läuft die Speicherbereinigung unter `{{ui:settings_other_title}}` nicht und meldet `Der Levelscan hat nichts gefunden, deshalb wurde diese Bereinigung abgelehnt`

## Ein Level lädt nicht

Der Ladebildschirm zeigt die Phase: `{{ui:root_loading_reading}}`, `{{ui:root_loading_validating}}`, `{{ui:root_loading_resources}}`, `{{ui:root_loading_building}}`

- **Eine Datei unter einer Webadresse.** Ein Level kann eine Datei über einen Link beziehen, statt sie in seinem Ordner zu haben. `{{ui:settings_general_title}}` → `{{ui:settings_general_resource-web-timeout}}` legt fest, wie viele Sekunden das Spiel auf eine solche Datei wartet
- **Ein beschädigtes Level.** Ein Level in `Json` ist Text, man kann es mit bloßem Auge lesen. Ein beschädigtes `Blob` wird komplett abgelehnt. Mehr - [[4_level-folder-and-backups]]
- **Ein Fehlerfenster.** Es bietet `{{ui:root_error_copy}}`, `{{ui:root_error_save}}` und `{{ui:root_error_open-reports-folder}}`. Der Bericht landet im Ordner `reports`. Hänge ihn an einen Fehlerbericht in [bullet-hero/releases](https://github.com/bullet-hero/releases/issues), [[11_help]]
- **`Das Level braucht mehr Objekte pro Frame, als dieses Gerät erlaubt`.** Das ist kein Ladefehler. Das Level läuft, aber ein Teil davon wird nicht gezeichnet. Mehr - [[1_level-budget]]

## "Update erforderlich"

Eine ältere Version des Spiels öffnet keine Dateien aus einer neueren. Aktualisiere das Spiel

| Meldung | Was zu tun ist |
|---|---|
| `Dieses Level wurde in einer neueren Version des Spiels erstellt...` | das Spiel aktualisieren |
| `Dieses Archiv enthält ein Level aus einer neueren Version des Spiels...` | das Spiel aktualisieren |
| `Die Zwischenablage enthält Editorinhalt, der in einer neueren Version des Spiels kopiert wurde...` | das Spiel aktualisieren |
| `Deine Einstellungen oder deine Statistik wurden von einer neueren Version des Spiels gespeichert...` | `{{ui:root_update-required_download}}`, `{{ui:root_update-required_keep}}` oder `{{ui:root_update-required_overwrite}}` |

Eine Karte mit der Markierung `{{ui:root_level-entry_newer-version}}` oder `{{ui:root_level-entry_newer-file}}` ist dieselbe Ablehnung. Sie erscheint, noch bevor das Level überhaupt geöffnet wird

### Einstellungen oder Statistik aus einer neueren Version

In diesem Fall läuft das Spiel mit Standardwerten. Bis es geschlossen wird, speichert es nichts Eigenes, und die neueren Dateien bleiben unangetastet. Das ist der anonyme Modus, [[4_settings]].
Mit `--suppress-game-saves` gibt es keine Schaltfläche `{{ui:root_update-required_overwrite}}`

Levelstatistik aus einer neueren Version wird nicht angezeigt. Spielst du das Level, wird sie überschrieben, außer das Speichern ist ausgeschaltet

### Warum das Spiel ablehnt

Jede Änderung am Dateiformat bekommt eine neue Generationsnummer. Ein Build liest keine Datei einer neueren Generation, damit er sie nicht falsch liest

## Ein geschütztes Level

Vor dem Öffnen fragt das Spiel nach einem `{{ui:level_passphrase_password}}`.
Das Passwort wird einmal pro Sitzung abgefragt und nur im Speicher gehalten

Verschlüsselt ist nur der Inhalt: Objekte, Keyframes, Themes. Titel, Cover und Medien bleiben lesbar, deshalb erscheint die Karte auch ohne Passwort

Zum Löschen eines geschützten Levels braucht es kein Passwort

> [!caution] Vorsicht
> Ein vergessenes Passwort lässt sich nicht wiederherstellen. Der Schlüssel wird nirgends gespeichert - nicht im Spiel, nicht in der Datei, bei niemandem

## Ein Archiv wird abgelehnt

| Meldung | Ursache |
|---|---|
| `{{ui:editor_create-level_archive-unsupported}}` | es ist `.7z`. Pack es als `.zip` neu |
| `{{ui:editor_create-level_archive-wrong-password}}` | das Passwort stimmt nicht |
| `{{ui:editor_create-level_archive-damaged}}` | das Archiv ist kaputt, lass es dir noch einmal schicken |
| `{{ui:editor_create-level_archive-not-archive}}` | die Datei ist gar kein Levelarchiv |

Ein umbenanntes Archiv ist kein Problem: das Spiel erkennt das Format an den Bytes der Datei.
Welche Archive angenommen werden - [[2_playing-levels]]

## Discord zeigt nicht an, was ich spiele

- **Kein Steam-Build.** Nur die Steam-Builds zeigen deine Aktivität in Discord
- **Discord ist geschlossen.** Die Discord-Desktop-App muss auf demselben Computer laufen. Erst nach dem Spiel gestartet? Der Status erscheint beim nächsten Bildschirmwechsel
- **Die Aktivität ist verborgen.** In Discord: `User Settings` -> `Activity Privacy` -> erkannte Aktivitäten teilen
- **Ein eigenes Level zeigt keinen Namen.** Das ist so gewollt: nur ein Workshop-Level oder ein mitgeliefertes Level wird genannt, und der Editor nennt sein Level nie. Warum - [[game-privacy-policy#Discord Rich Presence]]
