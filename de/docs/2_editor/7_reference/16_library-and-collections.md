---
title: Bibliothek und Sammlungen
date: 2026-10-02
tags: [level_author]
---

# Bibliothek und Sammlungen

Sammlungen enthalten die Ressourcen, die du in mehreren Levels wiederverwendest. Ein Level verweist nie auf eine Sammlung: Der Import kopiert die Ressource hinein, und das Level läuft überall

## Was eine Sammlung ist

**Eine Sammlung** ist ein Ordner mit wiederverwendbaren Ressourcen. Sie kann Ressourcen von sieben Arten enthalten:

| Art | Wie sie gespeichert wird |
|---|---|
| Prefabs, Themes, Formen, Effekte | Daten, eine Datei pro Eintrag |
| Texturen, Schriftarten, Audio | Mediendateien |

Eine Sammlung ist an kein Level gebunden. Sie liegt auf deinem Gerät und steht in jedem Level zur Verfügung, das du öffnest

## Quellen

Die Bibliothek zeigt Ressourcen aus drei Quellen. Jede ist ein Filter-Chip über der Liste:

| Chip | Was es ist | Änderbar |
|---|---|---|
| `{{ui:editor_library-source_library}}` | die Gerätebibliothek: `resources/prefabs`, `themes`, `shapes`, `effects` | ja |
| `{{ui:editor_library-source_local}}` | deine eigenen Sammlungen, `resources/collections` | ja |
| `{{ui:editor_library-source_workshop}}` | die Sammlungen, die du im Steam Workshop abonniert hast, direkt an Ort und Stelle gelesen. Nur in Steam-Builds | nein |

Eine schreibgeschützte Sammlung änderst du so: Ihre Einträge werden in eine eigene Sammlung kopiert

## Der Tab "Bibliothek"

`{{ui:settings_editor-settings_library}}` ist der letzte Tab auf dem Startbildschirm des Editors, nach `{{ui:settings_editor-settings_community}}`

Eine schmale Spalte mit Schaltflächen wählt die Art:
- `{{ui:editor_library_kind-collections}}`
- `{{ui:editor_library_kind-prefabs}}`, `{{ui:editor_library_kind-themes}}`, `{{ui:editor_library_kind-shapes}}`, `{{ui:editor_library_kind-effects}}`
- `{{ui:editor_library_kind-textures}}`, `{{ui:editor_library_kind-fonts}}`, `{{ui:field_common_audio}}`

Rechts daneben stehen der Seitentitel (links) und seine Schaltflächen (rechts) in einer Zeile. Darunter liegt die Liste.
Eine leere Liste sagt das in ihrer Mitte

Auf den Seiten der sieben Arten, von `{{ui:editor_library_kind-prefabs}}` bis `{{ui:field_common_audio}}`, nimmt `{{ui:editor_library_copy-target}}` eine eigene Zeile in voller Breite unter dem Titel ein. Die Quellen-Chips stehen in der Zeile darunter

Ein Fenster der Bibliothek (die Karte einer Sammlung, das Bild einer Textur, das Teilen-Fenster) schließt sich über das Kreuz in seiner Ecke. Eine Schaltfläche `{{ui:editor_library_close}}` gibt es nicht

Jede Zeile ist eine Schaltfläche. Ein Druck darauf tut das Wichtigste für ihre Art:

| Art | Druck auf eine Zeile |
|---|---|
| Sammlung | öffnet ihre Seite |
| Theme, Form, Effekt | öffnet den Editor |
| Textur | zeigt das Bild und seine Größe |
| Prefab, Schriftart, Audio | nichts. Eine Audiozeile hat ihre eigene Abspielschaltfläche |

Die kleinen Schaltflächen rechts in einer Zeile sind die anderen Aktionen, und das Mülleimersymbol löscht oder entfernt

`{{ui:editor_library_open-folder}}` zeigt den Ordner der aktuellen Seite im Dateimanager des Systems. Nur unter Windows, macOS und Linux verfügbar

