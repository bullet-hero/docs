---
title: Arquivos compactados e proteção
date: 2026-10-01
tags: [developer, level_author]
---

# Arquivos compactados e proteção

Um nível é exportado como pasta, tar.gz ou zip, opcionalmente com senha: zip com AES-256 ou OpenPGP. O SDK detecta o formato de um arquivo recebido pelos primeiros bytes, não pelo nome

## Modos de exportação

Um nível sai do dispositivo em uma das formas de `LevelExportMode`:

| Valor | Modo | O que é gravado | Proteção |
|---|---|---|---|
| 0 | `Folder` | uma pasta comum, com a mesma forma que no disco | nenhuma |
| 1 | `FolderProtectedLevel` | uma pasta em que só `level.json.gpg` é criptografado | OpenPGP |
| 2 | `TarGz` | `<name>.tar.gz` | nenhuma |
| 3 | `TarGzProtected` | `<name>.tar.gz.gpg` | OpenPGP |
| 4 | `Zip` | `<name>.zip` | nenhuma |
| 5 | `ZipProtected` | `<name>.zip.gpg` | OpenPGP |
| 6 | `ZipEncrypted` | `<name>.zip` com entradas em AES-256 | a do próprio zip |

O número é a identidade do modo e nunca muda. A ordem na lista suspensa do editor é definida à parte (`DisplayOrder`)

**Todo formato é um padrão aberto.** `tar -xzf`, `gpg -d` e qualquer compactador os abrem sem o jogo:

```bash
gpg -d level.tar.gz.gpg > level.tar.gz
tar -xzf level.tar.gz
```

## Dois esquemas de proteção

**`ZipEncrypted` é o jeito padrão de trancar um nível com senha.** Quem recebe tem um compactador, mas muito provavelmente não tem o gpg

**O OpenPGP tranca um documento, uma pasta e um arquivo compactado com um só esquema.** Só ele consegue proteger uma pasta

Em `FolderProtectedLevel` os metadados, a capa e a mídia continuam legíveis. Por isso o navegador de níveis ainda mostra o cartão

A extensão interna fica no nome: `level.json.gpg`. É exatamente o nome que `gpg -c level.json` dá ao arquivo, então o formato é conhecido sem adivinhação

## O que vai dentro

`LevelArchiveBuilder` calcula o conteúdo a partir do modelo, não da lista de arquivos da pasta. Um arquivo que o nível não referencia fica de fora. O relatório diz quantos arquivos assim ficaram

As referências do nível são tratadas assim:
- um recurso com `AbsolutePath` é copiado para o arquivo compactado. A referência dele é reescrita para `LevelPath`, mas só na cópia exportada
- `DirectUrl` fica como está e vai para o relatório: uma URL não pode viajar dentro de um arquivo
- um arquivo ausente vai para o relatório com o código `archive.resource_missing`

## Detecção pelos bytes

Qualquer um pode escrever um nome de arquivo. Por isso `ArchiveFormatSniffer` decide pelos primeiros 8 bytes:

| Primeiros bytes | Formato |
|---|---|
| `1F 8B` | `TarGz` |
| `50 4B 03 04`, `50 4B 05 06`, `50 4B 07 08`, `50 4B 30 30` | `Zip` |
| `37 7A BC AF 27 1C` | `SevenZip` |
| uma tag de pacote OpenPGP, verificada por último | `OpenPgp`: descriptografado e detectado de novo |

> [!warning] Aviso
> `.7z` não é lido nem gravado. Ele só é detectado para que a recusa diga o nome dele (`Unsupported`). Então a pessoa recompacta o nível como zip em vez de concluir que o arquivo está quebrado

## Leitura

`LevelArchiveReader.ReadAsync` recebe uma pasta ou um `Stream` com suporte a seek. Ele devolve `LevelArchiveContent`, em que `LevelArchiveOpenResult` é um destes valores:

| Resultado | Significado |
|---|---|
| `Ok` | lido |
| `PassphraseRequired` | não há senha, é preciso pedi-la |
| `WrongPassphrase` | a pessoa já digitou uma senha, e ela está errada |
| `Damaged` | o arquivo está danificado |
| `NotAnArchive` | isto não é um arquivo compactado |
| `Unsupported` | o formato é reconhecido, mas não é suportado |

`PeekMetaAsync` lê só os metadados, para um cartão ou um catálogo

Um servidor lê o que quer que alguém tenha decidido enviar. Por isso o leitor trabalha dentro de `ArchiveLimits`. Por padrão, os limites são:
- 4096 entradas
- 512 MiB por entrada
- 1 GiB no total

Nada é descompactado fora do armazenamento que foi dado ao leitor

A exportação pelo lado do editor - [[13_export-and-protection]]
