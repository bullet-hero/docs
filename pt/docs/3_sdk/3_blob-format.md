---
title: Formato Blob
date: 2026-10-01
tags: [developer]
---

# Formato Blob

Um arquivo .blob guarda os mesmos dados que o .json em forma binária: um cabeçalho de 24 bytes seguido dos dados. É um formato de nível de pleno direito, não um cache

Um nível pode ser salvo só em `.blob`

| Nível `volcano`, 19.341 objetos | Tamanho |
|---|---|
| `level.json` | 15,7 MB |
| `level.blob` | 5,1 MB, lido em 203 ms |

O `.blob` não promete legibilidade. Ele não pode ser lido a olho nem comparado com um diff, por isso não é o padrão em lugar nenhum

O codec de cada modelo é criado pelo gerador Roslyn

## Cabeçalho

| Deslocamento | Tamanho | Campo | Valor |
|---|---|---|---|
| 0 | 4 | magic | `uint` `0x4F424842`, bytes `42 48 42 4F` (`BHBO`) |
| 4 | 2 | geração do codec | `ushort`, `BlobFormat.Generation` = 1 |
| 6 | 2 | flags | `ushort`, bit 0 `FlagHashed` = há um hash. Os outros bits são reservados e devem ser 0 |
| 8 | 8 | comprimento dos dados | `long` |
| 16 | 8 | hash | `ulong`, xxHash64 dos dados com a geração do codec como semente |

O comprimento do cabeçalho `BlobFormat.HeaderLength` é de 24 bytes, e depois vêm os dados

## Ordem das verificações

`BlobFormat.ReadHeader` verifica o cabeçalho em uma ordem estrita. Nada é alocado até o cabeçalho passar:
1. magic
2. a geração do codec é igual a 1
3. não há flags desconhecidas
4. o comprimento declarado é igual ao real
5. o hash coincide, se `FlagHashed` estiver definida

Cada falha é uma `BlobFormatException` com a própria mensagem. "O arquivo está danificado" e "o arquivo é de uma build mais nova" pedem coisas diferentes ao jogador, por isso não são juntados em um só erro

O hash não é criptográfico de propósito. Ele detecta danos, e a camada OpenPGP protege contra adulteração. Mais - [[4_archives]]

## Codificação

- little-endian, números de largura fixa, sem varint
- uma string é uma contagem de bytes `int` seguida de UTF-8
- `null` é um comprimento de `-1`. Assim, uma lista vazia e uma lista ausente continuam diferentes depois de uma ida e volta
- um valor polimórfico começa com uma tag de um byte, `0xFF` é reservado para `null`. A tag é o `GetModelType()` do modelo, a mesma marca que o JSON grava em `[tag, data]`
- uma contagem lida de um arquivo é verificada em `BlobReader.ReadCount` antes de qualquer coisa ser alocada para ela

## Envelopes e duas gerações

Cada raiz com `[ModelGeneration]` grava o próprio envelope: o domínio como string, a geração do modelo como `int`, o comprimento do conteúdo e depois o próprio conteúdo. É assim que uma ferramenta lê a geração de um arquivo:

```csharp
var bytes = File.ReadAllBytes(path);
var reader = new BlobReader(bytes, BlobFormat.HeaderLength, bytes.Length - BlobFormat.HeaderLength);
var domain = reader.ReadString();
var generation = reader.ReadInt();
```

Aqui há duas gerações diferentes:
- **a geração do codec** no cabeçalho descreve a disposição dos bytes. Quando ela muda, todo `.blob` antigo se torna ilegível por inteiro: não há para onde recuar
- **a geração do modelo** em cada envelope descreve a forma de um domínio. Uma antiga é migrada, uma nova é recusada por meio de `NewerGenerationException`. Mais - [[5_versioning]]

Elas não podem ser unidas em um só número. A geração do modelo fica dentro do envelope, e só quem já conhece a disposição dos bytes consegue encontrar o envelope. Uma mudança de modelo nunca mexe na geração do codec

## Como estender o cabeçalho

O cabeçalho não tem bytes de reserva nem um campo com o próprio comprimento. Ele cresce de duas formas:
- **uma flag.** Há 15 bits livres. Um leitor antigo recusa um arquivo com uma flag desconhecida em vez de lê-lo errado
- **uma nova geração do codec.** Uma nova disposição pode mudar qualquer coisa, inclusive o comprimento do cabeçalho. Um leitor mais novo pode ler a geração antiga junto com a nova

Nada pode ser acrescentado depois dos dados. O comprimento declarado tem de coincidir com o real, por isso qualquer sobra no final é recusada. Novos dados de nível vão dentro dos dados, pela geração do modelo

> [!info] Vale saber
> Um conteúdo que não termina exatamente no comprimento declarado conta como dano nos dois sentidos. Às vezes uma raiz passa por todas as verificações do cabeçalho e mesmo assim não é interpretada. Então ela é pulada pelo comprimento e fica com os valores padrão. O salto é registrado em `SerializationReport`, nunca em silêncio
