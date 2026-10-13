---
title: Schwierigkeit und Kurve
date: 2026-10-02
tags: [level_author]
---

# Schwierigkeit und Kurve

Plane nach den Zahlen des Spielers - alle stehen auf [[6_avatar]] und [[7_damage]] - und nach einer Reaktion von 12-15 Frames. Zeig ein neues Muster zuerst in sicherer Form

Die eigene Schwierigkeit kannst du nicht beurteilen: Teste das Level mit jemandem, der es zum ersten Mal sieht

## Der Spieler in Zahlen

Die genauen Werte des Avatars stehen auf [[6_avatar]] und [[7_damage]]. Was sie für ein Level bedeuten:

| Was | Was es für das Design bedeutet |
|---|---|
| Hitbox des Spielers | viel kleiner als der gezeichnete Körper, deshalb verfehlt ein Geschoss, das den Körper streift, oft |
| Dash | durchquert fast sofort drei Viertel der Bildschirmhöhe |
| Unverwundbarkeit beim Dash | hält länger als der Dash selbst, deshalb ist ein Dash durch ein dünnes Hindernis sicher |
| Nach einem Treffer | ein kurzer Rückstoß ohne Kontrolle, dann ein Schonfenster, in dem weitere Treffer ignoriert werden |
| Menschliche Reaktion | 0.2-0.25 Sekunden, das sind 12-15 Frames bei 60 fps |
| Startwerte | 3 Leben, Geschwindigkeit 1.0, Checkpoints an |

Daraus folgen Faustregeln:
- eine Lücke von einer Einheit Breite ist breit, eine Lücke von 0.6 ist eng
- ein Dash legt so viel Strecke zurück wie eine halbe Sekunde Laufen

## Ein Treffer tötet nicht sofort

Nach einem Treffer wird der Spieler zurückgestoßen und hat kurz keine Kontrolle.
Danach werden weitere Treffer eine Weile ignoriert ([[7_damage]]). Eine Wand aus zehn Geschossen hintereinander kostet ein Leben, nicht zehn

> [!info] Gut zu wissen
> Die Intuition sagt das Gegenteil. Eine dichte Salve sieht nach sofortigem Tod aus. Tatsächlich ist sie billiger als ein einzelnes Geschoss, das genau dann ankommt, wenn die Unverwundbarkeit abgelaufen ist

## Was der Spieler wählt

Leben, Wiedergabegeschwindigkeit und Checkpoints wählt der Spieler auf dem Startbildschirm.
Standard sind 3 Leben, Geschwindigkeit 1.0, Checkpoints an

Du kannst Checkpoints setzen, aber niemanden zwingen, sie zu benutzen. Und du kannst nicht verbieten, mit halber Geschwindigkeit zu spielen

Plane nach den Standardwerten, aber bau nichts auf der Rechnung "hier stirbt er" auf.
Du gestaltest ein Gefühl, keine Strafe

## Die Schleife

Der Spieler wiederholt immer dieselbe Schleife: spielen, sterben, neu versuchen. Ein gutes Level baut seine Schichten darauf auf, und die Schleife muss sein:
- einfach am Anfang, ohne schwere Mechaniken gleich zu Beginn
- erweiterbar, damit neue Elemente nach und nach kommen und es nicht eintönig wird
- belohnend, denn eine sofortige Belohnung für die richtige Aktion hält die Motivation hoch

## Die Kurve: lehren, prüfen, variieren

1. Zeig das Muster in sicherer Form, in der ein Fehler fast unmöglich ist
2. Verlange es ernsthaft
3. Ändere eine Variable - Geschwindigkeit, Richtung, Anzahl - und verlange es erneut

Taucht ein Muster zum ersten Mal gleich in seiner schweren Form auf, bekommt das Level die Schuld.
Der Spieler stirbt und versteht nicht, was von ihm verlangt wurde

Auch Fairness hat eine Grenze. Zu viel "An-die-Hand-Nehmen" nimmt den Spaß genauso wie Unfairness

## Auswendiglernen

Ein Level, das sich nur aus dem Gedächtnis schaffen lässt, ist ein legitimes Genre. Es muss aber eine Entscheidung sein, kein Zufall

Die Grenze ist einfach: Nach dem Tod muss der Spieler verstehen, was genau er sich merken soll.
Ist es auch nach dem zehnten Tod noch unklar, ist das kein Auswendiglernen, sondern Rauschen

## Mit fremden Augen testen

Dein eigenes Level kannst du selbst nicht beurteilen.
Bis zur Veröffentlichung hast du deine schwere Stelle zweihundertmal geschafft, und für dich ist sie leicht

> [!tip] Empfehlung
> Gib das Level jemandem, der es zum ersten Mal sieht, und schau schweigend zu. Gib keine Hinweise. Eine Stelle, an der jemand dreimal stirbt und fragt, was verlangt wurde, ist nicht schwer, sondern unklar

## Fang kurz an

Mach dein erstes Level 1-2 Minuten lang.
Das Interesse geht eher zu Ende als der Song. Ein Level von vier Minuten ist viermal so viel Arbeit und zehnmal so viele Gründe aufzuhören

Weiter: [[1_readability-and-fairness|Lesbarkeit und Fairness]], [[4_composition-and-camera|Komposition und Kamera]]
