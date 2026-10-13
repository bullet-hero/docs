---
title: Schaden und Leben
date: 2026-10-02
tags: [advanced_player]
---

# Schaden und Leben

Jeder Treffer kostet ein Leben, stößt den Avatar {{v:avatar.knockback-time}} s zurück und gibt {{v:avatar.damage-timeout}} s Unverwundbarkeit. Standardmäßig spult ein Tod zum letzten Checkpoint zurück und stellt deine Leben wieder her

## Ein Treffer in drei Phasen

1. **Der Stoß, `{{v:avatar.knockback-time}}` s.** Du wirst mit `{{v:avatar.knockback-speed}}` Einheiten pro Sekunde von dem weggestoßen, was dich getroffen hat. Das sind etwa {{v:avatar.knockback-distance}} Einheiten, ein ganzer Dash, drei Viertel der Standard-Bildschirmhöhe. Währenddessen werden keine Eingaben angenommen. Aus dem Stoß kannst du nicht herausdashen: der Rückstoß hat Vorrang vor allem
2. **Die Steuerung kehrt zurück** nach diesen {{v:avatar.knockback-time}} s
3. **Du kannst nicht getroffen werden**, und zwar ganze `{{v:avatar.damage-timeout}}` s ab dem Moment des Treffers. Jeder Treffer in dieser Sekunde wird ignoriert

Stehst du genau auf dem, was dich getroffen hat, gibt es keine Richtung für den Stoß. Dann wirst du gar nicht zurückgestoßen

Ebenfalls nicht getroffen werden kannst du beim Erscheinen (`{{v:avatar.spawn-time}}` s) und während der `{{v:avatar.dash-invulnerability}}` s Dash-Schutz, [[6_avatar]]

> [!info] Gut zu wissen
> Wer in einer Gefahrenzone sitzen bleibt, verliert ein Leben, nicht zehn. Auch ein Stoß in eine zweite Gefahrenzone ist überlebbar. Eine dichte Salve sieht nach sofortigem Tod aus, kostet aber oft weniger als ein einzelnes Geschoss, das genau am Ende der Schutzsekunde ankommt

## Leben

Die Zahl der Leben wird auf dem Levelbildschirm gewählt: `{{ui:menu_levelview_options-lifes_option-zen}}`, `{{ui:menu_levelview_options-lifes_option-one}}`, `{{ui:menu_levelview_options-lifes_option-three}}` oder `{{ui:menu_levelview_options-lifes_option-custom}}` bis 16, [[2_playing-levels]]

Jeder Treffer kostet ein Leben. Ein Treffer, der das letzte nimmt, ist ein Tod.
`{{ui:menu_levelview_options-lifes_option-zen}}` reagiert auf Treffer wie jeder andere Durchlauf - der Stoß, der Schildring, der Partikelausbruch und die Schutzsekunde wirken wie gewohnt, und der Treffer zählt in der Statistik -, aber ein Leben wird nie verbraucht, also endet der Durchlauf nie

Deine Leben zeigt der Punktring um den Avatar: ein leuchtender Punkt ist ein Leben in Reserve, ein erloschener ist verbraucht.
Das Ergebnisfenster zeigt `{{ui:game_game-result_hits}}` und `{{ui:game_game-result_lives-left}}`

## Was ein Tod bewirkt

Standardmäßig beendet ein Tod den Durchlauf nicht:

1. Die Leveluhr bremst über `{{v:checkpoint.rewind-time}}` s Echtzeit sanft bis zum Stillstand ab. Die Musik sackt mit ab
2. Das Level springt zurück zum zuletzt erreichten Checkpoint. Die Leben werden wiederhergestellt
3. Die Uhr beschleunigt über weitere `{{v:checkpoint.rewind-time}}` s sanft wieder auf Spieltempo. Während der Beschleunigung kannst du nicht getroffen werden, sonst würde ein Checkpoint neben einer gefährlichen Stelle in der ersten Sekunde alle deine Leben kosten

Die Pause hält auch diese Beschleunigung an

Ist `Checkpoints` auf dem Levelbildschirm ausgeschaltet, geht das Zurückspulen zum Anfang des Levels

Soll ein Tod das Ergebnisfenster öffnen, schalte `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_open-menu-on-lose}}` ein. Die Wiedergabe hält dann an.
In diesem Fenster startet `{{ui:game_game-result_restart-checkpoint}}` einen neuen Versuch ab dem erreichten Checkpoint

## Checkpoints

Checkpoints setzt der Autor des Levels. Ob sie zählen, entscheidest du mit dem Schalter `Checkpoints`

Der erreichte Checkpoint ist der letzte an oder vor der aktuellen Position im Level. Zu ihm zurückzukehren macht also nichts rückgängig, es spult nur zurück

Der Autor kann einen Checkpoint so einstellen, dass er Leben wiederherstellt. Dann stellt das Passieren deine Leben einmal wieder her, mitten im Durchlauf

Der Fortschrittsbalken unten am Bildschirm hat an jedem Checkpoint eine Markierung. Der Balken wird unter `{{ui:settings_interface_label}}` → `{{ui:settings_interface_show-game-progress}}` eingeschaltet

Rekorde mit und ohne Checkpoints werden getrennt geführt, [[10_statistics]]

## Ohne Kollision

`{{ui:menu_levelview_options-no-collision_title}}` ist ein eigener Schalter, getrennt von `{{ui:menu_levelview_options-lifes_option-zen}}`, neben `Checkpoints` auf dem Levelbildschirm und im Startbereich des Editors. Schaltest du ihn ein, geht der Avatar durch alles hindurch: nichts kann ihn mehr berühren

Ein Durchlauf mit `{{ui:menu_levelview_options-no-collision_title}}` führt eigene Rekorde, getrennt von `{{ui:menu_levelview_options-lifes_option-zen}}` und von normalen Durchläufen, und das Ergebnisfenster kennzeichnet ihn mit dem Zusatz `· Ohne Kollision` beim Wert von `{{ui:menu_levelview_options-lifes_title}}`, [[10_statistics]]
