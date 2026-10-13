---
title: Metadaten und ein Level teilen
date: 2026-10-11
tags: [level_author]
---

# Metadaten und ein Level teilen

Die Metadaten sind das Cover des Levels: Name, Beschreibung, Bild, Autoren, Altersfreigabe und Inhaltswarnungen. Heute erreicht ein Level andere als Ordner oder über den Steam Workshop

> [!warning] Warnung
> Den offiziellen Server und die Website für Levels gibt es noch nicht. Sie kommen mit einem Update nach `gv 1.0.0`. Bis dahin teilt man ein Level als Ordner oder, in einem Steam-Build, über den Steam Workshop. Beide Wege stehen am Ende der Seite

## Die Metadatendatei

Das Cover des Levels liegt in einer eigenen Datei. Sie wird ohne das Level selbst gelesen.
So kann ein Katalog tausend Levels zeigen, ohne eines davon zu öffnen

## Identität

Das Level hat eine feste ID. Sie übersteht Umbenennungen und das Verschieben des Ordners.
Punktestände und Kommentare hängen an ihr, nicht am Namen

Dazu kommt deine eigene Versionsnummer für das Level. Erhöhe sie, wenn du es bearbeitest. Mit der Version des Formats hat sie nichts zu tun

## Name, Beschreibung und Logo

**Name und Beschreibung** lassen sich in mehrere Sprachen übersetzen. Sie haben keine Schlüssel: du schreibst den Text für jede Sprache direkt an Ort und Stelle.
Der Text wird im Level gespeichert. Darin unterscheidet er sich von den Texten der Spieloberfläche

**Das Logo** ist eine Datei neben dem Level, `logo.png` oder `logo.jpg`

Das Logo hat einen eigenen Eintrag, wie eine Ressource: Lizenz, Autoren, Link, KI-Generierung. Geöffnet wird er mit der Schaltfläche `{{ui:settings_level-settings_metadata-level-logo-metadata}}` unter dem Logo.
Ein neues Bild beginnt den Eintrag von vorn, und wer das Logo entfernt, entfernt auch seinen Eintrag. Mehr - [[4_resource-record]]

## Autoren

**Autoren** sind die Menschen, die das Level gemacht haben: das Mapping, das Design.
Die Autoren der Ressourcen werden getrennt genannt, im eigenen Eintrag jeder Ressource.
Texturen, Schriftarten und Audio haben Einträge, ebenso Themes, Effekte, Formen und Prefabs

> [!caution] Vorsicht
> Wer diese zwei Listen verwechselt, lässt den Musiker ungenannt

## Altersfreigabe

**Die Altersfreigabe** ist eine einzige Zahl, das Mindestalter. Sie wird als "12+" angezeigt. Zwei Freigaben werden wie einfache Zahlen verglichen

`{{ui:enum_age-rating_unrated}}` ist null. Das heißt, es wurde nichts angegeben, nicht dass der Inhalt unbedenklich ist

> [!info] Gut zu wissen
> Es gibt eine Skala, ohne getrennte Felder für ESRB, PEGI und RARS. Nutzerlevels werden keiner Prüfstelle vorgelegt, ein Wert für jede wäre also geraten

> [!caution] Vorsicht
> Die Freigabe ist die einzige Warnung auf der Karte. Wenn das Level blinkt oder laut wird, schreib das in die Beschreibung. In einem Spiel voller Drops und Glitch-Effekte ist Blinken häufig, und diese Zeile ist die ganze Warnung, die ein Spieler bekommt

## KI-Generierung

**`KI-Generierung`** gibt an, ob der eigene Inhalt des Levels per KI generiert wurde: das Design, die Objekte, die Texte.
Jede Ressource und das Logo geben das selbst an, in ihren eigenen Einträgen

| Wert | Bedeutung |
|---|---|
| `{{ui:enum_ai-generation_not-specified}}` | es wurde nichts angegeben. Das ist der Standard |
| `{{ui:enum_ai-generation_no}}` | du erklärst, dass keine KI-Generierung verwendet wurde |
| `KI-generiert` | du erklärst, dass der Inhalt per KI generiert wurde |

`{{ui:enum_ai-generation_not-specified}}` bedeutet "unbekannt". Das ist nicht dasselbe wie "nein"

Der Levelbildschirm im Menü zeigt "Enthält KI-generierte Inhalte", wenn das Level, sein Logo oder irgendeine Ressource `KI-generiert` angibt

Ein KI-Assistent setzt `{{ui:enum_ai-generation_yes}}` selbst, im selben Rückgängig-Schritt wie seine erste Reihe von Änderungen am Level. Mehr - [[7_ai-assistant]]

> [!info] Gut zu wissen
> Wie die Altersfreigabe ist das eine eigene Erklärung des Autors. Das Spiel prüft sie nicht

## Ein Level heute teilen

1. Pack den Levelordner als Zip und schick ihn
2. Die andere Person entpackt ihn in ihren eigenen Ordner `levels`
3. Das Level öffnet sich. Nichts wird installiert oder importiert

> [!warning] Warnung
> Jede Datei im Levelordner reist mit, auch eine unbenutzte. Räum ihn vor dem Verschicken auf

## Steam Workshop

Der Tab `{{ui:settings_level-settings_publication}}` der Leveleinstellungen schickt das Level hinaus: als Archiv und, in einem Steam-Build, in den Steam Workshop. Mehr - [[17_publishing]]

Steam-Builds lesen auch den Workshop: Sie zeigen und spielen die Levels, die du abonniert hast. Mehr - [[2_playing-levels]]

Lies vor dem Veröffentlichen [[1_licensing-basics|den Abschnitt über Rechte]]. Der Bericht im Tab `{{ui:settings_level-settings_publication}}` bewertet das Level und jeden Ressourceneintrag nach diesen Regeln

## Ein Level später teilen

Ein offizieller Server und eine Website sind geplant

Weiter: [[4_resource-record|Der Eintrag einer Ressource]], [[4_level-folder-and-backups|Der Levelordner und Sicherungen]]
