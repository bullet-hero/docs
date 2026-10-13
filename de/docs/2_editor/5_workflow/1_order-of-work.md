---
title: Die Reihenfolge der Arbeit
date: 2026-10-12
tags: [level_author]
---

# Die Reihenfolge der Arbeit

Zuerst der Song, die fps, das Beat-Raster und die Marker, dann ein Gerüst aus schlichten Formen und sein Testspiel. Deko, Theme und Effekte kommen zuletzt

Die Schritte gehen vom teuersten zum billigsten.
Je früher ein Schritt, desto mehr kostet es, ihn neu zu machen, sobald alles darauf aufbaut

## Das Fundament

1. **Der fertige Song.** Konvertiert, normalisiert, zugeschnitten. Alles andere wird daran gemessen. Den Song später zu ersetzen, verschiebt jeden Frame des Levels
2. **FPS und Levellänge.** Beides lässt sich ändern, aber die fps sind das Teure: Nach einer Änderung wird jeder Keyframe neu berechnet. Standard ist `60`, und meistens gibt es keinen Grund, das zu ändern
3. **Das Beat-Raster.** Segmente, Tempo, Versatz, Taktart. Solange das Beat-Raster falsch ist, rastet nichts richtig auf den Beats ein. Alles, was davor platziert wurde, muss später verschoben werden
4. **Marker auf der Struktur.** Intro, Strophe, Refrain, Break, Drop, Outro. Das sind zehn Minuten Arbeit, und die Marker sind auf jeder Zeitleiste sichtbar

## Das Gerüst und sein Testspiel

5. **Das Gerüst.** Die Hauptmuster in schlichten Formen. Keine Deko, kein Theme, keine Effekte
6. **Das Gerüst testspielen.** Vor der Deko: Ist ein Abschnitt erst dekoriert, willst du ihn nicht mehr löschen

> [!caution] Vorsicht
> Im Gerüst wird das Level eigentlich gestaltet. Und genau diese Phase wird am häufigsten übersprungen. Ein Gerüst, das keinen Spaß macht, wird durch Deko nicht spaßig. Es wird ein dekoriertes Level, das keinen Spaß macht

## Ausbauen

7. **Inhalt.** Bau die Muster aus und füge die Objekte hinzu, die bisher nur angedeutet waren
8. **Themes und Farbe.** Leg Farben von Anfang an als Verweise auf das Theme fest, nicht als feste Werte
9. **Effekte und Post-Processing.** Zuletzt. Sie lassen sich am leichtesten übertreiben, und solange sich das Level noch ändert, sind sie schwer zu beurteilen
10. **Metadaten.** Name, Beschreibung, Autoren, Altersfreigabe. Die Karte einer Ressource füllst du aus, sobald du die Ressource hinzufügst, nicht erst in diesem Schritt

## Drei Gewohnheiten, die Arbeit sparen

Das gilt genauso, ob du das Level baust oder der KI-Assistent:
- **Alles, was sich wiederholt, ist ein Prefab.** Bearbeite die Vorlage einmal, und jede Kopie folgt - [[2_reuse]]
- **Ein Umriss, den keine eingebaute Form hergibt, ist eine Levelform**, im Formeditor gezeichnet oder von der KI als Polygon angegeben. Sie zeichnet und trifft als ein Objekt, anders als ein Stapel Rechtecke
- **Nutze den ganzen 16:9-Frame.** Ein großer leerer Rand ist Bildschirm, den der Spieler sieht und das Level verschenkt. Halte Gefahr vom äußersten Rand fern, Deko darf ihn erreichen - [[4_composition-and-camera]]

## Was billig und was teuer zu ändern ist

**Am Ende billig zu ändern:** Farben über das Theme, Deko, Post-Processing, die Beschreibung des Levels

**Teuer:** die fps, der Song, das Beat-Raster und die Hierarchie

> [!warning] Warnung
> Ein neues Elternobjekt ändert Transformation, Lebensdauer und Zeichenreihenfolge eines Objekts auf einmal. Deshalb braucht das Umbauen eines fertigen Levels selten nur eine Änderung

Speichere bei jedem Schritt. Was Autospeichern und Rückgängig abdecken - [[4_not-losing-work]]

Weiter: [[2_reuse|Wiederverwendung: Prefabs, Kopieren, Generatoren]], [[4_not-losing-work|Damit keine Arbeit verloren geht]]
