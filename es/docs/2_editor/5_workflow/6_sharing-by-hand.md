---
title: Cómo compartir un nivel a mano
date: 2026-10-01
tags: [level_author]
---

# Cómo compartir un nivel a mano

Empaqueta la carpeta del nivel en zip o tar.gz y, si quieres contraseña, cífrala con gpg. En otro equipo, el nivel desempaquetado se juega al instante, y el juego lee esos archivos comprimidos por sí mismo

Un nivel es una carpeta de archivos. Un archivo comprimido es la misma carpeta, empaquetada para enviarla.
Todo lo que usa el nivel viaja con él: la canción, las imágenes, la portada

Dónde coloca el nivel quien lo recibe - [[2_metadata-and-sharing#Cómo compartir un nivel hoy]]

## Qué no entra en el archivo comprimido

- un recurso que el nivel toma de un enlace. El enlace queda como estaba
- un archivo al que nada del nivel hace referencia

El informe de exportación del juego enumera ambos. Más - [[13_export-and-protection#Exportar el nivel]]

## Cinco tipos

Cada uno se abre con herramientas que la otra parte ya tiene:

| Archivo | Qué contiene | Se abre con |
|---|---|---|
| `level.json.gpg` | solo el documento del nivel, con contraseña, dentro de la carpeta del nivel | gpg |
| `LEVEL_FOLDER.tar.gz` | toda la carpeta como un solo archivo comprimido | 7-Zip, Keka, Ark, el Explorador de archivos |
| `LEVEL_FOLDER.tar.gz.gpg` | el mismo archivo comprimido con contraseña | gpg |
| `LEVEL_FOLDER.zip` | la misma carpeta como zip | Windows con doble clic, sin instalar nada |
| `LEVEL_FOLDER.zip.gpg` | el mismo zip con contraseña | gpg |

Por defecto, el juego pone la contraseña al archivo comprimido con los medios propios de zip, AES-256. Cualquier compresor excepto el Explorador de archivos abre un archivo así: pide la contraseña.
El juego escribe los tipos `.gpg` si se le pide

## Antes de ejecutar los comandos

Sustituye dos partes en los comandos:
- `LEVEL_FOLDER` - el nombre de la carpeta del nivel, es decir, su id. Es una cadena larga de dígitos y letras, el nombre de la carpeta dentro de `levels`
- `YOUR_PASSWORD` - la contraseña en sí

Una contraseña escrita en la línea de comandos queda en el historial de la shell.
Quita `--batch --pinentry-mode loopback --passphrase YOUR_PASSWORD` del comando, y gpg pedirá la contraseña en pantalla

## El documento del nivel con gpg

El cifrado coloca `level.json.gpg` junto al original. El archivo original se queda donde está: elimínalo tú cuando hayas comprobado el resultado.
El descifrado vuelve a escribir el documento con su propio nombre. El archivo cifrado se queda donde está:

```bash
gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json.gpg > level.json
```

## Un archivo comprimido tar.gz

La carpeta se empaqueta desde dentro: el archivo comprimido contiene los propios archivos del nivel, sin una carpeta alrededor.
Para desempaquetar, la carpeta de destino ya tiene que existir, tar no la crea. `mkdir` funciona igual en cmd, en PowerShell y en una terminal de Mac o Linux:

```bash
tar -czf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER .
mkdir LEVEL_FOLDER
tar -xzf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER
```

Empaquetado y cifrado en una sola pasada. El archivo comprimido sin proteger nunca llega al disco.
La segunda línea descifra y desempaqueta el archivo comprimido de vuelta en la misma carpeta:

```bash
tar -czf - -C LEVEL_FOLDER . | gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD -o LEVEL_FOLDER.tar.gz.gpg
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD LEVEL_FOLDER.tar.gz.gpg | tar -xz -C LEVEL_FOLDER
```

## Un archivo comprimido zip

En Windows - en PowerShell, que está en cualquier equipo. El asterisco empaqueta el contenido de la carpeta, no la carpeta en sí.
`Expand-Archive` crea la carpeta por sí mismo, no hace falta `mkdir` antes:

```
Compress-Archive -Path LEVEL_FOLDER\* -DestinationPath LEVEL_FOLDER.zip
Expand-Archive -Path LEVEL_FOLDER.zip -DestinationPath LEVEL_FOLDER
```

En Mac o Linux - zip y unzip:

```bash
cd LEVEL_FOLDER && zip -r ../LEVEL_FOLDER.zip .
unzip LEVEL_FOLDER.zip -d LEVEL_FOLDER
```

Un zip con una contraseña que pida 7-Zip lo crea el propio 7-Zip. Tiene que estar instalado:

```
7z a -tzip -mem=AES256 -pYOUR_PASSWORD LEVEL_FOLDER.zip .\LEVEL_FOLDER\*
```

## El juego los vuelve a leer

Todos los tipos funcionan en ambos sentidos. Lo que escribió el juego lo abren gpg, tar y zip. Lo que hicieron gpg, tar y zip lo lee el juego.
Por eso se eligieron herramientas estándar y no un formato propio

> [!tip] Consejo
> El juego mira qué es un archivo, no cómo se llama. Por eso un archivo comprimido renombrado se sigue abriendo. El juego reconoce `7z` pero no lo acepta: nombra el formato en lugar de declarar el archivo dañado. Vuelve a empaquetar ese archivo comprimido como zip

> [!caution] Precaución
> **UNA CONTRASEÑA OLVIDADA NO SE PUEDE RECUPERAR**. La clave no se guarda en ninguna parte: ni en el juego, ni en el archivo, ni en manos de nadie. No hay restablecimiento, ni recuperación, ni forma de esquivarlo. Un nivel con la contraseña perdida se pierde con ella. Apunta la contraseña antes de cerrar el editor

A continuación: [[4_level-folder-and-backups|La carpeta del nivel y las copias de seguridad]], [[4_not-losing-work|No perder tu trabajo]]
