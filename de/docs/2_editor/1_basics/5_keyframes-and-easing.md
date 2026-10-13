---
title: Keyframes und Easing
date: 2026-10-12
tags: [level_author]
---

# Keyframes und Easing

Ein Keyframe ist ein Wert in einem Frame einer Spur, plus das Easing, mit dem er erreicht wird. Alles im Level, was sich bewegt, die Farbe wechselt oder an- und ausgeht, ist eine Liste von Keyframes

Die Grundideen - [[3_how-the-editor-thinks]]. Jedes Feld des Keyframe-Inspectors - [[5_object-properties]]

## Was sich animieren lässt

Jede Spur hat ihre eigenen Keyframes, unabhängig von den anderen:

| Besitzer | Spuren |
|---|---|
| jedes Objekt | Position, Drehung, Skalierung, Größe, Anker, Drehpunkt |
| Form | Farbe, UV |
| Text | Farbe, Schriftgröße, `{{ui:editor_dummy_text-11}}` (wie viel vom Text geschrieben ist), `{{ui:editor_dummy_text-12}}` (wie viel davon hinter der Maske verborgen ist) |
| Kamera | Position, Drehung, Zoom, Drehpunkt, Erschütterung |
| Level | Hintergrund, Theme, Bildschirmgrenze, jeder der 12 Post-Processing-Effekte |
| Spieler | Größe, Geschwindigkeit, Sichtbarkeit, Steuerung, Kollision |

Ein Farb-Keyframe einer Form kann auch ein Verlauf über das Rechteck des Objekts sein. Sein Feld `{{ui:editor_keyframe-color_layout}}` wählt die Anordnung: `{{ui:enum_color4-x4-key-type_value}}` (eine Farbe), `{{ui:enum_color4-x4-key-type_vertical}}` (von unten nach oben), `{{ui:enum_color4-x4-key-type_horizontal}}` (von links nach rechts) oder `{{ui:enum_color4-x4-key-type_bari-centrical}}` (eine Farbe in jeder Ecke)

Ein Schriftgrößen-Keyframe ist entweder eine einzelne Zahl, eine feste Größe in Welteinheiten, oder ein Bereich mit eingeschaltetem `{{ui:field_common_auto-size}}`. Der Text wird beim `{{ui:field_common_max}}` des Bereichs gezeichnet und schrumpft in Richtung `{{ui:field_common_min}}`, bis er in sein Rechteck passt

Die Keyframes eines Objekts zählen ab dem Start seiner Spanne. Verschiebst du das Objekt in der Zeit, wandert also seine ganze Animation mit

Die Position wird relativ zum Elternobjekt angegeben. Ein Keyframe speichert den Wert selbst, keinen Zuwachs gegenüber dem vorigen Keyframe

Sichtbarkeit, Steuerung und Kollision des Spielers sind entweder an oder aus. Diese Keyframes haben kein Easing: es gibt nichts zu überblenden

Der erste Keyframe auf einer leeren Spielerspur ändert nichts auf dem Bildschirm: Sichtbarkeit, Steuerung und Kollision sind am Anfang an, Größe und Geschwindigkeit haben die üblichen Werte des Spielers. Ist die Steuerung aus oder der Spieler ausgeblendet, lässt sich der Spieler nicht lenken: der Cursor verschwindet, und ein Druck wird nicht erkannt. Ein ausgeblendeter Spieler wird trotzdem getroffen: darüber entscheidet nur die Kollision

## Text: Füllung und Erscheinen

Zwei Textspuren verbergen Zeichen auf unterschiedliche Weise. Beide nehmen einen Anteil von 0 bis 1 und zählen die Zeichen des Texts

**`{{ui:editor_dummy_text-11}}`** ist der Anteil des Texts, der geschrieben ist: 0 - nichts, 1 - alles. Ein nicht geschriebenes Zeichen wird gar nicht gezeichnet, die Zeile wird also kürzer. Eine leere Spur schreibt den ganzen Text. Jeder Keyframe legt die Richtung fest:
- `{{ui:enum_text-fill-direction_forward}}` (Standard) - ab dem ersten Zeichen, wie eine Schreibmaschine
- `{{ui:enum_text-fill-direction_backward}}` - ab dem letzten Zeichen
- `{{ui:enum_text-fill-direction_from-center}}` - wächst aus der Mitte heraus
- `{{ui:enum_text-fill-direction_to-center}}` - wächst von beiden Enden herein und trifft sich in der Mitte

**`{{ui:editor_dummy_text-12}}`** ist der Anteil der Zeichen, die hinter der Maske verborgen sind: 0 - alle sichtbar, 1 - alle maskiert. Ein verborgenes Zeichen behält seinen Platz und wird als Maskenzeichen gezeichnet, standardmäßig `{{v:text.appearing-mask-default}}`. Die Maske ist das Feld `{{ui:editor_inspector-appearing_mask}}` des Textobjekts, und stehen mehrere Zeichen darin, nimmt jedes verborgene Zeichen eines davon. Eine leere Spur verbirgt nichts. Jeder Keyframe legt den Modus fest:
- `{{ui:enum_text-appearing-mode_random}}` (Standard) - verstreut, aber bei jedem Durchlauf gleich verstreut. Ein Zeichen, das bei 0,3 verborgen ist, ist auch bei 0,6 noch verborgen, der Text löst sich also auf, statt zu flackern
- `{{ui:enum_text-appearing-mode_forward}}` - die verborgenen Zeichen stehen am Ende, der Text erscheint von seinem Anfang her
- `{{ui:enum_text-appearing-mode_backward}}` - die verborgenen Zeichen stehen am Anfang

