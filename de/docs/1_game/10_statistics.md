---
title: Statistik
date: 2026-10-02
tags: [advanced_player]
---

# Statistik

Das Spiel zählt Versuche, Tode, Treffer und Zeit für jedes Level und für das ganze Gerät. Alles liegt lokal im Ordner stats. Ein Rekord wird für jede Kombination von Bedingungen getrennt geführt

## Zwei Dateien

| Datei | Inhalt |
|---|---|
| `stats/statistics.json` | alles über dich: über alle Levels und Bildschirme hinweg |
| `stats/<LevelId>.json` | alles, was du mit einem Level gemacht hast |

Die Dateien sind JSON, Zeiten sind in UTC. Nichts wird irgendwohin gesendet

Der Ordner `stats` liegt neben `levels` im Ordner des Spiels, [[1_installation]]. Er liegt nie in einem Level.
Ein Level, das du einem Freund schickst, kommt also nicht schon abgeschlossen an. Und dein Fortschritt übersteht es, wenn du das Level löschst und neu importierst

## Der Tab "Profil"

`{{ui:settings_common_title}}` → `{{ui:settings_profile_tab}}` zeigt die gemeinsame Datei des Geräts:

| Abschnitt | Zeilen |
|---|---|
| `{{ui:settings_profile_section-account}}` | `{{ui:settings_profile_first-played}}`, `{{ui:settings_profile_last-played}}`, `{{ui:settings_profile_launches}}`, `{{ui:settings_profile_app-time}}` |
| `{{ui:field_common_time}}` | `{{ui:settings_profile_menu-time}}`, `{{ui:settings_profile_game-time}}`, `{{ui:settings_profile_editor-time}}`, `{{ui:settings_profile_loading-time}}` |
| `{{ui:settings_profile_section-totals}}` | `{{ui:settings_profile_attempts}}`, `{{ui:settings_profile_clears}}`, `{{ui:settings_profile_deaths}}`, `{{ui:settings_profile_hits}}`, `{{ui:settings_profile_levels-played}}`, `{{ui:settings_profile_levels-cleared}}`, `{{ui:settings_profile_frames}}` |
| `{{ui:settings_profile_section-streaks}}` | `{{ui:settings_profile_streak-current}}`, `{{ui:settings_profile_streak-longest}}` |
| `{{ui:settings_profile_section-avatar}}` | `{{ui:settings_profile_dashes}}`, `{{ui:settings_profile_distance}}` |
| `{{ui:settings_profile_section-tutorial}}` | `{{ui:settings_profile_tutorial-completions}}`, `{{ui:settings_profile_tutorial-first}}`, `{{ui:settings_profile_tutorial-last}}` - ein Abschluss zählt nur, wenn jeder Schritt des [[13_sandbox|Tutorials in der Sandbox]] erledigt ist |
| `{{ui:settings_profile_section-editor}}` | `{{ui:settings_profile_levels-created}}`, `{{ui:settings_profile_levels-deleted}}`, `{{ui:settings_profile_objects}}`, `{{ui:settings_profile_operations}}`, `{{ui:settings_profile_generators}}`, `{{ui:settings_profile_resources}}` |
| `{{ui:settings_profile_section-devices}}` | `{{ui:settings_profile_device-keyboard}}`, `{{ui:settings_profile_device-touch}}`, `{{ui:settings_profile_device-gamepad}}`, `{{ui:settings_profile_device-gyro}}` |

Die Zeit wird in echten Sekunden gezählt, nicht in Levelzeit. Zeitlupe an einem Checkpoint und ein Durchlauf mit halber Geschwindigkeit zählen so lange, wie sie tatsächlich gedauert haben

Die Gerätezeilen zeigen, welches Gerät den Avatar beim Spielen gesteuert hat. Ein nur angeschlossenes Gerät zählt nicht

## Pro Level

Die Datei eines Levels enthält:

- wann du es zum ersten und zum letzten Mal gespielt hast
- die echte Zeit im Level und die Zahl der Sitzungen
- Versuche (jeder Neustart ist ein neuer), Abschlüsse, Tode, Treffer, Dashes
- Rückkehr zu einem Checkpoint und abgebrochene Durchläufe
- den weitesten erreichten Punkt und den ersten Abschluss
- wo im Level du stirbst: nach Anteil der Länge und nach Checkpoint

## Rekorde

Ein Rekord wird pro Kombination von Bedingungen geführt: Leben, Geschwindigkeit, Checkpoints an oder aus, Kollision an oder aus und der Bot.
Die Geschwindigkeit zählt auf die Hundertstel genau, so wie auf dem Bildschirm

Zen (0 Leben) zählt trotzdem Treffer: jede Kollision geht in seine Zahlen ein, nur die Leben und das Ende des Durchlaufs bleiben verschont

Ein Durchlauf schlägt den Rekord mit denselben Bedingungen, wenn er, in dieser Reihenfolge:

1. weiter gekommen ist
2. weniger Treffer kassiert hat
3. mit mehr Leben geendet hat
4. weniger Dashes gebraucht hat

Ein Rekord speichert auch den Seed des Durchlaufs und die Version des Levels zu diesem Zeitpunkt.
Die Version gehört nicht zu den Bedingungen. So bleibt ein Rekord, der vor der Überarbeitung des Levels aufgestellt wurde, sichtbar, mit der Version daneben

**Ein Durchlauf aus dem Editor zählt, stellt aber keine Rekorde auf.** Er erhöht Versuche, Tode und Treffer. Rekord, bester Fortschritt und erster Abschluss entstehen dabei nicht, weil das Level nur im Speicher existierte

## Schreiben, Löschen, Einfrieren

Das Spiel schreibt die Statistik alle 30 Sekunden. Und sofort am Ende eines Durchlaufs, bei einem Bildschirmwechsel und beim Beenden.
Ein Absturz kostet höchstens 30 Sekunden Daten

- **Löschen:** `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_other_cache-title}}`. Dort findest du `{{ui:settings_other_cache-orphan-statistics}}` und `{{ui:settings_other_cache-all-statistics}}`
- **Mit dem Level löschen:** beim Löschen eines Levels wird `{{ui:root_level-delete_statistics}}` angeboten
- **Einfrieren:** der anonyme Modus stoppt jedes Schreiben, bis das Spiel geschlossen wird, [[4_settings]]
- **Auf ein anderes Gerät mitnehmen:** exportiere das Profil und importiere es dort. Beim Zusammenführen bleibt bei jedem Zähler der größere Wert, [[14_profile-transfer]]

> [!warning] Warnung
> Ein von Hand kopierter Levelordner behält die ID des Levels. Original und Kopie teilen sich eine Statistikdatei
