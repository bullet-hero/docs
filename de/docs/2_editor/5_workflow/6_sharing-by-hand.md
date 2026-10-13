---
title: Ein Level von Hand teilen
date: 2026-10-01
tags: [level_author]
---

# Ein Level von Hand teilen

Pack den Levelordner als zip oder tar.gz und verschlüssle ihn für ein Passwort mit gpg. Auf einem anderen Rechner läuft das entpackte Level sofort, und das Spiel liest solche Archive selbst

Ein Level ist ein Ordner mit Dateien. Ein Archiv ist derselbe Ordner, zum Verschicken gepackt.
Alles, was das Level verwendet, reist mit: der Song, die Bilder, das Cover

Wohin der Empfänger das Level legt - [[2_metadata-and-sharing#Ein Level heute teilen]]

## Was nicht ins Archiv kommt

- eine Ressource, die das Level über einen Link bezieht. Der Link bleibt, wie er war
- eine Datei, auf die nichts im Level verweist

Der Exportbericht des Spiels führt beides auf. Mehr - [[13_export-and-protection#Level exportieren]]

## Fünf Arten

Jede öffnet sich mit Werkzeugen, die die Gegenseite schon hat:

| Datei | Was drin ist | Öffnet sich mit |
|---|---|---|
| `level.json.gpg` | nur das Leveldokument, hinter einem Passwort, im Levelordner | gpg |
| `LEVEL_FOLDER.tar.gz` | der ganze Ordner als ein Archiv | 7-Zip, Keka, Ark, Explorer |
| `LEVEL_FOLDER.tar.gz.gpg` | dasselbe Archiv hinter einem Passwort | gpg |
| `LEVEL_FOLDER.zip` | derselbe Ordner als zip | Windows per Doppelklick, ohne Installation |
| `LEVEL_FOLDER.zip.gpg` | dasselbe zip hinter einem Passwort | gpg |

Standardmäßig setzt das Spiel das Passwort mit den eigenen Mitteln von zip, AES-256. Jedes Archivprogramm außer dem Explorer öffnet ein solches Archiv: Es fragt nach dem Passwort.
Die `.gpg`-Arten schreibt das Spiel auf Wunsch

## Bevor du die Zeilen ausführst

Ersetze zwei Stellen in den Zeilen:
- `LEVEL_FOLDER` - der Name des Levelordners, also seine ID. Das ist eine lange Folge aus Ziffern und Buchstaben, der Name des Ordners in `levels`
- `YOUR_PASSWORD` - das Passwort selbst

Ein in die Kommandozeile getipptes Passwort bleibt im Verlauf der Shell.
Entferne `--batch --pinentry-mode loopback --passphrase YOUR_PASSWORD` aus der Zeile, dann fragt gpg auf dem Bildschirm nach dem Passwort

## Das Leveldokument mit gpg

Die Verschlüsselung legt `level.json.gpg` neben das Original. Die Originaldatei bleibt, wo sie ist: Lösch sie selbst, sobald du das Ergebnis geprüft hast.
Die Entschlüsselung schreibt das Dokument wieder unter seinem eigenen Namen. Die verschlüsselte Datei bleibt, wo sie ist:

```bash
gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json.gpg > level.json
```

## Ein tar.gz-Archiv

Der Ordner wird von innen gepackt: Das Archiv enthält die Leveldateien selbst, ohne einen Ordner darum.
Zum Entpacken muss der Zielordner schon existieren, tar legt ihn nicht an. `mkdir` funktioniert gleich in cmd, in PowerShell und im Terminal unter Mac oder Linux:

```bash
tar -czf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER .
mkdir LEVEL_FOLDER
tar -xzf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER
```

Packen und Verschlüsseln in einem Durchgang. Das ungeschützte Archiv landet gar nicht erst auf der Festplatte.
Die zweite Zeile entschlüsselt das Archiv und entpackt es zurück in denselben Ordner:

```bash
tar -czf - -C LEVEL_FOLDER . | gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD -o LEVEL_FOLDER.tar.gz.gpg
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD LEVEL_FOLDER.tar.gz.gpg | tar -xz -C LEVEL_FOLDER
```

## Ein zip-Archiv

Unter Windows - in PowerShell, die jeder Rechner hat. Der Stern packt den Inhalt des Ordners, nicht den Ordner selbst.
`Expand-Archive` legt den Ordner selbst an, vorher ist kein `mkdir` nötig:

```
Compress-Archive -Path LEVEL_FOLDER\* -DestinationPath LEVEL_FOLDER.zip
Expand-Archive -Path LEVEL_FOLDER.zip -DestinationPath LEVEL_FOLDER
```

Unter Mac oder Linux - zip und unzip:

```bash
cd LEVEL_FOLDER && zip -r ../LEVEL_FOLDER.zip .
unzip LEVEL_FOLDER.zip -d LEVEL_FOLDER
```

Ein zip mit Passwort, nach dem 7-Zip fragt, erstellt 7-Zip selbst. Es muss installiert sein:

```
7z a -tzip -mem=AES256 -pYOUR_PASSWORD LEVEL_FOLDER.zip .\LEVEL_FOLDER\*
```

## Das Spiel liest sie zurück

Alle Arten funktionieren in beide Richtungen. Was das Spiel geschrieben hat, öffnen gpg, tar und zip. Was gpg, tar und zip erstellt haben, liest das Spiel.
Deshalb fiel die Wahl auf Standardwerkzeuge und nicht auf ein eigenes Format

> [!tip] Tipp
> Das Spiel schaut darauf, was eine Datei ist, nicht darauf, wie sie heißt. Ein umbenanntes Archiv öffnet sich also trotzdem. `7z` erkennt das Spiel, nimmt es aber nicht an: Es nennt das Format, statt die Datei für kaputt zu erklären. Pack ein solches Archiv als zip neu

> [!caution] Vorsicht
> **EIN VERGESSENES PASSWORT LÄSST SICH NICHT WIEDERHERSTELLEN**. Der Schlüssel ist nirgends gespeichert: nicht im Spiel, nicht in der Datei, bei niemandem. Es gibt kein Zurücksetzen, keine Wiederherstellung und keinen Umweg. Ein Level mit verlorenem Passwort ist mit ihm verloren. Schreib das Passwort auf, bevor du den Editor schließt

Weiter: [[4_level-folder-and-backups|Der Levelordner und Sicherungen]], [[4_not-losing-work|Damit keine Arbeit verloren geht]]