Um eine Zeile einzutippen, animiere `{{ui:editor_dummy_text-11}}` von 0 bis 1. Um sie aus dem Rauschen zu entschlüsseln, animiere `{{ui:editor_dummy_text-12}}` von 1 bis 0

## Ratschläge

- Setz Keyframes nur für das, was sich bewegt. Eine Spur ohne Keyframes nimmt den Standardwert
- Für eine Änderung genau auf einem Beat nimm `Constant`, zum Beispiel einen Theme-Wechsel beim Drop
- Die Drehung springt nicht zurück: ein Keyframe bei 0 Grad und einer bei 720 drehen das Objekt zweimal. In Radiant, wie die Datei und der KI-Assistent es schreiben, sind das 0 und 12,566

## Zwischen zwei Keyframes

Vor dem ersten Keyframe und nach dem letzten bleibt der Wert stehen.
Zwischen zwei Keyframes nimmt das Spiel den Anteil der vergangenen Zeit, schickt ihn durch das Easing und überblendet die beiden Werte

Der Anteil wird in Zeit gezählt, nicht in gezeichneten Frames. Die Kurve ist also bei 30 und bei 144 fps dieselbe

**Das Easing gehört zum späteren Keyframe des Paars.** Das Easing eines Keyframes legt den Abschnitt fest, der vom vorigen Keyframe bei diesem ankommt.
Das Easing des ersten Keyframes einer Spur ist also nie zu sehen. Ein neuer Keyframe bekommt `Linear`

Das Feld `{{ui:hint_editor_inspector_ease_header}}` öffnet das Fenster `{{ui:editor_search-title_ease}}`, in dem jedes Easing als eigene Kurve gezeichnet ist.
Du kannst mehrere Keyframes auswählen, sogar auf verschiedenen Spuren, und sie in einem Rückgängig-Schritt ändern

## 29 Easings

`Linear` ist eine Gerade. `Constant` hält den vorigen Wert und springt beim Keyframe

Die anderen 27 sind neun Familien zu je drei: `In`, `Out` und `InOut`. Zum Beispiel `InSine`, `OutSine`, `InOutSine`

| Familie | Form |
|---|---|
| `Sine` | die weichste Kurve |
| `Quad`, `Cubic`, `Quart`, `Quint` | Potenzen 2, 3, 4 und 5 |
| `Expo` | exponentiell |
| `Circ` | ein Viertelkreis |
| `Back` | geht über den Bereich hinaus und kommt zurück |
| `Elastic` | schwingt um den Wert |

`In` beginnt langsam und endet schnell. `Out` beginnt schnell und kommt zur Ruhe. `InOut` ist an beiden Enden langsam.
Von `Sine` bis `Expo` ist jede Familie schärfer als die vorige

> [!caution] Vorsicht
> `Back` und `Elastic` verlassen den Bereich: `Out` schießt über das Ziel hinaus, `In` weicht hinter den Start zurück. Der Collider bewegt sich mit dem Objekt. Ein Projektil, das am Rand einer sicheren Zone anhalten soll, dringt also für ein paar Frames in sie ein

## Zufallswerte

Ein Wert in einem Keyframe muss keine einzelne Zahl sein:
- eine Zahl: `{{ui:field_common_value}}`, `{{ui:enum_color-type_random-min-max}}`, `{{ui:enum_float-type_random-min-max-step}}`
- ein Vektor (Position, Skalierung und Ähnliches): `{{ui:field_common_value}}`, `{{ui:enum_vector-type_random-rect}}`, `{{ui:enum_vector-type_random-rect-step}}`, `{{ui:enum_vector-type_random-circle}}`, `{{ui:enum_color-type_random-lerp}}`, `{{ui:enum_vector-type_random-lerp-step}}`
- eine Farbe: `{{ui:field_common_value}}`, `{{ui:editor_events-timeline_track_theme}}`, `{{ui:enum_color-type_random-min-max}}`, `{{ui:enum_color-type_random-lerp}}`

`{{ui:enum_vector-type_random-rect}}` wählt jede Achse einzeln. `{{ui:enum_color-type_random-lerp}}` wählt eine Zahl für alle Achsen, der Punkt landet also auf der Linie zwischen A und B.
Die Formen mit Schritt runden das Ergebnis auf ein Vielfaches des Schritts ab. Ein Schritt von 0 schaltet das Raster aus, und der Wert verhält sich wie die Form ohne Schritt.
Danach wird der Keyframe wie jeder andere überblendet

Derselbe Seed ergibt dasselbe Level. Die Zufallszahl wird aus dem Seed, dem Frame des Keyframes, der Ebene, dem Startframe des Objekts, der Spur und dem Kanal berechnet. Mehr - [[8_determinism]]

Weiter: [[2_rhythm-and-structure|Rhythmus und Struktur]], [[6_themes|Themes]]
