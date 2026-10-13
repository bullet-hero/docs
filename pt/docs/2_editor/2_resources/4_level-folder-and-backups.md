---
title: A pasta do nível e os backups
date: 2026-10-11
tags: [level_author]
---

# A pasta do nível e os backups

Um nível vive na própria pasta, dentro de levels na pasta do jogo. Não renomeie os arquivos que ele usa, e um backup completo é uma cópia da pasta do nível

## O que há na pasta

A pasta do nível fica em `levels`, dentro da pasta do jogo. Onde fica a pasta do jogo - [[1_installation]]

| Arquivo | O que é |
|---|---|
| `level.json` | o conteúdo do nível. No formato binário - `level.blob` |
| `metadata.json` | nome, descrição, autores, tags. No formato binário - `metadata.blob` |
| `logo.png` ou `logo.jpg` | a capa |
| a música, as imagens, as fontes | todo o resto que o nível usa, logo ao lado de `level.json` |

Ao lado de `levels` fica `resources`, com as bibliotecas de todo o dispositivo: `themes`, `effects`, `shapes`, `prefabs`.
Elas não fazem parte do nível. Você exporta para lá o que quer reutilizar, e importa de lá

A mesma pasta `resources` contém `collections`, uma pasta por coleção. Mais - [[16_library-and-collections]]

Um nível enviado a outra pessoa leva dentro de si tudo o que precisa. As bibliotecas não viajam com ele

## O que não alterar à mão

> [!caution] Cuidado
> Não renomeie os arquivos que o nível usa. As referências a eles são armazenadas pelo nome, por isso um arquivo renomeado é um arquivo que falta

Não edite `level.json` em um editor de texto enquanto o nível estiver aberto no jogo. Salvar pelo editor sobrescreve suas edições sem nenhum aviso

Não mantenha na pasta do nível nada que o nível não use. Tudo isso viaja junto com a pasta

O formato do arquivo é decidido pela extensão, não por um campo interno. Por isso mudar o formato no editor grava um arquivo novo e exclui o antigo.
Caso contrário, haveria dois arquivos no disco, e não daria para saber qual é o verdadeiro

## Quando falta um dos dois arquivos

Uma pasta que tem só um entre `level.json` e `metadata.json` continua aparecendo na lista de níveis. Os binários `level.blob` e `metadata.blob` contam do mesmo jeito

| Falta | No jogo | No editor |
|---|---|---|
| `level.json` | o card está completo, mas o nível não pode ser iniciado | é restaurado a partir da cópia de salvamento automático mais recente. Sem cópias, um nível vazio é gravado |
| `metadata.json` | o card mostra o nome da pasta, e o nível pode ser jogado | um novo `metadata.json` é gravado com o nome da pasta e as configurações padrão |

Um `metadata.json` que o jogo não consegue ler conta como ausente. O editor o move para `metadata.json.bak` antes de gravar o novo, por isso nada se perde

O editor pergunta antes de gravar qualquer coisa. Um nível integrado ou da `Oficina` nunca é alterado no lugar: um sem `metadata.json` é oferecido como cópia, e um sem `level.json` não pode ser aberto

## Backups e recuperação

**Um backup completo é uma cópia da pasta do nível.** Ele contém tudo, recursos incluídos.
Faça uma cópia antes de cada grande reformulação e coloque a data nela

**O salvamento automático mantém só o arquivo do nível.** Sem metadados, música ou imagens.
Cada salvamento automático coloca uma cópia em `backups/<level id>/` na pasta do jogo, fora de `levels`. São mantidas `25` cópias. Como restaurar uma cópia - [[4_not-losing-work#Salvamento automático]]

**Um nível em `Json` que parou de abrir não está perdido.** O arquivo é texto, por isso dá para abri-lo em qualquer editor de texto e corrigi-lo a olho. O próprio jogo não abre um nível que falha ao carregar, por isso a aba `{{ui:settings_level-settings_raw}}` não ajuda aqui. Ela mostra o modelo de um nível que já está aberto

Um `Blob` não pode ser recuperado desse jeito. Ele é binário, e um arquivo danificado é recusado inteiro em vez de ser lido em parte

O que saber antes de editar na aba `{{ui:settings_level-settings_raw}}` - [[4_not-losing-work#A aba de dados brutos]]

A seguir: [[4_not-losing-work]], [[2_metadata-and-sharing]]
