---
title: KI-Assistent
date: 2026-10-13
tags: [level_author]
---

# KI-Assistent

Ein KI-Client mit MCP bearbeitet das offene Level im Editor, während du zusiehst. Jeder KI-Batch ist ein Rückgängig-Schritt. Veröffentlichen, Dateien löschen, fremde Levels überschreiben kann er nicht

Das Spiel bringt dafür unter Windows, Linux und Mac einen MCP-Server mit. Die KI bearbeitet über dieselben Operationen wie du, also erscheint jede Änderung sofort im Viewport und landet wie deine eigene im Verlauf

Jeder Client, der MCP spricht, funktioniert, etwa eine Chat-App oder ein Coding-Assistent. Nichts im Spiel ist an eine bestimmte KI gebunden

## Einen Client verbinden

1. Öffne `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}`
2. Setz den Haken bei `{{ui:settings_game-editor_mcp-enabled}}`. Die Statuszeile unter den Einstellungen zeigt den Port, auf dem der Editor lauscht
3. Drück `{{ui:settings_game-editor_mcp-copy-config}}`. In der Zwischenablage liegt jetzt die Client-Konfiguration mit beiden ausgefüllten Pfaden
4. Füge sie in die MCP-Servereinstellungen deines Clients ein
5. Öffne ein Level im Editor oder bitte die KI, den Editor oder ein Level selbst zu öffnen

Die kopierte Konfiguration sieht so aus:

```json
{ "mcpServers": { "bullet-hero": { "command": "<path to BH.MCP>", "args": ["--endpoint", "<path to endpoint.json>"] } } }
```

Die Serverdatei `BH.MCP` liegt neben dem Spiel:

| System | Serverdatei |
|---|---|
| Windows | `<game folder>/BH.MCP.exe` |
| Linux | `<game folder>/BH.MCP` |
| Mac | `<game>.app/Contents/Resources/mcp/osx-arm64/BH.MCP`, auf Intel `osx-x64` statt `osx-arm64` |

Verbinden kann sich nur dieser Rechner, und nur ein Client gleichzeitig.
Smartphones und Tablets haben keinen MCP-Abschnitt: Den Assistenten gibt es nur auf dem Desktop

Es können mehrere Kopien des Spiels gleichzeitig laufen. Die KI arbeitet in der zuletzt gestarteten, bis du sie bittest zu wechseln, und sie kann alle auflisten. Jede Kopie nimmt trotzdem nur einen Client. Für mehrere Kopien lass `{{ui:settings_game-editor_mcp-port}}` auf `0`, denn zwei Kopien können nicht auf demselben Port lauschen

## Was die KI kann und was nicht

Die KI kann fast alles, was du kannst:
- das Level lesen: die Hierarchie, Objekte, Keyframes, Ereignisse und Ressourcen
- Objekte, Keyframes, Marker, Checkpoints, Audiospuren und das Beat-Raster erstellen, ändern und löschen
- Generatoren ausführen, Prefabs packen und platzieren, im Prefab-Modus arbeiten
- eine Textur, Schriftart oder Audiodatei ins Level importieren
- nach dem Import den Herkunftseintrag einer Textur, Schriftart oder Audiodatei ausfüllen: Titel, Beschreibung, Link, Quellen und Autoren - [[4_resource-record]]
- die mitgelieferten Themes, Schriftarten und Oberflächensounds des Spiels verwenden. `resources_list` markiert sie als Teil des Spiels, und sie brauchen keinen Import. Das Spiel liefert keine vorgefertigten Effekte mit: Ein Effekt, den die KI platziert, ist einer, den das Level schon enthält, oder ein neuer, den sie erstellt
- jeden Umriss aus seinen Ecken als Levelform zeichnen, eine Form mit einem Verlauf färben, Schriftart und Ausrichtung eines Texts festlegen, die Themes des Levels erstellen und bearbeiten
- rückgängig machen und wiederholen, das offene Level speichern, ein anderes Level öffnen, ein neues erstellen
- die Wiedergabe starten und pausieren, wie deine Abspielschaltfläche
- das Spiel auf einen anderen Bildschirm wechseln lassen, etwa den Editor, ein Level oder die Einstellungen, mit denselben Argumenten wie beim Start - [[12_launch-arguments]]
- das Spiel starten, wenn es nicht läuft, sofern der Server neben dem installierten Spiel liegt und MCP schon an ist

Ein so gestarteter Durchlauf zählt in deiner Statistik wie jeder andere, deshalb startet die KI einen nur, wenn du sie darum bittest

