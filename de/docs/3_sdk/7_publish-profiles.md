---
title: Veröffentlichungsprofile
date: 2026-10-01
tags: [developer, level_author]
---

# Veröffentlichungsprofile

Welche Levels ein Dienst annimmt, steht in einer PublishProfile-Datei: Lizenzen, Quellen der Ressourcen, Pflichtfelder, Größengrenzen. Ein neuer Dienst ist eine Datei, keine Änderung am Analyzer

## Ein Profil sind Daten

Ein Veröffentlichungsprofil (`PublishProfile`) ist ein Modell, das wie jede andere Wurzel serialisiert wird, mit eigener Generation

Ein Level kann in den Steam Workshop, auf den offiziellen Server, auf einen Community-Server oder in den Katalog eines Store-Builds gehen. Jeder Ort beantwortet dieselben Fragen auf seine Weise. Die Antworten ändern sich über die Jahre, der Code nicht

Was ein Profil entscheidet:

| Feld | Bedeutung |
|---|---|
| `ProfileKey` | welcher Dienst das ist, wird in jedem Bericht wiederholt |
| `AllowedLicenses` | die Werte von `TypicalLicenseType`, die der Dienst annimmt |
| `AllowedUriTypes` | wie Ressourcen bezogen werden dürfen. Eine leere Liste heißt: auf jede Art |
| `AllowUnknownLicense`, `AllowPermissionInstead` | ob eine unbekannte Lizenz oder eine schriftliche Erlaubnis genügt |
| `RequireResourceMeta`, `RequireResourceUrl`, `RequireAttribution`, `RequireAgeRating`, `RequireLevelAuthors`, `RequireHashes` | was ausgefüllt sein muss |
| `MaxResourceBytes`, `MaxDataFileBytes`, `MaxTotalBytes` | Größengrenzen, 0 heißt keine Grenze |
| `Sources`, `UnknownSourceTrust` | eine Liste von Websites und die Bewertung für eine Website, die nicht darauf steht |

Welche Lizenzen akzeptabel sind, entscheidet nur das Profil. Das sieht wie eine Eigenschaft der Lizenz aus, ist aber in Wahrheit eine Eigenschaft des empfangenden Dienstes

## Vier eingebaute Profile

| Fabrikmethode | `ProfileKey` | Wofür |
|---|---|---|
| `CreateOpen()` | `local` | ein Level auf deinem Gerät. Nichts ist Pflicht |
| `CreateStandard()` | `standard` | ein öffentlicher Server |
| `CreateWorkshop()` | `workshop` | der Steam Workshop. Jede Variante von CC BY geht durch, fehlende Dokumente erzeugen nur Warnungen |
| `CreateStrict()` | `strict` | ein Store-Build, strenger als `standard` |

| Was | `standard` | `strict` |
|---|---|---|
| Lizenzen | CC0 1.0, CC BY 4.0 und 3.0, CC BY-NC 4.0 und 3.0, SIL OFL 1.1, MIT, Apache 2.0, die Unlicense | wie bei `standard` |
| woher Ressourcen kommen | aus dem Levelordner, aus dem Spiel oder per Direktlink | keine Links |
| Namensnennung und Hashes | - | Pflicht |
| Grenze pro Ressource | 64 MiB | 32 MiB |
| Grenze pro Datendatei | 32 MiB | 16 MiB |
| Grenze pro Level | 256 MiB | 128 MiB |

> [!tip] Empfehlung
> Füge keine Fabrikmethode für deinen Dienst hinzu. Nimm eines der vier Profile, ändere die Felder, die du brauchst, und liefere es als JSON-Datei aus

### Warum diese Lizenzen und Größen

- Lizenzen der GPL-Familie sind aus `standard` ausgeschlossen. Ein GPL-Werk, das über den App Store verbreitet wird, kollidiert mit den Bedingungen von Apple
- CC BY-SA ist ausgeschlossen: ShareAlike würde eine Änderung der Lizenz des Levels selbst erzwingen
- CC BY-ND ist ausgeschlossen: NoDerivatives verbietet die Bearbeitung, auf der das Spiel aufbaut
- die strengen Größen sind das, was ein Telefon über ein Mobilfunknetz herunterladen kann

## Woher eine Ressource kam

Das Lizenzfeld sagt, was der Autor behauptet. `SourceTrust` sagt, was diese Behauptung wert ist, je nach der Website, von der die Ressource stammt:

| Bewertung | Ergebnis | Beispiele |
|---|---|---|
| `Approved` | veröffentlichen | Kenney, ccMixter, Incompetech |
| `PartiallyApproved` | veröffentlichen, der Eintrag ist einen Blick wert | Pixabay, SoundImage |
| `RequiresLicenseCheck` | die Lizenz mit der echten Seite abgleichen | OpenGameArt, Free Music Archive, Wikimedia Commons |
| `RequiresResourceCheck` | zuerst das Werk selbst identifizieren | Rawpixel, itch.io |
| `NotAllowed` | ablehnen | YouTube, SoundCloud, Spotify |
| `Unknown` | kein Eintrag, `UnknownSourceTrust` entscheidet | - |

`TrustedSourceCatalog.CreateDefault()` gibt 25 Websites zurück. Das ist eine Startliste. Jeder Betreiber soll sie ändern. Daher darf sich nichts darauf verlassen, dass ein Eintrag vorhanden ist

Eine leere Liste `Sources` schaltet die Bewertung der Quellen ab

Streaming-Plattformen stehen als `NotAllowed` in der Liste, statt zu fehlen. Eine fehlende Website wird über `UnknownSourceTrust` bewertet, und in `standard` und `strict` verlangt diese Bewertung eine Prüfung, statt abzulehnen

Der Katalog und [[ugc-licensing-policy]] beschreiben dasselbe und werden gemeinsam bearbeitet

## Was mit der Antwort zu tun ist

Der Aufruf ist `ValidationFacade.ValidateForPublish`. Mehr - [[6_validation]]

`PublishReadinessReport` hat:
- `HasErrors` - Befunde in der Gruppe `Error`
- `NeedsManualReview` - Befunde in der Gruppe `Warning`
- `IsReady`

Was danach passiert, entscheidet das Profil nicht. Der Client blockiert das Hochladen bei Fehlern. Der Server stellt das Level in eine Prüfwarteschlange, statt es zu veröffentlichen

Dieselbe Prüfung aus Sicht des Autors - [[5_publish-readiness]]
