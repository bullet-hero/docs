---
title: "Frames, Zeit und die Länge eines Levels"
date: 2026-10-12
tags: [level_author]
---

# Frames, Zeit und die Länge eines Levels

Ein Level zählt die Zeit in eigenen Frames, nicht in Bildschirmframes, und läuft daher auf jeder Hardware gleich. Die Länge legst du fest, die fps lässt du am besten beim Standard, 60

## Levelframes und Bildschirmframes

Ein Levelframe hat mit einem Bildschirmframe nichts zu tun.
Der Bildschirm zeichnet so viele Frames pro Sekunde, wie die Hardware schafft. Ein Level zählt die Zeit in eigenen Frames, und wie viele es pro Sekunde sind, steht im Level selbst. Standard ist `60`

Ein Level läuft also bei 60 Hz, bei 144 Hz und auf einem Handy, das auf 30 gefallen ist, gleich. Die Treffgenauigkeit hängt nicht von der Grafikkarte ab

Ein Frame ist eine Zelle, kein Zeitpunkt. Endet ein Objekt in Frame 100 und beginnt ein anderes in Frame 100, überschneiden sie sich nicht

Genauer: Frames zählen ab 1, und Frame f umfasst die Zeit von (f-1)/fps bis f/fps, linker Rand eingeschlossen, rechter nicht. Frame 1 beginnt also ganz am Anfang des Songs

## Die Länge eines Levels

Die Länge des Levels legst du fest. Die Länge des Songs kommt aus der Datei. Sie müssen nicht übereinstimmen

Inhalt hinter dem Ende des Levels ist erlaubt. Er wird einfach nie abgespielt, und die Validierung beschwert sich nicht darüber. Ein Objekt darf über das Ende hinausreichen, aber der KI-Assistent kann keines erstellen, das danach beginnt

Ein Kind, das aus der Spanne seines Elternobjekts herausragt, verhält sich genauso. Das Level behält, was du eingetragen hast, und die wirksame Lebenszeit wird getrennt berechnet

Um die Lebenszeiten von Kindern und Elternobjekten aneinander anzupassen, nimm den Modifikator `{{ui:mod_span_fit}}` in `{{ui:editor_generators_text}}`. Er zieht entweder die Kinder hinein oder verbreitert die Elternobjekte

## Die fps des Levels

Je höher die fps, desto genauer triffst du den Beat. Und desto mehr Frames braucht dieselbe Länge.
Der Bereich ist 1 bis 1000, Standard ist `60`

> [!tip] Empfehlung
> Lass die fps beim Standard. Bei 60 hört das Ohr eine Verschiebung um einen Frame nicht, und die Zahl der Keyframes wächst mit der fps

Die Zeitleiste ist auf `1000000` Frames begrenzt. Das sind bei 60 fps etwa 4,6 Stunden und bei 1000 etwa 17 Minuten

> [!warning] Warnung
> Die fps eines fertigen Levels zu ändern heißt, jeden Keyframe darin neu zu berechnen. Das erledigt der Modifikator `{{ui:mod_framerate_remap}}`, von Hand ist das nicht machbar

Weiter: [[5_keyframes-and-easing]], [[2_rhythm-and-structure]], [[1_order-of-work]]
