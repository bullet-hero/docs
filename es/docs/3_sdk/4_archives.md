---
title: Archivos comprimidos y protección
date: 2026-10-01
tags: [developer, level_author]
---

# Archivos comprimidos y protección

Un nivel se exporta como carpeta, tar.gz o zip, con contraseña opcional: zip con AES-256 u OpenPGP. El SDK detecta el formato de un archivo recibido por sus primeros bytes, no por su nombre

## Modos de exportación

Un nivel sale del dispositivo en una de las formas de `LevelExportMode`:

| Valor | Modo | Qué se escribe | Protección |
|---|---|---|---|
| 0 | `Folder` | una carpeta normal, con la misma forma que en el disco | ninguna |
| 1 | `FolderProtectedLevel` | una carpeta en la que solo está cifrado `level.json.gpg` | OpenPGP |
| 2 | `TarGz` | `<name>.tar.gz` | ninguna |
| 3 | `TarGzProtected` | `<name>.tar.gz.gpg` | OpenPGP |
| 4 | `Zip` | `<name>.zip` | ninguna |
| 5 | `ZipProtected` | `<name>.zip.gpg` | OpenPGP |
| 6 | `ZipEncrypted` | `<name>.zip` con entradas en AES-256 | la propia de zip |

El número es la identidad del modo y nunca cambia. El orden en la lista desplegable del editor se fija aparte (`DisplayOrder`)

**Todos los formatos son estándares abiertos.** `tar -xzf`, `gpg -d` y cualquier gestor de archivos comprimidos los abren sin el juego:

```bash
gpg -d level.tar.gz.gpg > level.tar.gz
tar -xzf level.tar.gz
```

## Dos esquemas de protección

**`ZipEncrypted` es la forma predeterminada de proteger un nivel con contraseña.** El destinatario tiene un gestor de archivos comprimidos, pero lo más probable es que no tenga gpg

**OpenPGP protege un documento, una carpeta y un archivo comprimido con un solo esquema.** Solo él puede proteger una carpeta

En `FolderProtectedLevel` los metadatos, la portada y los archivos multimedia siguen siendo legibles. Así el explorador de niveles sigue mostrando la tarjeta

La extensión interior se queda en el nombre: `level.json.gpg`. Es exactamente el nombre que `gpg -c level.json` da al archivo, así que el formato se conoce sin adivinar

## Qué va dentro

`LevelArchiveBuilder` calcula el contenido a partir del modelo, no de la lista de archivos de la carpeta. Un archivo al que el nivel no hace referencia se queda fuera. El informe dice cuántos archivos así se han quedado fuera

Las referencias del nivel se tratan así:
- un recurso con `AbsolutePath` se copia dentro del archivo comprimido. Su referencia se reescribe a `LevelPath`, pero solo en la copia exportada
- `DirectUrl` se queda tal cual y va al informe: una URL no puede viajar dentro de un archivo
- un archivo que falta va al informe con el código `archive.resource_missing`

## Detección por bytes

Cualquiera puede escribir un nombre de archivo. Por eso `ArchiveFormatSniffer` decide por los primeros 8 bytes:

| Primeros bytes | Formato |
|---|---|
| `1F 8B` | `TarGz` |
| `50 4B 03 04`, `50 4B 05 06`, `50 4B 07 08`, `50 4B 30 30` | `Zip` |
| `37 7A BC AF 27 1C` | `SevenZip` |
| una etiqueta de paquete OpenPGP, comprobada en último lugar | `OpenPgp`: se descifra y se detecta de nuevo |

> [!warning] Advertencia
> `.7z` no se lee ni se escribe. Solo se detecta para que el rechazo lo nombre (`Unsupported`). Así la persona vuelve a empaquetar el nivel como zip en lugar de pensar que el archivo está roto

## Lectura

`LevelArchiveReader.ReadAsync` acepta una carpeta o un `Stream` que permita moverse por él (seekable). Devuelve `LevelArchiveContent`, donde `LevelArchiveOpenResult` es uno de estos valores:

| Resultado | Significado |
|---|---|
| `Ok` | leído |
| `PassphraseRequired` | no hay contraseña, hay que pedirla |
| `WrongPassphrase` | la persona ya ha introducido una contraseña y es incorrecta |
| `Damaged` | el archivo está dañado |
| `NotAnArchive` | no es un archivo comprimido |
| `Unsupported` | el formato se reconoce, pero no es compatible |

`PeekMetaAsync` lee solo los metadatos, para una tarjeta o un catálogo

Un servidor lee lo que alguien haya decidido subir. Por eso el lector trabaja dentro de `ArchiveLimits`. De forma predeterminada son:
- 4096 entradas
- 512 MiB por entrada
- 1 GiB en total

No se descomprime nada fuera del almacenamiento que se le ha dado

La exportación desde el lado del editor - [[13_export-and-protection]]