### Sammlungen

`{{ui:editor_library_open-folder}}` und `{{ui:editor_library_refresh}}` stehen rechts vom Seitentitel. `Neue Sammlung` und `{{ui:editor_library_import-archive}}` stehen in einer eigenen Zeile darunter, rechtsbündig

- `Neue Sammlung` erstellt eine leere Sammlung und öffnet ihre Karte
- `{{ui:editor_library_import-archive}}` fügt eine Sammlung aus einer `.zip`- oder `.tar.gz`-Datei oder aus einem passwortgeschützten Archiv hinzu: ein `.zip` mit eigenem Passwort, `.zip.gpg` oder `.tar.gz.gpg`. Ist diese Sammlung schon auf dem Gerät, fragt das Spiel, ob sie ersetzt werden soll

Ein passwortgeschütztes Archiv öffnet das Fenster `{{ui:editor_library_passphrase-title}}`: `{{ui:editor_library_passphrase-needed}}`. Gib das Passwort ein und drücke `{{ui:editor_library_open}}`.
Ein falsches Passwort zeigt `{{ui:editor_library_passphrase-wrong}}`
- `{{ui:editor_library_open-folder}}` öffnet `resources/collections`
- `{{ui:editor_library_refresh}}` liest die Ordner erneut ein

Deine eigenen Sammlungen haben `{{ui:editor_library_edit}}` und das Mülleimersymbol. Der Mülleimer fragt zuerst nach und löscht dann die Sammlung mit allen ihren Dateien

### Die Karte einer Sammlung

`{{ui:editor_library_edit}}` öffnet ein Fenster mit der Karte der Sammlung:
- `{{ui:editor_library_field-name}}`, `{{ui:field_common_description}}`
- `{{ui:editor_library_field-authors}}`, durch Kommas getrennt
- `{{ui:editor_library_field-license}}`: `{{ui:editor_library_license-unspecified}}` oder eine der typischen Lizenzen
- `{{ui:editor_library_set-cover}}` wählt ein png-Bild. Die Zeile daneben sagt, ob es ein Cover gibt

`{{ui:editor_save_text}}` schreibt die Karte. `{{ui:editor_cancel_text}}`, das Kreuz oder ein Klick außerhalb des Fensters verwirft die Änderungen

### Die Seite einer Sammlung

| Element | Was es tut |
|---|---|
| `{{ui:settings_common_back}}` | kehrt zur Liste zurück |
| `{{ui:editor_library_edit}}` | öffnet die Karte. Nur bei deinen eigenen Sammlungen |
| `{{ui:editor_share_share}}` | öffnet das Teilen-Fenster: `{{ui:editor_share_archive}}` als `.zip` oder `.tar.gz`, mit oder ohne Passwort, und im Steam-Build für eine eigene Sammlung auch `{{ui:editor_share_steam}}` |
| `{{ui:editor_library_open-folder}}` | öffnet den eigenen Ordner der Sammlung |
| `{{ui:editor_library_delete}}` | löscht die Sammlung, nach einer Rückfrage |

Darunter steht der Inhalt. Eine Zeile öffnet den Eintrag so wie auf der Seite seiner Art, und das Mülleimersymbol entfernt den Eintrag aus der Sammlung

Eine schreibgeschützte Sammlung zeigt `{{ui:editor_library_read-only}}`

Mehr zu `{{ui:editor_share_share}}` - [[17_publishing]]

### Prefabs, Themes, Formen, Effekte

Jede dieser Seiten zeigt jeden Eintrag aus jeder Quelle. Die Chips grenzen die Liste ein

`{{ui:editor_library_copy-target}}` wählt eine deiner eigenen Sammlungen. Standardmäßig steht dort `{{ui:editor_library_copy-target-none}}`. Sobald ein Ziel gewählt ist, bekommt jede Zeile von anderswo `{{ui:editor_library_copy-to}}`

