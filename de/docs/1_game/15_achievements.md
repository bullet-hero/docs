---
title: Erfolge
date: 2026-10-17
tags: [player]
---

# Erfolge

Erfolge schalten sich anhand deiner Statistik von selbst frei. Es zählen nur Level anderer Leute und nur fair gespielte Läufe. Die Liste findest du im Hauptmenü unter `{{ui:menu_main_achievements-btn}}`

## Die Liste

`{{ui:menu_main_achievements-btn}}` im Hauptmenü öffnet alle Erfolge deines Builds, nach Gruppen. Ein gesperrter Erfolg zeigt deinen Fortschritt, ein freigeschalteter den Tag der Freischaltung. Ein geheimer Erfolg erscheint als `{{ui:menu_achievements_hidden_name}}`, bis er freigeschaltet ist

## Was zählt

**Ein fairer Lauf** ist einer, bei dem:

- kein Bot spielt
- Kollisionen an sind
- die Geschwindigkeit `{{v:achievements.fair-min-speed}}` oder höher ist
- du Leben hast: ein Lauf in `{{ui:menu_levelview_options-lifes_option-zen}}` zählt nur, wo ein Erfolg genau das verlangt

Checkpoints sind erlaubt. Ein aus dem Editor gestarteter Lauf zählt nie, er setzt auch keinen Rekord - [[10_statistics]]

**Nicht dein eigenes Level.** Ein Level, das du auf diesem Gerät im Editor geöffnet hast, ist deins. Es abzuschließen zählt nur für den Erfolg, der das Testen deines eigenen Levels belohnt. Mitgelieferte Level, Workshop-Level und Level von Freunden zählen

## Wo es gespeichert wird

`stats/achievements.json`, neben der Statistik. Die Datei merkt sich nur, wann jeder Erfolg freigeschaltet wurde. Ob ein Erfolg freigeschaltet ist, wird jedes Mal aus der Statistik entschieden, darum kann die Datei nicht verloren gehen: Lösch sie, und beim nächsten Start kommt alles Verdiente mit dem Datum dieses Tages zurück

Das Löschen der Statistik in den Einstellungen behält deine Erfolge. Profilübertragung und Steam Cloud nehmen die Datei mit: Auf zwei Geräten landen alle Erfolge, die auf einem der beiden freigeschaltet wurden - [[14_profile-transfer]]

## Steam

In einem Steam-Build wird jeder Erfolg auch auf Steam freigeschaltet, und Steam zeigt seine eigene Benachrichtigung. Steams Eintrag gewinnt: Ein Erfolg, den Steam hat, wird im Spiel mit Steams Datum freigeschaltet. Einer, den das Spiel hat und Steam nicht, wird erneut freigeschaltet, wenn deine Statistik ihn noch rechtfertigt

## Google Play

In der Google-Play-Version wird jeder Erfolg auch in Google Play Spiele freigeschaltet, sobald du dort angemeldet bist, und Google Play Spiele zeigt seine eigene Benachrichtigung. Sein Eintrag gewinnt wie der von Steam. Ohne Anmeldung bleiben die Erfolge nur im Spiel

Alle anderen Builds und die Google-Play-Version ohne Anmeldung zeigen die eigene Benachrichtigung des Spiels oben auf dem Bildschirm
