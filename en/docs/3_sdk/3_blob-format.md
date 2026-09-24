---
title: Blob format
date: 2026-09-24
tags: [developer]
---

# Blob format

The byte layout of a .blob file: the 24-byte header, the order it is checked in and the envelopes inside

`.blob` holds the same data as `.json`, only in binary. It is an equal level format, not a cache: a level may be saved as `.blob` alone

| Level `volcano`, 19 341 objects | Size |
|---|---|
| `level.json` | 15.7 MB |
| `level.blob` | 5.1 MB, reads in 203 ms |

What `.blob` does not promise is readability. It cannot be read by eye or diffed, so it is the default nowhere

The codec for every model is produced by the Roslyn generator

## The header

| Offset | Size | Field | Value |
|---|---|---|---|
| 0 | 4 | magic | `uint` `0x4C424842`, the bytes `42 48 42 4C` (`BHBL`) |
| 4 | 2 | codec generation | `ushort`, `BlobFormat.Generation` = 2 |
| 6 | 2 | flags | `ushort`, bit 0 `FlagHashed` = the hash is present. Every other bit is reserved and must be 0 |
| 8 | 8 | payload length | `long` |
| 16 | 8 | hash | `ulong`, xxHash64 of the payload, seeded with the codec generation |

The header is `BlobFormat.HeaderLength` = 24 bytes long, and the payload follows it

## The order of the checks

`BlobFormat.ReadHeader` checks the header in a fixed order. Nothing is allocated until the header passes:
1. the magic
2. the codec generation equals 2
3. no unknown flags are set
4. the declared length equals the real one
5. the hash matches, if `FlagHashed` is set

Each failure is a `BlobFormatException` with its own message. "This file is damaged" and "this file is from a newer build" ask different things of a player, so they are never merged into one error

The hash is not cryptographic on purpose. It catches corruption, and forgery is the job of the OpenPGP layer. More - [[4_archives]]

## Encoding

- little-endian, fixed-width numbers, no varints
- a string is an `int` byte count followed by UTF-8
- `null` is a length of `-1`. So an empty list and a missing one stay different after a round trip
- a polymorphic value starts with a one-byte tag, `0xFF` is reserved for `null`. The tag is the model's `GetModelType()`, the same discriminator JSON writes in `[tag, payload]`
- a count read from the file is checked by `BlobReader.ReadCount` before anything is allocated for it

## Envelopes and the two generations

Every root marked `[ModelGeneration]` writes its own envelope: the domain as a string, the model generation as an `int`, the length of its content, then the content. This is how a tool reads the generation of a file:

```csharp
var bytes = File.ReadAllBytes(path);
var reader = new BlobReader(bytes, BlobFormat.HeaderLength, bytes.Length - BlobFormat.HeaderLength);
var domain = reader.ReadString();
var generation = reader.ReadInt();
```

There are two different generations here:
- **the codec generation** in the header describes the byte layout. When it changes, every older `.blob` becomes unreadable whole: there is nothing to fall back to. It went from 1 to 2 when an envelope stopped carrying two `ushort` numbers and started carrying one `int`
- **the model generation** in each envelope describes the shape of one domain. An older one is migrated, a newer one is refused with `NewerGenerationException`. More - [[5_versioning]]

> [!info] Worth knowing
> Content that does not end exactly at its declared length is treated as damage, in either direction. Sometimes a root passes every header check and still fails to parse. Then it is skipped by its length and left at defaults. The skip is recorded in `SerializationReport`, never silently
