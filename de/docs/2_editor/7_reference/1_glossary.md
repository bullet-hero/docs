---
title: Glossar
date: 2026-10-11
tags: [level_author]
---

# Glossar

Die zentrale Begriffsliste des Projekts. Die Oberfläche des Spiels, diese Dokumentation und alle anderen Texte über Bullet Hero verwenden diese Wörter, und ein neuer Begriff kommt zuerst hierher

## Levelinhalt

| Begriff | Bedeutung |
|---|---|
| **Level** | Alles, woraus eine Partie besteht: Objekte, Audio, Ereignisse und die eigenen Ressourcen |
| **Objekt** | Ein vom Autor erstelltes Element auf der Zeitleiste, mit eigener Lebensdauer, Transformation und eigenem Elternobjekt |
| **Leeres Objekt** | Ein Objekt, das nichts zeichnet: eine Transformation, eine Lebensdauer und Kinder. Jeder andere Typ fügt sein Eigenes darauf hinzu |
| **Form** | Echte Geometrie, die ein Objekt zeichnet, kein Bild. Das Spiel erzeugt rund 500 davon selbst |
| **Collider** | Womit ein Objekt trifft. Er muss nicht dem entsprechen, was das Objekt zeichnet |
| **Prefab** | Eine wiederverwendbare Vorlage aus Objekten, die so oft wie nötig in ein Level gesetzt wird |
| **Prefab-Modus** | Den eigenen Inhalt einer Vorlage bearbeiten statt des Levels um sie herum |
| **Effekt** | Ein Erzeuger: In jedem Frame erstellt er aus wenigen Parametern eigene Objekte |
| **Frame-Objekt** | Ein Objekt, das ein Effekt erzeugt hat. Die Engine verwaltet es: Es lässt sich weder auswählen noch bearbeiten |
| **Theme** | Eine Palette, auf die das Level per Index verweist: Umfärben ist eine Änderung, nicht hundert |

## Zeit und Animation

| Begriff | Bedeutung |
|---|---|
| **Frame** | Die Zeiteinheit des Levels. Ein Frame ist eine Zelle, und die Zeit ist die Grenze zwischen zwei Zellen |
| **Keyframe** | Ein vom Autor festgelegter Wert in einem Frame. Zwischen zwei Keyframes wird der Wert interpoliert |
| **Spur** | Eine Reihe von Keyframes einer animierbaren Eigenschaft: Position, Drehung, Lautstärke |
| **Zeitleiste** | Die Frame-Achse, auf der das Level bearbeitet wird: ein Tab für jede Inhaltsart |
| **Spanne** | Wann ein Objekt existiert: ein Startframe und eine Länge, aber kein Endframe |
| **Abspielkopf** | Der Frame, der gerade angezeigt wird |
| **Easing** | Wie ein Wert vom vorigen Keyframe zu diesem übergeht |
| **Marker** | Ein benannter Punkt auf dem Lineal des Levels, um an die richtige Stelle zurückzukehren |
| **Checkpoint** | Wohin ein Tod den Spieler zurückschickt |

## Platzierung und Zeichnen

| Begriff | Bedeutung |
|---|---|
| **Anker** | Eine Kante, die der Kante des Elternobjekts folgt: Schrumpft das Elternobjekt, wandert das Kind mit |
| **Ebene** | Die Zeichenreihenfolge, und sie ist relativ: Die Ebene eines Kindes wird zur Ebene seines Elternobjekts addiert |
| **Drehpunkt** | Der Punkt, um den sich ein Objekt dreht und skaliert, innerhalb seines eigenen Rahmens |
| **Gizmo** | Die Ziehgriffe, die im Viewport über dem ausgewählten Objekt gezeichnet werden |
| **Einrasten** | Ein Ziehen an etwas ausrichten: mit dem Magneten an den Inhalt, mit dem Beat-Schalter an die Musik |

## Musik

| Begriff | Bedeutung |
|---|---|
| **Beat** | Das eigene Raster der Musik: Der Autor legt es fest, und beim Spielen liest es nichts |
| **Beat-Segment** | Ein Abschnitt mit konstantem Tempo, mit eigenem Tempo, eigener Phase und Taktlänge |
| **BPM** | Beats pro Minute - wie schnell ein Beat-Segment läuft |
| **Tippen** | Ein Druck beim Einklopfen des Tempos. Genug davon beschreiben ein Beat-Segment |

## Automatisierung und Daten

| Begriff | Bedeutung |
|---|---|
| **Generator** | Automatisiertes Erstellen: Er erzeugt Levelinhalt aus wenigen Parametern |
| **Modifikator** | Ein Generator, der Vorhandenes bearbeitet oder entfernt, statt etwas hinzuzufügen |
| **Seed** | Die Zahl, aus der jeder Zufallswert eines Levels entsteht: Ein Durchlauf wiederholt sich exakt gleich |
| **Rohdaten** | Das ganze gespeicherte Modell als ein bearbeitbarer Baum. Hier wird nichts geprüft, und das ist Absicht |
| **KI-Assistent** | Ein KI-Client, der über MCP mit dem Editor verbunden ist. Er bearbeitet das offene Level, während du zusiehst, ein Rückgängig-Schritt pro Paket |

## Ressourcen und Teilen

| Begriff | Bedeutung |
|---|---|
| **Bibliothek** | Ressourcen auf dem Gerät zur Wiederverwendung in mehreren Levels: deine Bibliothek, deine Sammlungen und die, die du abonniert hast |
| **Sammlung** | Ein Ordner mit wiederverwendbaren Ressourcen von bis zu sieben Arten. Beim Importieren wird daraus kopiert, also hängt das Level nicht von ihr ab |
