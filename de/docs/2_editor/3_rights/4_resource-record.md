---
title: Der Ressourceneintrag
date: 2026-10-02
tags: [level_author]
---

# Der Ressourceneintrag

Der Eintrag hält fest, woher eine Ressource stammt und zu welchen Bedingungen: Link, Lizenz, Erlaubnisse, Autoren. Ein leeres Lizenzfeld heißt "niemand hat geprüft", so eine Ressource wird abgelehnt

> [!tip] Empfehlung
> Füll den Eintrag aus, sobald du die Ressource hinzufügst. Das ist der einzige Moment, in dem du noch weißt, woher sie kommt

## Was der Eintrag enthält

Jede deiner Ressourcen in einem Level hat ihren eigenen Eintrag. Er wird im Level gespeichert und reist mit ihm.
So geht die Namensnennung nicht verloren: wo auch immer das Level landet, die Datei trägt mit sich, woher sie stammt und zu welchen Bedingungen

Die Felder des Eintrags:
- **Titel** und **Beschreibung** des Originalwerks, beide lassen sich in andere Sprachen übersetzen
- **Url** - die Seite des Werks: der Beitrag oder die Seite des Autors, eine Store-Seite
- **Lizenz** - die Bedingungen, zu denen das Werk verbreitet wird
- **Erlaubnisse** - [[2_legal-resource-paths|Möglichkeit B]], ein Eintrag pro Rechteinhaber, mit Umfang, Daten und Nachweis
- **Autoren** - alle, die für diese Ressource genannt werden müssen, getrennt von den Autoren des Levels selbst
- **Quellen** - freier Text zur Herkunft, für alles, was ein Link nicht ausdrücken kann
- **Hashes** - die Inhalts-Hashes der Dateien der Ressource
- **KI-Generierung** - ob das Werk von einer KI erzeugt wurde: `{{ui:enum_ai-generation_not-specified}}`, `{{ui:enum_ai-generation_no}}` oder `{{ui:enum_ai-generation_yes}}`

**Der Link zeigt auf die Seite mit den Bedingungen, nicht auf einen direkten Download.** Ein Moderator braucht die Seite, nicht die Datei

## Ein leeres Feld heißt "unbekannt"

> [!caution] Vorsicht
> Ein leeres Lizenzfeld ist `NoSpecifiedLicense`, und so eine Ressource wird abgelehnt. Es heißt nicht "die Bedingungen sind in Ordnung". Es heißt "niemand hat geprüft"

Das ganze Modell funktioniert so: ein leerer Wert heißt "nichts angegeben", nicht "alles erlaubt".
Eine Altersfreigabe `Unrated`, ein Erlaubnisumfang `Undefined` und eine KI-Generierung `{{ui:enum_ai-generation_not-specified}}` funktionieren genauso

`NoSpecifiedLicense` kann zusätzlich angeben, woher die Datei stammt: YouTube, SoundCloud, Spotify.
Das Urteil ändert sich dadurch nicht. Der Moderator sieht nur, welches Gespräch bevorsteht

## Hashes

Füll Hashes vom ersten Tag an aus, auch wo sie nicht verlangt werden.
Die Beschwerde eines Rechteinhabers nennt ein Werk. Um darauf zu antworten, muss jedes Level mit diesem Werk gefunden werden.
Über den Namen ist das Raterei, über den Hash eine exakte Suche

## Veraltete Einträge

Ein Eintrag zu einer Ressource, die das Level nicht mehr hat, ergibt einen Ratschlag, keinen Fehler.
Er blockiert nichts, aber es lohnt sich trotzdem, ihn zu entfernen

## Eine Ressource auf der Levelkarte

Der Eintrag einer Ressource kann so markiert werden, dass er auf der Levelkarte erscheint. Das ist für Musik gedacht.
Unter den Autoren des Levels erscheint dann eine Zeile mit dieser Ressource. Alles andere bleibt in der vollständigen Namensnennung

## Der Eintrag des Levelbilds

Auch das Levelbild hat einen Eintrag. Das Levelbild ist keine Ressource des Levels, sein Eintrag wird daher am Levelbild im Metadaten-Tab geöffnet, mit der Schaltfläche `{{ui:settings_level-settings_metadata-level-logo-metadata}}`

- Ein neues Bild beginnt den Eintrag von vorn, und er enthält nur den Hash der Datei. Ein anderes Bild ist ein anderes Werk, und die bisherigen Autoren würden fälschlich genannt
- Wird dieselbe Datei erneut gewählt, bleibt der Eintrag, wie er ist
- Das Entfernen des Levelbilds entfernt auch seinen Eintrag. Rückgängig bringt beides zurück

Eine Ressource oder ein Levelbild mit `{{ui:enum_ai-generation_yes}}` lässt den Levelbildschirm die Zeile "Enthält KI-generierte Inhalte" anzeigen

Weiter: [[5_publish-readiness]], [[2_metadata-and-sharing]]
