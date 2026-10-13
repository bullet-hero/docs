---
title: Installation
date: 2026-10-14
tags: [player]
---

# Installation

Das Spiel speichert Levels, Einstellungen und Statistik in einem Datenordner. Updates sind sicher: eine neue Version liest alle alten Daten. Unter Android löscht die Deinstallation auch die Levels

Hier herunterladen - [[download]]

## Wo deine Dateien liegen

| System | Ordner |
|---|---|
| Windows | `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` |
| Android | `/storage/emulated/0/Android/data/com.vertoker.BulletHero/files` |

Am schnellsten öffnest du ihn aus dem Spiel: `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general-open_folder}}`

Was darin liegt:

| Ordner | Inhalt |
|---|---|
| `levels` | deine Levels, jedes in einem eigenen Ordner |
| `backups` | die automatischen Speicherungen des Editors |
| `stats` | Statistik |
| `settings.json` | Einstellungen |
| `reports` | Fehlerberichte |

## Deinstallieren

Unter Windows, Linux und Mac liegt bei der kostenlosen Version ein Deinstallationsprogramm neben dem Spiel: `unins000.exe` unter Windows, `unins000` unter Linux und `unins000` neben `Bullet Hero.app` auf dem Mac. Starte es, und es entfernt das Spiel von selbst, ohne eine einzige Rückfrage. Deine Levels, Einstellungen und Statistik bleiben im Datenordner

Es entfernt nur die eigenen Dateien des Spiels. Alles, was du selbst in den Ordner des Spiels gelegt hast, bleibt, und der Ordner verschwindet erst, wenn er leer ist. Läuft das Spiel, schließt das Deinstallationsprogramm es zuerst, so wie seine Schließen-Schaltfläche, und den MCP-Server der KI gleich mit. Ein Level mit ungespeicherten Änderungen verliert sie, also speichere es vor der Deinstallation

Mit dem Windows-Installer installiert, wird das Spiel wie jedes andere Programm entfernt, in den Windows-Einstellungen unter Apps

Eine Store-Version entfernt ihr Store

## Aktualisieren

Eine neue Version des Spiels liest alle alten Daten problemlos, egal welches Update und egal was sich geändert hat

Eine alte Version öffnet keine Levels aus einer neueren. Wenn das Spiel dich zum Aktualisieren auffordert, aktualisiere es

In der Google-Play- und der RuStore-Version bietet das Hauptmenü ein neues Update an, und es lädt im Hintergrund. Ist es bereit, zeigt das Hauptmenü `{{ui:menu_update-ready_text}}` - tippe auf `{{ui:menu_update-ready_install-btn}}`. Nach einem geschafften Level kann sie dich bitten, das Spiel zu bewerten

> [!caution] Vorsicht
> Unter Android löscht die Deinstallation des Spiels auch alle deine Levels. Exportiere vor der Deinstallation das Profil - [[14_profile-transfer]]
