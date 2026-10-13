---
title: Bereit zum Veröffentlichen
date: 2026-10-02
tags: [level_author]
---

# Bereit zum Veröffentlichen

Jeder Dienst prüft ein Level nach eigenen Regeln, einer kann es also annehmen und ein anderer ablehnen. Nur ein Fehler blockiert das Veröffentlichen, eine Warnung schickt das Level in die Moderation

Die Prüfung läuft von selbst im Tab `{{ui:settings_level-settings_publication}}` der Leveleinstellungen, in jedem Build. Das Ziel wählt das Profil: `{{ui:editor_share_archive}}` wird mit `{{ui:editor_publish_profile-local}}` geprüft, dem lockersten, `{{ui:editor_share_steam}}` mit dem Workshop-Profil. Das Standardprofil ist das Profil eines öffentlichen Servers, und das Profil des Store-Builds wird im Spiel nicht angeboten, seine Grenzen stehen unten. Mehr - [[17_publishing]]

## Drei Urteile

| Urteil | Was passiert |
|---|---|
| **`Error`** | der Dienst lehnt ab, der Upload wird blockiert, bevor er beginnt |
| **`Warning`** | veröffentlichbar, aber ein Mensch sieht sich das Level an. Der Server stellt es in die Moderationswarteschlange |
| **`Advice`** | ein Hinweis, blockiert nichts |

Ein Level, das auf deinem Gerät bleibt, wird von nichts bewertet

## Das Workshop-Profil

Vorerst lockerer als das Standardprofil, weil die Lizenzrichtlinie noch überarbeitet wird:
- jede CC-BY-Lizenz geht durch, 3.0 und 4.0: BY, BY-SA, BY-NC, BY-NC-SA, BY-ND, BY-NC-ND. Außerdem CC0, SIL OFL, MIT, Apache und die Unlicense
- weiterhin abgelehnt: alle Rechte vorbehalten, Lizenzen der GPL-Familie und ein eigener Lizenztext
- nur eine Warnung: keine Lizenz angegeben, eine Ressource ohne Eintrag, kein Link zur Quellseite
- Altersfreigabe und Levelautoren sind nicht nötig
- die Größengrenzen sind dieselben wie im Standardprofil

> [!caution] Vorsicht
> Musik unter CC BY-ND wird angenommen, aber nach CC 4.0 gilt Musik, die mit einem bewegten Bild synchronisiert ist, immer als Bearbeitung, und ND verbietet das Verbreiten von Bearbeitungen. Ein Level auf einem ND-Song kann auf Verlangen des Rechteinhabers entfernt werden. Nimm besser einen anderen Song

## Was einen Fehler ergibt

Im Standardprofil:
- die eigene Lizenz des Levels wird nicht akzeptiert
- keine Altersfreigabe
- niemand ist für das Level genannt
- eine Ressource hat keinen Eintrag
- die Lizenz einer Ressource wird abgelehnt oder ist nicht angegeben
- eine Ressource wird auf eine Weise geholt, die der Dienst nicht akzeptiert
- eine Ressource stammt von einer Website, die nicht erlaubt ist
- etwas überschreitet die Größengrenzen

## Was eine Warnung ergibt

- eine Ressource hat keinen Link zu ihrer Quellseite. Ein selbst gemachtes Werk hat keine solche Seite, daher blockiert das nie
- eine Erlaubnis ohne Umfang oder ohne Nachweis
- eine abgelaufene Erlaubnis
- eine Website mit mehr als einer Art von Bedingungen

## Was einen Ratschlag ergibt

- ein Eintrag zu einer Ressource, die das Level nicht mehr hat

## Warum, und was zu tun ist

Jede Zeile des Berichts nennt ihre Ressource: über den Dateinamen oder den Namen, den du ihr gegeben hast. Das `?` am Ende der Zeile klappt die Details auf: welche Lizenz die Ressource hat, welche der Dienst stattdessen akzeptiert, wie viel sie im Vergleich zur Grenze wiegt und wo man es behebt

## Größengrenzen

| Grenze | Standardprofil | Store-Build |
|---|---|---|
| Pro Ressource | `{{v:publish.standard.max-resource-mb}} MB` | `{{v:publish.strict.max-resource-mb}} MB` |
| Pro Datendatei | `{{v:publish.standard.max-data-file-mb}} MB` | `{{v:publish.strict.max-data-file-mb}} MB` |
| Pro Level | `{{v:publish.standard.max-level-mb}} MB` | `{{v:publish.strict.max-level-mb}} MB` |

Ein Store-Build verlangt außerdem Namensnennung und Hashes und lehnt beliebige Links ab.
Die kleineren Größen sind keine strengere Meinung. Sie sind das, was ein Handy über ein Mobilfunknetz tatsächlich herunterladen kann

## Ein sauberer Bericht

> [!caution] Vorsicht
> Ein sauberer Bericht nur über die Metadaten heißt nicht "bereit". Zwei Prüfungen brauchen die Leveldatei selbst: eine Ressource ohne Eintrag und woher eine Ressource geholt wird. Ein Durchlauf nur über die Metadaten heißt "nichts falsch an dem, was gelesen wurde"

## Warum Dienste unterschiedlich bewerten

Die Regeln eines Dienstes sind eine Datendatei, kein Code.
Jeder Dienst stellt dieselben gut ein Dutzend Fragen und beantwortet sie auf seine Weise:
- welche Lizenzen akzeptabel sind
- wie Ressourcen geholt werden dürfen
- ob eine unbekannte Lizenz geduldet wird
- was ausgefüllt sein muss
- wie groß ein Level sein darf

Ein Dienst bringt seine eigenen Antworten mit, ein anderer ersetzt sie. Deshalb kann dasselbe Level für einen Dienst bereit sein und von einem anderen abgelehnt werden

> [!info] Gut zu wissen
> Dieselbe Prüfung läuft sowohl automatisch auf deinem Rechner als auch bei der manuellen Moderation auf dem Server. Ein Client ohne Netzwerk bewertet ein Level trotzdem korrekt, weil die Regeln, mit denen er gebaut wurde, mit ihm reisen

Weiter: [[4_resource-record]], [[2_metadata-and-sharing]]
