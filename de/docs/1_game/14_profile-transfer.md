---
title: Profilübertragung
date: 2026-10-02
tags: [player]
---

# Profilübertragung

Dein ganzes Profil passt in eine Zip-Datei: Levels, Statistik, Einstellungen und die Bibliothek. Exportiere es vor einer Neuinstallation oder einem Gerätewechsel und importiere es dort

Die Schaltflächen liegen unter `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_profile-transfer_title}}`. Das funktioniert unter Windows, Mac, Linux und Android. Unter iOS gibt es das nicht

## Was in die Datei kommt

| Teil | Im Datenordner | Standardmäßig angehakt |
|---|---|---|
| `{{ui:settings_profile-transfer_category-levels}}` | `levels` | ja |
| `{{ui:settings_profile-transfer_category-statistics}}` | `stats` | ja |
| `{{ui:settings_profile-transfer_category-settings}}` | `settings.json` | ja |
| `{{ui:settings_profile-transfer_category-library}}` | `resources` | ja |
| `{{ui:settings_profile-transfer_category-backups}}` | `backups` | nein |
| `{{ui:settings_profile-transfer_category-reports}}` | `reports` | nein |
| `{{ui:settings_profile-transfer_category-recordings}}` | `recordings` | nein |

Die Datei ist ein gewöhnliches Zip und öffnet sich in jedem Archivprogramm. Darin liegen dieselben Ordner wie im Datenordner ([[1_installation]]), dazu `profile.json`, das die Datei beschreibt

## Export

1. Drücke `{{ui:settings_profile-transfer_export}}`
2. Hake die Teile an, die du brauchst
3. Wähle, wo die Datei gespeichert wird

Der Export funktioniert überall, wo sich die Einstellungen öffnen: im Hauptmenü, in einem pausierten Durchlauf und im Editor. Die Statistik wird vorher auf die Festplatte geschrieben, die Datei ist also aktuell

## Import

1. Öffne die Einstellungen aus dem Hauptmenü und drücke `{{ui:settings_profile-transfer_import}}`
2. Wähle die Zip-Datei
3. Hake die Teile an und wähle den Modus
4. Bestätige

Der Import funktioniert nur aus dem Hauptmenü. Ein laufendes Level oder ein offener Editor hält seine Dateien fest, und sie lassen sich nicht unter ihm austauschen

| Modus | Was passiert |
|---|---|
| `{{ui:settings_profile-transfer_mode-replace}}` | jeder angehakte Teil wird geleert und aus der Datei gefüllt |
| `{{ui:settings_profile-transfer_mode-merge}}` | Levels werden hinzugefügt. Ein Level, das es auf beiden Seiten gibt, wird komplett durch die neuere Kopie ersetzt. Bei der Statistik bleibt bei jedem Zähler der größere Wert und der bessere Rekord. Bibliotheksdateien, automatische Speicherungen und Berichte werden nur hinzugefügt, deine bleiben |

Jeder Import fragt noch einmal nach, bevor er etwas schreibt. Ein Ersetzen nennt die Teile, die es leert, ein Zusammenführen sagt, wie viele Levels es hinzufügt, ersetzt und behält

**Einstellungen von einer anderen Geräteart.** Ein Profil vom Handy, das auf einem Computer importiert wird (oder umgekehrt), behält deine eigene Steuerung und Grafik. Alles andere kommt aus der Datei

Das Spiel lehnt eine Datei aus einer neueren Version des Spiels ab - aktualisiere zuerst das Spiel. Es lehnt auch eine Datei ab, die kein Zip ist, ein Zip, das kein Profil ist, ein passwortgeschütztes Zip und eine beschädigte Datei. In keinem dieser Fälle wird etwas geändert

## Sicherung

Vor jedem Import speichert das Spiel die Teile, die es gleich ersetzt, in eine Sicherung. Sie liegt im Ordner `profile-backups` im Datenordner. Es gibt nur eine: der nächste Import überschreibt sie

- `{{ui:settings_profile-transfer_backup-restore}}` spielt die Sicherung zurück. Was sie ersetzt, wird zur neuen Sicherung, also lässt sich auch eine Wiederherstellung rückgängig machen
- `{{ui:settings_profile-transfer_backup-save-as}}` speichert eine Kopie, wo du willst
- `{{ui:settings_profile-transfer_backup-delete}}` löscht sie
- `{{ui:settings_profile-transfer_clear-cache}}` löscht den ganzen Ordner `profile-backups`: die Sicherung und alles, was eine abgebrochene Übertragung zurückgelassen hat

`{{ui:settings_profile-transfer_backup-to-folder}}` ist bei einem Import standardmäßig angehakt: das Spiel fragt gleich, wo eine Kopie außerhalb des Spiels aufbewahrt werden soll

> [!caution] Vorsicht
> Unter Android liegt die Sicherung im Datenordner des Spiels und wird zusammen mit dem Spiel gelöscht. Exportiere vor der Deinstallation das Profil oder speichere die Sicherung woanders

Schließt sich das Spiel mitten in einem Import, stellt der nächste Start das Profil so wieder her, wie es war

## Wechsel zwischen Builds unter Android

Eine aus einer Datei installierte Kopie des Spiels (itch.io und Ähnliches) lässt sich nicht über Google Play aktualisieren, und umgekehrt. Die Builds sind unterschiedlich signiert, deshalb lehnt Android das Update ab. So wechselst du:

1. Exportiere das Profil und speichere die Datei außerhalb des Spiels
2. Deinstalliere das Spiel
3. Installiere den anderen Build
4. Importiere das Profil
