---
title: Bots
date: 2026-10-02
tags: [player, advanced_player]
---

# Bots

Ein Bot spielt ein Level für dich mit deiner eigenen Steuerung. Er sieht, was kommt, sucht freien Platz und bewegt dieselbe Figur wie du: er läuft, dasht, nimmt Schaden und stirbt

**Ein Bot garantiert keinen Abschluss.** Er wird nicht müde, kann aber verlieren. Muss ein Muster schon eine Sekunde vor seiner Ankunft richtig angegangen werden, wird der Bot getroffen. Kaputt ist dann nichts

**Ein Bot belastet das Gerät.** Die Suche nach freiem Platz ist echte Arbeit in jedem Frame. Rechne auf einem schwachen Gerät mit Framedrops. In einem schweren Level sind die ersten Sekunden am schlimmsten

Einen Bot wählst du mit der Bedingung `{{ui:menu_levelview_options-bot}}` auf dem Levelbildschirm: `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}` oder `{{ui:enum_bot-kind_warm}}`. Er wird für jeden Durchlauf gewählt, wie Leben und Geschwindigkeit

> [!info] Gut zu wissen
> Ein Bot kann nicht schummeln, und das ist Bauweise, kein Versprechen. Er hat dieselbe Steuerung wie du und nichts darüber hinaus: dieselbe Geschwindigkeit, denselben Dash, dieselbe Hitbox, denselben Schaden. Er kommt durch nichts hindurch, durch das du nicht auch kämst

## Ein Level hat den Bot geschlagen?

Bots werden besser durch Levels, die sie noch nicht kennen. Ein solches Level lohnt sich zu schicken

Eröffne ein Issue in [bullet-hero/releases](https://github.com/bullet-hero/releases/issues). Schreib, welcher Bot wo verloren hat, und hänge den Levelordner an

## Zwei Bots

In jedem Frame gibt ein Bot eine Eingabe, genau wie eine Tastatur, und sonst nichts. Er hat keinen Zugriff auf die Position des Avatars, sein Leben oder den Zustand des Levels.
Antwortet der Bot in einem Frame nicht, steuert in diesem Frame dein Gerät

| | `{{ui:enum_bot-kind_reflex}}` | `{{ui:enum_bot-kind_warm}}` |
|---|---|---|
| Was er weiß | die nächsten 1,5 Sekunden, in jedem Frame neu berechnet | das ganze Level, einmal berechnet |
| Wann er das Gerät belastet | in jedem Frame, solange er läuft | einmal, vor dem Durchlauf |
| Was er kann | dem ausweichen, was er vor sich sieht | einem Plan folgen, den keine Vorausschau je finden würde |
| Was ihn aus dem Tritt bringt | ein Muster, das eine Sekunde früher hätte angegangen werden müssen | ein Level, das sich unter ihm geändert hat |
| Wie er steuert | per Richtung | per Ziel |

Der Warm-Bot zielt auf null Schaden. Er bezahlt das mit einer zusätzlichen Ladephase, `{{ui:root_loading_baking}}`. Sie kann Dutzende Sekunden dauern

Das `?` neben `{{ui:menu_levelview_options-bot}}` warnt vorab davor, mit einem Absatz pro Bot. `{{ui:root_loading_cancel}}` bricht die Berechnung ab und übergibt den Durchlauf dir.
Die Route des Warm-Bots hängt vom Seed ab, [[8_determinism]]

## Wo Bots sonst noch spielen

- **Der Testspieler des Editors**: `{{ui:settings_common_title}}` → `{{ui:settings_game-editor_title}}` → `{{ui:settings_game-editor-player_bot}}`. Dort spielt nur der Reflex-Bot: er braucht keine Vorbereitung und übersteht das Zurückspulen. Mehr - [[5_bot-playtest]]
- **Der Hintergrund des Hauptmenüs**: die Arena hinter den Schaltflächen ist ein Reflex-Bot, der live und ganz ohne Vorausschau spielt

Der Bot gehört zu den Bedingungen eines Rekords. Deshalb ersetzt ein Bot-Durchlauf nie dein bestes Ergebnis, [[10_statistics]]
