---
title: Do que um nível precisa
date: 2026-10-02
tags: [level_author]
---

# Do que um nível precisa

O mínimo é uma música. Todo o resto é opcional, e quase tudo fica por sua conta

## O que um nível pode usar

| O quê | Detalhes | Onde fica |
|---|---|---|
| Áudio | pelo menos uma faixa, pode haver várias | a pasta do nível |
| Imagens | quando uma forma não basta | a pasta do nível |
| Fontes | `ttf`, `otf`, `ttc` | a pasta do nível |
| Formas | 497 integradas e qualquer uma desenhada no `{{ui:hint_level_shape-editor_header}}` | integradas ao jogo ou ao nível |
| Temas, efeitos, prefabs | dados, não arquivos | dentro de `level.json` |

Áudio, imagens e fontes são arquivos de verdade.
Só eles aumentam o peso da pasta, precisam de um registro de origem antes da publicação e podem se perder em uma mudança de lugar

Sem fonte própria, o texto é desenhado com o que o sistema tiver

**O jogo não traz nenhuma textura.** As formas integradas são geometria, não imagens. Elas não têm pixels, não pesam nada e não há de onde carregá-las

> [!tip] Recomendação
> Recorra a uma forma antes de uma imagem, sempre. Uma imagem é um arquivo que pode se perder em uma mudança de lugar, memória no carregamento e uma linha no registro de licenças. Uma forma não custa nada disso

## O peso da pasta

Não há limite rígido. Mas um nível viaja por cópia, e quem o recebe vê o peso da pasta

Uma música de 4 minutos em `ogg` pesa 4-6 MB. A mesma música em `wav` fica em torno de 40 MB

## Várias origens para um recurso

Um recurso pode ter uma lista de lugares de onde buscá-lo: um arquivo ao lado do nível, um caminho absoluto, um link direto.
O jogo percorre a lista até algo carregar

> [!tip] Recomendação
> Use um link como complemento do arquivo, não no lugar dele. Um site pode sair do ar, mudar de endereço ou começar a servir outra coisa. Um arquivo na pasta fica onde o nível está

## Direitos sobre os arquivos

Se o nível sair do seu disco, cada arquivo nele precisa de uma licença que permita isso.
Isso se resolve pelos recursos que você escolhe logo no começo

Mais - [[2_editor/3_rights/index]]

A seguir: [[2_preparing-the-track]], [[3_images-and-fonts]]
