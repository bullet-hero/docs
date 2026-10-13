---
title: O registro do recurso
date: 2026-10-02
tags: [level_author]
---

# O registro do recurso

O registro anota de onde vem um recurso e em que termos: o link, a licença, as permissões, os autores. Um campo de licença vazio significa "ninguém verificou", e esse recurso é recusado

> [!tip] Recomendação
> Preencha o registro assim que adicionar o recurso. É o único momento em que você ainda lembra de onde ele veio

## O que o registro contém

Cada recurso seu em um nível tem o próprio registro. Ele é armazenado dentro do nível e viaja com ele. Assim a atribuição não se perde: aonde quer que o nível vá, o arquivo leva consigo de onde veio e em que termos

Os campos do registro:
- **Título** e **descrição** da obra original, os dois podem ser traduzidos para outros idiomas
- **Url** - a página da obra: a publicação ou a página do autor, uma página de loja
- **Licença** - os termos em que a obra é distribuída
- **Permissões** - [[2_legal-resource-paths|opção B]], uma entrada por titular de direitos, com alcance, datas e prova
- **Autores** - todos que precisam receber crédito por este recurso, separados dos autores do próprio nível
- **Origens** - texto livre sobre a procedência, para o que um link não consegue expressar
- **Hashes** - os hashes do conteúdo dos arquivos do recurso
- **Geração por IA** - se a obra foi gerada por IA: `{{ui:enum_ai-generation_not-specified}}`, `{{ui:enum_ai-generation_no}}` ou `{{ui:enum_ai-generation_yes}}`

**O link aponta para a página com os termos, não para um download direto.** Um moderador precisa da página, não do arquivo

## Um campo vazio significa "desconhecido"

> [!caution] Cuidado
> Um campo de licença vazio é `NoSpecifiedLicense`, e esse recurso é recusado. Não significa "os termos estão em ordem". Significa "ninguém verificou"

O modelo inteiro funciona assim: um valor vazio significa "nada declarado", não "tudo permitido". Uma classificação etária `Unrated`, um alcance de permissão `Undefined` e uma geração por IA `{{ui:enum_ai-generation_not-specified}}` funcionam do mesmo jeito

`NoSpecifiedLicense` pode indicar ainda de onde o arquivo foi tirado: YouTube, SoundCloud, Spotify. O veredito não muda por causa disso. O moderador simplesmente vê que conversa tem pela frente

## Hashes

Preencha os hashes desde o primeiro dia, mesmo onde não são exigidos. A reclamação de um titular de direitos cita uma obra. Para respondê-la, é preciso encontrar todos os níveis com essa obra. Pelo nome é adivinhação, pelo hash é uma busca exata

## Registros obsoletos

O registro de um recurso que o nível já não tem gera uma sugestão, não um erro. Ele não bloqueia nada, mas ainda vale a pena removê-lo

## Um recurso no cartão do nível

O registro de um recurso pode ser marcado para aparecer no cartão do nível. Isso é pensado para a música. Uma linha com esse recurso aparece então sob os autores do nível. Todo o resto fica nos créditos completos

## O registro da capa

A capa do nível também tem registro. A capa não é um recurso do nível, então o registro dela é aberto junto à capa, na aba de metadados, com o botão `{{ui:settings_level-settings_metadata-level-logo-metadata}}`

- Uma imagem nova recomeça o registro do zero, e ele contém só o hash do arquivo. Outra imagem é outra obra, e os autores anteriores receberiam um crédito indevido
- O mesmo arquivo escolhido de novo deixa o registro como está
- Remover a capa remove também o registro dela. Desfazer traz os dois de volta

Um recurso ou uma capa com `{{ui:enum_ai-generation_yes}}` faz a tela do nível mostrar a linha "Contém conteúdo gerado por IA"

A seguir: [[5_publish-readiness]], [[2_metadata-and-sharing]]
