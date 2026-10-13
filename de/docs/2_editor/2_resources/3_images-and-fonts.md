---
title: Bilder und Schriftarten
date: 2026-10-02
tags: [level_author]
---

# Bilder und Schriftarten

Reicht eine Form, nimm eine Form: keine Datei, kein Speicher, keine Rechtefrage. Ein Bild so groß wie sein Platz auf dem Bildschirm, höchstens {{v:texture.mobile-max-side}} für ein mobiles Level, sonst {{v:texture.desktop-max-side}}

Runde die Bildgröße auf eine Zweierpotenz auf

## Formate und Größe

Alles, was die Engine aus den Bytes einer Datei dekodieren kann, wird geladen. In der Praxis sind das `png` und `jpg`

Das Spiel begrenzt die Dateigröße nicht, die Hardware schon:

| Gerät | Längste Seite |
|---|---|
| Android, garantiert | 4096 |
| Android, meistens | 8192-16384 |
| Desktop-PC | bis 32768 |

## Speicher

**Die eigentliche Grenze ist der Speicher.** Im Speicher liegt ein Bild als rohe Pixel, egal wie viel die Datei wiegt.
Ein `png` braucht 4 Bytes pro Pixel. Ein `jpg` braucht 3, weil es keine Transparenz hat

| Größe | Speicher (`png`) |
|---|---|
| 512 mal 512 | 1 MB |
| 1024 mal 1024 | 4 MB |
| 2048 mal 2048 | 16 MB |
| 4096 mal 4096 | 64 MB |
| 8192 mal 8192 | 256 MB |

> [!caution] Vorsicht
> Eine 8192er-Textur ist ein Viertel Gigabyte für ein einziges Bild. Auf einem Handy ist das nicht langsam, sondern ein Absturz

## Was der Spieler entscheidet

Drei Punkte in den Grafikeinstellungen jedes Spielers entscheiden, wie viel Speicher ein Bild braucht:
- ob Bilder beim Laden komprimiert werden. Kompression teilt die Zahlen oben durch 4-8
- die längste Seite eines Bilds im Speicher. Halbe Seite - ein Viertel des Speichers
- ob Mipmaps erzeugt werden, verkleinerte Kopien zum Zeichnen in kleiner Größe

Ein Handy komprimiert Bilder standardmäßig und begrenzt sie auf {{v:texture.mobile-max-side}}. Ein Desktop-PC behält das volle Bild und begrenzt es auf {{v:texture.desktop-max-side}}

**Dein Teil sind die Felder am Bild, vor allem, was es darstellt.** Sie stehen neben dem Bild in der Ressourcenliste.
Ein Foto übersteht Verkleinern und Kompression am besten. Eine Zeichnung mit harten Kanten übersteht sie schlechter

`{{ui:enum_texture-kind_pixel-art}}` bekommt nie Mipmaps, egal was das Gerät bevorzugen würde. Es startet außerdem unkomprimiert und ungeglättet, und die Felder `{{ui:level_resources_texture-compression}}` und `{{ui:level_resources_texture-sampling}}` können das ändern

## Mipmaps

Mipmaps verhindern, dass ein kleines Bild flimmert. Sie sind verkleinerte Kopien, die statt des vollen Bilds gezeichnet werden, solange es auf dem Bildschirm klein ist.
Sie kosten ein Drittel mehr Speicher

Ohne Mipmaps wird ein verkleinertes Bild nicht weich, es kräuselt sich. Ein Spieler kann sie ausschalten, und `{{ui:enum_texture-kind_pixel-art}}` bekommt sie nie

Ein 4096er-Bild, das auf dem Bildschirm 200 Pixel einnimmt, kostet 256-mal so viel Speicher wie dasselbe Bild, das vorher auf 256 verkleinert wurde

## Formen vor Bildern

Eine Form ist in jeder Hinsicht günstiger als ein Bild: keine Datei, kein Speicher, keine Rechtefrage.
Eingebaute Formen sind echte Geometrie, kein Bild auf einem Rechteck. Sie haben keine transparenten Ränder, die gezeichnet und wieder verworfen werden

Das zeigt sich auf dem Handy. Auf einem Mobilchip der Mittelklasse verbringt eine Szene mit 1000 Objekten 95-97 % der GPU-Zeit mit dem Schattieren von Pixeln.
Eine Form bedeckt 29,4 % ihres Rechtecks. Der Rest eines texturierten Quads ist transparente Verschwendung

Ein Bild brauchst du, wenn du genau ein Bild brauchst: ein Logo, ein Foto, handgezeichnete Grafik.
Für eine geometrische Form nimm eine Form. Gibt es die benötigte nicht, zeichne sie im `{{ui:hint_level_shape-editor_header}}`

## Schriftarten

Schriftarten laden als `ttf`, `otf`, `ttc`. Ohne eigene Schriftart wird Text mit dem gezeichnet, was das System hat, und das unterscheidet sich von Gerät zu Gerät

Der `{{ui:settings_level-settings_fontcache}}` ist der Satz von Zeichen, die vorab zum Zeichnen vorbereitet werden. Ein Generator baut ihn aus dem Text neu, den das Level enthält.
Starte den Generator, sobald sich der Text nicht mehr ändert

Weiter: [[1_level-budget]], [[2_mobile-devices]]
