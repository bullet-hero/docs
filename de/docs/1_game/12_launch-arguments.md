---
title: Startargumente
date: 2026-10-15
tags: [advanced_player, developer]
---

# Startargumente

Startargumente öffnen sofort einen Bildschirm, ein Level oder einen Durchlauf, Schalter ändern einen einzelnen Start. Sie folgen auf die ausführbare Datei: in Verknüpfung, Terminal oder Steam

Ohne Argumente öffnet das Spiel das Hauptmenü

Ein über MCP verbundener KI-Assistent kann dieselben Argumente an ein bereits laufendes Spiel senden - [[7_ai-assistant]]

## Syntax

- jedes Argument beginnt mit zwei Bindestrichen: `--editor`
- ein Wert folgt nach einem Leerzeichen oder nach `=`: `--speed 1.5` und `--speed=1.5` sind dasselbe
- Groß- und Kleinschreibung des Schlüssels spielt keine Rolle: `--Editor` funktioniert auch
- Zahlen schreibt man mit Punkt, egal welche Systemsprache: `1.5`, nie `1,5`
- ein Wert mit Leerzeichen steht in doppelten Anführungszeichen: `--level "D:\My Levels\Volcano"`

**Ein Argument, mit dem das Spiel nichts anfangen kann, stoppt den Start nie.** Es wird verworfen, eine Zeile dazu landet im Log, und das Spiel öffnet seinen gewohnten Bildschirm. Wo das Log liegt - [[11_help#Logs]]

**Unbekannte Argumente werden ignoriert.** Das Spiel liest nur seine eigenen Argumente, die mit zwei Bindestrichen. Die eigenen Argumente von Unity mit einem Bindestrich, zum Beispiel `-screen-width`, gehen unangetastet durch. Damit stellst du Auflösung und Vollbild ein

## Bildschirme

| Argument | Was sich öffnet |
|---|---|
| `--menu` | das Hauptmenü, wie ohne Argumente |
| `--editor` | der Leveleditor |
| `--game` | das in `--level` angegebene Level, und der Durchlauf startet sofort |
| `--settings` | das Hauptmenü mit dem Einstellungsbildschirm darüber |

Es wird höchstens ein Bildschirmargument übergeben. Zwei verschiedene heben sich gegenseitig auf, und das Menü öffnet sich mit einer Warnung im Log

`--settings` kann einen Tab nennen: `general`, `audio`, `controls`, `keybindings`, `graphics`, `interface`, `game-editor`, `profile`, `other`. Ohne Namen öffnen sich die Einstellungen auf dem Tab, auf dem du zuletzt warst. Ein unbekannter Name wird verworfen, und die Einstellungen öffnen sich trotzdem

Die Einstellungen öffnen sich einmal pro Start. Kehrst du später ins Menü zurück, öffnen sie sich nicht erneut. Was jeder Tab enthält - [[4_settings]]

## Ein Level wählen

`--level` nennt ein Level über seine Kennung (`LevelId`) oder über den Pfad zu seinem Ordner. Ein Titel funktioniert nie: Titel wiederholen sich, werden übersetzt und bearbeitet. Ein Wert, der sich als Kennung lesen lässt, wird immer als Kennung genommen

Das Level wird unter denen gesucht, die das Spiel bereits in seiner Liste zeigt. Einen Ordner, der nicht in der Liste steht, findet das Spiel nicht

| Zusammen mit | Was passiert |
|---|---|
| nichts | das Menü öffnet sich auf dem Levelbildschirm und wartet auf `{{ui:menu_levelview_play-btn}}` |
| `--editor` | der Editor öffnet sich mit diesem Level |
| `--game` | der Durchlauf startet sofort |

Ein Passwort wird nie als Argument übergeben. Ein geschütztes Level fragt auf dem Bildschirm danach und öffnet sich nach der Antwort

## Bedingungen des Durchlaufs

Diese Bedingungen füllen die Steuerelemente des Levelbildschirms aus, und der Durchlauf startet, als hättest du `{{ui:menu_levelview_play-btn}}` gedrückt. Sie wirken nur zusammen mit `--game`. Ohne es werden sie ignoriert, mit einer Warnung im Log

| Argument | Wert | Steuerelement auf dem Levelbildschirm |
|---|---|---|
| `--speed` | über `0` und bis `2`, auf `0.1` gerundet | `{{ui:field_common_speed}}` |
| `--lives` | von `0` bis `16`, `0` ist `{{ui:menu_levelview_options-lifes_option-zen}}` | `{{ui:menu_levelview_options-lifes_title}}` |
| `--seed` | `0` oder eine positive ganze Zahl, `0` bedeutet einen neuen Seed bei jedem Durchlauf | `{{ui:level_level-view_seed-value}}` |
| `--bot` | `none`, `reflex`, `warm` | `{{ui:menu_levelview_options-bot}}` |
| `--checkpoints`, `--no-checkpoints` | - | `{{ui:menu_levelview_options-checkpoints_title}}` |
| `--no-collision` | - | `{{ui:menu_levelview_options-no-collision_title}}` |

Eine weggelassene Bedingung nimmt ihren Standardwert: 3 Leben, Geschwindigkeit `1.0`, Checkpoints an, kein Bot, Seed `0`, Kollision an

Ein so gestarteter Durchlauf ist ein gewöhnlicher Durchlauf. Er geht in die Statistik ein wie jeder andere, [[10_statistics]]

## Schalter für den ganzen Start

Diese drei funktionieren mit jedem Bildschirm und ändern nie eine gespeicherte Einstellung:

| Argument | Was es tut |
|---|---|
| `--autosave on`, `--autosave off` | schaltet das Autospeichern des Editors für diesen Start ein oder aus. Der Einstellungstab `{{ui:settings_game-editor_title}}` zeigt den erzwungenen Wert und lässt ihn nicht ändern |
| `--suppress-game-saves` | anonymer Modus für den ganzen Start. Im Spiel lässt er sich nicht ausschalten, [[4_settings#Anonymer Modus]] |
| `--frame-stats` | schreibt eine Zusammenfassung der Frame-Zeiten ins Log, mit GPU- und CPU-Zeit. Dient für Leistungsmessungen |
| `--frame-stats-windows` | schreibt, während ein Level läuft, zusätzlich alle {{v:performance.window-hop-seconds}} s Spielzeit eine Zeile: den Level-Frame und den Median der CPU- und GPU-Zeit. Schaltet auch `--frame-stats` ein. Dient zur Prüfung der [[17_performance-rating]] |

`--frame-stats` schreibt alle 30 Sekunden eine Zeile pro Bildschirm, und außerdem jedes Mal, wenn das Fenster über dem Bildschirm wechselt. Die ersten 3 Sekunden eines Bildschirms werden nicht gezählt

## Kombinationen

| Befehl | Ergebnis |
|---|---|
| nichts oder `--menu` | Menü |
| `--editor` | der Editor ohne geöffnetes Level |
| `--settings` | Menü, Einstellungen offen auf dem Tab, auf dem du zuletzt warst |
| `--settings graphics` | dasselbe, auf dem Tab `{{ui:settings_graphics_title}}` |
| `--level X` | Menü auf dem Bildschirm von Level X, wartet auf `{{ui:menu_levelview_play-btn}}` |
| `--level X --game` | Level X, ein laufender Durchlauf |
| `--level X --editor` | der Editor mit geöffnetem Level X |
| `--game` ohne `--level` | Menü und eine Warnung |
| `--menu --editor` | Menü und eine Warnung |
| `--speed 2` ohne `--game` | die Bedingung wird ignoriert, mit einer Warnung |
| `--editor --autosave off` | der Editor, Autospeichern nur für diesen Start aus |
| `--autosave maybe` | mit einer Warnung ignoriert, deine Einstellung entscheidet |
| `--suppress-game-saves` | Menü. Keine der eigenen Speicherungen des Spiels aus diesem Start erreicht die Festplatte |
| `--level X --game --suppress-game-saves` | Level X, ein laufender Durchlauf, und danach bleibt keine Statistik zurück |
| `--editor --suppress-game-saves` | der Editor. Levelspeicherungen, automatische Speicherung und Sicherungen werden geschrieben, Einstellungen und Statistik nicht |

## Beispiele

Unter Windows, aus einem Terminal oder einer Verknüpfung:

```bash
"Bullet Hero.exe" --editor
"Bullet Hero.exe" --level 5f2b0e6a-1c3d-4b5e-8a9f-0d1e2f3a4b5c --game --lives 1 --speed 1.5
"Bullet Hero.exe" --level "C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero\levels\Volcano" --editor
```

In Steam nehmen die Startoptionen des Spiels nur die Argumente, ohne die ausführbare Datei: `--editor --autosave off`

## Android

Android hat keine Kommandozeile. Die Argumente werden im String-Extra `bh` des Intents übergeben, der das Spiel startet, und genau wie eine getippte Zeile zerlegt. Vom Computer aus geht das mit `adb`:

```bash
adb shell "am start -S -n com.vertoker.BulletHero/com.unity3d.player.UnityPlayerGameActivity -e bh '--frame-stats --editor'"
```

- **Die Anführungszeichen sind wichtig.** Das ganze `am start` steht in doppelten Anführungszeichen, der Wert von `bh` in einfachen. Sonst zerlegt die Shell des Geräts die Zeile: nur das erste Argument erreicht `bh`, und der Rest geht als eigene Parameter an `am`
- **`-S` beendet zuerst das laufende Spiel.** Die Argumente werden einmal gelesen, beim Start. Sie an ein bereits laufendes Spiel zu senden, ändert nichts

iOS hat überhaupt keine Startargumente
