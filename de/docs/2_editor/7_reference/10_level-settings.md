---
title: Leveleinstellungen
date: 2026-10-02
tags: [level_author]
---

# Leveleinstellungen

Alles, was zum Level selbst gehört: Länge, fps, Seed, Ausrichtung, Metadaten, Veröffentlichung. Hier wird das Level auch gestartet, gegen die Regeln geprüft und aus einer Kopie wiederhergestellt

## Spielen

Die Startoptionen gelten **nur für diesen Durchlauf**. Nichts davon wird im Level gespeichert

Mit `{{ui:settings_level-settings_life-text}}`, `{{ui:field_common_speed}}`, `{{ui:settings_level-settings_checkpoints-toggle}}` und dem Autolevel kannst du einen Abschnitt üben, ohne ihn zu bearbeiten

> [!tip] Tipp
> Der `{{ui:settings_level-settings_seed}}` hier hat Vorrang vor dem eigenen Seed des Levels. Er ist die oberste der drei Stufen. Damit spielst du genau den Durchlauf noch einmal, den du gerade gesehen hast. `0` bedeutet: den eigenen Seed des Levels verwenden oder bei jedem Durchlauf einen neuen

Mehr - [[3_difficulty-curve]]

## Grundlagen

Länge in Frames, Framerate und die beiden Seeds des Levels

`{{ui:settings_level-settings_core-seed-value}}` ist der eigene Seed des Levels. Er gehört zum Inhalt, und eine Änderung lässt sich rückgängig machen.
`0` bedeutet "bei jedem Durchlauf ein neuer Seed". Das ist der Standard, also spielt sich ein gewöhnliches Level jedes Mal anders

> [!tip] Tipp
> `{{ui:settings_level-settings_core-runtime-seed-value}}` zeigt nur, welchen Seed diese Editorsitzung ermittelt hat. `{{ui:settings_level-settings_core-runtime-seed-regenerate}}` würfelt einen neuen nur für die Sitzung: Nichts wird geschrieben, und nichts landet im Rückgängig-Verlauf. Beim Neuladen des Levels wird der Seed erneut ermittelt

> [!info] Gut zu wissen
> **Ein Frame ist eine Zelle, und die Zeit ist eine Grenze.** Frames zählen ab 1. Frame *f* deckt die Zeit von (*f*-1)/fps bis ausschließlich *f*/fps ab. Ein Level aus N Frames enthält die Frames 1 bis N. N+1 ist die Endgrenze, kein Frame

Mehr - [[4_frames-and-time]]

## Levelausrichtung

Wie das Gerät während dieses Levels gehalten wird

`{{ui:enum_level-orientation_horizontal}}` und `{{ui:enum_level-orientation_vertical}}` drehen das Gerät des Spielers für die Dauer des Levels. Diese Wahl hat Vorrang vor der Einstellung des Spielers.
Einen Monitor kann man nicht drehen. Auf dem Desktop läuft ein vertikales Level deshalb zwischen seitlichen Balken, und genau so soll es aussehen

`{{ui:enum_level-orientation_not-specified}}` überlässt die Wahl dem Spieler. Das ist kein Standard, sondern eine Aussage über dein Level: Es liest sich in **beiden** Ausrichtungen richtig.
Das Spiel passt dafür nichts an: Nichts wird verschoben, beschnitten oder skaliert. Inhalt jenseits der horizontalen Ränder liegt in der einen Ausrichtung außerhalb des Bildschirms und ist in der anderen sichtbar.
Wähle es erst, nachdem du das Level in beiden Richtungen geprüft hast

## Gefahrenzone

Aktionen, die Dateien löschen oder neu schreiben statt Inhalt

> [!caution] Vorsicht
> Die Auswahllisten `{{ui:settings_level-settings_quot-level-quot-file-format}}` und `{{ui:settings_level-settings_quot-metadata-quot-file-format}}` schreiben das Level und seine Metadaten neu auf die Festplatte. Ein Formatwechsel **löscht die Datei im alten Format**. Sonst passiert nichts: kein Neuladen, keine neue Simulation, deine Auswahl und der Rückgängig-Verlauf bleiben. Geschrieben wird genau das, was schon im Speicher liegt

> [!caution] Vorsicht
> `{{ui:settings_level-settings_delete-level-open}}` entfernt den Ordner des Levels von der Festplatte. Das lässt sich nicht rückgängig machen

Mehr - [[4_not-losing-work]]

## Regeln

Probleme, die die Validierung in diesem Level gefunden hat:
- kaputte Verweise
- doppelte IDs
- Zyklen von Elternobjekten
- zu tief verschachtelte Prefabs
- überlappende Beat-Segmente

> [!info] Gut zu wissen
> **Manche Befunde lassen sich beheben, einzeln oder mit `{{ui:settings_level-settings_rules-fix-all}}`.** Die Korrekturen landen in einem Entwurf: `{{ui:editor_save_text}}` übernimmt sie als eine Operation, die sich rückgängig machen lässt, `{{ui:settings_level-settings_raw-discard}}` verwirft sie. Befunde im Objektgraphen (IDs, Elternobjekte, Prefab-Verschachtelung) haben keine Korrektur, und das ist Absicht: Jeder davon ist eine inhaltliche Entscheidung, die nur du treffen kannst, und eine automatische Korrektur würde stillschweigend eine von mehreren gültigen Antworten wählen

