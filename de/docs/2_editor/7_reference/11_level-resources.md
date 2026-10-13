---
title: Levelressourcen
date: 2026-10-12
tags: [level_author]
---

# Levelressourcen

Texturen, Formen, Themes, Effekte und Prefabs eines Levels liegen in seinem Ordner und reisen mit ihm. Jede Ressource hat eine eigene Karte mit Quelle, Lizenz und Autoren

## Bibliothek

Ressourcen, die auf **diesem Gerät** gespeichert sind. Alle Levels, die du hier öffnest, teilen sie sich

Beim Importieren wird die Ressource *ins Level* kopiert.
Ein Level ist ein Ordner mit Dateien, und es trägt alles in sich, was es braucht. Genau das hält es tragbar

Die Bibliothek ist also eine Erleichterung für dich. Wer dein Level spielt, hängt nie von ihr ab

Die Bibliothek listet drei Quellen auf, jede als Chip: `{{ui:editor_library-source_library}}`, `{{ui:editor_library-source_local}}` und in einem Steam-Build `{{ui:editor_library-source_workshop}}`.
Die Wahl eines Eintrags importiert ihn mit seinen Abhängigkeiten. Hat das Level schon eine andere Version, fragt das Spiel, welche behalten werden soll

Mehr - [[16_library-and-collections]], [[2_reuse]]

## Texturen

Bilder, die dieses Level mitbringt.
**Das Spiel selbst liefert keine Texturen mit.** Jede Textur, die ein Level verwendet, wurde hier hinzugefügt

Ein Level ist nur ein Ordner mit Dateien. Eine Textur liegt darin und reist mit dem Level: Ordner zippen, verschicken, entpacken, spielen

Formen sind **keine** Texturen, sondern echte Geometrie. Sie brauchen nichts aus diesem Tab

Mehr - [[3_images-and-fonts]]

## Formen

Die eigenen Formen des Levels. Sie kommen zu den rund 500 Formen hinzu, die das Spiel erzeugt

Eine Form ist **echte Geometrie**, kein Bild.
Das Rechteck des Objekts ist der Rahmen der Form, und die beiden Arten von Formen sitzen unterschiedlich darin:
- **Eine eingebaute Form behält ihre Proportionen.** Ihre längere Seite füllt das Rechteck, also zeichnet ein `Triangle` mit der Größe (2, 2) 2 breit und etwa 1,73 hoch
- **Eine Form, die das Level definiert, wird auf das Rechteck gestreckt**, so wie sie in ihrem Rahmen gezeichnet wurde. Ein Umriss vom KI-Assistenten wird in den Rahmen eingepasst und füllt das Rechteck also genau

> [!tip] Tipp
> **Eine Form und eine Hitbox sind dieselbe Art von Daten.** Ein Objekt trägt zwei Verweise: einen für das, was gezeichnet wird, und einen für das, was trifft. Keiner leitet sich vom anderen ab. Ein harmloser Warnstrahl, eine Hitbox, die einfacher ist als ihre Grafik, und eine unsichtbare Wand sind deshalb alle gewöhnlicher Inhalt

Mehr - [[1_level-needs]]

### Namen der eingebauten Formen

Der Name einer eingebauten Form wird aus Teilen zusammengesetzt, immer in dieser Reihenfolge. `Circle_S2_T8_I` ist die rechte Hälfte eines Kreises als Ring mit 1/8 des Radius Dicke, invertiert

| Teil | Bedeutung |
|---|---|
| Form | `Square`, `Circle`, `Triangle`, `RightTriangle` oder ein regelmäßiges Vieleck: `Pentagon`, `Hexagon` und so weiter |
| `S2`, `S4`, `S8` | ein Sektor: eine Hälfte, ein Viertel, ein Achtel. Er beginnt senkrecht nach oben und läuft im Uhrzeigersinn, also ist `S2` die rechte Hälfte. Kein `S` - die ganze Form |
| `_2` nach `S4` | das andere Viertel: das untere rechte statt des oberen rechten. Es gibt es nur dort, wo die Form eine andere Figur ergibt |
| `T2`, `T4`, `T8`, `T16`, `T32` | ein Ring mit 1/2, 1/4, 1/8, 1/16 oder 1/32 des Radius Dicke. Kein `T` - gefüllt |
| `I` | invertiert: der Rahmen (oder sein Sektor) ohne die Form |

Eine Form ohne weitere Teile, etwa `Circle`, ist die ganze gefüllte Form. Nicht jede Kombination existiert. Die Hälfte eines Quadrats ist einfach ein Rechteck, das erledigt eine schmalere Größe

## Themes

Ein Theme ist eine **Palette**. Die Farben des Levels können auf sie verweisen, statt feste Werte zu enthalten

Ein Wechsel des aktiven Themes gestaltet alles, was darauf verweist, auf einmal um.
Das aktive Theme lässt sich auf der Ereignis-Zeitleiste animieren. So ändert ein Level mitten im Song sein ganzes Aussehen

