---
title: Seiten schreiben
date: 2026-10-13
tags: [contributor]
---

# Seiten schreiben

Die Seiten sind Markdown-Dateien im offenen Repository bullet-hero/docs. Eine Änderung kommt als Pull Request: ein Fork, ein Branch, die Änderung in jeder Sprache, ein Abgleich mit dem Styleguide

## Repositorys

Jedes Repository des Projekts liegt in der Organisation [bullet-hero](https://github.com/bullet-hero). Die offenen:

| Repository | Was es enthält |
|---|---|
| [bullet-hero/releases](https://github.com/bullet-hero/releases) | die Releases enthalten jeden öffentlichen Build des Spiels, die Issues enthalten Bugs und Wünsche der Spieler zum Spiel |
| [bullet-hero/sdk](https://github.com/bullet-hero/sdk) | den Code des SDK, die Issues enthalten Bugs und Wünsche zum SDK |
| [bullet-hero/docs](https://github.com/bullet-hero/docs) | diese Seiten und ihre Übersetzungen |
| [bullet-hero/backend](https://github.com/bullet-hero/backend) | den Server, vorerst leer |

Der Code des Spiels (`bullet-hero/game`) und der Website (`bullet-hero/frontend`) ist geschlossen

Diese Seite handelt von bullet-hero/docs

## Wie du eine Änderung einreichst

1. Forke [bullet-hero/docs](https://github.com/bullet-hero/docs) und lege einen Branch an
2. Bearbeite Seiten oder füge neue hinzu, im unten beschriebenen Format
3. Ändere die Seite in jeder Sprache, oder schreib im Pull Request, welche Sprachen die Änderung noch brauchen. Mehr - [[translating]]
4. Gleich den Text mit dem [[style-guide]] ab
5. Öffne einen Pull Request mit einer kurzen Beschreibung, was sich geändert hat und warum

**Fakten kommen aus dem Spiel, dem SDK oder deren Dokumentation.** Zahlen, Feldnamen, Dateinamen, Tastenkürzel und Adressen werden nie geraten. Du bist dir bei etwas nicht sicher? Schreib es in den Pull Request, nicht auf die Seite

Eine angenommene Änderung erscheint innerhalb weniger Minuten auf [bullethero.space](https://bullethero.space/): Jeder Push auf `master` baut die Website neu

> [!tip] Tipp
> Die Website selbst bauen kannst du nicht, denn ihr Code ist geschlossen. Die beste Vorschau ist Obsidian: Ein Link, den Obsidian nicht findet, wird auch auf der Website nicht gefunden

## Wie das Repository funktioniert

- **Nur Markdown.** Es gibt keinen eigenen Build und keine Skripte
- **Es ist ein [Obsidian](https://obsidian.md/)-Vault.** Öffne den Wurzelordner des Repositorys als Vault, dann funktionieren Links, Einbettungen und Vorschauen genauso wie auf der Website. Jeder andere Markdown-Editor geht auch
- **Es ist ein Submodul der Website.** Die Website bindet das Repository als ihren Ordner `content/` ein, kompiliert die Seiten beim Build und rendert jede vorab. Die Website wird aus dem neuesten `master` dieses Repositorys gebaut

## Was wohin gehört

| Pfad | Was er enthält | Adresse auf der Website |
|---|---|---|
| `<lang>/docs/1_game/` | für Spieler: Installation, Spielen, Einstellungen, die Mechaniken | `/docs/game` |
| `<lang>/docs/2_editor/` | für Levelautoren: Anleitung und Referenz zum Editor | `/docs/editor` |
| `<lang>/docs/3_sdk/` | für Entwickler: das offene SDK und das Levelformat | `/docs/sdk` |
| `<lang>/docs/4_server/` | für Serverbetreiber: offizielle und Community-Server | `/docs/server` |
| `<lang>/docs/5_changelog/` | das Änderungsprotokoll, eine Seite pro Spielversion | `/docs/changelog` |
| `<lang>/notes/` | Artikel, Community, Regeln zum Bearbeiten, öffentliche Dokumente und Richtlinien, nach Datum | `/notes/<name>` |
| `<lang>/tags/` | Tag-Seiten | `/tags/<tag>` |
| `<lang>/download.md` | die Download-Seite | `/download` |
| `assets/` | Bilder für alle Sprachen | in Seiten eingebettet |

`<lang>` ist ein Sprachordner: `en`, `ru`, `zh`, `zh-Hant`, `ja`, `ko`, `es`, `de`, `pt` oder `fr`. Eine Datei außerhalb von `docs/`, `notes/`, `tags/` und `download.md` wird keine Seite

**Die Dokumentation beschreibt, wie die Dinge jetzt funktionieren.** Eine Änderungsgeschichte, eine Meinung oder ein Essay ist eine Notiz in `notes/`

## Dateinamen und Reihenfolge

- **Die Reihenfolge in der Seitenleiste bestimmt ein Präfix `N_`** an jeder Datei und jedem Ordner in `docs/`: `1_`, `2_` und weiter, bis `10_` und darüber hinaus
- **Das Präfix landet nie in der Adresse.** `1_game/3_controls.md` öffnet sich unter `/docs/game/controls`
- **`index.md` hat kein Präfix.** Sie ist die Startseite ihres Ordners. Sie übernimmt die Position des Ordners und gibt der Gruppe in der Seitenleiste ihren Namen
- **Um die Reihenfolge zu ändern, benenne die Dateien um.** Aktiviere in Obsidian "Interne Links automatisch aktualisieren", dann korrigiert es jeden Link selbst
- **Ein Name ohne Präfix ist innerhalb einer Sprache eindeutig.** Fallen zwei Dateien auf dieselbe Adresse, meldet das der Build der Website
- **Ein Name mit Präfix ist in jeder Sprache gleich.** `en/docs/2_editor/4_craft/3_difficulty-curve.md` und `ru/docs/2_editor/4_craft/3_difficulty-curve.md` sind dieselbe Seite
- **`notes/` hat keine Präfixe und keine Unterordner.** Benenne `notes/cookie-policy` nie um: Das Cookie-Banner der Website verlinkt darauf

## Frontmatter, Titel und Beschreibung

Jede Seite beginnt so:

```md
---
title: Difficulty and the curve
date: 2026-09-24
tags: [level_author]
---

# Difficulty and the curve

One line that says what the page is, up to 200 characters, no markup
```

- **`title`, die H1 und die Beschreibung werden in der Sprache der Seite geschrieben.** Das Beispiel oben stammt aus der englischen Fassung
- **Das Frontmatter besteht aus `title`, `date` und `tags`.** Sonst wird nichts gelesen. `date` im Format `YYYY-MM-DD` ist das Datum der letzten Aktualisierung, nicht der Erstellung. Wenn du eine Datei bearbeitest, setz `date` auf den Tag der Änderung
- **`# H1` ist Pflicht und gleich `title`.** Die Website zeigt nur den Inhalt der Seite, daher ist die H1 der sichtbare Titel
- **Der erste Absatz nach der H1 ist die Beschreibung** in Listen, in der Suche und in Linkvorschauen. Er wird nach 200 Zeichen abgeschnitten. Schreib ihn als eine Zeile, ohne Links und ohne Formatierung. Er beantwortet kurz die Frage der Seite, statt zu beschreiben, was auf der Seite steht, [[style-guide#Seiteneinstieg]]
- **Abschnitte sind `##`, Unterabschnitte `###`.** Sie erzeugen Anker und das Inhaltsverzeichnis. Tiefere Ebenen braucht es nicht

## Zielgruppen-Tags

Jede Dokumentationsseite hat 1 bis 3 Tags aus dieser Liste. Tags werden in `snake_case` ohne `#` geschrieben. Die Website zeigt sie auf der Seite an

| Tag | Auf der Website | Wer |
|---|---|---|
| `player` | [[player]] | ein normaler Spieler |
| `advanced_player` | [[advanced_player]] | ein Spieler, der sich für die Mechaniken interessiert |
| `level_author` | [[level_author]] | baut Levels im Editor |
| `developer` | [[developer]] | baut etwas auf dem SDK auf oder erweitert das Spiel |
| `server_host` | [[server_host]] | betreibt einen Server für sich und Freunde |
| `server_advanced` | [[server_advanced]] | ein großer Serverbetreiber, bereit, einen Server zu erweitern oder selbst zu schreiben |
| `contributor` | [[contributor]] | bearbeitet die Texte und Übersetzungen in diesem Repository |

Notizen in `notes/` verwenden stattdessen thematische Tags, derzeit `legal` ([[legal]])

Der Leser sieht den Code des Tags nie. Die Bezeichnung kommt von der Tag-Seite `<lang>/tags/<code>.md`:

- ihr `title` ist die Bezeichnung
- ihr erster Absatz beschreibt die Zielgruppe
- die Liste der getaggten Seiten fügt die Website selbst hinzu

Ein neuer Tag braucht eine solche Seite in jeder Sprache

Um einen Tag im Text zu erwähnen, verlinke seine Seite: `[[level_author]]`. Der Link zeigt die Bezeichnung in der Sprache des Lesers

## Links

| Was | Wie |
|---|---|
| Eine andere Seite | `[[3_difficulty-curve]]`, über den vollen Dateinamen mit Präfix |
| Ein Abschnitt einer Seite | `[[3_difficulty-curve#Anchor]]` |
| Die Startseite eines Ordners | `[[2_editor/4_craft/index]]`, mit Pfad, da jede solche Seite `index` heißt |
| Eine externe Website | `[text](https://…)`, mit voller Adresse und Schema |

Links führen zu einer Adresse ohne Sprache, deshalb funktioniert eine Quelle in jeder Sprache. `[[cookie-policy]]` schickt einen englischen Leser auf die englische Seite, einen russischen auf die russische, einen chinesischen auf die chinesische, einen japanischen auf die japanische, einen koreanischen auf die koreanische, einen spanischen auf die spanische, einen deutschen auf die deutsche, einen portugiesischen auf die portugiesische und einen französischen auf die französische

Verlinke nur Seiten, die es gibt. Der Build der Website meldet jeden Link, den er nicht auflösen konnte

## Bilder

Bilder liegen in `assets/` im Wurzelordner des Repositorys und werden mit `![[file.png]]` eingebettet

Ein Ordner dient allen Sprachen. Text, der auf ein Bild gezeichnet ist, wird mit der Seite nicht übersetzt

## Callouts

| Syntax | Farbe | Verwendung |
|---|---|---|
| `> [!note]`, `> [!info]`, `> [!tip]` | blau | Kontext, eine Abkürzung, eine Empfehlung |
| `> [!warning]`, `> [!caution]` | gelb | kostet Zeit oder Qualität, zerstört Arbeit |
| `> [!danger]`, `> [!bug]` | rot | werden dargestellt, aber der Styleguide verwendet sie nicht |

Welches Callout du wählst, sein Titel und die Grenze von zwei pro Seite - [[style-guide]]

## Zahlen, Versionen und UI-Bezeichnungen

Eine Zahl, die das Spiel festlegt - die Geschwindigkeit des Avatars, ein Standardwert in den Einstellungen, eine Größengrenze - und die aktuelle Version werden nicht in die Seite getippt. Sie stehen in `values.yaml` im Wurzelordner des Repositorys, und die Seite schreibt einen Platzhalter, den die Website beim Build füllt:

- `\{{v:avatar.move-speed}}` ist ein Wert aus `values.yaml`. Die Website schreibt ihn so, wie die Sprache der Seite Zahlen schreibt, `0.15` im Englischen und `0,15` im Russischen
- `\{{ui:menu_main_sandbox-btn}}` ist eine UI-Bezeichnung aus `game/<lang>.yaml`, in der Sprache der Seite
- `\{{` ist ein wörtliches Paar geschweifter Klammern

Ein Schlüssel, den es nicht gibt, stoppt den Build der Website, deshalb kommt eine neue Zahl zuerst in `values.yaml`. Eine Version, die als Zeitpunkt in der Geschichte genannt wird ("seit `gv 1.0.0`"), bleibt Text. Obsidian zeigt den Platzhalter so, wie er geschrieben ist

## Code und anderes Markup

- **Syntaxhervorhebung** gibt es nur für `ts`, `tsx`, `js`, `json`, `csharp`, `bash`, `yaml`, `css` und `md`. Andere Sprachen werden als reiner Text angezeigt
- **GFM-Tabellen, Aufgabenlisten, Fußnoten und `==highlights==`** funktionieren
- **Kein MDX und kein JSX.** `{` und `<` werden so angezeigt, wie sie sind
