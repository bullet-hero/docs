---
title: Hilfe und Fehlerberichte
date: 2026-10-02
tags: [player, level_author]
---

# Hilfe und Fehlerberichte

Fehler im Spiel gehören in die Issues von releases, Fragen in den Discord. Gib die Versionszeile aus den Einstellungen an und die Schritte, nach denen der Fehler auftritt

Schau zuerst in [[5_troubleshooting]]. Ein fehlendes Level, "das Spiel braucht ein Update" und ein abgelehntes Archiv sind dort beschrieben

## Wohin schreiben

| Was | Wohin |
|---|---|
| ein Fehler im Spiel oder im Editor, ein Wunsch für das Spiel | [bullet-hero/releases](https://github.com/bullet-hero/releases/issues) |
| ein Fehler im SDK oder seinem Code | [bullet-hero/sdk](https://github.com/bullet-hero/sdk/issues) |
| ein Fehler oder eine veraltete Angabe in der Dokumentation | [bullet-hero/docs](https://github.com/bullet-hero/docs), [[community]] |
| eine Frage, Hilfe bei einem Level, eine Diskussion | [Discord](https://discord.gg/gkHQrp9NgS) |

Nachrichten auf GitHub sind öffentlich. Jeder kann sie lesen und ergänzen.
Für die Dokumentation kannst du ein Issue oder einen Pull Request schicken

Nicht sicher, ob es ein Fehler ist? Frag zuerst im Discord

Alle Links des Projekts - [[links]]

## Was in einen Fehlerbericht gehört

Ein Fehler, der sich reproduzieren lässt, wird behoben. "Es ist abgestürzt" lässt sich meist nicht beheben: niemand weiß, was er wiederholen soll

1. **Die Versionszeile.** Klicke auf dem Einstellungsbildschirm auf die Versionszeile, und sie wird von selbst kopiert. Sie sieht so aus: `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`, [[4_settings]]
2. **Plattform und Gerät:** das System und bei einem Handy das Modell
3. **Schritte:** was du getan hast, was du erwartet hast und was passiert ist
4. **Das Level,** wenn der Fehler daran hängt: sein Ordner als Archiv oder das Archiv, das du geöffnet hast. Ist das Level geschützt, sag das dazu
5. **Der Fehlerbericht,** wenn es ein Fehlerfenster gab. `{{ui:root_error_save}}` schreibt ihn in den Ordner `reports`, `{{ui:root_error_open-reports-folder}}` öffnet ihn, [[1_installation]]

> [!tip] Tipp
> Hänge Dateien an die Nachricht an, statt sie in den Text einzufügen. Ein Log ist lang und im Text schwer zu lesen

## Logs

Das Spiel schreibt während des Laufs ein Log. Es hilft, wenn es gar kein Fehlerfenster gab

- **Windows:** `Player.log` im Datenordner des Spiels, `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` (der Standardort von Unity)
- **Android:** das Log geht an logcat. Ist das Gerät mit einem Computer verbunden, gibt `adb logcat -s Unity` es aus
- **Andere Systeme:** noch nicht beschrieben
