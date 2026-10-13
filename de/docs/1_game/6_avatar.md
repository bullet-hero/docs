---
title: Avatar und Bewegung
date: 2026-10-02
tags: [advanced_player]
---

# Avatar und Bewegung

Der Avatar läuft mit {{v:avatar.move-speed}} Einheiten pro Sekunde, ein Dash trägt ihn {{v:avatar.dash-distance}} Einheiten in {{v:avatar.dash-time}} s. Die Hitbox, ein Kreis mit Radius {{v:avatar.hitbox-radius}} Einheiten, ist kleiner als das gezeichnete Quadrat ({{v:avatar.body-size}} Einheiten)

Diese Seite ist die maßgebliche Quelle für den Avatar. Das Spiel und beide Bots sind nach diesen Zahlen gebaut, und das SDK hält sie als Konstanten `AvatarRules` fest. Code, der dieser Seite widerspricht, ist ein Fehler im Code

Entfernungen sind in Welteinheiten angegeben. Die Standardkamera ist genau {{v:camera.default-height}} Einheiten hoch (`ValueRules.DefaultZoom`), eine Einheit ist also ein Zehntel der Bildschirmhöhe, und der Körper des Avatars ist eine halbe Einheit breit.
Der Kamerazoom ändert, wie viel du siehst, aber nicht die Zahlen unten

## Die Zahlen

| Was | Wert | Einfach gesagt |
|---|---|---|
| Laufgeschwindigkeit | `{{v:avatar.move-speed}}` E/s | durchquert den Bildschirm von oben nach unten in zwei Dritteln einer Sekunde |
| Dash-Geschwindigkeit | `{{v:avatar.dash-speed}}` E/s | {{v:avatar.dash-to-walk-ratio}}-mal schneller als Laufen |
| Dash-Dauer | `{{v:avatar.dash-time}}` s | |
| Dash-Weite | `{{v:avatar.dash-distance}}` Einheiten | Geschwindigkeit × Dauer, drei Viertel der Bildschirmhöhe |
| Dash-Abklingzeit | `{{v:avatar.dash-cooldown}}` s | ab dem Beginn des Dashs gezählt |
| Dash-Unverwundbarkeit | `{{v:avatar.dash-invulnerability}}` s | ebenfalls ab dem Beginn, sie dauert also {{v:avatar.dash-invulnerability-margin}} s länger als die Bewegung selbst |
| Kürzester Dash | `{{v:avatar.arrival-distance}}` Einheiten | so viel wie die Ankunftsdistanz, noch näher und du stehst schon auf dem Ziel |
| Rückstoßgeschwindigkeit | `{{v:avatar.knockback-speed}}` E/s | {{v:avatar.knockback-to-walk-ratio}}-mal schneller als Laufen, [[7_damage]] |
| Rückstoßdauer | `{{v:avatar.knockback-time}}` s | währenddessen keine Steuerung |
| Schadenspause | `{{v:avatar.damage-timeout}}` s | jeder weitere Treffer in dieser Zeit wird ignoriert |
| Körpergröße | `{{v:avatar.body-size}}` Einheiten | das gezeichnete Quadrat |
| Hitbox | Radius `{{v:avatar.hitbox-radius}}` Einheiten | {{v:avatar.hitbox-scale}} des Körpers, absichtlich kleiner als das, was du siehst |
| Erscheinen und Verschwinden | `{{v:avatar.spawn-time}}` s | wächst heran und schrumpft zu einem Punkt |
| Einfluss der Spielergröße auf die Geschwindigkeit | voll, `{{v:avatar.size-speed-influence}}` | ein größerer Avatar bewegt sich proportional schneller. Gemeint ist die Spur der Spielergröße im Level, nicht der Kamerazoom |
| Drehgeschwindigkeit | `{{v:avatar.turn-speed}}` /s | rein optisch: wohin der Körper zeigt |
| Ankunftsdistanz | `{{v:avatar.arrival-distance}}` Einheiten | näher als das am Cursor gilt als auf ihm stehend |

Daraus abgeleitet, und genau diese Werte entscheiden über ein Ausweichen:

