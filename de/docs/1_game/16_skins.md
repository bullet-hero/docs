---
title: Skins
date: 2026-10-15
tags: [player, advanced_player]
---

# Skins

Der Körper des Avatars ist ein Raster aus Zellen, und ein Skin legt fest, was jede Zelle zeichnet: eine Form und eine der Farben des Skins. Ein Skin kann außerdem die Augen, die Hände, den Schatten und die Effekte ausschalten. Stelle einen im Hauptmenü unter `{{ui:menu_main_avatar-btn}}` aus fertigen Formen, einer Palette und einem Raster-Editor zusammen oder schreibe die Datei von Hand

Ein Skin ändert nur das Aussehen. Hitbox, Geschwindigkeit und Hitbox-Ring sind bei jedem Skin gleich

## Der Avatar-Hub

`{{ui:menu_main_avatar-btn}}` im Hauptmenü öffnet einen eigenen Bildschirm. Links läuft dein Avatar, die rechte Hälfte nimmt das Panel ein. `{{ui:menu_avatar_bot}}` unten links übergibt dir den Avatar, damit du den Skin in Bewegung ausprobieren kannst, und der Regler `{{ui:menu_avatar_damage}}` daneben zeigt, wie der Skin Zellen verliert, wenn das Leben sinkt. Die Leiste oben im Panel springt zu jedem Abschnitt:

| Abschnitt | Was er tut |
|---|---|
| `{{ui:menu_avatar_tab-shapes}}` | fertige Formen, gezeichnet mit den Augen und Händen, die zu ihnen gehören. Ein Klick setzt die Form auf deinen Skin und behält deine Farben. Die runden und die Vieleck-Formen haben Augen, die gemusterten nicht. Die erste Karte ist der klassische Avatar: er wird als Ganzes getragen, samt Farben |
| `{{ui:menu_avatar_tab-colors}}` | die Körperfarben und die Augen. Wähle ein Ziel, dann eine Farbe. Hände, Spuren und die Dash-Tönung folgen deinen Farben von selbst |
| `{{ui:menu_avatar_elements}}` | jede Schaltfläche schaltet einen Teil des Avatars ein oder aus |
| `{{ui:menu_avatar_editor}}` | das Raster selbst: seine Größe, die Teile in seinen Zellen, Form, Farbe, Drehung, Spiegelung und Skalierung jedes Teils und eigene Formen |

`{{ui:menu_avatar_randomize}}` oben rechts gibt deinem Skin eine zufällige Form und zufällige Farben. Solange der klassische Avatar getragen wird, ist die Schaltfläche aus. `{{ui:menu_avatar_tab-skins}}` daneben listet deine Skin-Dateien auf: ein Klick auf eine Datei zieht den Skin an, und die Schaltflächen exportieren, löschen, importieren und duplizieren. `{{ui:menu_avatar_create}}` erstellt einen neuen Skin aus einer zufälligen Form in zufälligen Farben. Eine Datei, die das Spiel nicht lesen kann, lässt sich dort trotzdem löschen

Jede Änderung wird sofort gespeichert. Die erste Änderung am klassischen Avatar legt eine neue Skin-Datei an, und ab dann trägst du diese Datei

### Der Editor

1. `{{ui:menu_avatar_paint}}` setzt das gewählte Teil in eine Zelle, `{{ui:menu_avatar_erase}}` leert sie. Ziehe über das Raster, um mehrere Zellen auf einmal zu bearbeiten
2. `{{ui:menu_avatar_pieces}}` listet auf, was die Zellen zeichnen können. `+` kopiert das gewählte Teil, `-` entfernt es, und seine Zellen bekommen das erste Teil
3. Das gewählte Teil nimmt eine eingebaute Form oder eine eigene Form des Skins. `{{ui:menu_avatar_new-mesh}}` zeichnet eine neue: setze Punkte und verbinde dann drei davon zu einem Dreieck
4. `{{ui:menu_avatar_columns}}` und `{{ui:menu_avatar_rows}}` ändern die Größe des Rasters. Die Zellen sind quadratisch, also ergibt ein Raster, das höher als breit ist, einen hohen Körper
5. `{{ui:menu_avatar_rotate-left}}` und `{{ui:menu_avatar_rotate-right}}` drehen den ganzen Skin um eine Vierteldrehung: das Raster und jedes Teil mit ihm

Die Oberseite eines Skins ist seine Vorderseite: der Avatar dreht sich so, dass sie dorthin zeigt, wohin er sich bewegt

Eine Änderung, die den Körper kaputt macht (zu wenige Zellen oder Zellen in zwei Stücken), wird nicht gespeichert. Der Grund steht unter dem Raster, bis du ihn behebst

## Wo Skins liegen

Im Ordner `skins` im Datenordner ([[1_installation]]). Ein Skin ist eine `.json`-Datei. `selection.json` daneben merkt sich, welchen Skin du trägst

- am Computer öffnet `{{ui:menu_avatar_open-folder}}` den Ordner
- am Handy nutze `{{ui:menu_avatar_import}}` und `{{ui:menu_avatar_export}}`: sie öffnen die Dateiauswahl des Systems

Skins wandern mit der Profilübertragung und mit Steam Cloud mit - [[14_profile-transfer]]

## Die Datei

So sieht ein exportierter Skin aus, gekürzt:

