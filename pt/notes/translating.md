---
title: Traduzir
date: 2026-10-13
tags: [contributor]
---

# Traduzir

Uma tradução é uma cópia do arquivo em inglês no mesmo caminho, dentro da pasta do seu idioma, em que só o texto é traduzido. Um fato que aparece em qualquer idioma é levado para todos os outros

## Caminhos espelhados

Cada página fica no mesmo caminho, com o mesmo nome de arquivo, em cada pasta de idioma:

```
en/docs/2_editor/4_craft/3_difficulty-curve.md
ru/docs/2_editor/4_craft/3_difficulty-curve.md
zh/docs/2_editor/4_craft/3_difficulty-curve.md
ja/docs/2_editor/4_craft/3_difficulty-curve.md
ko/docs/2_editor/4_craft/3_difficulty-curve.md
es/docs/2_editor/4_craft/3_difficulty-curve.md
```

O que não muda:

- o nome do arquivo e o nome de cada pasta, prefixos incluídos
- `date` e `tags` no frontmatter (`title` é traduzido)
- os `[[wiki-links]]`: os destinos deles são nomes de arquivo, idênticos em todos os idiomas
- os links externos, os nomes de imagens, os blocos de código e o código inline: arquivos, campos, chaves, valores, comandos
- a estrutura: os mesmos títulos na mesma ordem, as mesmas listas, tabelas e destaques

Os títulos dos destaques são traduzidos para o idioma da página. Mais - [[style-guide]]

## O inglês é a alternativa

Quando uma página falta em um idioma, o site mostra a página em inglês com um aviso. O contrário não funciona: uma página que existe só em `ru/` dá um 404 para quem lê em inglês

> [!caution] Cuidado
> Nunca adicione uma página em outro idioma antes que ela apareça em `en/`. Os leitores de todos os outros idiomas vão receber um link quebrado

## Cada idioma carrega cada fato

O inglês manda só nos endereços, não no conteúdo. Um fato pode aparecer primeiro em qualquer idioma e depois é levado para todos os outros. Depois de uma mudança, cada versão contém tudo o que todas as versões sabem

- **Adicionar, nunca remover.** A informação que falta é escrita em cada idioma que não a tem
- **Contradições não se resolvem no chute.** Duas versões dão números diferentes ou afirmações opostas? Confira a fonte (o jogo, o SDK) e levante a questão no pull request
- **Nada é excluído sem perguntar,** nem mesmo um texto que parece desatualizado

Uma diferença de redação não é um problema. Uma diferença no que o leitor aprende é um problema

## Comparar versões

O repositório tem uma skill para o Claude Code, `compare-translations` (em `.claude/skills/`). Ela faz essa comparação. Sem ela, faça as mesmas duas passadas à mão

**A passada estrutural** compara as versões elemento por elemento: o frontmatter, o H1, o primeiro parágrafo, os títulos, o número de parágrafos, itens de lista, linhas de tabela e destaques, os destinos dos links, as imagens, o código

**A passada de significado** lê cada seção lado a lado e procura fatos que uma versão tem e outra não: números e unidades, nomes de campos, botões e teclas, condições e exceções, avisos, os passos de um procedimento e a ordem deles, exemplos

## O chinês tradicional é gerado

`zh-Hant/` não é traduzido à mão. Um script o converte a partir de `zh/`: OpenCC, caracteres tradicionais com o vocabulário de Taiwan. Uma correção em uma página em chinês tradicional vai para a página de `zh/`, e a próxima conversão a leva junto. Uma edição feita diretamente em `zh-Hant/` é sobrescrita

## Idioma novo

Um idioma novo é adicionado inteiramente neste repositório, o código do site não muda:

1. Copie `frontend/en.yaml` para `frontend/<code>.yaml`, por exemplo `frontend/de.yaml`, e traduza os valores. Esses são os textos próprios do site: o menu, os botões, a pesquisa, o aviso de cookies. Mantenha as chaves e cada `{name}` como estão
2. Crie a pasta `<code>/` ao lado de `en/`, `ru/`, `zh/`, `zh-Hant/`, `ja/`, `ko/` e `es/` e traduza as páginas dentro dela. Uma página sem tradução é mostrada em inglês com um aviso

Uma chave com as formas `one` / `few` / `many` / `other` depende de uma quantidade. Dê a ela todas as formas de que o seu idioma precisa, a build aponta as que faltam. Uma chave não traduzida é mostrada em inglês. A build lista essas chaves como avisos

Antes de uma tradução grande, abra uma issue em [bullet-hero/docs](https://github.com/bullet-hero/docs), para que duas pessoas não traduzam a mesma coisa
