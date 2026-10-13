---
title: Übersetzen
date: 2026-10-13
tags: [contributor]
---

# Übersetzen

Eine Übersetzung ist eine Kopie der englischen Datei unter demselben Pfad im Ordner deiner Sprache, nur mit übersetztem Text. Ein Fakt aus irgendeiner Sprache wird in alle anderen übertragen

## Gespiegelte Pfade

Jede Seite liegt in jedem Sprachordner unter demselben Pfad und mit demselben Dateinamen:

```
en/docs/2_editor/4_craft/3_difficulty-curve.md
ru/docs/2_editor/4_craft/3_difficulty-curve.md
zh/docs/2_editor/4_craft/3_difficulty-curve.md
ja/docs/2_editor/4_craft/3_difficulty-curve.md
ko/docs/2_editor/4_craft/3_difficulty-curve.md
es/docs/2_editor/4_craft/3_difficulty-curve.md
de/docs/2_editor/4_craft/3_difficulty-curve.md
fr/docs/2_editor/4_craft/3_difficulty-curve.md
```

Was unverändert bleibt:

- der Dateiname und jeder Ordnername, Präfixe eingeschlossen
- `date` und `tags` im Frontmatter (`title` wird übersetzt)
- `[[wiki-links]]`: Ihre Ziele sind Dateinamen, in jeder Sprache gleich
- externe Links, Bildnamen, Codeblöcke und Inline-Code: Dateien, Felder, Schlüssel, Werte, Befehle
- die Struktur: dieselben Überschriften in derselben Reihenfolge, dieselben Listen, Tabellen und Callouts

Die Titel der Callouts werden in die Sprache der Seite übersetzt. Mehr - [[style-guide]]

## Englisch ist der Fallback

Fehlt eine Seite in einer Sprache, zeigt die Website die englische Seite mit einem Hinweis.
Umgekehrt funktioniert das nicht: Eine Seite, die es nur in `ru/` gibt, ergibt für einen englischen Leser einen 404

> [!caution] Vorsicht
> Füge nie eine Seite in einer anderen Sprache hinzu, bevor sie in `en/` erscheint. Die Leser aller anderen Sprachen bekommen sonst einen kaputten Link

## Jede Sprache enthält jeden Fakt

Englisch führt nur bei den Adressen, nicht beim Inhalt.
Ein Fakt kann zuerst in irgendeiner Sprache auftauchen und wird dann in alle anderen übertragen. Nach einer Änderung enthält jede Fassung alles, was alle Fassungen wissen

- **Hinzufügen, nie entfernen.** Fehlende Informationen werden in jede Sprache geschrieben, der sie fehlen
- **Widersprüche werden nicht durch Raten gelöst.** Zwei Fassungen nennen unterschiedliche Zahlen oder gegensätzliche Aussagen? Prüfe die Quelle (das Spiel, das SDK) und sprich die Frage im Pull Request an
- **Nichts wird ohne Nachfrage gelöscht,** auch kein Text, der veraltet aussieht

Ein Unterschied in der Formulierung ist kein Problem. Ein Unterschied in dem, was der Leser erfährt, ist eines

## Fassungen vergleichen

Das Repository hat einen Skill für Claude Code, `compare-translations` (in `.claude/skills/`). Er macht diesen Vergleich. Ohne ihn gehst du dieselben zwei Durchgänge von Hand durch

**Der Strukturdurchgang** vergleicht die Fassungen Element für Element: Frontmatter, die H1, den ersten Absatz, die Überschriften, die Anzahl der Absätze, Listenpunkte, Tabellenzeilen und Callouts, die Linkziele, Bilder, Code

**Der Bedeutungsdurchgang** liest jeden Abschnitt nebeneinander und sucht nach Fakten, die eine Fassung hat und einer anderen fehlen: Zahlen und Einheiten, Namen von Feldern, Schaltflächen und Tasten, Bedingungen und Ausnahmen, Warnungen, die Schritte eines Ablaufs und ihre Reihenfolge, Beispiele

## Traditionelles Chinesisch wird erzeugt

`zh-Hant/` wird nicht von Hand übersetzt. Ein Skript wandelt es aus `zh/` um: OpenCC, traditionelle Schriftzeichen mit taiwanischem Wortschatz. Eine Korrektur an einer Seite in traditionellem Chinesisch gehört in die `zh/`-Seite, und die nächste Umwandlung überträgt sie. Eine Änderung direkt in `zh-Hant/` wird überschrieben

## Neue Sprache

Eine neue Sprache wird komplett in diesem Repository hinzugefügt, der Code der Website ändert sich nicht:

1. Kopiere `frontend/en.yaml` nach `frontend/<code>.yaml`, zum Beispiel `frontend/de.yaml`, und übersetze die Werte. Das sind die eigenen Texte der Website: das Menü, die Schaltflächen, die Suche, das Cookie-Banner. Lass die Schlüssel und jedes `{name}` unverändert
2. Lege den Ordner `<code>/` neben `en/`, `ru/`, `zh/`, `zh-Hant/`, `ja/`, `ko/`, `es/` und `de/` an und übersetze Seiten hinein. Eine Seite ohne Übersetzung wird auf Englisch mit einem Hinweis angezeigt

Ein Schlüssel mit den Formen `one` / `few` / `many` / `other` hängt von einer Anzahl ab. Gib ihm jede Form, die deine Sprache braucht, der Build nennt die fehlenden.
Ein nicht übersetzter Schlüssel wird auf Englisch angezeigt. Der Build listet solche Schlüssel als Warnungen auf

Öffne vor einer großen Übersetzung ein Issue in [bullet-hero/docs](https://github.com/bullet-hero/docs), damit nicht zwei Leute dasselbe übersetzen
