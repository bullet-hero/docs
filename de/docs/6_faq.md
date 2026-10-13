---
title: FAQ
date: 2026-10-02
tags: [player, level_author]
---

# FAQ

Bullet Hero ist eine kostenlose Mischung aus Rhythmusspiel und Bullet Hell. Kein Konto nötig, noch kein Server. Spieler bauen Levels im Editor und geben sie als Ordner oder Archiv weiter

## Das Spiel

### Was ist Bullet Hero?

Eine Mischung aus *Rhythmusspiel* und *Bullet Hell*. Ein Level ist Musik und Formen, die sich zu ihr bewegen. Du steuerst ein kleines Quadrat, und es muss bis zum Ende des Tracks überleben

Bullet Hero ist als Engine für das Genre gebaut. Deshalb stammen die meisten Levels von Spielern, gebaut im eingebauten Editor.
Mehr - [[1_game/index]]

### Ist das Spiel kostenlos?

Ja. Das Spiel hat keine Käufe, keine Werbung und keine kostenpflichtigen Inhalte.
Mehr - [[1_licensing-basics]]

### Wo bekommt man es?

Alle Builds und Stores - [[download]]

Das Spiel ist veröffentlicht, Version `gv {{v:version.gv}}`. Die Builds sind nicht signiert

### Braucht es ein Konto oder Internet?

Nein. Es gibt keine Konten und keinen Server, und das Spiel sendet nichts irgendwohin

Internet braucht nur eine Art von Level: eines, das eine Datei von der Webadresse seines Autors lädt.
Mehr - [[1_installation]]

### Wo werden die Levels gespeichert?

Im Ordner `levels` im Datenordner des Spiels. So öffnest du ihn: `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general-open_folder}}`.
Mehr - [[1_installation]]

## Levels spielen

### Wie spielt man ein Level, das einem jemand geschickt hat?

Leg den Ordner in `levels` und drück in der Levelliste `{{ui:root_level-browser_refresh}}`.
Ein Archiv (`.zip`, `.tar.gz`) öffnest du über den Editor, mit dem Generator `{{ui:gen_level_archive}}`.
Mehr - [[2_playing-levels]]

### Das Spiel sagt, das Level stammt aus einer neueren Version. Was jetzt?

Aktualisiere das Spiel. Eine alte Version öffnet keine Dateien aus einer neueren, damit sie sie nie falsch liest.
Mehr - [[5_troubleshooting]]

### Lässt sich ein vergessenes Levelpasswort wiederherstellen?

Nein. Der Schlüssel wird nirgends gespeichert: nicht im Spiel, nicht in der Datei, bei niemandem.
Mehr - [[5_troubleshooting]]

### Kann das Spiel ein Level selbst spielen?

Ja, mit der Bedingung `{{ui:menu_levelview_options-bot}}` auf dem Levelbildschirm: `{{ui:enum_bot-kind_reflex}}` oder `{{ui:enum_bot-kind_warm}}`. Ein Bot hat dieselbe Steuerung wie du, und er kann auch verlieren.
Mehr - [[9_bots]]

## Levels bauen

### Wie baut man ein erstes Level?

`{{ui:menu_main_editor-btn}}` im Hauptmenü, dann `{{ui:settings_editor-settings_editor-settings}}`, dann `{{ui:settings_editor-settings_create-level}}`.
Kopier einen Track in den Levelordner, stell das Tempo (BPM) ein, setz ein Objekt mit zwei Keyframes und starte einen Testlauf.
Mehr - [[2_first-level]]

### Welche Musikdateien funktionieren?

`ogg`, `mp3` und `wav`, sonst nichts. `flac`, `aiff` und Tracker-Module laden nicht

`ogg` ist die beste Wahl. Die Datei ist 8-10 Mal kleiner als `wav` und fügt, anders als `mp3`, am Anfang keine Stille hinzu.
Mehr - [[2_preparing-the-track]]

### Kann ich jeden beliebigen Song verwenden?

Auf deiner eigenen Festplatte wird nichts geprüft. Die Lizenz der Musik zählt erst, wenn ein Level einem Dienst angeboten wird, und solche Dienste gibt es noch nicht.
Mehr - [[1_licensing-basics]]

### Wie teilt man ein Level?

Von Hand, als Ordner oder Archiv. Ein Steam-Build kann ein Level außerdem im Steam Workshop veröffentlichen. Einen offiziellen Server gibt es noch nicht.
Mehr - [[6_sharing-by-hand]], [[17_publishing]]

## Das Projekt

### Gibt es Online-Bestenlisten oder einen Levelkatalog?

Noch nicht. Der offizielle Server und die Community-Server sind in Entwicklung.
Mehr - [[4_server/index]]

### Warum ist der Code des Spiels geschlossen?

Dafür habe ich persönliche Gründe.
Wenn die Entwicklung endgültig aufhört, werden alle Repositorys offen, und die Organisation [bullet-hero](https://github.com/bullet-hero) kann an jemand anderen übergeben werden

Das SDK, die Dokumentation und der künftige Server sind schon offen. Mehr - [[index]]

### Einen Bug gefunden?

Melde einen Bug im Spiel unter [bullet-hero/releases](https://github.com/bullet-hero/releases/issues). Mit Fragen komm auf [Discord](https://discord.gg/gkHQrp9NgS).
Wo du schreibst und was du anhängst - [[11_help]]

Alle Links des Projekts - [[links]]
