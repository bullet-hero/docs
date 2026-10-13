---
title: Steuerung
date: 2026-10-02
tags: [player]
---

# Steuerung

Du kannst mit Maus, Touchscreen, Gamepad oder Bewegungssensor spielen. Mit der Maus steuert die gehaltene linke Taste den Avatar, und Leertaste, Shift oder die rechte Taste lösen den Dash aus

Die Eingabe wird in den Steuerungseinstellungen neu belegt, Gamepad-Tasten nicht

Die Steuerung Schritt für Schritt lernen oder jeden Modus ausprobieren, ohne ein Level zu starten - [[13_sandbox]]

## Geräte

Die ganze Steuerung wird unter `{{ui:settings_common_title}}` → `{{ui:settings_controls_title}}` eingestellt, eine Gruppe pro Gerät

| Gerät | Standardmodus | Bewegen | Dash |
|---|---|---|---|
| `{{ui:enum_control-device_keyboard-mouse}}` | `{{ui:enum_control-mode_absolute}}` | linke Taste halten, der Avatar folgt der Maus | `Space`, `Shift`, die rechte Maustaste oder ein Doppelklick (0,3 s) |
| `{{ui:enum_control-device_touchscreen}}` | `{{ui:enum_control-mode_relative}}` | einen Finger irgendwo über den Bildschirm ziehen | ein zweiter Finger |
| `{{ui:enum_control-device_gamepad}}` | `{{ui:field_common_direction}}` | einer der beiden Sticks | jede Taste außer `Start` und `Select` |
| `{{ui:enum_control-device_device-gyro}}` | `{{ui:field_common_direction}}` | das Gerät aus der Waagerechten kippen, volle Geschwindigkeit bei 20° | ein Tippen irgendwo auf den Bildschirm |

Die Maus allein reicht: die linke Taste steuert den Avatar, `{{ui:settings_controls-keyboard-mouse_km-dash-button}}` löst den Dash aus. Die Tastatur ist optional

Am Gamepad pausiert `Start` das Spiel und setzt es fort. Gamepad-Tasten werden nicht neu belegt: im Spiel löst jede Taste außer `Start` und `Select` den Dash aus, auch die rechte Aktionstaste. Im Pausenmenü wirkt die rechte Aktionstaste als "zurück", wie in jedem Menü

## Steuerungsmodi

| Modus | Was deine Eingabe bedeutet |
|---|---|
| `{{ui:enum_control-mode_absolute}}` | eine Position. Der Cursor springt dorthin, der Avatar holt ihn ein |
| `{{ui:enum_control-mode_relative}}` | eine Bewegung. Der Cursor summiert sie auf, der Avatar holt den Cursor ein |
| `{{ui:field_common_direction}}` | eine Richtung. Einen Cursor gibt es gar nicht |

Die Bewegung ist in jedem Modus sofort: keine Beschleunigung und kein Rutschen

In den Cursor-Modi holt der Avatar den Cursor mit seiner eigenen Laufgeschwindigkeit ein. Deshalb hängt er einer schnellen Maus hinterher.
Ein Dash geht in Richtung Cursor. Ist der Cursor nah, wird der Dash kürzer und endet genau auf ihm

Was passiert, wenn du die Steuertaste loslässt oder den Finger hebst, entscheidet ein Kontrollkästchen - `{{ui:settings_controls-keyboard-mouse_km-cursor-return}}` für die Maus, `{{ui:settings_controls-touchscreen_touch-cursor-return}}` für den Touchscreen:

- an - der Avatar bleibt stehen, wo er ist, der Cursor kehrt zu ihm zurück. Das ist der Standard für die Maus
- aus - der Cursor bleibt, wo du ihn gelassen hast, und der Avatar läuft zu ihm. Nur Schaden kann den Cursor verschieben. Das ist der Standard für den Touchscreen

Im Modus `{{ui:field_common_direction}}` gibt ein halb gedrückter Stick halbe Geschwindigkeit. Ein Dash geht immer seine volle Länge

