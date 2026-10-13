---
title: Öffentlicher Server und seine Erweiterung
date: 2026-10-02
tags: [server_advanced]
---

# Öffentlicher Server und seine Erweiterung

Für einen öffentlichen Server gibt es schon das offene SDK: dieselben Modelle und Prüfungen wie im Client, gebaut ohne Unity. Protokoll, Server-API und Moderationswerkzeuge sind noch offen

> [!warning] Warnung
> Es gibt noch keinen Servercode und kein Protokoll. Unten steht der Teil des SDK, auf dem der Server laufen wird, und er funktioniert bereits. Adressen, das Nachrichtenformat und die API des Servers selbst stehen hier nicht, es gibt sie nicht

## Das SDK läuft auf einem Server

Das SDK ist das offene Datenmodell des Spiels: Modelle, Serialisierung in JSON und in ein Binärformat, Validierungsregeln, Generatoren.
Dieselben Quellen, die Unity kompiliert, bauen ohne die Engine als gewöhnliche `netstandard2.1`-Bibliothek. Ein Server oder ein Hilfsprogramm kann darauf verweisen:

```bash
dotnet build -c Release BH.SDK.csproj
dotnet pack  -c Release BH.SDK.csproj
```

Das Paket heißt `BulletHero.SDK`. Der Code liegt unter [github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk), unter MIT

Die SDK-Version stimmt meist mit der Spielversion überein und verspricht noch keine API-Stabilität. Mehr - [[5_versioning]]

**Client und Server führen dieselben Prüfungen über dieselben Modelle aus.** Ein Level, das der Editor für bereit hält, ist auch für den Server bereit. Es gibt keinen zweiten Regelsatz, der abgeglichen werden müsste

## ValidateForPublish

Ein Aufruf beantwortet die Frage "darf dieses Level hier veröffentlicht werden":

```csharp
new ValidationFacade().ValidateForPublish(meta, profile, level, now, payload)
```

Er führt drei Durchläufe auf einmal aus:

1. deklarative Regeln über das Level und seine Metadaten
2. Prüfungen des Levelgraphen
3. die eigenen Bedingungen des Dienstes aus seinem `PublishProfile`

**Das Level selbst zu übergeben ist optional.** `metadata.json` ist eine eigene Datei, damit ein Katalog Tausende Levels bewerten kann, ohne ein einziges zu öffnen. Dieser günstige Durchlauf deckt den Großteil der Richtlinie ab

Zwei Prüfungen brauchen aber `level.json`: eine Ressource ganz ohne Eintrag und die Art, wie Ressourcen bezogen werden. Ein sauberer Bericht allein aus den Metadaten heißt "keine Fehler in dem, was gelesen wurde". `IsReady` bleibt `false`, bis die Leveldatei geprüft ist

`payload` trägt die gemessenen Größen: jeder Ressource, von `level.json`, von `metadata.json`, des ganzen Levels. Ohne es lassen sich die Größengrenzen des Profils nicht prüfen

Bei der Prüfung wird nichts repariert, und das ist Absicht. Inhalte auf dem Weg nach draußen stillschweigend zu ändern, ist das Letzte, was ein Dienst braucht. Mehr - [[6_validation]]

## Drei Urteile

| Gruppe | Bedeutung | Was der Server tut |
|---|---|---|
| `Error` | der Dienst lehnt ab | weist das Hochladen zurück (`HasErrors`) |
| `Warning` | kann veröffentlicht werden, aber ein Mensch muss draufschauen | stellt das Level in die Moderationswarteschlange (`NeedsManualReview`) |
| `Advice` | vermerkt | nichts |

Der Client blockiert ein Hochladen bei denselben Fehlern, bevor es überhaupt beginnt. Ein Level, das dein Server ablehnen würde, kommt selten bei ihm an

## Dein eigenes PublishProfile