```json
{"g":3,"v":{
  "id":"9b2f0d64-1c3a-4e8b-8f21-6a0c5d7e9f13",
  "name":"Hex knight",
  "size":1.0,
  "columns":5,"rows":5,
  "mask":60651675406,
  "cells":[0,0,0,0,1,1,1,0,0,1,2,1,0,0,1,1,1,0,0,0,0],
  "parts":[
    {"shape":"00000000-0000-0000-0000-000000016000","color":0},
    {"shape":"00000000-0000-0000-0000-000000001000","color":1,"scale":0.9},
    {"shape":"4d1f6c2a-7b3e-4f10-9a55-2c8e01b7d001","color":2,"rotation":90.0,"mirror":true}
  ],
  "colors":[[0,{"r":0.51,"g":0.76,"b":0.96,"a":1.0}],[0,{"r":0.2,"g":0.4,"b":0.9,"a":1.0}],[0,{"r":1.0,"g":1.0,"b":1.0,"a":1.0}]],
  "meshes":[{"id":"4d1f6c2a-7b3e-4f10-9a55-2c8e01b7d001","vts":[[0,{"x":-0.5,"y":-0.5}],[0,{"x":0.5,"y":-0.5}],[0,{"x":0.0,"y":0.5}]],"idxs":[0,1,2]}],
  "elements":125
}}
```

`g` ist die Generation des Dateiformats, `v` enthält den Skin. Am einfachsten exportierst du einen Skin und bearbeitest die Kopie

| Schlüssel | Was es ist |
|---|---|
| `id` | wer der Skin ist: eine eigene GUID. Das Spiel benennt die Datei danach, findet einen Skin aber über diesen Schlüssel, deshalb spielt der Dateiname keine Rolle |
| `name` | der Name in der Liste |
| `size` | wie groß der Körper gezeichnet wird, von `{{v:skin.size-min}}` bis `{{v:skin.size-max}}` des klassischen. Die Hitbox ändert sich nicht |
| `columns`, `rows` | Breite und Höhe des Rasters, von `{{v:skin.grid-min}}` bis `{{v:skin.grid-max}}`. Die Zellen sind quadratisch: die längere Seite füllt den ganzen Körper |
| `mask` | welche Zellen gefüllt sind, als eine 64-Bit-Zahl: die Zelle in Spalte `x` und Zeile `y` ist Bit `y * 8 + x`, Zeile 0 unten. Eine Zeile ist immer 8 Bit breit, egal was `columns` sagt |
| `cells` | das Teil, das jede gefüllte Zelle zeichnet, als Index in `parts`, in der Reihenfolge der Bits vom niedrigsten an. Bleibt es leer, zeichnet jede Zelle Teil 0 |
| `parts` | was eine Zelle zeichnet: `shape` (die ID einer eingebauten Form oder die `id` einer der `meshes` des Skins), `color` (ein Index in `colors`), `rotation` (Grad), `mirror` und `scale` (von `{{v:skin.part-scale-min}}` bis `{{v:skin.part-scale-max}}` der Zelle) |
| `colors` | die Körperfarben, von 1 bis `{{v:skin.colors-max}}`. Eine Farbe wird als `[0,{"r":…,"g":…,"b":…,"a":…}]` geschrieben, jeder Kanal von 0 bis 1 |
| `meshes` | bis zu `{{v:skin.meshes-max}}` eigene Formen des Skins: eine `id` (eine beliebige GUID, die keiner eingebauten Form gehört), Punkte `vts` im Kasten von -0.5 bis 0.5 und Dreiecke `idxs` aus je drei Punkten |
| `elements` | welche Teile des Avatars gezeichnet werden, als Summe aus: Augen 1, Hände 2, Schatten 4, Spur 8, Dash-Spur 16, Treffereffekt 32, Dash-Farbe 64. 127 zeichnet alles, ein neuer Skin beginnt mit 125: alles außer den Händen. Das Raster wird immer gezeichnet |
| `eyes`, `hands`, `shadow`, `move_effect`, `dash_effect`, `damage_effect`, `dash_body` | die Farben des übrigen Avatars, in derselben Form wie `colors`. Ein in `elements` ausgeschalteter Teil behält seine Farbe |

Ein weggelassener Schlüssel behält den Wert des klassischen Avatars. Die ID einer eingebauten Form kopierst du am einfachsten aus einem exportierten Skin: die gemusterten Presets unter `{{ui:menu_avatar_tab-shapes}}` nutzen nur eingebaute Formen. Eine von Hand geschriebene Datei darf `id` weglassen - `{{ui:menu_avatar_import}}` gibt ihr eine

## Was ein Skin einhalten muss

- `columns` und `rows` liegen zwischen `{{v:skin.grid-min}}` und `{{v:skin.grid-max}}`, und `mask` füllt keine Zelle außerhalb davon
- mindestens `{{v:skin.filled-min}}` Zellen sind gefüllt, und alle berühren sich an einer Kante: der Körper ist ein Stück
- `cells` ist leer oder enthält genau ein Teil für jede gefüllte Zelle
- höchstens `{{v:skin.parts-max}}` Teile, und Form und Farbe jedes Teils existieren
- Körper und Schatten werden mit einer Deckkraft von mindestens `{{v:skin.body-alpha-min}}` gezeichnet

Ein Skin, der eine Regel bricht, erscheint in `{{ui:menu_avatar_tab-skins}}` ausgegraut mit dem Grund und kann nicht getragen werden. Ebenso eine zweite Datei mit derselben `id`. Geht der getragene Skin kaputt, wird der klassische Avatar gezeichnet und deine Wahl bleibt erhalten. Ein Skin aus einer neueren Version des Spiels zeigt `{{ui:menu_avatar_newer}}`

## Leben

Das Leben zeigen nur die gefüllten Zellen. Verlorene Zellen bleiben als dunkle Geister stehen, vom Rand zur Mitte, und die letzte Zelle hält, solange noch etwas Leben übrig ist. Je weniger Zellen gefüllt sind, desto mehr Leben ist jede wert - [[7_damage]]