Ein Theme, eine Form oder ein Effekt öffnet sich im selben Editor wie in den Leveleinstellungen. `{{ui:editor_save_text}}` schreibt die Änderung dorthin, wo der Eintrag liegt: in `{{ui:editor_library-source_library}}` oder in deine Sammlung.
Ein Eintrag aus dem Workshop öffnet sich schreibgeschützt, und `{{ui:editor_save_text}}` ist aus. Um ihn zu ändern, kopiere ihn in eine eigene Sammlung

`{{ui:editor_library_new-entry}}` erstellt ein neues Theme, eine neue Form oder einen neuen Effekt im Editor. Der Eintrag wird in die Zielsammlung gespeichert oder in `{{ui:editor_library-source_library}}`, wenn kein Ziel gewählt ist. Prefabs entstehen in einem Level, und sie haben kein `{{ui:editor_library_new-entry}}`

Einträge, die du ändern kannst, haben das Mülleimersymbol, und es fragt zuerst nach

Jede Zeile hat `{{ui:editor_share_share}}`. Die Schaltfläche packt den Eintrag mit allem, was er braucht (zum Beispiel die Formen, Texturen und verschachtelten Prefabs eines Prefabs), in ein `.zip` oder `.tar.gz`, mit oder ohne Passwort, als Sammlung aus einem Eintrag. Der Empfänger importiert diese Datei über `{{ui:editor_library_import-archive}}`, wie jede Sammlung

`{{ui:editor_library_open-folder}}` öffnet den Ordner der Gerätebibliothek für diese Art, zum Beispiel `resources/themes`

### Texturen, Schriftarten, Audio

Diese Seiten zeigen die Dateien aller Sammlungen. Für Dateien gibt es keine persönliche Bibliothek, also leben diese Arten nur in Sammlungen

- eine Texturzeile zeigt das Bild
- eine Audiozeile hat eine Abspielschaltfläche. Es läuft immer nur eine Spur, und sie stoppt, wenn du die Seite verlässt
- eine Schriftartzeile hat keine Vorschau

`{{ui:editor_library_add-file}}` legt eine Datei vom Gerät in die Zielsammlung, ohne Ziel ist die Schaltfläche also aus. Eine Textur ist png oder jpg, eine Schriftart ttf oder otf, Audio mp3, wav oder ogg.
Hat die Sammlung schon eine Datei mit denselben Bytes, wird nichts hinzugefügt, und das Spiel sagt das

Zeilen haben `{{ui:editor_library_copy-to}}` und das Mülleimersymbol

### Was eine Kopie mitnimmt

Eine Kopie nimmt alles mit, was der Eintrag braucht: die Formen, Texturen, Schriftarten und verschachtelten Prefabs eines Prefabs, die Partikelform eines Effekts.
Die Angaben zur Urheberschaft dieser Ressourcen gehen ebenfalls mit

## Der Tab "Sammlungen"

`{{ui:editor_library_kind-collections}}` ist ein Tab der Leveleinstellungen, direkt nach `{{ui:editor_library_kind-prefabs}}`. Oben gibt es zwei Modi: `Importieren` und `{{ui:editor_collections_mode-build}}`

### Importieren

1. Der Tab zeigt eine Liste von Sammlungen. Drücke auf die, die du brauchst
2. Hake die Einträge ab, die du brauchst. `{{ui:editor_collections_select-all}}` und `{{ui:editor_collections_select-none}}` haken alles ab oder entfernen alle Haken
3. Die Zeile `Ausgewählt: N, Abhängigkeiten hinzugefügt: M` zeigt, was ins Level kommt. Abhängigkeiten werden von selbst hinzugefügt
4. Drücke `Importieren`

Der ganze Import ist ein Rückgängig-Schritt

Texturen, Schriftarten und Audio bekommen im Level neue IDs, und ihre Dateien werden unter einem eindeutigen Namen in den Levelordner kopiert.
Eine Datei, die das Level Byte für Byte schon hat, wird nicht ein zweites Mal kopiert: Der Import nimmt die eigene Textur, Schriftart oder Spur des Levels

### Eine Sammlung bauen

