---
title: Veröffentlichung
date: 2026-10-11
tags: [level_author]
---

# Veröffentlichung

Ein Level wird nur aus dem Tab "Veröffentlichung" der Leveleinstellungen verschickt: als Archiv oder in den Steam Workshop. Der Bericht prüft das Level von selbst, Fehler darin blockieren den Versand

## Der Tab "Veröffentlichung"

`Veröffentlichung` ist ein Tab der Leveleinstellungen. Es ist der einzige Ort, von dem aus ein Level irgendwohin verschickt wird

Oben zeigt `{{ui:editor_share_destination}}` den gewählten Versandweg. Ein Druck darauf öffnet `{{ui:editor_share_pick-title}}`: die Wege, die dieser Build auf diesem Gerät bietet, jeder mit einer einzeiligen Beschreibung.
`{{ui:editor_share_archive}}` ist standardmäßig gewählt. Die letzte Wahl bleibt gespeichert, bis das Spiel geschlossen wird

Darunter:
- die eigenen Einstellungen des Wegs
- sein Bericht
- die Schaltfläche, die ihn ausführt: `{{ui:editor_share_export}}` oder `Veröffentlichen`

Hat dieser Build auf diesem Gerät keine Wege, zeigt der Tab `{{ui:editor_share_none}}`

## Der Bericht

Der Bericht prüft von selbst: wenn sich ein Weg öffnet und wenn sich eine seiner Einstellungen ändert. Eine Schaltfläche dafür gibt es nicht.
Er beginnt mit der Zeile `Fehler: N, Warnungen: N, Hinweise: N`, gefolgt von einer Zeile pro Befund

Fehler blockieren den Vorgang. Über Warnungen und Hinweise entscheidest du selbst

Der Weg bestimmt die Regeln, nach denen das Level beurteilt wird. `{{ui:editor_share_archive}}` prüft gegen den Satz `{{ui:editor_publish_profile-local}}`, `{{ui:editor_share_steam}}` gegen die Workshop-Regeln. Was jeder Satz verlangt und was jedes Urteil bedeutet - [[5_publish-readiness]]

## Versandwege

| Weg | Wo es ihn gibt | Was er verschickt |
|---|---|---|
| `{{ui:editor_share_archive}}` | auf jedem Gerät mit einem Speicherdialog. Nicht unter iOS | ein Level, eine Sammlung oder eine Ressource, als Datei |
| `{{ui:editor_share_steam}}` | nur im Steam-Build | ein Level oder eine eigene Sammlung |

Ein Weg, den dieser Build oder dieses Gerät nicht hat, steht einfach nicht in der Liste

## Archiv

Für ein Level:

| Element | Was es tut |
|---|---|
| `{{ui:editor_share_format}}` | einer von sieben Exportmodi, vom einfachen Ordner bis zum passwortgeschützten Archiv |
| `{{ui:editor_share_passphrase}}` | nur in geschützten Modi sichtbar. Ein geschützter Modus mit leerem Passwort startet nicht |
| `{{ui:editor_share_export}}` | schreibt das Level dorthin, wohin du zeigst |