Die Richtlinie eines Dienstes ist eine Datei, ein serialisiertes Modell des SDK. Ein strengerer oder lockererer Server ist eine andere Datei, kein Fork des Codes

**Ein Level, das auf dem Gerät des Spielers bleibt, wird gar nicht geprüft.** Das Profil zählt nur in dem Moment, in dem das Level einem Dienst angeboten wird. Wie ein Autor ein Level auf diesen Moment vorbereitet - [[5_publish-readiness]]

Presets:

| Preset | Schlüssel | Wofür |
|---|---|---|
| `CreateOpen()` | `local` | Levels auf dem Gerät, nichts ist Pflicht |
| `CreateStandard()` | `standard` | ein öffentlicher Server, die Richtlinie aus [[ugc-licensing-policy]] |
| `CreateStrict()` | `strict` | Store-Builds, keine Direktlinks, ein Hash an jeder Ressource |

Die wichtigsten Felder:

| Feld | Was es entscheidet |
|---|---|
| `AllowedLicenses` | welche typischen Lizenzen angenommen werden, eine leere Liste nimmt alle an |
| `AllowedUriTypes` | wie Ressourcen bezogen werden dürfen, eine leere Liste erlaubt jeden Weg |
| `AllowUnknownLicense` | ob eine Ressource über ihre Bedingungen schweigen darf |
| `AllowPermissionInstead` | ob die Erlaubnis des Rechteinhabers eine abgelehnte Lizenz ersetzen kann (geht immer zur Prüfung) |
| `RequireResourceMeta`, `RequireResourceUrl`, `RequireAttribution` | was der Eintrag jeder Ressource enthalten muss |
| `RequireAgeRating`, `RequireLevelAuthors`, `RequireHashes` | was das Level angeben muss |
| `MaxResourceBytes`, `MaxDataFileBytes`, `MaxTotalBytes` | Größengrenzen, null heißt keine Grenze |
| `Sources`, `UnknownSourceTrust` | die Liste vertrauenswürdiger Websites und wie eine Website außerhalb der Liste bewertet wird |

Die beiden öffentlichen Presets:

| | `standard` | `strict` |
|---|---|---|
| Direktlinks zu Ressourcen | erlaubt | verboten |
| Nennung des Autors an jeder Ressource | nicht Pflicht | Pflicht |
| Inhaltshash in jedem Eintrag | nicht Pflicht | Pflicht |
| Größte Ressource | {{v:publish.standard.max-resource-mb}} MB | {{v:publish.strict.max-resource-mb}} MB |
| Größte `level.json` oder `metadata.json` | {{v:publish.standard.max-data-file-mb}} MB | {{v:publish.strict.max-data-file-mb}} MB |
| Größtes Level | {{v:publish.standard.max-level-mb}} MB | {{v:publish.strict.max-level-mb}} MB |
| Eine Website außerhalb der Liste | `RequiresLicenseCheck` | `RequiresResourceCheck` |

Alle Presets und Felder - [[7_publish-profiles]]

### Warum standard keine GPL hat

Lizenzen der GPL-Familie fehlen in `standard` mit Absicht. Ein GPL-Werk, das über den App Store verbreitet wird, kollidiert mit den Bedingungen von Apple. Ein Katalog, der sie zuließe, könnte später nicht unter iOS ausgeliefert werden

> [!info] Gut zu wissen
> Die Liste vertrauenswürdiger Websites, die mit dem SDK ausgeliefert wird, ist nur ein Ausgangspunkt. Websites ändern ihre Bedingungen, daher sollte jeder Serverbetreiber sie im eigenen Profil überschreiben. Nichts darf damit rechnen, dass eine bestimmte Website auf der Liste steht

## Moderation

Was der offizielle Server zusätzlich zur Prüfung plant. Ein öffentlicher Server wird es höchstwahrscheinlich auch brauchen:

- **Eine Moderationswarteschlange.** Sie wird von Befunden der Gruppe `Warning` gefüllt
- **Meldungen und Sperren** von Levels und Nutzern. Die Regeln von Google Play und App Store verlangen beides für alle Inhalte, die andere Menschen sehen
- **Entfernen per Hash.** Ein Ressourceneintrag kann die Inhaltshashes seiner Dateien als `sha256:<hex>` speichern. Eine Meldung nennt ein Werk, und mit Hashes wird jedes Level, das es enthält, per Suche gefunden statt durch Raten anhand von Titeln. Der Editor hält den Hash fest, wenn eine Ressource importiert wird
- **Nutzungsbedingungen.** Sie decken ab, was die Lizenz nicht abdeckt: die Erklärung des Autors, dass er die Rechte hält, das Recht des Serverbetreibers, ein Level zu entfernen, das Recht, Titel und Cover in Listen anzuzeigen

**Der Steam Workshop funktioniert anders.** Valve speichert die Dateien, und auf der Seite von Bullet Hero gibt es keine Moderationswarteschlange. Das Spiel prüft ein Level oder eine Sammlung vor dem Hochladen, und ein Fehler blockiert das Hochladen - [[17_publishing]]. Nach der Veröffentlichung entscheidet das Spiel nur, was davon heruntergeladen wird

## Archivformate

Ein Level ist ein Ordner mit Dateien, und ein Archiv macht es tragbar. Was das SDK liest und schreibt:

| Format | Lesen | Schreiben | Hinweis |
|---|---|---|---|
| `.tar.gz` | ja | ja | der Standard |
| `.zip` | ja | ja | lässt sich pro Eintrag mit AES-256 verschlüsseln |
| `.tar.gz.gpg`, `.zip.gpg` | ja | ja | eine passwortgeschützte OpenPGP-Nachricht, der einzige Schutz, den es für `.tar.gz` gibt |
| `level.json.gpg` | ja | ja | eine einzelne geschützte Leveldatei |
| `.7z` | nein | nein | wird erkannt, damit es mit klarem Namen abgelehnt werden kann |

Das Format wird an den ersten Bytes der Datei erkannt, nicht an der Endung. Der Name ist der einzige Teil einer Datei, den jeder ändern kann

`tar -xzf`, `gpg -d` und jedes zip-Archivprogramm öffnen jedes Format, das geschrieben wird. Zum Entpacken eines Levels braucht man das Spiel nicht. Mehr - [[4_archives]]

## Was nicht entschieden ist

- das Protokoll zwischen dem Spiel und einem Server, und ob es für OWS und NOWS dasselbe sein wird
- die Server-API: Hochladen, Katalog, Suche, Konten
- wie man das Spiel auf einen Community-Server richtet
- wie der Server selbst erweitert wird und in welcher Sprache
- gemeinsames Spielen auf einem Server: Transport, Autorität, Synchronisierung des Levels und Lobbys

Für das gemeinsame Spielen ist nur eines ausgearbeitet: wie der Avatar eines Spielers auf eine Netzwerknachricht hin erscheint und verschwindet

Das Veröffentlichen von Levels bei einem beliebigen Dienst kommt frühestens mit dem Update nach `gv 1.0.0`. Die Daten, auf die sich die Prüfung stützt, müssen in die Levels gelangen, bevor sie veröffentlicht werden

## Levellizenz und jeder Server

Standardmäßig wird ein Level unter *CC BY-NC* verbreitet, und der Autor kann in den Metadaten des Levels eine andere Lizenz wählen. Die Erlaubnis, ein Level weiterzugeben, geht von seinem Autor direkt an jeden Empfänger. Deshalb darf kein Server, weder der offizielle noch ein Community-Server, ein Level unter *CC BY-NC* kommerziell hosten

Ein Server mit anderem Code unter einer anderen Lizenz ändert nichts an den Rechten am Inhalt. Die vollständigen Regeln für Autoren - [[ugc-licensing-policy]]