| Was | Wert |
|---|---|
| Kürzester Dash: Weite | `{{v:avatar.arrival-distance}}` Einheiten |
| Kürzester Dash: Dauer | deutlich unter einem Frame |
| Kürzester Dash: Abklingzeit und Unverwundbarkeit | jeweils deutlich unter einem Frame |
| Häufigste Dashes | höchstens jeden zweiten Frame |
| Rückstoßweite | `{{v:avatar.knockback-distance}}` Einheiten |

Was bei einem Treffer passiert - [[7_damage]]

## Bewegung

Du steuerst den Avatar auf eine von zwei Arten, und das Spiel mischt sie nie:
- **Richtung**: WASD, ein Gamepad-Stick, das Gyroskop. Der Avatar bewegt sich dorthin, wohin du drückst, mit Laufgeschwindigkeit. Ein halb gedrückter Stick gibt halbe Geschwindigkeit, ein anderes "langsames Gehen" gibt es nicht
- **Cursor**: die Maus oder ein Finger. Der Avatar jagt dem Punkt nach, statt sich dorthin zu teleportieren. Er bewegt sich mit seiner eigenen Laufgeschwindigkeit und hängt einer schnellen Maus hinterher

Die Bewegung ist in beiden Fällen sofort: keine Beschleunigung, kein Rutschen, keine Trägheit. Du hältst im selben Frame an, in dem du aufhörst, dich zu bewegen

## Der Dash

Die Unverwundbarkeit dauert {{v:avatar.dash-invulnerability-margin}} s länger als die Bewegung. Genau dieser Puffer nach der Landung erlaubt es, *durch* ein Hindernis zu dashen

Während eines Dashs steuerst du weiter. Der Dash geht dorthin, wohin du willst: entlang der gehaltenen Richtung oder zum Zielpunkt, und das kann sich mitten im Dash ändern. Ein Dash ohne gehaltene Richtung bewegt sich nirgendwohin

Mit einem Cursor geht der Dash dorthin, wohin du zeigst, und hält dort an:

| Abstand zum Cursor | Was passiert |
|---|---|
| mehr als {{v:avatar.dash-distance}} Einheiten | ein voller Dash in seine Richtung. Du hältst vor dem Cursor an |
| von {{v:avatar.arrival-distance}} bis {{v:avatar.dash-distance}} Einheiten | ein verkürzter Dash, der genau auf dem Cursor endet |
| weniger als {{v:avatar.arrival-distance}} Einheiten | kein Dash |

Ein verkürzter Dash ist derselbe Dash in kleinerem Maßstab. Weg, Unverwundbarkeit und Abklingzeit schrumpfen gemeinsam: ein halb so langer Dash schützt halb so lange und lädt doppelt so schnell nach. Billiger wird er dadurch nie. Zwei halbe Dashes kosten genau so viel wie ein voller und legen dieselbe Strecke zurück

Ein Dash, der nicht stattfindet, kostet nichts: die Abklingzeit startet nicht, nichts wird verbraucht. Wer per Richtung spielt und nichts gedrückt hält, bekommt dieselbe Antwort - keinen Dash

Der Körper färbt sich während des Dashs tiefer blau und kehrt über die nächsten {{v:avatar.dash-tint-fade}} s zu seiner normalen Farbe zurück. Nichts anderes ändert die Farbe des Körpers, nicht einmal ein Treffer - ein Dash ist deine eigene Bewegung, deshalb nur er

Die Dash-Spur und dieses Blau hängen von der Länge des Dashs ab: ein voller Dash zeigt sie vollständig, der kürzeste mit `{{v:avatar.dash-effect-min}}` davon, alles dazwischen proportional. Ein kurzer Dash wirft seine Partikel langsamer aus, so sieht die Spur genau so lang aus wie der Dash

### Zwei Stile, ein Budget

- Im Modus `{{ui:field_common_direction}}` geht ein Dash immer die vollen {{v:avatar.dash-distance}} Einheiten. Eine verlässliche Weite ohne Zielen, aber auch kein Anhalten auf halbem Weg
- Mit einem Cursor wählst du die Länge und kannst genau auf einem Punkt anhalten. Ein kurzer Dash bedeutet kürzeren Schutz und einen verwundbaren Frame mehr pro Dash. Zeige weit weg, und der volle Dash ist wieder da

Auf gerader Linie legen beide dieselbe Strecke in derselben Zeit zurück. Keiner der Stile ist stärker: der eine bietet Präzision, der andere Einfachheit