1. `{{ui:editor_collections_target}}` wählt `Eine neue Sammlung` oder eine deiner eigenen. Eine neue übernimmt ihren Namen aus dem Feld `{{ui:editor_library_field-name}}`
2. Hake die Ressourcen des Levels ab, von jeder der sieben Arten
3. Drücke `{{ui:editor_collections_build}}`

Eine neue Sammlung bekommt die Autoren des Levels

Aus einem geschützten Level lässt sich keine Sammlung bauen. Mehr - [[13_export-and-protection]]

## Ressourcenauswahl und Suche

Die Suche und die Fenster zur Ressourcenauswahl haben für Prefabs, Themes, Formen und Effekte eine Stufe `{{ui:settings_editor-settings_library}}`. Sie zeigt alle Quellen.
Die Auswahlfenster sind die Felder für Form, Collider, Effekt und Theme sowie `{{ui:cmd_editor_place-prefab}}`

Die Wahl eines Eintrags aus der Bibliothek importiert ihn mit seinen Abhängigkeiten ins Level und weist ihn zu. Ein Konflikt stellt dieselbe Frage wie im Tab "Sammlungen"

Die Bibliotheksbrowser in den Ressourcen-Tabs des Levels funktionieren genauso und zeigen die Quellen-Chips. Mehr - [[11_level-resources]]

## Konflikte

Ein importierter Eintrag kann schon mit derselben ID im Level sein:
- derselbe Inhalt - es ist nichts zu tun
- anderer Inhalt - das Fenster `{{ui:editor_resource-conflict_title}}` öffnet sich

Das Fenster listet jeden Konflikt auf, jeden mit einem Schalter `{{ui:editor_resource-conflict_copy}}`:

| Wahl | Ergebnis |
|---|---|
| behalten (Schalter aus) | die Version des Levels bleibt und wird verwendet |
| `{{ui:editor_resource-conflict_copy}}` | die Version der Sammlung wird unter einer neuen ID hinzugefügt. Alles, was mit ihr zusammen importiert wurde, verweist auf die Kopie |

`{{ui:editor_resource-conflict_all-keep}}` und `{{ui:editor_resource-conflict_all-copy}}` stellen alle Schalter auf einmal. `Importieren` übernimmt die Wahl, `{{ui:editor_cancel_text}}` importiert nichts

Keine Version gewinnt stillschweigend. Jeder Konflikt mit anderem Inhalt wird in diesem Fenster entschieden

## Urheberschaft

Die Einträge zu den Ressourcen eines Levels umfassen Themes, Effekte, Formen und Prefabs ebenso wie Texturen, Schriftarten und Audio.
Der Import kopiert die nötigen Einträge ins Level, also kommt die Urheberschaft zusammen mit der Ressource an

Mehr - [[4_resource-record]]

## Auf der Festplatte

Sammlungen liegen in `resources/collections/<collection-guid>/` im Datenordner des Spiels. Das ist derselbe Ordner `resources` neben `levels`, in dem die Gerätebibliothek liegt. Mehr - [[4_level-folder-and-backups]]

| Pfad | Was er enthält |
|---|---|
| `collection.json` oder `collection.blob` | das Manifest: Name, Beschreibung, Autoren, Lizenz, die Einträge für Texturen, Schriftarten und Audio und die Angaben zur Urheberschaft von allem darin |
| `cover.png` | das Cover, optional |
| `prefabs/`, `themes/`, `shapes/`, `effects/` | eine `<guid>.json` oder `<guid>.blob` pro Eintrag, dieselben Dateien wie in der Gerätebibliothek |
| `media/` | Dateien für Texturen, Schriftarten und Audio |

Eine Sammlung wird als Archiv weitergegeben: `{{ui:editor_share_share}}` auf ihrer Seite, `{{ui:editor_library_import-archive}}` in der Liste.
Ein Archiv, das keine Sammlung ist, wird abgelehnt

Weiter: [[17_publishing]], [[2_reuse]], [[4_resource-record]]
