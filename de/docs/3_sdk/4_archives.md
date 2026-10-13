---
title: Archive und Schutz
date: 2026-10-01
tags: [developer, level_author]
---

# Archive und Schutz

Ein Level wird als Ordner, tar.gz oder zip exportiert, auf Wunsch mit Passwort: zip mit AES-256 oder OpenPGP. Das SDK erkennt das Format einer empfangenen Datei an ihren ersten Bytes, nicht am Namen

## Exportmodi

Ein Level verlässt das Gerät in einer der Formen von `LevelExportMode`:

| Wert | Modus | Was geschrieben wird | Schutz |
|---|---|---|---|
| 0 | `Folder` | ein einfacher Ordner, dieselbe Form wie auf der Festplatte | keiner |
| 1 | `FolderProtectedLevel` | ein Ordner, in dem nur `level.json.gpg` verschlüsselt ist | OpenPGP |
| 2 | `TarGz` | `<name>.tar.gz` | keiner |
| 3 | `TarGzProtected` | `<name>.tar.gz.gpg` | OpenPGP |
| 4 | `Zip` | `<name>.zip` | keiner |
| 5 | `ZipProtected` | `<name>.zip.gpg` | OpenPGP |
| 6 | `ZipEncrypted` | `<name>.zip` mit AES-256-Einträgen | der eigene von zip |

Die Nummer ist die Identität des Modus, sie ändert sich nie. Die Reihenfolge in der Auswahlliste des Editors wird getrennt festgelegt (`DisplayOrder`)

**Jedes Format ist ein offener Standard.** `tar -xzf`, `gpg -d` und jedes Archivprogramm öffnen sie ohne das Spiel:

```bash
gpg -d level.tar.gz.gpg > level.tar.gz
tar -xzf level.tar.gz
```

## Zwei Schutzverfahren

**`ZipEncrypted` ist der Standardweg, ein Level mit einem Passwort zu sperren.** Der Empfänger hat ein Archivprogramm, aber höchstwahrscheinlich kein gpg

**OpenPGP sperrt ein Dokument, einen Ordner und ein Archiv mit einem Verfahren.** Nur damit lässt sich ein Ordner schützen

In `FolderProtectedLevel` bleiben die Metadaten, das Cover und die Medien lesbar. So zeigt der Levelbrowser die Karte weiterhin an

Die innere Endung bleibt im Namen: `level.json.gpg`. Genau so nennt `gpg -c level.json` die Datei, daher ist das Format ohne Raten bekannt

## Was hineinkommt

`LevelArchiveBuilder` ermittelt den Inhalt aus dem Modell, nicht aus der Dateiliste des Ordners. Eine Datei, auf die das Level nicht verweist, bleibt draußen. Der Bericht nennt, wie viele solcher Dateien ausgelassen wurden

Die Verweise des Levels werden so behandelt:
- eine Ressource mit `AbsolutePath` wird ins Archiv kopiert. Ihr Verweis wird auf `LevelPath` umgeschrieben, aber nur in der exportierten Kopie
- `DirectUrl` bleibt, wie es ist, und kommt in den Bericht: Eine URL kann nicht in einer Datei mitreisen
- eine fehlende Datei kommt mit dem Code `archive.resource_missing` in den Bericht

## Erkennung an den Bytes

Einen Dateinamen kann jeder schreiben. Deshalb entscheidet `ArchiveFormatSniffer` anhand der ersten 8 Bytes:

| Erste Bytes | Format |
|---|---|
| `1F 8B` | `TarGz` |
| `50 4B 03 04`, `50 4B 05 06`, `50 4B 07 08`, `50 4B 30 30` | `Zip` |
| `37 7A BC AF 27 1C` | `SevenZip` |
| ein OpenPGP-Paket-Tag, zuletzt geprüft | `OpenPgp`: wird entschlüsselt und erneut erkannt |

> [!warning] Warnung
> `.7z` wird weder gelesen noch geschrieben. Es wird nur erkannt, damit die Ablehnung es beim Namen nennt (`Unsupported`). Dann packt man das Level als zip neu, statt die Datei für kaputt zu halten

## Lesen

`LevelArchiveReader.ReadAsync` nimmt einen Ordner oder einen `Stream` mit Suchzugriff. Es gibt `LevelArchiveContent` zurück, wobei `LevelArchiveOpenResult` einer dieser Werte ist:

| Ergebnis | Bedeutung |
|---|---|
| `Ok` | gelesen |
| `PassphraseRequired` | es gibt kein Passwort, es muss abgefragt werden |
| `WrongPassphrase` | es wurde bereits ein Passwort eingegeben, und es ist falsch |
| `Damaged` | die Datei ist beschädigt |
| `NotAnArchive` | das ist kein Archiv |
| `Unsupported` | das Format ist erkannt, wird aber nicht unterstützt |

`PeekMetaAsync` liest nur die Metadaten, für eine Karte oder einen Katalog

Ein Server liest, was auch immer jemand hochladen wollte. Deshalb arbeitet der Leser innerhalb von `ArchiveLimits`. Standardmäßig sind das:
- 4096 Einträge
- 512 MiB pro Eintrag
- 1 GiB insgesamt

Nichts wird außerhalb des Speichers entpackt, der dafür übergeben wurde

Export aus Sicht des Editors - [[13_export-and-protection]]