Auf dem Touchscreen im Modus `{{ui:enum_control-mode_absolute}}` sitzt der Cursor über deinem Finger (`{{ui:settings_controls-touchscreen_touch-finger-offset-y}}`). So verdeckt der Finger den Avatar nicht

Während ein Finger den Avatar steuert, löst ein zweiter Finger den Dash aus, wo immer er landet - auch auf einem Bereich oder einer Schaltfläche. Die Oberfläche bekommt diese Berührung nicht, also drückt ein Dash nie versehentlich etwas

Die genauen Zahlen - [[6_avatar]]

## Bewegungssensor

Der Bewegungssensor hat keine Kalibrierung. Der Avatar steht still, wenn das Handy flach liegt, Bildschirm nach oben

- kippe die rechte Kante nach unten, und der Avatar geht nach rechts
- kippe die obere Kante nach unten, und er geht nach oben
- `{{ui:settings_controls-device_sensitivity}}` 1 gibt volle Geschwindigkeit bei 20°. Bei 2 reicht die halbe Neigung

Der Sensor folgt dem Bildschirm: drehst du das Handy ins Querformat und zurück, bleibt rechts rechts.
Der Sensor hat zwei Modi, `{{ui:enum_control-mode_absolute}}` und `{{ui:field_common_direction}}`

## Neu belegen

- **Die Spieleingabe** liegt unter `{{ui:settings_controls_title}}`: der Modus, `{{ui:settings_controls-keyboard-mouse_dash-keys}}`, `{{ui:settings_controls-keyboard-mouse_km-dash-button}}`, Empfindlichkeit, Totzone, Glättung, Invertierung, der Bildschirm-Joystick und die Dash-Schaltfläche. `{{ui:settings_controls_reset}}` setzt jedes Gerät auf die Standardwerte dieser Plattform zurück
- **Tastenkürzel** liegen unter `{{ui:settings_keybindings_label}}`. Fast alle gehören zum Editor. Außerhalb des Editors gibt es `{{ui:settings_keybindings_window_toggle_fullscreen}}` (standardmäßig `F11`), `{{ui:settings_keybindings_window_settings_save}}` (`Ctrl+S`, während die Einstellungen offen sind) und die Navigationstasten. `{{ui:settings_keybindings_reset}}` macht jede Neubelegung rückgängig

Wenn das Spiel auf eine Taste wartet, zeigt es `Drücke eine Taste für "..."`.
Dann gilt die Regel `{{ui:settings_escape-cancels_backspace}}`

Bei Tasten speichert das Spiel nur, was du neu belegt hast. Wird eine Standardbelegung später besser, kommt sie bei dir an, außer du hast genau diese Belegung selbst geändert. Der Tab `{{ui:settings_controls_title}}` wird vollständig gespeichert, neue Standardwerte dafür kommen also nicht bei dir an

Die Tastenkürzel des Editors - [[3_speed-and-shortcuts]]

## Mehrere Geräte gleichzeitig

Ein Gerät steuert den Avatar - das, das du zuletzt benutzt hast.
Der Wechsel passiert von selbst, im selben Frame, ganz ohne Menü

Das Spiel fragt jedes aktive Gerät in jedem Frame ab. Ein unberührtes Gamepad sendet Nullen, und das zählt nicht als Benutzung

Im ersten Frame wurde noch nichts benutzt, also entscheidet die Plattform: die Maus am Computer, der Touchscreen am Handy

Dash und Pause funktionieren von jedem aktiven Gerät aus, egal welches gerade steuert. Eine Gamepad-Taste löst den Dash aus, während die Maus steuert. Ein Dash allein übernimmt die Steuerung nicht

Ein Gerät kann den Avatar nur steuern, wenn:

- es als aktiv markiert ist
- die Plattform es unterstützt
- es gerade verbunden ist

`{{ui:settings_controls-active_now}}` oben zeigt, welches gerade steuert

> [!tip] Tipp
> Ein Steuerungsschema scheint nichts zu tun? Meist wurde danach ein anderes Gerät berührt. Schau zuerst auf `{{ui:settings_controls-active_now}}`
