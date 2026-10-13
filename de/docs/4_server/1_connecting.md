---
title: Mit einem Server verbinden
date: 2026-10-01
tags: [player]
---

# Mit einem Server verbinden

Das Spiel bekommt den offiziellen Server OWS für alle Builds und Community-Server NOWS nur für den vollen Build. Bullet Hero moderiert NOWS nicht, verbinde dich also nur mit Betreibern, die du kennst

> [!warning] Warnung
> Es gibt noch keine Server, und das Spiel kann sich nicht mit ihnen verbinden. Es gibt kein Adressformat, keinen Verbindungsbildschirm und keine Konten

## Welche Server es geben wird

| | OWS | NOWS |
|---|---|---|
| Voller Name | Official Web Services | Non-official web services |
| Wer ihn betreibt | Bullet Hero | jeder |
| Wer moderiert | Bullet Hero | der Betreiber des Servers |
| Welche Builds sich verbinden | alle | nur der volle Build |

**OWS ist der Standardserver.** Jeder Build des Spiels auf jeder Plattform kennt ihn, einrichten musst du nichts

**NOWS sind Community-Server.** Bullet Hero kontrolliert und moderiert sie nicht

**Der Steam Workshop ist auf dem PC ein dritter Kanal für Levels.** Steam-Builds listen und starten die Inhalte, die du abonniert hast, und veröffentlichen aus dem Editor Levels und Sammlungen dort - [[17_publishing]]

## Welche Builds sich verbinden

| Build | Woher | OWS | NOWS |
|---|---|---|---|
| Store-Build | Google Play, App Store | ja | nein |
| Voller Build | [GitHub](https://github.com/bullet-hero/releases) und die Website des Projekts | ja | ja |

Ein Store-Build kann sich auf keinem Weg mit einem Community-Server verbinden.
Die Unterstützung für NOWS wird beim Kompilieren aus ihm entfernt, nicht hinter einer Einstellung versteckt

Der Grund sind die Regeln der Stores. Ein Store beurteilt, was ein Programm kann, nicht welche Schaltflächen es zeigt. Und Inhalte, die andere Menschen sehen, müssen nach seinen Regeln moderiert werden

Der volle Build soll eine eigene Anwendungs-ID bekommen, damit er sich unter Android neben der Store-Version installieren lässt. Im Moment teilen sich alle Android-Builds eine ID, `com.vertoker.BulletHero`

## Was OWS haben wird

- Konten und Nutzungsbedingungen
- eine Prüfung jedes Levels vor der Veröffentlichung: Ein Level mit einem Fehler wird abgelehnt, ein Level mit einer Warnung geht an einen Moderator
- Meldungen zu Levels und Nutzern und deren Sperrung

Was ein Konto speichert, ist noch nicht entschieden. Der Server bekommt eine eigene Datenschutzerklärung, die zusammen mit dem Server erscheint. Sie wird das Konto beschreiben und erklären, wie man es löscht. Die Erklärungen des Spiels und der Website gelten nicht für den Server - [[game-privacy-policy]], [[privacy-policy]]

## Wann

Das Veröffentlichen im Steam Workshop funktioniert in Steam-Builds bereits. Für den Rest gibt es keine Termine. Die Reihenfolge ist: OWS, dann der Build für Google Play, dann der Build für den App Store

Gemeinsames Spielen auf einem Server gibt es noch nicht, es ist nicht entworfen

## Risiken fremder Server

Einen Community-Server betreibt eine Person, die du höchstwahrscheinlich nicht kennst.
Bullet Hero kontrolliert und moderiert solche Server nicht. Die EULA des vollen Builds sagt das direkt

| Risiko | Warum |
|---|---|
| Levels mit ungeprüften Rechten | der Betreiber entscheidet, was er prüft, und prüft vielleicht gar nichts. Ein Level kann Musik enthalten, die sein Autor nicht weitergeben durfte |
| Niemand moderiert die Inhalte | es gibt keine Garantie, dass sich jemand ansieht, was hochgeladen wird |
| Dateien von anderen Websites | die Standardrichtlinie erlaubt einem Level, eine Datei per Direktlink zu beziehen. Wenn du ein solches Level öffnest, lädt das Spiel die Datei von einer Website herunter, die der Autor des Levels gewählt hat. Deshalb verbieten Store-Builds das |
| Der Betreiber sieht deinen Datenverkehr | es gibt noch kein Protokoll, daher ist unbekannt, was genau der Server erhält. Geh davon aus, dass der Betreiber alles sieht, was du sendest |
| Der Server kann verschwinden | ein Level, das nur auf diesem Server existiert, verschwindet mit ihm |

Standardmäßig wird ein Level unter *CC BY-NC* verbreitet, und der Autor kann in den Metadaten des Levels eine andere Lizenz wählen. Ein Server muss die Lizenz jedes Levels respektieren. Unter *CC BY-NC* darf niemand ein Level kommerziell hosten, auch kein Community-Server, und ein Server, der für solche Levels Geld verlangt, verletzt die Lizenz jedes ihrer Autoren

> [!tip] Empfehlung
> Verbinde dich nur mit Servern, deren Betreiber du kennst. Behalte eine eigene Kopie jedes Levels, das dir wichtig ist: Ein Level ist ein Ordner mit Dateien, und die Kopie auf deiner Festplatte hängt von keinem Server ab

## EULA

Der volle Build wird mit einer EULA ausgeliefert. Sie sagt: Community-Server sind Dienste Dritter, Bullet Hero kontrolliert und moderiert sie nicht

Store-Builds werden dich bitten, vor dem Veröffentlichen eines Levels eine EULA zu akzeptieren

Keiner dieser Texte ist bisher geschrieben

## Was du als Nächstes lesen kannst

- [[ugc-licensing-policy]] - welche Regeln ein Level für die Veröffentlichung erfüllen muss
- [[2_hosting]] - wenn du selbst einen Server betreiben willst
