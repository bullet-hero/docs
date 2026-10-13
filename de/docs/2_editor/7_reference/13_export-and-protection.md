---
title: Export und Schutz
date: 2026-10-11
tags: [level_author]
---

# Export und Schutz

Der Export speichert das Level als Ordner oder Archiv außerhalb des Spiels, mit jeder Datei, die es nutzt. Ein Passwort verschlüsselt den Inhalt, ein vergessenes ist nicht wiederherstellbar

## Level exportieren

Das liegt im Tab `{{ui:settings_level-settings_publication}}` der Leveleinstellungen: Ziel `{{ui:editor_share_archive}}`, der Modus in `{{ui:editor_share_format}}` und `{{ui:editor_share_passphrase}}` für einen geschützten Modus. Mehr - [[17_publishing]]

Ein Archiv enthält das Level, seine Metadaten und jede Datei, die es verwendet.
Ein Song, der außerhalb des Levelordners liegt, wird ebenfalls hineinkopiert. Sein Verweis wird auf die Kopie im Archiv umgestellt

Der Ordner `ai` des Levels, in dem ein KI-Assistent seine Notizen zum Level ablegt, wird ebenfalls eingepackt, außer `{{ui:settings_level-settings_metadata-level-ai-share}}` ist in den Levelmetadaten abgewählt. Ein Modus mit Passwort packt ihn nie ein: Lesbare Designnotizen neben einem verschlüsselten Level würden das Passwort sinnlos machen. Der Bericht sagt, wenn der Ordner weggelassen wurde. Mehr - [[7_ai-assistant#Der Ordner ai]]

| `{{ui:editor_share_format}}` | Was du bekommst | Geöffnet mit |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_folder}}` | denselben Ordner, den das Level auf der Festplatte hat. Zippe ihn und verschicke ihn | nichts nötig |
| `{{ui:settings_level-settings_export-mode_folder-protected}}` | denselben Ordner, mit verschlüsseltem Leveldokument. Metadaten, Cover und Medien bleiben lesbar, also zeigt ein Levelbrowser weiterhin seine Karte | gpg für das Leveldokument |
| `{{ui:settings_level-settings_export-mode_zip}}` | eine Datei | ein Doppelklick im Windows Explorer, nichts zu installieren |
| `{{ui:settings_level-settings_export-mode_targz}}` | eine Datei | jedes Archivprogramm |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | ein Zip mit eigener AES-256-Verschlüsselung. Die übliche Bedeutung eines Passworts auf einem Archiv | 7-Zip oder jedes andere Archivprogramm, das nach dem Passwort fragt |
| `{{ui:settings_level-settings_export-mode_zip-protected}}`, `{{ui:settings_level-settings_export-mode_targz-protected}}` | dasselbe Archiv, verpackt in `.gpg` | gpg |

Der Windows Explorer öffnet keine der Passwortoptionen. Das ist der Preis eines Passworts

Eine Sammlung oder eine einzelne Ressource aus der Bibliothek nimmt dieselben fünf Archivmodi an, die mit Passwort eingeschlossen. Die beiden Ordnermodi gibt es nur für ein Level. Mehr - [[17_publishing#Archiv]]

> [!tip] Tipp
> Alles, was nicht mitreisen konnte (eine Ressource hinter einer URL, eine Datei, auf die nichts verweist), steht nach dem Export im Bericht

> [!warning] Warnung
> Ein Passwort schützt den Inhalt beim Versand und vor beiläufigem Kopieren. Es ist kein DRM: Wer die Datei und das Passwort hat, kann sie immer öffnen

## Level schützen

Verschlüsselt das Dokument des Levels auf der Festplatte. Beim Öffnen des Levels wird nach dem Passwort gefragt

Geschützt ist der **Inhalt**: Objekte, Keyframes, Themes.
Metadaten, Cover und Medien bleiben lesbar. So zeigt der Levelbrowser die Karte des Levels auch ohne Passwort

Das Passwort wird einmal pro Sitzung abgefragt und nur im Speicher gehalten.
Es wird nirgends geschrieben, also funktioniert das Autospeichern weiter

Um den Schutz zu entfernen, lass das Feld leer und drücke `{{ui:settings_level-settings_protect-apply}}`

> [!caution] Vorsicht
> Ein vergessenes Passwort lässt sich nicht wiederherstellen. Nirgends wird ein Schlüssel aufbewahrt, und ohne das Passwort gibt es keinen Weg in die Datei
