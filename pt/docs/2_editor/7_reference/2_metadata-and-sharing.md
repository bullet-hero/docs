---
title: Metadados e compartilhamento de um nível
date: 2026-10-15
tags: [level_author]
---

# Metadados e compartilhamento de um nível

Os metadados são a vitrine do nível: nome, descrição, imagem, autores, classificação etária, dificuldade e avisos sobre o conteúdo. Hoje um nível chega a outra pessoa como pasta ou pela Oficina Steam

> [!warning] Aviso
> O servidor oficial e o site de níveis ainda não existem. Eles chegam em uma atualização depois do `gv 1.0.0`. Até lá, um nível é compartilhado como pasta ou, em uma build da Steam, pela Oficina Steam. As duas formas são descritas no fim da página

## O arquivo de metadados

A vitrine do nível fica em um arquivo próprio. Ele é lido sem o nível em si.
Assim um catálogo pode mostrar mil níveis sem abrir nenhum deles

## Identidade

O nível tem um ID estável. Ele sobrevive a mudanças de nome e a mudanças de pasta.
As pontuações e os comentários ficam ligados a ele, não ao nome

Há também um número de versão próprio do nível. Aumente-o quando editar. Ele não tem relação com a versão do formato

## Nome, descrição e capa

**O nome e a descrição** podem ser traduzidos para vários idiomas. Eles não têm chaves: você escreve o texto de cada idioma ali mesmo.
O texto é salvo dentro do nível. É isso que o diferencia do texto da própria interface do jogo

**A capa** é um arquivo ao lado do nível, `logo.png` ou `logo.jpg`

A capa tem um registro próprio, como um recurso: licença, autores, link, geração por IA. Ele é aberto com o botão `{{ui:settings_level-settings_metadata-level-logo-metadata}}` embaixo da capa.
Uma imagem nova começa o registro do zero, e remover a capa remove também o registro dela. Mais - [[4_resource-record]]

## Autores

**Os autores** são as pessoas que fizeram o nível: o mapeamento, o design.
Os autores dos recursos recebem crédito à parte, no registro próprio de cada recurso.
Texturas, fontes e áudio têm registros, e também temas, efeitos, formas e prefabs

> [!caution] Cuidado
> Se você confundir essas duas listas, o músico fica sem crédito

## Classificação etária

**A classificação etária** é um único número, a idade mínima. Ela aparece como "12+". Duas classificações são comparadas como números comuns

`{{ui:enum_age-rating_unrated}}` é zero. Significa que nada foi declarado, não que o conteúdo é seguro

> [!info] Vale saber
> Há uma única escala, sem campos separados para ESRB, PEGI e RARS. Os níveis de usuários não são enviados a nenhum órgão de classificação, então um valor para cada um seria um palpite

> [!caution] Cuidado
> A classificação é o único aviso do cartão. Se o nível pisca ou fica alto, diga isso na descrição. Em um jogo de drops e efeitos de glitch, piscadas são comuns, e essa linha é todo o aviso que o jogador recebe

## Dificuldade

**A dificuldade** é um único número inteiro: o quanto o nível é difícil. Um número maior nunca é mais fácil

`1` é `{{ui:enum_difficulty-tier_auto}}`, e cada número seguinte é o grau seguinte, até `{{v:difficulty.scale-max}}`, `{{ui:enum_difficulty-tier_singularity}}`. O jogador vê só o nome do grau e o ícone dele, nunca o número

`{{ui:enum_difficulty-tier_undefined}}` é zero ou menos. É o valor padrão, e nada é desenhado para ele. Um arquivo de metadados sem dificuldade abre como `{{ui:enum_difficulty-tier_undefined}}`

Quem define o valor é você, e um moderador que republica o nível pode sobrescrevê-lo. Continua sendo um só campo: o nível não guarda o valor do autor e o do moderador lado a lado

Um valor acima de `{{v:difficulty.scale-max}}` é mantido como foi escrito e aparece como `{{ui:enum_difficulty-tier_singularity}}`. O editor só o reescreve quando você escolhe outro grau. Por enquanto a escala termina aí. A próxima será construída a partir dos níveis que as pessoas realmente fazem

No arquivo de metadados o campo se chama `difficulty`

Mais - [[2_playing-levels#Dificuldade]]

## Geração por IA

**`Geração por IA`** diz se o conteúdo próprio do nível foi gerado por IA: o design, os objetos, os textos.
Cada recurso e a capa dizem isso por si mesmos, nos próprios registros

| Valor | Significado |
|---|---|
| `{{ui:enum_ai-generation_not-specified}}` | nada foi declarado. É o valor padrão |
| `{{ui:enum_ai-generation_no}}` | você declara que nenhuma geração por IA foi usada |
| `Gerado por IA` | você declara que o conteúdo foi gerado por IA |

`{{ui:enum_ai-generation_not-specified}}` significa "desconhecido". Não é o mesmo que "não"

A tela do nível no menu mostra "Contém conteúdo gerado por IA" se o nível, a capa dele ou qualquer recurso diz `Gerado por IA`

Um assistente de IA define `{{ui:enum_ai-generation_yes}}` sozinho, no mesmo passo de desfazer do primeiro lote de edições dele no nível. Mais - [[7_ai-assistant]]

> [!info] Vale saber
> Assim como a classificação etária, esta é uma declaração do próprio autor. O jogo não a verifica

## Compartilhar um nível hoje

1. Compacte a pasta do nível em um zip e envie
2. A outra pessoa descompacta o zip na própria pasta `levels`
3. O nível abre. Nada é instalado nem importado

> [!warning] Aviso
> Todo arquivo da pasta do nível vai junto com ela, mesmo um que não é usado. Limpe a pasta antes de enviar

## Oficina Steam

A aba `{{ui:settings_level-settings_publication}}` das configurações do nível envia o nível para fora: como arquivo compactado e, em uma build da Steam, para a Oficina Steam. Mais - [[17_publishing]]

As builds da Steam também leem a Oficina: elas mostram os níveis que você assinou e permitem jogá-los. Mais - [[2_playing-levels]]

Antes de publicar, leia [[1_licensing-basics|a seção sobre direitos]]. O relatório da aba `{{ui:settings_level-settings_publication}}` avalia o nível e o registro de cada recurso por essas regras

## Compartilhar um nível depois

Há planos para um servidor e um site oficiais

A seguir: [[4_resource-record|O registro do recurso]], [[4_level-folder-and-backups|A pasta do nível e os backups]]
