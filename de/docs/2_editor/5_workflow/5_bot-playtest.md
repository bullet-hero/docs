---
title: Wie ein Bot dein Level spielt
date: 2026-10-02
tags: [level_author]
---

# Wie ein Bot dein Level spielt

Ein Bot spielt das Level mit derselben Steuerung wie du und prüft Lesbarkeit, nicht Schwierigkeit. Er garantiert nicht, dass das Level schaffbar ist

Er beobachtet, was fliegt, sucht freien Raum und bewegt dieselbe Figur wie du.
Er läuft, macht Dashes, nimmt Schaden und stirbt

Der Bot wird vor dem Start eines Levels gewählt, neben Leben und Geschwindigkeit

## Ein Bot im Editor

Im Editor steuert ein Bot den Vorschauspieler:
1. Öffne `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_player_title}}`
2. Setz den Haken bei `{{ui:settings_game-editor-player_bot}}`
3. Schalte den Vorschauspieler in der Werkzeugleiste ein

Beim Vorschauspieler gibt es keine Wahl des Bots, es ist immer `{{ui:enum_bot-kind_reflex}}`. Nur dieser Bot braucht nichts im Voraus vorbereitet.
Er arbeitet weiter, während du das Level bearbeitest, bei jeder Wiedergabegeschwindigkeit, auch rückwärts

Direkt nach dem Ziehen des Abspielkopfs spielt der Bot einen Moment lang schlechter: Er lernt neu, was vor ihm liegt

Während du einen Gizmo-Griff ziehst oder in ein Textfeld tippst, hört der Vorschauspieler nicht auf deine Steuerung

**`{{ui:settings_game-editor-player_bot-debug}}`** in denselben Einstellungen zeichnet über das Level. Es ist standardmäßig aus, und seine drei Teile sind an, sodass du nach dem Einschalten sofort das ganze Bild siehst:
- `{{ui:settings_game-editor-player_bot-debug-grid}}` - wie viel freien Raum jeder Teil des Bildschirms nach Ansicht des Bots hat. Rot ist, wo er einen Treffer erwartet, und die Farbe verblasst, je mehr Raum da ist. Wo er sich sicher fühlt, wird nichts gezeichnet
- `{{ui:settings_game-editor-player_bot-debug-target}}` - der Punkt, den er ansteuert. Ein Ziel, das sich nicht bewegt, heißt, dass der Bot zufrieden ist, nicht festhängt
- `{{ui:settings_game-editor-player_bot-debug-reach}}` - wie weit er zu kommen erwartet: der innere Ring zu Fuß, der äußere mit einem Dash. Er wählt nie ein Ziel außerhalb davon

Gezeichnet wird nur `{{ui:enum_bot-kind_reflex}}`. Schalte es bei pausierter Wiedergabe ein, dann steht das Bild still

**Ein voller Durchlauf mit jedem Bot.** In den Leveleinstellungen gibt es im Tab `{{ui:settings_level-settings_play}}` dieselbe Liste `{{ui:settings_level-settings_bot}}` wie auf dem Levelbildschirm im Menü: `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}`, `{{ui:enum_bot-kind_warm}}`. Das startet einen echten Durchlauf des Levels, nicht den Vorschauspieler

## Das Ergebnis lesen

Ein Bot prüft Lesbarkeit, nicht Schwierigkeit:
- der Bot schafft einen Abschnitt, der für dich schwer ist, ganz ruhig. Dann ist der Abschnitt gut lesbar, und dir fehlt Übung
- der Bot wird immer wieder an derselben Stelle getroffen. Schau dir diese Stelle an: Meistens ist es eine Gefahr, die keinen Raum zum Ausweichen lässt. Ein Mensch liest sie auch nicht besser

## Was ein Bot verspricht und was nicht

**Ein Bot garantiert nicht, dass das Level schaffbar ist.** Er ist ein Spieler, der nicht müde wird, kein Spieler, der nicht verliert.
Verlangt ein Abschnitt, eine Sekunde vorher richtig in ein Muster einzusteigen, wird der Bot getroffen. Das ist kein Fehler

> [!info] Gut zu wissen
> Ein Bot kann nicht schummeln, so ist er gebaut. Er hat dieselbe Steuerung wie ein Spieler und nicht mehr: dieselbe Geschwindigkeit, denselben Dash, dieselbe Hitbox, denselben Schaden. Wo ein Spieler nicht durchkommt, kommt auch der Bot nicht durch

**Ein Bot belastet das Gerät.** Er sucht in jedem Frame nach freiem Raum.
Auf einem schwachen Gerät ist mit Framedrops zu rechnen. Bei einem schweren Level sind die ersten Sekunden am schlimmsten

## Ein Level, das den Bot besiegt hat

Bots werden nur an Levels besser, die sie noch nicht kennen. Levels, die ein Bot schon schafft, bringen ihm nichts bei

Hat dein Level den Bot besiegt? Schick es ein:
1. Öffne ein Issue in [bullet-hero/releases](https://github.com/bullet-hero/releases/issues)
2. Schreib, welcher Bot wo verloren hat
3. Häng den Levelordner an

Weiter: [[1_readability-and-fairness|Lesbarkeit und Fairness]], [[3_difficulty-curve|Schwierigkeit]]
