---
title: Formato Blob
date: 2026-10-01
tags: [developer]
---

# Formato Blob

Un archivo .blob guarda los mismos datos que .json en forma binaria: una cabecera de 24 bytes seguida de los datos. Es un formato de nivel de pleno derecho, no una caché

Un nivel puede guardarse solo en `.blob`

| Nivel `volcano`, 19 341 objetos | Tamaño |
|---|---|
| `level.json` | 15,7 MB |
| `level.blob` | 5,1 MB, se lee en 203 ms |

`.blob` no promete legibilidad. No se puede leer a simple vista ni comparar con un diff, así que no es el formato predeterminado en ningún sitio

El códec de cada modelo lo crea el generador de Roslyn

## Cabecera

| Desplazamiento | Tamaño | Campo | Valor |
|---|---|---|---|
| 0 | 4 | magic | `uint` `0x4F424842`, bytes `42 48 42 4F` (`BHBO`) |
| 4 | 2 | generación del códec | `ushort`, `BlobFormat.Generation` = 1 |
| 6 | 2 | indicadores | `ushort`, bit 0 `FlagHashed` = hay un hash. Los demás bits están reservados y deben ser 0 |
| 8 | 8 | longitud de los datos | `long` |
| 16 | 8 | hash | `ulong`, xxHash64 de los datos con la generación del códec como semilla |

La longitud de la cabecera `BlobFormat.HeaderLength` es de 24 bytes, y a continuación van los datos

## Orden de las comprobaciones

`BlobFormat.ReadHeader` comprueba la cabecera en un orden estricto. No se reserva memoria hasta que la cabecera pasa:
1. magic
2. la generación del códec es igual a 1
3. no hay indicadores desconocidos
4. la longitud declarada es igual a la real
5. el hash coincide, si `FlagHashed` está activado

Cada fallo es una `BlobFormatException` con su propio mensaje. "El archivo está dañado" y "el archivo es de una compilación más reciente" piden cosas distintas al jugador, así que no se juntan en un solo error

El hash no es criptográfico a propósito. Detecta daños, y la capa OpenPGP protege contra la manipulación. Más - [[4_archives]]

## Codificación

- little-endian, números de ancho fijo, sin varint
- una cadena es una cantidad de bytes `int` seguida de UTF-8
- `null` es una longitud de `-1`. Así una lista vacía y una lista ausente siguen siendo distintas después de guardarlas y volver a leerlas
- un valor polimórfico empieza con una etiqueta de un byte, `0xFF` está reservado para `null`. La etiqueta es el `GetModelType()` del modelo, la misma marca que JSON escribe en `[tag, data]`
- una cantidad leída de un archivo se comprueba en `BlobReader.ReadCount` antes de reservar nada para ella

## Sobres y dos generaciones

Cada raíz con `[ModelGeneration]` escribe su propio sobre: el dominio como cadena, la generación del modelo como `int`, la longitud del contenido y luego el propio contenido. Así lee una herramienta la generación de un archivo:

```csharp
var bytes = File.ReadAllBytes(path);
var reader = new BlobReader(bytes, BlobFormat.HeaderLength, bytes.Length - BlobFormat.HeaderLength);
var domain = reader.ReadString();
var generation = reader.ReadInt();
```

Aquí hay dos generaciones distintas:
- **la generación del códec** en la cabecera describe la disposición de los bytes. Cuando cambia, todos los `.blob` antiguos se vuelven ilegibles por completo: no hay nada a lo que volver
- **la generación del modelo** en cada sobre describe la forma de un dominio. Una antigua se migra, una nueva se rechaza mediante `NewerGenerationException`. Más - [[5_versioning]]

No se pueden unir en un solo número. La generación del modelo está dentro del sobre, y solo quien ya conoce la disposición de los bytes puede encontrar el sobre. Un cambio del modelo nunca mueve la generación del códec

## Ampliar la cabecera

La cabecera no tiene bytes de reserva ni un campo con su propia longitud. Crece de dos maneras:
- **un indicador.** Quedan 15 bits libres. Un lector antiguo rechaza un archivo con un indicador desconocido en lugar de leerlo mal
- **una nueva generación del códec.** Una nueva disposición puede cambiar cualquier cosa, incluida la longitud de la cabecera. Un lector más reciente puede leer la generación antigua junto a la nueva

No se puede añadir nada después de los datos. La longitud declarada debe coincidir con la real, así que cualquier cola sobrante se rechaza. Los nuevos datos del nivel van dentro de los datos, a través de la generación del modelo

> [!info] Conviene saber
> El contenido que no termina exactamente en su longitud declarada cuenta como daño en ambas direcciones. A veces una raíz pasa todas las comprobaciones de la cabecera y aun así no se puede analizar. Entonces se salta según su longitud y conserva sus valores predeterminados. El salto queda registrado en `SerializationReport`, nunca en silencio
