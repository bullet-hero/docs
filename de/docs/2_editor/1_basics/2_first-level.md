---
title: "Dein erstes Level: der Weg"
date: 2026-10-02
tags: [level_author]
---

# Dein erstes Level: der Weg

Sechs Schritte bis zum ersten Testlauf: Level erstellen, Song hinzufügen, Rhythmus festlegen, Objekte platzieren, Testlauf starten, speichern

## Sechs Schritte

Das ist nur die Reihenfolge der Arbeit. Was jedes Feld macht, erklärt die Hilfe neben seinem Bereich

**1. Level erstellen.** `{{ui:settings_editor-settings_editor-settings}}` → `{{ui:settings_editor-settings_create-level}}`. Wähle ein Preset, gib einen Namen und eine Dauer an. Die Dauer lässt sich später ändern

**2. Song hinzufügen.** Kopiere die Audiodatei in den Levelordner und binde sie ein. `ogg` funktioniert am besten, `flac` wird nicht geladen. Mehr - [[2_preparing-the-track]]

**3. Rhythmus festlegen.** Der Tab `{{ui:editor_inspector-beat_tab}}`: BPM, Versatz, Beats pro Takt. Das Raster ist nicht für das Spiel da, sondern für dich: Inhalte rasten daran ein

Du kennst das Tempo nicht? Klopf es im Fenster `{{ui:editor_beat-window_title}}` (`Shift+T`) zum Song mit. Für das Tippen selbst gibt es keine Standardtaste

**4. Erste Objekte platzieren.** Erstelle ein Objekt, gib ihm eine Form und setze zwei Keyframes auf seine Position. Den Wert zwischen den Keyframes bewegt das Spiel selbst

**5. Prüfen.** Starte einen Testlauf direkt aus dem Editor. Höchstwahrscheinlich bewegt sich alles entweder viel zu schnell oder viel zu langsam. Das ist normal: die Geschwindigkeit stimmt man immer nach Gehör ab

**6. Speichern.** `Ctrl+S`

Autospeichern ist standardmäßig an. {{v:editor.autosave-delay}} Sekunden nach einer ungespeicherten Änderung speichert es das Level und legt eine Kopie davon in `backups/<level id>/` ab. Mehr - [[4_not-losing-work#Autospeichern]]

## Halte das erste Level klein

> [!tip] Empfehlung
> Nimm einen kurzen Song, 1-2 Minuten. Ein Level von 4 Minuten ist viermal so viel Arbeit und zehnmal so viele Gründe, es unfertig liegen zu lassen

Fang mit dem einfachsten Muster an, das funktioniert, nicht mit dem schwierigsten, das dir eingefallen ist.
Spiel das Level selbst von Anfang bis Ende durch, bevor du es jemandem zeigst

Generatoren, Prefabs und Modifikatoren heb dir für später auf. In einem großen Level sparen sie Zeit, im ersten stehen sie im Weg

## Der Song und die Rechte

Ein Song für dich selbst braucht niemandes Erlaubnis. Die Rechte werden erst beim Veröffentlichen geprüft.
Mehr - [[1_licensing-basics]]

Die vollständigen Regeln für das Veröffentlichen auf dem offiziellen Server - [[ugc-licensing-policy]]

## Wie geht es weiter?

Wie der Editor funktioniert - [[3_how-the-editor-thinks]]

Nach dem ersten Testlauf - Leveldesign: [[2_editor/4_craft/index]]

Wenn das Level über eine Skizze hinauswächst - [[1_order-of-work]]
