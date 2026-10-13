---
title: Den Song vorbereiten
date: 2026-10-01
tags: [level_author]
---

# Den Song vorbereiten

Wandle den Song in ogg um: er wiegt 8-10-mal weniger als wav und fügt anders als mp3 keine Stille am Dateianfang ein. Außer ogg laden nur mp3 und wav

## Formate

`oga`, `mp2`, `aiff`, `flac` und die Tracker-Module `mod`, `xm`, `it`, `s3m` werden nicht angenommen

> [!caution] Vorsicht
> `flac` lädt überhaupt nicht: die Engine dekodiert es nicht. Wandle es vorher um

> [!warning] Warnung
> Ein `mp3`-Encoder fügt am Anfang ein paar Millisekunden Stille ein, und verschiedene Encoder fügen unterschiedlich viel ein. Wird der Song mit einem anderen Encoder neu kodiert, verschiebt sich die ganze Beat-Zuordnung

## Versatz

Selbst in `ogg` beginnt ein Song fast nie genau auf dem ersten Beat. Dafür gibt es den Versatz des Beat-Segments.
Er wird in Bruchteilen von Frames angegeben und ist damit feiner als ein Frame

Die Reihenfolge ist: zuerst das Tempo, dann der Versatz und erst danach der Inhalt

## Lautheit

Normalisiere den Song, bevor du ihn ins Level packst. Eine Spitzennormalisierung auf -1 dB ist ein vernünftiger Standard

Ein Level, das deutlich leiser ist als das nächste, wirkt, als wäre das Spiel kaputt, nicht der Song

## Länge

Die Länge des Levels und die Länge des Songs sind verschiedene Zahlen, sie müssen nicht übereinstimmen.
Ein Level kann enden, bevor der Song endet. So lässt sich ein Schluss mit Ausblenden bauen

## Mehrere Audiospuren

Es kann mehrere Audiospuren geben. Jede hat ihre eigene Position auf der Zeitleiste, ihre eigene Geschwindigkeit, Lautstärke und Effektkette

Effekte: Chorus, Kompressor, Verzerrung, Echo, Flanger, Filter, Normalisierung, Equalizer, Tonhöhenverschiebung, Hall

Ein Effekt auf einer Audiospur ist überall zu hören, wo diese Spur spielt, nicht nur dort, wo du ihn haben wolltest

Weiter: [[3_where-to-get-resources]], [[2_rhythm-and-structure]]
