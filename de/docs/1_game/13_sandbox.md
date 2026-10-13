---
title: Sandbox und Tutorial
date: 2026-10-02
tags: [player]
---

# Sandbox und Tutorial

Die Sandbox ist eine Arena im Hauptmenü, in der du den Avatar bewegen, jeden der sechs Angriffe auf dich abfeuern und das Tutorial mit sechs Schritten machen kannst. Ein Level brauchst du dafür nicht

Beim ersten Start bietet das Spiel das Tutorial einmal an: `{{ui:menu_tutorial-offer_confirm}}` öffnet die Sandbox mit dem Tutorial, `{{ui:menu_tutorial-offer_cancel}}` schließt das Angebot endgültig. Die Sandbox selbst bleibt in beiden Fällen im Menü

## Der Bereich

Die Sandbox hat einen Bereich links. Ein Klick auf seinen Griff klappt den Bereich ein, Ziehen am Griff macht ihn breiter oder schmaler. Der Bereich hat fünf Tabs:

| Tab | Was er tut |
|---|---|
| `{{ui:sandbox_tab_home}}` | was die Sandbox ist und was jeder Tab tut |
| `{{ui:sandbox_tab_tutorial}}` | die Schritte des Tutorials und was gerade zu tun ist |
| `{{ui:sandbox_tab_controls}}` | der Modus des Geräts, mit dem du gerade steuerst, der Schalter für den Bewegungssensor und ein Weg zu allen Steuerungseinstellungen |
| `{{ui:sandbox_tab_attacks}}` | feuert jeden der sechs Angriffe von Hand ab oder lässt Wellen von selbst kommen |
| `{{ui:sandbox_tab_game}}` | Leben, Angriffsgeschwindigkeit, der Bot und die freie Kamera |

`{{ui:settings_common_title}}` öffnet die Einstellungen des Spiels über der Sandbox. `{{ui:sandbox_panel_exit}}` führt zurück ins Hauptmenü

## Pause

Die Pausenschaltfläche liegt oben rechts auf dem Bildschirm. Auch `Esc` öffnet die Pause, statt die Sandbox zu verlassen. Die Pause hält alles an, wie in einem Level: den Avatar, die Angriffe und das Tutorial. Das Pausenfenster bietet `{{ui:root_error_continue}}`, `{{ui:settings_common_title}}` und `{{ui:game_game-result_back-to-menu}}`

## Tutorial

Sechs Schritte, der Reihe nach:

1. `{{ui:sandbox_tutorial_move_title}}` - etwa eine Bildschirmbreite zurücklegen
2. `{{ui:sandbox_tutorial_dash_title}}` - dreimal dashen
3. `{{ui:sandbox_tutorial_dodge_title}}` - 10 Sekunden unter verlangsamten Salven ohne Treffer überstehen. Ein Treffer startet die Zählung neu
4. `{{ui:sandbox_tutorial_dash-through_title}}` - der Ring wächst über die Bildschirmränder hinaus, der einzige Ausweg ist also ein Dash durch seinen Rand. Du musst zwei Ringe schaffen - ein misslungener Ring macht einen schon geschafften nicht ungültig. Während eines Dashs trifft dich nichts
5. `{{ui:sandbox_tutorial_choose-mode_title}}` - probiere die Modi auf dem Tab `{{ui:sandbox_tab_controls}}` aus und drücke `{{ui:sandbox_tutorial_confirm-mode}}`
6. `{{ui:sandbox_tutorial_done_title}}` - `{{ui:sandbox_tutorial_play-level}}` startet das Tutorial-Level

Während ein Schritt in der Arena gespielt wird, klappt der Bereich ein, und der Schritt erscheint als kleine Karte oben auf dem Bildschirm. Berührungen gehen durch die Karte hindurch. Der Griff öffnet den Bereich trotzdem. Bei den Schritten `{{ui:sandbox_tutorial_choose-mode_title}}` und `{{ui:sandbox_tutorial_done_title}}` öffnet sich der Bereich von selbst, auf dem Tab `{{ui:sandbox_tab_tutorial}}`

Ein Treffer oder ein Tod startet nur den Schritt neu, in dem er passiert ist, nicht das ganze Tutorial, und der Schritt wird rot, bis er geschafft ist. Geschaffte Schritte sind grün

Ein Klick auf einen Schritt in der Liste startet diesen Schritt, auch einen schon geschafften. Nach einem geschafften Schritt geht das Tutorial zum nächsten nicht geschafften weiter. Das Tutorial gilt erst als abgeschlossen, wenn jeder Schritt geschafft ist - erst dann wird es auch in die Statistik geschrieben. `{{ui:sandbox_tutorial_restart}}` auf demselben Tab startet es jederzeit neu

> [!warning] Warnung
> Mit `{{ui:sandbox_game_immortal}}` auf dem Tab `{{ui:sandbox_tab_game}}` werden Treffer gar nicht gezählt, also sehen die Schritte `{{ui:sandbox_tutorial_dodge_title}}` und `{{ui:sandbox_tutorial_dash-through_title}}` sie auch nicht. Behalte ein paar Leben, während du das Tutorial machst

## Steuerung

Modi ändern sich für das Gerät, das gerade steuert, und werden sofort gespeichert. Der Bewegungssensor hat keinen Modus `{{ui:enum_control-mode_relative}}`. Was jeder Modus bedeutet - [[3_controls#Steuerungsmodi]]

## Angriffe und Spiel

- `{{ui:sandbox_attacks_auto}}` feuert zufällige Wellen mit einem Abstand von `{{ui:sandbox_attacks_gap}}`, wie im Hintergrund des Hauptmenüs
- `{{ui:sandbox_attacks_clear}}` entfernt alle Angriffe vom Bildschirm
- `{{ui:sandbox_game_speed}}` verlangsamt oder beschleunigt nur die Angriffe. Der Avatar bewegt sich immer mit seiner eigenen Geschwindigkeit
- Leben: `{{ui:sandbox_game_immortal}}`, 1, 3 oder 5. Sind sie aufgebraucht, kommen sie zurück, die Sandbox endet nicht
- `{{ui:sandbox_game_bot}}` übergibt den Avatar an denselben Bot, der im Hintergrund des Hauptmenüs spielt
- `{{ui:sandbox_game_free-camera}}` lässt dich über die Bildschirmränder hinausschauen: die Ansicht bewegst du mit der mittleren Maustaste oder zwei Fingern, zoomen geht mit dem Mausrad oder durch Auseinanderziehen der Finger. Der blaue Rahmen zeigt, was die Levelkamera sieht, und `{{ui:sandbox_camera_back}}` bringt die Ansicht dorthin zurück. Steuerung, Dash und Angriffe funktionieren genauso wie ohne sie
- Ein Tod läuft ab wie in einem Level: die Angriffe werden langsamer und verschwinden, der Avatar erscheint in der Mitte mit vollen Leben