> [!tip] Tipp
> Ein Kind, das über die Spanne seines Elternobjekts hinausragt, wird **nicht** gemeldet. Das sind gültige Daten, die sich wie vorgesehen verhalten. Wenn du die Lebensdauern doch angepasst haben willst, starte den Modifikator `{{ui:mod_span_fit}}` aus den Generatoren. Er zieht die Kinder hinein oder dehnt die Elternobjekte aus

Mehr - [[4_not-losing-work]]

## Metadaten

Alles über das Level, was nicht das Level selbst ist: Name, Beschreibung, Logo, Lizenz, Altersfreigabe und Autoren

Name und Beschreibung werden pro Sprache geschrieben, direkt hier.
Ein Spieler, dessen Sprache du nicht ausgefüllt hast, bekommt die erste, die du ausgefüllt hast

> [!info] Gut zu wissen
> Hier sind keine Übersetzungsschlüssel nötig. Ein Level ist Inhalt, kein Teil der Oberfläche des Spiels

Lizenz und Autoren reisen mit dem Level mit, wohin es auch geteilt wird. So bleibt die Namensnennung auch nach einem erneuten Hochladen erhalten

Mehr - [[2_metadata-and-sharing]]

## Level-Tags

Tags sind deine eigenen Wörter. Sie werden genau so angezeigt, wie sie geschrieben sind, und nie übersetzt.
Ein Spieler filtert damit die Levels im Levelbrowser

Schreibe die Tags durch Kommas getrennt. Halte sie kurz und allgemein: ein Genre, eine Stimmung, eine Mechanik.
Ein Tag hilft nur, wenn andere Levels ihn auch verwenden. Ein Tag, den sonst niemand eintippt, filtert nichts

## Sammlungen

Holt Ressourcen aus einer Sammlung ins Level oder baut eine Sammlung aus den eigenen Ressourcen des Levels. Der Tab steht direkt nach `{{ui:editor_library_kind-prefabs}}`

- `Importieren` - eine Sammlung öffnen, Einträge abhaken, `Importieren` drücken. Abhängigkeiten kommen mit, und der ganze Import ist ein Rückgängig-Schritt
- `{{ui:editor_collections_mode-build}}` - die Ressourcen des Levels abhaken und `{{ui:editor_collections_build}}` drücken, in `{{ui:editor_collections_target-new}}` oder in eine deiner eigenen

Ein Eintrag, den das Level schon in einer anderen Version hat, öffnet `{{ui:editor_resource-conflict_title}}`. Nichts wird stillschweigend überschrieben

Mehr - [[16_library-and-collections]]

## Veröffentlichung

Der einzige Ort, von dem aus ein Level irgendwohin geschickt wird: als Archiv oder in den Steam Workshop

`{{ui:editor_share_destination}}` wählt das Ziel. Darunter stehen die eigenen Bedienelemente dieses Ziels, sein Bericht und die Schaltfläche, die es ausführt.
Der Bericht prüft das Level von selbst, ohne dass du eine Schaltfläche drücken musst. Fehler blockieren den Vorgang, Warnungen und Hinweise nicht

Mehr - [[17_publishing]]

## Verlauf

Jede Bearbeitung dieser Sitzung ist hier eine Zeile. Die neueste steht oben, wie bei einem `git log`

Die Spalte ganz links ist die Hauptlinie.
Eine eigene Spalte ist ein Zweig. Das ist eine Linie, die du zurückgelassen hast, als du eine Bearbeitung rückgängig gemacht hast und einen anderen Weg gegangen bist

Der Ring markiert, wo du gerade bist. Der grüne Kreis markiert das letzte Speichern

Ein Klick auf eine Zeile führt das Level genau in diesen Zustand zurück.
Der Weg dorthin wendet eine Operation pro Frame an. So siehst du zu, wie sich das Level verändert, statt auf einen eingefrorenen Bildschirm zu warten

> [!warning] Warnung
> Solange der Weg läuft, ist der Editor schreibgeschützt. Die Kamera bewegen und den Abspielkopf ziehen kannst du weiterhin, bearbeiten aber nicht. Abbrechen hält den Weg dort an, wo er gerade ist, und das ist immer ein echter Zustand des Levels

> [!tip] Tipp
> Der Verlauf existiert nur in der aktuellen Sitzung. Er wird nie auf die Festplatte geschrieben, und beim erneuten Öffnen des Levels beginnt er von vorn. Seine Größe ist begrenzt: Zuerst fallen die ältesten verlassenen Zweige weg, dann die ältesten Bearbeitungen

## Rohdaten

Das ganze gespeicherte Levelmodell als ein Baum aus Feldern. Das ist die Datei selbst, bevor der Editor sie verarbeitet

> [!caution] Vorsicht
> **Hier wird nichts validiert.** Das ist der Notausgang für alles, was noch kein anderer Bildschirm abdeckt. Es schreibt auch einen Wert, den der Rest des Editors für unmöglich hält

Ein gefüllter Punkt neben einem Feld bedeutet, dass du es in dieser Sitzung geändert hast.
Ein hohler Punkt bedeutet, dass sich etwas darin geändert hat. Ohne ihn wäre eine Änderung drei Stufen tief in einem eingeklappten Zweig unsichtbar

Die Schaltfläche `{{ui:settings_level-settings_raw-apply}}` ist ausgeblendet, nicht deaktiviert, wenn es nichts zu übernehmen gibt.
Ein leeres Übernehmen würde ohne Grund einen Levelaustausch auf den Rückgängig-Stapel legen

Mehr - [[4_not-losing-work]]
