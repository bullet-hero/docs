---
title: Warum Bullet Hero
date: 2026-10-03
tags: [player, level_author]
---

# Warum Bullet Hero

Bullet Hero ist kostenlos, läuft auf Windows und Android, SDK, Dokumentation und Builds sind offen. Der Kern schafft Tausende Objekte auf dem Bildschirm, auch auf Smartphones, und hat über 8000 Tests

## Kostenlos

Das Spiel ist kostenlos und bleibt es. Es wird darin keine Käufe, keine Werbung und keine kostenpflichtigen Inhalte geben

Eine Monetarisierung über freiwillige Spenden schließe ich nicht aus, aber darüber hinaus nichts

## Überall verfügbar, alles universell

Das Spiel gibt es überall, wohin ich es portieren konnte
- Plattformen: Windows, Android (später iOS, Linux, Mac)
- Stores: Steam, Google Play (später App Store)

Alles im Spiel funktioniert mit jeder Steuerung, die Levels sind überall dieselben, und jeder Teil des Spiels (der Editor, der Multiplayer, die Server) funktioniert überall gleich

## Ein hoher Anteil an offenem Code

Das SDK, die Dokumentation, die Builds und der Server liegen in offenen Repositorys. Geschlossen sind nur das Spiel selbst und die Website.
Alle Repositorys - [[links]]

## Der schnellste technische Kern

Tausende Objekte auf dem Bildschirm, Hunderte Effekte und Texte gleichzeitig. Und all das läuft auf Smartphones mit einem Ziel von 60 FPS (oft mehr)

## Ein sehr stabiler technischer Kern

Das Spiel hat viele Mechanismen, die das Spiel und seine Datenmodelle stabil halten
- Versionierung von allem (mehr dazu - [[5_versioning]])
- Multimodale Versionierung und Datenmigration, Leveldaten gehen nicht kaputt
- Über 8000 Tests im ganzen Spiel, buchstäblich jeder Aspekt des Spiels ist durch Tests abgedeckt

Und viele weitere Prüfungen. Zusammen mit dem schnellen Kern ergibt das ein sehr hohes Verhältnis von Stabilität zu Leistung

## Multiplayer (in Entwicklung)

Multiplayer in jeder Form: auf einem Gerät, lokal, über einen Server, und viele interessante Interaktionen

## Offene Server (in Entwicklung)

Ein offizieller Server und Community-Server, die jeder betreiben kann. Der Servercode wird offen sein. Levelkataloge und grundlegende Kommunikation kommen zusammen mit dem Server.
Mehr - [[4_server/index]]

## Viele Sprachen

Das Spiel soll die meisten Sprachen der Welt von Haus aus unterstützen. Ich finde, ein Spiel sollte überhaupt keine Sprachbarriere haben

Natürlich kann niemand alle Sprachen der Welt beherrschen, aber dank der Fortschritte bei KI und dank der Community ist dieses Ziel durchaus erreichbar

## Offene Lizenzpolitik

Alle Spieldaten kommen mit einer flexiblen Auswahl an Lizenzen (überwiegend [Creative Commons](https://creativecommons.org/))
für deine Levels und die Ressourcen, die du verwendest. Das macht die Wiederverwendung fremder Ressourcen offener

Mehr - [[ugc-licensing-policy]]

## Integration mit jedem Dienst, wo es geht

Das Spiel hat über 10 Build-Varianten, und jede hat ihre eigenen Integrationen, je nachdem, über welchen Store sie vertrieben wird

Mehr - [[download]]

## Determinismus und Stabilität

Das Spiel hat deterministischen Zufall, und jeder seiner Faktoren hängt am Seed und an den Parametern des Levels.
Das heißt, der Zufall lässt sich immer wiederholen, wenn du das Level kennst und den Seed hast

Mehr - [[8_determinism]]

## Editor

Das Spiel hat einen großen und flexiblen Leveleditor, in dem du fast alles erstellen kannst

Der Editor hat viele einzigartige Funktionen: [[8_generators]], Debugging und mehr

## Offenes Levelformat

Das C#-SDK liest und schreibt Levels genauso wie das Spiel. Das Spiel und der Server arbeiten damit, und du kannst es auch.
Damit kannst du eigene, einzigartige Levels oder Ressourcen erstellen oder eigene Dienste darauf aufbauen

Mehr - [[3_sdk/index]]