Was jeder Modus schreibt und womit man es öffnet - [[13_export-and-protection#Level exportieren]]

Für eine Sammlung oder eine einzelne Ressource bietet `{{ui:editor_share_format}}` fünf dieser Modi an, und alle sind Archive. Ordnermodi gibt es nicht:

| `{{ui:editor_share_format}}` | Was du bekommst | Womit man es öffnet |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_zip}}` | eine Datei | ein Doppelklick im Windows Explorer, nichts zu installieren |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | ein Zip mit eingebauter AES-256-Verschlüsselung | 7-Zip oder ein anderes Archivprogramm, es fragt nach dem Passwort |
| `{{ui:settings_level-settings_export-mode_zip-protected}}` | das ganze Zip, verpackt in OpenPGP | gpg |
| `{{ui:settings_level-settings_export-mode_targz}}` | eine Datei | jedes Archivprogramm |
| `{{ui:settings_level-settings_export-mode_targz-protected}}` | ein tar.gz, verpackt in OpenPGP | gpg |

`{{ui:editor_share_passphrase}}` erscheint in den drei Passwortmodi. Mit leerem Passwort wird nichts exportiert.
Die Prüfung einer Sammlung weiter unten gilt hier, unter denselben Regeln `{{ui:editor_publish_profile-local}}`

## Steam Workshop

Nur in Steam-Builds. Die Elemente:

| Element | Was es tut |
|---|---|
| `{{ui:editor_publish_visibility}}` | wer den Eintrag sieht: `{{ui:editor_publish_visibility-public}}`, `{{ui:editor_publish_visibility-friends-only}}` oder `{{ui:editor_publish_visibility-private}}`. Standardmäßig `{{ui:editor_publish_visibility-private}}` |
| `{{ui:editor_publish_changelog}}` | die Änderungsnotiz für diesen Upload. Ein mehrzeiliges Feld, mit seinem Label in einer eigenen Zeile |
| `Titel und Beschreibung gehen hoch in` | die Sprache, in der der Text des Eintrags genommen wird (siehe unten) |
| `{{ui:editor_share_steam-descriptors}}` | fünf Kontrollkästchen, die eigenen Inhaltsbeschreibungen von Steam (siehe unten) |
| `Veröffentlichen` | lädt das Level hoch |

Das Level wird immer gegen die Workshop-Regeln geprüft. Eine Wahl der Regeln gibt es hier nicht

Der Workshop-Eintrag wird aus dem Level gefüllt:
- Titel und Beschreibung sind Name und Beschreibung des Levels, in einer Sprache
- die Vorschau ist das Cover des Levels, png oder jpg, nicht größer als 1 MB. Jedes andere Cover wird übersprungen, und der Eintrag wird ohne Bild hochgeladen
- die Tags setzt das Spiel selbst, siehe "Workshop-Tags" unten

Der erste Druck auf `Veröffentlichen` erstellt den Eintrag. Die nächsten aktualisieren denselben Eintrag.
Das Spiel findet ihn über die eigene ID des Levels unter den Einträgen, die du veröffentlicht hast, also wird nichts im Level gespeichert

Ein geschütztes Level lässt sich nicht veröffentlichen. Mehr - [[13_export-and-protection]]

Der Upload enthält den Ordner `ai` des Levels, in dem ein KI-Assistent seine Notizen zum Level ablegt, außer `{{ui:settings_level-settings_metadata-level-ai-share}}` ist in den Levelmetadaten abgewählt. Jeder, der abonniert, bekommt ihn mit dem Level. Mehr - [[7_ai-assistant#Der Ordner ai]]

> [!warning] Warnung
> Wenn du die rechtliche Vereinbarung des Steam Workshop nicht akzeptiert hast, wird der Eintrag hochgeladen, bleibt aber verborgen. Akzeptiere die Vereinbarung auf der Seite des Eintrags. Das Spiel öffnet diese Seite im Steam-Overlay

### Sprache des Titels

Steam zeigt einen Titel und eine Beschreibung pro Eintrag. Das Spiel nimmt die erste Sprache, die es findet, in dieser Reihenfolge:
1. `{{ui:settings_game-editor_publish-language}}` in den Einstellungen `{{ui:settings_game-editor_title}}`: `{{ui:enum_publish-language_english}}` (der Standard) oder `{{ui:enum_publish-language_system}}`, die Sprache des Geräts. Mehr - [[14_editor-settings]]
2. deine eigene Sprache, also die Sprache der Oberfläche des Spiels
3. Englisch
4. die erste Sprache, in der der Text geschrieben wurde

Die Beschreibung wird zuerst in der Sprache des Titels gesucht, damit beide zusammenpassen.
Ein Name, der nicht lokalisiert ist (einfacher Text), geht genau so hoch, wie er geschrieben ist, und die Zeile zeigt `{{ui:editor_share_steam-language-as-written}}`

### Inhaltsbeschreibungen

`{{ui:editor_share_steam-descriptors}}` hat fünf Kontrollkästchen, die eigenen Inhaltsbeschreibungen von Steam:
- `{{ui:editor_share_steam-descriptor-mature}}`
- `{{ui:editor_share_steam-descriptor-violence}}`
- `{{ui:editor_share_steam-descriptor-some-nudity}}`
- `{{ui:editor_share_steam-descriptor-frequent-nudity}}`
- `{{ui:editor_share_steam-descriptor-adult-only}}`

Sie werden bei jeder Veröffentlichung mitgeschickt und nie im Level gespeichert. Jede Veröffentlichung schickt den ganzen Satz, also entfernt ein nicht angehaktes Kästchen die Beschreibung auch von einem schon veröffentlichten Eintrag.
Sie gehen in einer zweiten Aktualisierung direkt nach dem Upload hoch. Schlägt dieser Teil fehl, ist der Eintrag trotzdem veröffentlicht, und das Ergebnis sagt, dass die Inhaltsbeschreibungen nicht gesetzt wurden

### Nach dem Veröffentlichen

Bei Erfolg zeigt das Formular, welcher Eintrag erstellt oder aktualisiert wurde, und eine Schaltfläche `{{ui:editor_publish_open-item}}`. Sie öffnet die Seite des Eintrags in Steam

Bei einem Fehler zeigt das Formular:
- den Grund in einfachen Worten, `Veröffentlichung fehlgeschlagen: ...`
- `Was gesendet wurde und was Steam geantwortet hat: ...` - eine technische Zeile auf Englisch. Es lohnt sich, sie dem Entwickler zu zitieren, wenn du ein Problem meldest
- ein `?`, das aufklappt, warum Steam auf diese Weise ablehnt, und drei Links: `{{ui:editor_publish_help-docs}}` (diese Seite), `{{ui:editor_publish_help-steam-support}}` und `{{ui:editor_publish_help-agreement}}`

Die eigenen Logzeilen des Spiels zum Veröffentlichen sind immer auf Englisch, egal welche Sprache die Oberfläche hat

| Grund | Was zu tun ist |
|---|---|
| `{{ui:enum_workshop-failure_steam-not-running}}` | Steam starten und das Spiel aus Steam neu starten |
| `{{ui:enum_workshop-failure_not-owner}}` | von diesem Konto aus veröffentlichen oder eine Kopie des Levels anlegen, dann geht sie als neuer Eintrag hoch |
| `{{ui:enum_workshop-failure_access-denied}}` | das Konto besitzt das Spiel nicht, das Konto ist eingeschränkt (noch keine Käufe auf Steam) oder der Workshop ist für es gesperrt |
| `{{ui:enum_workshop-failure_invalid-param}}` | der Workshop des Spiels ist nicht für Uploads eingerichtet, oder Steam läuft unter der ID eines anderen Spiels. Steam und das Spiel neu starten |
| `{{ui:enum_workshop-failure_limit-exceeded}}` | alte Einträge in deinen Workshop-Dateien löschen |
| `{{ui:enum_workshop-failure_connection}}` | die Verbindung und den Status von Steam prüfen |
| `{{ui:enum_workshop-failure_invalid-request}}` | ein Titel bis 128 Zeichen, eine Beschreibung bis 8000, eine Vorschau in png oder jpg bis 1 MB |
| `{{ui:enum_workshop-failure_staging}}` | den freien Speicherplatz prüfen und dass die Leveldateien in keinem anderen Programm geöffnet sind |

Wird ein neuer Eintrag erstellt, sein Upload aber abgelehnt, löscht das Spiel diesen leeren Eintrag, damit kein verwaister Eintrag im Workshop bleibt

## Builds ohne Steam

Ein Build ohne Steam zeigt `{{ui:editor_share_steam}}` nicht in der Liste. `{{ui:editor_share_archive}}` bleibt

## Eine Sammlung teilen

Eine Sammlung wird von ihrer Seite im Tab "Bibliothek" aus geteilt. `{{ui:editor_share_share}}` öffnet denselben Bereich in einem Fenster: `{{ui:editor_share_archive}}` und im Steam-Build für eine eigene Sammlung auch `{{ui:editor_share_steam}}`

Die Prüfung einer Sammlung:
- sie hat einen Namen
- sie hat eine angegebene Lizenz
- sie ist nicht leer
- jede Datei, die sie nennt, ist darin
- jede Ressource, auf die ihre Einträge verweisen, ist darin enthalten

Eine fehlende Lizenz hängt vom Weg ab. Für `{{ui:editor_share_archive}}` ist sie eine Warnung, und der Export läuft. Für `{{ui:editor_share_steam}}` ist sie ein Fehler.
Fehler blockieren den Vorgang. Mehr zu Sammlungen - [[16_library-and-collections]]

## Eine einzelne Ressource teilen

Jede Zeile für ein Theme, eine Form, einen Effekt oder ein Prefab in der Bibliothek hat ebenfalls eine Schaltfläche `{{ui:editor_share_share}}`.
Sie packt die Ressource mit allem, was sie braucht (zum Beispiel die Formen, Texturen und verschachtelten Prefabs eines Prefabs), als Sammlung aus einem Eintrag

Nur `{{ui:editor_share_archive}}` steht zur Verfügung, mit denselben fünf Formaten wie für eine Sammlung, die mit Passwort eingeschlossen. Der Empfänger importiert die Datei über `{{ui:editor_library_import-archive}}`, wie jede Sammlung

## Workshop-Tags

Das Spiel setzt die Tags selbst:

| Eintrag | Tags |
|---|---|
| Level | `level` |
| Sammlung | `collection` und einer für jede enthaltene Art: `prefabs`, `themes`, `shapes`, `effects` |

Texturen, Schriftarten und Audio bekommen keine Tags und kommen nicht allein in den Workshop. Sie gehen innerhalb einer Sammlung mit, als das, was ihre Prefabs, Themes, Formen und Effekte verwenden. Eine Sammlung nur aus Medien wird mit einer Zeile abgelehnt, die den Grund nennt, und eine solche Sammlung teilt man besser als Archiv

> [!info] Gut zu wissen
> Die eigenen "Kollektionen" von Steam sind kuratierte Listen von Workshop-Einträgen, eine Funktion von Valve. Mit den Sammlungen von Bullet Hero haben sie nichts zu tun

## Abonnements

Der Steam-Build liest, was du abonniert hast:
- Levels erscheinen in der Levelliste unter `{{ui:editor_library-source_workshop}}`, [[2_playing-levels]]
- Sammlungen erscheinen in der Bibliothek des Editors unter dem Chip `{{ui:editor_library-source_workshop}}`, schreibgeschützt

Weiter: [[5_publish-readiness]], [[1_licensing-basics]], [[16_library-and-collections]]