### Dash um Dash

**Ein gehaltener Dash ist keine Unverwundbarkeit.** Abklingzeit und Schutz sind gleich lang, eine gehaltene Taste ergibt also eine durchgehende Kette von Dashes. Aber zwischen zwei Dashes gibt es immer genau einen Frame, in dem du getroffen werden kannst, bei jeder Framerate, auf einem langsamen Handy genau wie auf einem schnellen PC.
Die engste Kette ist ein Dash höchstens jeden zweiten Frame

## Die Hitbox

Der Punktring auf dem Avatar ist genau entlang der Hitbox gezeichnet. Ein Geschoss hat den Umriss gestreift und nichts bewirkt? So ist es gewollt

Solange du unverwundbar bist (im Dash oder direkt nach einem Treffer), gibt es überhaupt keine Hitbox

Derselbe Ring zeigt deine Leben: ein leuchtender Punkt ist ein Leben in Reserve

Die Sichtbarkeit des Rings stellst du unter `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_hitbox-ring-opacity}}` ein. `0` blendet ihn aus, aber Levels sind für jemanden ausbalanciert, der ihn sieht

Der Körper ist ein Raster aus {{v:avatar.grid-cells}} Quadraten, {{v:avatar.grid-side}} mal 5. Wenn Leben verloren gehen, verschwinden Quadrate vom Rand zur Mitte nicht, sondern verblassen: ein verlorenes Quadrat bleibt als blasser Geist stehen, das Raster zeigt also immer alle {{v:avatar.grid-cells}}, und das Leben liest sich an der Zahl der noch leuchtenden ab.
Die Geisterquadrate sind durchsichtig genug, um den Hitbox-Ring unter dem Körper zu zeigen.
Bei null Leben leuchtet genau ein Quadrat - das letzte.
Jeder Verlust von Leben wird über `{{v:avatar.health-loss-time}}` s gezeigt, jede Erholung über `{{v:avatar.health-gain-time}}` s, egal um wie viele Leben es geht.
Schaltest du `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics_avatar-render}}` aus, wird der Körper zu einem einzelnen Quadrat, das verblasst. Das ist für schwache Geräte

## Erscheinen und Verschwinden

Der Avatar wächst über `{{v:avatar.spawn-time}}` s ins Level hinein und schrumpft beim Tod über `{{v:avatar.spawn-time}}` s zu einem Punkt. In beiden Fällen reagiert er nicht auf Eingaben, und während er erscheint, kann er nicht getroffen werden

## Skalierung

Ein Level kann Größe und Geschwindigkeit des Avatars mit eigenen Spuren animieren. Es kann auch die Steuerung für eine Weile wegnehmen oder Kollisionen ausschalten

- Lauf-, Dash- und Rückstoßgeschwindigkeit werden mit einer gemeinsamen Zahl multipliziert. Bei halber Geschwindigkeit ist der Dash also auch halb so lang ({{v:avatar.half-speed-dash-distance}} Einheiten)
- Ein größerer Avatar bewegt sich proportional schneller, weil auch seine Ausweichwege gewachsen sind. Größe meint hier die eigene Größe des Avatars aus der Spur der Spielergröße. Der Kamerazoom ändert weder Geschwindigkeit noch Entfernungen noch Zeitfenster: der Avatar legt {{v:avatar.move-speed}} Einheiten pro Sekunde zurück, egal was die Kamera tut
- Die Hitbox ist ein Bruchteil des gezeichneten Körpers, sie wächst und schrumpft also mit dem Avatar
- Das Zielen des Dashs nutzt die aktuelle Weite, nicht die 7,5 aus der Tabelle. In einem Level mit halber Geschwindigkeit verlangt ein Cursor in {{v:avatar.half-speed-dash-distance}} Einheiten Entfernung schon einen vollen Dash, und die Schwelle von {{v:avatar.arrival-distance}} Einheiten wird zu {{v:avatar.half-speed-arrival-distance}}, weil auch der Dash darüber halb so lang ist
- Zeitfenster in Sekunden skalieren nicht: Abklingzeit, Unverwundbarkeit, Schadenspause, Erscheinen. Nur die Länge des Dashs selbst skaliert seine beiden eigenen Zeitfenster

Bots folgen denselben Regeln, [[9_bots]]
