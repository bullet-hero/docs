---
title: Server für Freunde
date: 2026-10-01
tags: [server_host]
---

# Server für Freunde

Du brauchst die offenen Serverwerkzeuge, den vollen Build des Spiels für jeden Spieler und eine PublishProfile-Datei. Moderation und die Lizenzen der Levels liegen beim Betreiber des Servers

> [!warning] Warnung
> Die Serverwerkzeuge sind nicht veröffentlicht, das Protokoll ist nicht entworfen. Diese Seite enthält nur, was bereits entschieden ist

## Was du brauchst

- **Serverwerkzeuge.** Sie werden offen sein, unter MIT. Es ist derselbe Code, auf dem der offizielle Server läuft. Du kannst deinen eigenen Server auf diesen Werkzeugen aufbauen oder auf allem, was darauf basiert
- **Den vollen Build des Spiels für alle, die sich verbinden.** Builds aus Google Play und dem App Store verbinden sich nicht mit Community-Servern. Den vollen Build gibt es auf [GitHub](https://github.com/bullet-hero/releases) und auf der Website des Projekts
- **Ein Veröffentlichungsprofil.** Die Datei `PublishProfile` entscheidet, welche Levels dein Server annimmt. Mehr - [[7_publish-profiles]]
- **Einen Rechner für den Server.** Systemanforderungen, Laufzeitumgebung, Ports und die Art, ihn zu starten, sind noch nicht bekannt

## Veröffentlichungsprofil

Das Profil legt fest, welche Lizenzen angenommen werden, woher ein Level Dateien beziehen darf und wie groß es höchstens sein darf.
Dafür muss kein Code geändert werden

Der offizielle Server läuft mit dem Preset `standard`, das in der Serverkonfiguration gesetzt ist. Fang damit an und lockere oder verschärfe es nach deinem Bedarf

## Was du übernimmst

- **Moderation.** Bullet Hero moderiert keine Community-Server. Die EULA des vollen Builds teilt das jedem Spieler mit
- **Kein Kommerz.** Standardmäßig wird ein Level unter *CC BY-NC* verbreitet, und der Autor kann eine andere Lizenz wählen. Respektiere die Lizenz jedes Levels. Ein Level unter *CC BY-NC* darf kostenlos gehostet und geteilt werden, aber du darfst kein Geld dafür verlangen und auch auf keine andere Weise daran verdienen
- **Rechte an Ressourcen.** Ein Level kann fremde Musik und Grafik enthalten. Wie streng das geprüft wird, entscheidet dein Profil. Eine Beschwerde über ein fremdes Werk landet aber bei dir. Die Regeln des offiziellen Servers - [[ugc-licensing-policy]]

Die Erlaubnis zur nicht kommerziellen Verbreitung gibt der Autor jedes Levels, nicht das Spiel. Deshalb kann nur der Autor eine Ausnahme machen

## Was unbekannt ist

- wie das Spiel einen Server findet und sich mit ihm verbindet
- ob ein Community-Server Konten haben wird
- wie Levels hochgeladen werden und in die Liste kommen
- ob ein Server für wenige Leute anders eingerichtet wird als ein öffentlicher

Was es für einen großen Server bereits gibt - [[3_advanced-hosting]]