Sie kann nicht:
- im Steam Workshop veröffentlichen
- ein Level oder irgendeine Datei löschen
- ein anderes Level oder eine andere Datei überschreiben. Ein Import, dessen Dateiname schon vergeben ist, wird abgelehnt
- ein schreibgeschütztes Level öffnen oder ein geschütztes Level, dessen Passwort du in dieser Sitzung nicht eingegeben hast
- ein anderes Level öffnen, solange das offene ungespeicherte Änderungen hat

**Ein KI-Batch ist ein Schritt im Verlauf.** Er erscheint im Tab `{{ui:settings_level-settings_history}}` als `{{ui:op_group_ai-batch}}` mit der eigenen Beschriftung der KI. Ein `Ctrl+Z` entfernt den ganzen Batch. Mehr zum Verlauf - [[10_level-settings#Verlauf]]

**Die KI legt nie zwei Objekte auf dieselbe Ebene, während beide spielen.** Würde ein Batch das tun, hebt sie das spätere Objekt im selben Schritt auf die nächste freie Ebene und sagt das. Prefab-Inhalt ist die Ausnahme: Er darf sich Ebenen mit dem Rest des Levels teilen

Der erste KI-Batch, der ein Level ändert, setzt dessen `{{ui:settings_level-settings_metadata-level-ai-generated}}` auf `{{ui:enum_ai-generation_yes}}`, im selben Schritt. Wird der Batch rückgängig gemacht, wird auch das zurückgesetzt. Mehr - [[2_metadata-and-sharing#KI-Generierung]]

## Du hast Vorrang

Die KI kämpft nie mit dir um den Editor:
- während du einen Gizmo-Griff ziehst oder den Abspielkopf über die Zeitleiste ziehst, werden die Änderungen der KI abgelehnt, und sie wartet und versucht es erneut
- die KI übernimmt den Abspielkopf nur, solange du untätig bist: nicht abspielst, nicht ziehst, nicht tippst, nicht speicherst
- der Editor beginnt ein Level beim Öffnen abzuspielen, deshalb kann die KI es pausieren, um sich Frames anzusehen. Ein Level, das die KI selbst öffnet oder erstellt, bleibt pausiert. Schaust du der Wiedergabe absichtlich zu, fragt die KI vor dem Pausieren
- berührst du den Editor, während die KI sich einen Frame ansieht, hört die KI sofort auf. Der Abspielkopf bleibt, wo du ihn hingesetzt hast
- solange ein Gang durch den Verlauf läuft, kann die KI ebenfalls nicht bearbeiten

Solange ein Client verbunden ist, zeigt der Viewport oben rechts unter den Suchschaltflächen `AI` an. Die Farbe ist der Zustand: grün - verbunden, gelb - die KI arbeitet, rot - der letzte Aufruf der KI endete mit einem Fehler.
Nachdem sich der Client getrennt hat, bleibt das Abzeichen noch {{v:mcp.badge-hold-seconds}} Sekunden stehen, damit eine KI, die sich für jeden Schritt neu verbindet, nicht blinkt. Es wird zusammen mit den Viewport-Werkzeugen ausgeblendet.
Fahr mit der Maus darüber, um den Zustand in Worten zu lesen: `{{ui:editor_agent-badge_connected}}`, und während die KI arbeitet, die Beschriftung dessen, was sie gerade tut.
Das Kreuz daneben trennt den Client und weist ihn ab, und das Abzeichen verschwindet

Ein Stopp wird nicht gespeichert. `{{ui:settings_game-editor_mcp-enabled}}` aus- und wieder einzuschalten oder das Spiel neu zu starten, hebt ihn auf

## Was die KI sieht

Die KI betrachtet das Level auf zwei Arten:
- **ein Schema.** Ein Bild eines beliebigen Frames, außerhalb des Bildschirms berechnet. Es bewegt den Abspielkopf nicht. Es zeigt Formen und Hitboxen, aber keine Texte und keine Effekte
- **eine Aufnahme.** Echte Pixel, genau so, wie das Level zeichnet, aufgenommen über deinen Abspielkopf. Für einen Moment springt der Abspielkopf auf diesen Frame, und die Overlays des Editors verschwinden. Dann kehrt der Abspielkopf dorthin zurück, wo du ihn gelassen hast, außer `{{ui:settings_game-editor_mcp-follow-ai}}` ist an. Das Bild ist durch die Levelkamera gerahmt, nicht durch die Editorkamera. Für einen genauen Blick auf ein Detail kann die KI stattdessen ein Rechteck der Welt rahmen. Das Level ändert sich nicht

Ein Standbild eines Effekts nach einem Sprung kommt dem nahe, was durchgehende Wiedergabe zeigt, ist aber nicht immer identisch

Die KI kann die Musik nicht hören. Sie verwandelt den Song in Zahlen: Tempo, Beats, Takte, Abschnitte, wie laut jedes Frequenzband ist.
Das ist eine Schätzung mit einer Konfidenz, und sie kann danebenliegen, zum Beispiel um das halbe oder doppelte Tempo. Das Beat-Raster, das du im Level festgelegt hast, gilt mehr als die Schätzung der KI.
Ein Beat-Raster, das die KI aus der Analyse vorschlägt, rundet ein Tempo, das weniger als 0.01 % von einer ganzen Zahl entfernt ist, auf diese Zahl, und sein Versatz ist immer kürzer als ein Takt. Ein Vorschlag für einen Teil des Songs nimmt das eigene Tempo dieses Teils, also bekommt ein Song mit wechselndem Tempo ein Segment pro Tempo

Wenn es auf das Timing ankommt, kann die KI dich deshalb bitten zuzuhören. Sie spielt im Editor einen Bereich von bis zu {{v:mcp.max-play-seconds}} Sekunden ab, und das bewegt auch den Abspielkopf. Berührst du den Editor, stoppt die Wiedergabe an der Stelle, wo sie ist

Solange der Ton des Editors stummgeschaltet ist, spielt die KI nichts ab und bittet dich, den Ton einzuschalten

Die eigenen Aktionen der KI machen keine Oberflächensounds: Ein Rückgängig, ein Speichern oder eine Ablehnung, die sie auslöst, ist stumm. Zu hören ist nur, was sie absichtlich abspielt

## Der Ordner ai

Die KI bewahrt ihr Gedächtnis über das Level im Ordner `ai` im Levelordner auf. Die nächste Sitzung liest ihn mit jedem Client zuerst und macht dort weiter, wo die letzte aufgehört hat

Was dort liegt:
- `CONTEXT.md` - das Briefing, die Musik, der Abschnittsplan, Entscheidungen, deine Anmerkungen und offene Fragen
- andere Dateien, die die KI behalten will, nur `.md` oder `.json`
- `manifest.json` - ob der Ordner mit dem Level reist. Die KI kann das nicht ändern

Der Ordner erscheint erst, wenn die KI zum ersten Mal etwas zu schreiben hat. Eine Datei fasst bis zu {{v:mcp.ai-file-max-kb}} KB, der ganze Ordner bis zu {{v:mcp.ai-folder-max-mb}} MB. Das sind einfache Textdateien: Du kannst sie selbst lesen, bearbeiten oder löschen

> [!warning] Warnung
> Der Ordner `ai` gehört nicht zum Verlauf des Levels. `Ctrl+Z` macht nicht rückgängig, was die KI dort geschrieben hat

**Der Ordner reist standardmäßig mit dem Level**: in einem exportierten Archiv und bei einem Upload in den Steam Workshop. Um ihn zu Hause zu behalten, entferne den Haken bei `{{ui:settings_level-settings_metadata-level-ai-share}}` im Tab `{{ui:settings_level-settings_metadata}}` der Leveleinstellungen. Das Kästchen erscheint, sobald der Ordner existiert. Es wird sofort in eine Datei gespeichert, also macht `Ctrl+Z` auch das nicht rückgängig

Ein Exportmodus mit Passwort nimmt den Ordner nie mit, egal was das Kästchen sagt. Mehr - [[13_export-and-protection#Level exportieren]]

Eine Kopie des Levels auf diesem Gerät nimmt den Ordner mit, denn eine Kopie ist kein Teilen

## Einstellungen

Alle liegen unter `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}` und werden nur auf diesem Gerät gespeichert:
- `{{ui:settings_game-editor_mcp-enabled}}` - ob sich überhaupt ein Client verbinden kann. Standardmäßig aus
- `{{ui:settings_game-editor_mcp-port}}` - der Port, auf dem der Editor lauscht. `0` wählt bei jedem Start einen freien
- `{{ui:settings_game-editor_mcp-follow-ai}}` - an: Nach einer Aufnahme bleibt der Abspielkopf pausiert auf dem Frame, den sich die KI angesehen hat
- `{{ui:settings_game-editor_mcp-reveal-edits}}` - wählt nach jeder Änderung der KI aus, was sie erstellt oder geändert hat, und lokalisiert es
- `{{ui:settings_game-editor_mcp-operation-delay}}` - wie lange der Editor zwischen zwei Operationen der KI wartet, damit du folgen kannst. `0` wendet jede sofort an

Jede Einstellung und ihr Standardwert - [[14_editor-settings#KI-Agent]]

Weiter: [[4_not-losing-work]], [[13_export-and-protection]]