Themes lassen sich in der Bibliothek des Geräts speichern und in anderen Levels wiederverwenden

Mehr - [[6_themes]], [[5_color-and-postprocessing]]

## Effekte

Partikeleffekte aus `VFX Graph`, die das Level platzieren kann

Effekte sind eine **optionale Bereicherung**. Ein Level, das nie einen verwendet, spielt sich genau wie vorgesehen

Ein Effekt verwendet denselben Zufall aus dem Seed wie alles andere im Level. Deshalb läuft er auf jedem Gerät identisch ab.
Effekte lassen sich in der Bibliothek des Geräts speichern und in anderen Levels wiederverwenden

**Das Spiel liefert keine vorgefertigten Effekte mit.** Jeder Effekt, den ein Level verwendet, wurde darin erstellt oder aus der Bibliothek genommen

Mehr - [[1_level-budget]]

## Prefabs

Wiederverwendbare Gruppen von Objekten.
Ein Prefab enthält seine eigenen Vorlagenobjekte. Beim Platzieren eines Prefabs werden echte Kopien davon ins Level geschrieben

Eine spätere Bearbeitung der Vorlage überträgt sich auf jede Platzierung.
Eine Platzierung kann trotzdem durch Überschreibungen pro Instanz von der Vorlage abweichen

> [!warning] Warnung
> Prefabs haben **keine vom Spiel definierten Presets**, Effekte ebenfalls nicht. Das Spiel liefert Presets nur für Themes, Schriftarten, Oberflächensounds und die eingebauten Formen. Die Bibliothek ist der einzige Weg, ein Prefab zwischen Levels zu teilen: deine Gerätebibliothek oder eine Sammlung. Mehr - [[16_library-and-collections]]

Mehr - [[2_reuse]]

## Metadaten der Ressource

Titel, Beschreibung, Quellen, Lizenz und Autoren einer Ressource

So bleibt die Namensnennung erhalten.
Eine Textur, Schriftart oder Audiodatei, die von irgendwoher stammt, trägt im Level mit sich, woher sie kommt und unter welchen Bedingungen. Dieser Eintrag geht überallhin mit, wohin das Level geht

> [!tip] Empfehlung
> Fülle sie aus, wenn du die Ressource hinzufügst. Das ist der einzige Moment, in dem du noch weißt, woher sie kommt

Mehr - [[4_resource-record]]

## Theme-Editor

Die Slots eines Themes und die Farben darin

> [!caution] Vorsicht
> Levelinhalt verweist auf einen Slot über seine Position. Deshalb **gestaltet ein Umnummerieren der Slots alles um, was auf sie verweist**

> [!tip] Tipp
> Speichere ein fertiges Theme in der Bibliothek des Geräts. Dann kannst du es in anderen Levels verwenden

Mehr - [[6_themes]], [[5_color-and-postprocessing]]

## Farbverweis auf ein Theme

Lässt diese Farbe auf einen **Slot im Theme des Levels** verweisen statt auf einen festen Wert

Wenn sich das Theme ändert, wird alles, was auf einen Slot verweist, auf einmal umgestaltet.
Themes lassen sich auf der Ereignis-Zeitleiste animieren. So ändert ein Level mitten im Song seine ganze Palette, ohne ein einziges Objekt anzufassen

> [!tip] Tipp
> Die Farbfelder zeigen die Palette im Frame des Keyframes, den du bearbeitest, nie am Abspielkopf. Das Fenster nennt die Themes zu beiden Seiten dieses Frames. Um gegen ein späteres Aussehen zu wählen, bearbeite einen Keyframe, der später liegt

Mehr - [[6_themes]], [[5_color-and-postprocessing]]

## Formeditor

Baut eine Form aus Punkten und den Kanten zwischen ihnen

Du bearbeitest Punkte und Kanten. **Dreiecke werden automatisch abgeleitet und nie bearbeitet.**
Eine Ecke, die sich drei Dreiecke teilen, ist also ein Punkt zum Ziehen, nicht drei, die auseinanderfallen

> [!warning] Warnung
> Kanten gibt es nur im Editor, das Format speichert Dreiecke. Eine Kante, die keine Schleife schließt, fällt deshalb beim Speichern weg. Der Editor meldet das, statt sie stillschweigend zu verwerfen

Mehr - [[3_images-and-fonts]]

## Lizenzen

Die Bedingungen, unter denen dieses Level und seine Ressourcen stehen

Ein Level trägt jede Datei in sich, die es braucht: Bilder, Schriftarten, Audio. Jede Datei kann ihre eigenen Bedingungen haben.
**Diese Bedingungen werden pro Ressource festgehalten**, nicht nur für das Level als Ganzes. So kann ein Level aus geliehenen Teilen genau angeben, was geliehen wurde und unter welchen Bedingungen

> [!tip] Empfehlung
> Lies sie, bevor du etwas aus dem Level eines anderen wiederverwendest

Mehr - [[1_licensing-basics]]
