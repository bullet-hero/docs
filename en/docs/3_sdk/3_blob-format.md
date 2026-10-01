---
title: Blob format
date: 2026-10-01
tags: [developer]
---

# Blob format

A .blob file holds the same data as .json in binary form: a 24-byte header followed by the data. It is an equal level format, not a cache

A level can be saved in `.blob` only

| Level `volcano`, 19,341 objects | Size |
|---|---|
| `level.json` | 15.7 MB |
| `level.blob` | 5.1 MB, read in 203 ms |

`.blob` makes no promise of readability. It cannot be read by eye or compared with a diff, so it is not the default anywhere

The codec for every model is created by the Roslyn generator

## Header

| Offset | Size | Field | Value |
|---|---|---|---|
| 0 | 4 | magic | `uint` `0x4F424842`, bytes `42 48 42 4F` (`BHBO`) |
| 4 | 2 | codec generation | `ushort`, `BlobFormat.Generation` = 1 |
| 6 | 2 | flags | `ushort`, bit 0 `FlagHashed` = a hash is present. The other bits are reserved and must be 0 |
| 8 | 8 | data length | `long` |
| 16 | 8 | hash | `ulong`, xxHash64 of the data with the codec generation as the seed |

The header length `BlobFormat.HeaderLength` is 24 bytes, followed by the data

## Order of checks

`BlobFormat.ReadHeader` checks the header in a strict order. Nothing is allocated until the header passes:
1. magic
2. the codec generation equals 1
3. no unknown flags
4. the declared length equals the real one
5. the hash matches, if `FlagHashed` is set

Every failure is a `BlobFormatException` with its own message. "The file is damaged" and "the file is from a newer build" ask different things of the player, so they are not merged into one error

The hash is deliberately not cryptographic. It catches damage, and the OpenPGP layer protects against tampering. More - [[4_archives]]

## Encoding

- little-endian, fixed-width numbers, no varint
- a string is a byte count `int` followed by UTF-8
- `null` is a length of `-1`. So an empty list and a missing list stay different after a round trip
- a polymorphic value starts with a one-byte tag, `0xFF` is reserved for `null`. The tag is the model's `GetModelType()`, the same marker that JSON writes in `[tag, data]`
- a count read from a file is checked in `BlobReader.ReadCount` before anything is allocated for it

## Envelopes and two generations

Every root with `[ModelGeneration]` writes its own envelope: the domain as a string, the model generation as an `int`, the length of the content, then the content itself. This is how a tool reads the generation of a file:

```csharp
var bytes = File.ReadAllBytes(path);
var reader = new BlobReader(bytes, BlobFormat.HeaderLength, bytes.Length - BlobFormat.HeaderLength);
var domain = reader.ReadString();
var generation = reader.ReadInt();
```

There are two different generations here:
- **the codec generation** in the header describes the byte layout. When it changes, every old `.blob` becomes unreadable as a whole: there is nothing to fall back to
- **the model generation** in each envelope describes the shape of one domain. An old one migrates, a new one is refused through `NewerGenerationException`. More - [[5_versioning]]

They cannot be merged into one number. The model generation lies inside the envelope, and only someone who already knows the byte layout can find the envelope. A model change never moves the codec generation

## Extending the header

The header has no spare bytes and no field with its own length. It grows in two ways:
- **a flag.** 15 bits are free. An old reader refuses a file with an unfamiliar flag rather than reading it wrong
- **a new codec generation.** A new layout can change anything, including the header length. A newer reader can read the old generation alongside the new one

Nothing can be appended after the data. The declared length must match the real one, so any extra tail is refused. New level data goes inside the data, through the model generation

> [!info] Worth knowing
> Content that does not end exactly at its declared length counts as damage in both directions. Sometimes a root passes every header check and still does not parse. Then it is skipped by its length and keeps its default values. The skip is recorded in `SerializationReport`, never silently
