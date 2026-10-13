---
title: Como compartilhar um nível manualmente
date: 2026-10-01
tags: [level_author]
---

# Como compartilhar um nível manualmente

Compacte a pasta do nível em zip ou tar.gz e, para ter senha, criptografe com gpg. Em outra máquina, o nível descompactado já pode ser jogado, e o próprio jogo lê esses arquivos compactados

Um nível é uma pasta de arquivos. Um arquivo compactado é a mesma pasta, empacotada para envio.
Tudo o que o nível usa vai junto: a música, as imagens, a capa

Onde quem recebe coloca o nível - [[2_metadata-and-sharing#Compartilhar um nível hoje]]

## O que não entra no arquivo compactado

- um recurso que o nível pega de um link. O link continua como estava
- um arquivo ao qual nada no nível faz referência

O relatório de exportação do jogo lista os dois. Mais - [[13_export-and-protection#Exportar o nível]]

## Cinco tipos

Cada um abre com ferramentas que o outro lado já tem:

| Arquivo | O que tem dentro | Abre com |
|---|---|---|
| `level.json.gpg` | só o documento do nível, protegido por senha, dentro da pasta do nível | gpg |
| `LEVEL_FOLDER.tar.gz` | a pasta inteira como um único arquivo compactado | 7-Zip, Keka, Ark, Explorador de Arquivos |
| `LEVEL_FOLDER.tar.gz.gpg` | o mesmo arquivo compactado protegido por senha | gpg |
| `LEVEL_FOLDER.zip` | a mesma pasta como zip | Windows com um clique duplo, sem instalar nada |
| `LEVEL_FOLDER.zip.gpg` | o mesmo zip protegido por senha | gpg |

Por padrão, o jogo põe senha no arquivo compactado com os recursos do próprio zip, AES-256. Qualquer compactador, exceto o Explorador de Arquivos, abre esse arquivo compactado: ele pede a senha.
O jogo grava os tipos `.gpg` quando solicitado

## Antes de rodar as linhas

Troque dois pontos nas linhas:
- `LEVEL_FOLDER` - o nome da pasta do nível, ou seja, o id dele. É uma sequência longa de dígitos e letras, o nome da pasta dentro de `levels`
- `YOUR_PASSWORD` - a senha em si

Uma senha digitada na linha de comando fica no histórico do shell.
Tire `--batch --pinentry-mode loopback --passphrase YOUR_PASSWORD` da linha, e o gpg pede a senha na tela

## O documento do nível com gpg

A criptografia coloca `level.json.gpg` ao lado do original. O arquivo original continua onde está: exclua-o você mesmo depois de conferir o resultado.
A descriptografia grava o documento de novo com o nome dele. O arquivo criptografado continua onde está:

```bash
gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json.gpg > level.json
```

## Um arquivo compactado tar.gz

A pasta é compactada por dentro: o arquivo compactado contém os próprios arquivos do nível, sem uma pasta em volta.
Para descompactar, a pasta de destino já precisa existir, o tar não a cria. `mkdir` funciona igual no cmd, no PowerShell e em um terminal no Mac ou no Linux:

```bash
tar -czf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER .
mkdir LEVEL_FOLDER
tar -xzf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER
```

Compactação e criptografia em uma só passada. O arquivo compactado sem proteção nunca chega ao disco.
A segunda linha descriptografa e descompacta o arquivo compactado de volta na mesma pasta:

```bash
tar -czf - -C LEVEL_FOLDER . | gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD -o LEVEL_FOLDER.tar.gz.gpg
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD LEVEL_FOLDER.tar.gz.gpg | tar -xz -C LEVEL_FOLDER
```

## Um arquivo compactado zip

No Windows - no PowerShell, que toda máquina tem. O asterisco compacta o conteúdo da pasta, não a pasta em si.
`Expand-Archive` cria a pasta sozinho, sem precisar de `mkdir` antes:

```
Compress-Archive -Path LEVEL_FOLDER\* -DestinationPath LEVEL_FOLDER.zip
Expand-Archive -Path LEVEL_FOLDER.zip -DestinationPath LEVEL_FOLDER
```

No Mac ou no Linux - zip e unzip:

```bash
cd LEVEL_FOLDER && zip -r ../LEVEL_FOLDER.zip .
unzip LEVEL_FOLDER.zip -d LEVEL_FOLDER
```

Um zip com senha que o 7-Zip vai pedir é feito pelo próprio 7-Zip. Ele precisa estar instalado:

```
7z a -tzip -mem=AES256 -pYOUR_PASSWORD LEVEL_FOLDER.zip .\LEVEL_FOLDER\*
```

## O jogo os lê de volta

Todos os tipos funcionam nos dois sentidos. O que o jogo gravou, o gpg, o tar e o zip abrem. O que o gpg, o tar e o zip fizeram, o jogo lê.
Por isso foram escolhidas ferramentas padrão, e não um formato próprio

> [!tip] Dica
> O jogo olha o que um arquivo é, não como ele se chama. Por isso um arquivo compactado renomeado continua abrindo. O jogo reconhece `7z`, mas não o aceita: ele informa o formato em vez de declarar o arquivo corrompido. Compacte esse arquivo de novo como zip

> [!caution] Cuidado
> **UMA SENHA ESQUECIDA NÃO PODE SER RECUPERADA**. A chave não fica armazenada em lugar nenhum: nem no jogo, nem no arquivo, nem com ninguém. Não há redefinição, nem recuperação, nem jeito de contornar. Um nível com a senha perdida se perde junto com ela. Anote a senha antes de fechar o editor

A seguir: [[4_level-folder-and-backups|A pasta do nível e os backups]], [[4_not-losing-work|Não perder seu trabalho]]
