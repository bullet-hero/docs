---
title: Prontidão para publicar
date: 2026-10-02
tags: [level_author]
---

# Prontidão para publicar

Cada serviço verifica um nível pelas próprias regras, então um pode aceitá-lo e outro recusá-lo. Só um erro bloqueia a publicação, um aviso manda o nível para a moderação

A verificação roda sozinha na aba `{{ui:settings_level-settings_publication}}` das configurações do nível, em qualquer versão. O destino escolhe o perfil: `{{ui:editor_share_archive}}` é verificado pelo perfil `{{ui:editor_publish_profile-local}}`, o mais permissivo, e `{{ui:editor_share_steam}}`, pelo perfil da Oficina. O perfil padrão é o de um servidor público, e o perfil da versão para lojas não é oferecido no jogo, os limites dele estão abaixo. Mais - [[17_publishing]]

## Três veredictos

| Veredicto | O que acontece |
|---|---|
| **`Error`** | o serviço recusa, o envio é bloqueado antes de começar |
| **`Warning`** | dá para publicar, mas uma pessoa vai olhar o nível. O servidor o coloca na fila de moderação |
| **`Advice`** | uma observação, não bloqueia nada |

Um nível que fica no seu dispositivo não é avaliado por nada

## O perfil da Oficina

Por enquanto é mais permissivo que o padrão, porque a política de licenças ainda vai ser reescrita:
- passa qualquer licença CC BY, 3.0 e 4.0: BY, BY-SA, BY-NC, BY-NC-SA, BY-ND, BY-NC-ND. Também CC0, SIL OFL, MIT, Apache e a Unlicense
- continuam recusados: todos os direitos reservados, licenças da família GPL e um texto de licença próprio
- só um aviso: nenhuma licença indicada, um recurso sem registro, nenhum link para a página de origem
- classificação etária e autores do nível não são obrigatórios
- os limites de tamanho são os mesmos do perfil padrão

> [!caution] Cuidado
> Música CC BY-ND é aceita, mas pela CC 4.0 uma música sincronizada com imagem em movimento sempre conta como adaptação, e ND proíbe distribuir adaptações. Um nível feito sobre uma música ND pode ser retirado a pedido do titular dos direitos. Melhor escolher outra música

## O que gera um erro

No perfil padrão:
- a licença própria do nível não é aceita
- não há classificação etária
- ninguém recebe crédito pelo nível
- um recurso não tem registro
- a licença de um recurso é recusada ou não foi indicada
- um recurso é obtido de um jeito que o serviço não aceita
- um recurso é tirado de um site não permitido
- algo ultrapassa os limites de tamanho

## O que gera um aviso

- um recurso não tem link para a página de origem. Uma obra de sua própria autoria não tem essa página, então isso nunca bloqueia
- uma permissão sem alcance ou sem prova
- uma permissão expirada
- um site com mais de um tipo de termos

## O que gera uma sugestão

- o registro de um recurso que o nível já não tem

## Por que e o que fazer

Cada linha do relatório nomeia o próprio recurso: pelo nome do arquivo ou pelo nome que você deu a ele. O `?` no fim da linha expande os detalhes: que licença o recurso tem, quais o serviço aceita no lugar dela, quanto ele pesa em relação ao limite e onde corrigir

## Limites de tamanho

| Limite | Perfil padrão | Versão para lojas |
|---|---|---|
| Por recurso | `{{v:publish.standard.max-resource-mb}} MB` | `{{v:publish.strict.max-resource-mb}} MB` |
| Por arquivo de dados | `{{v:publish.standard.max-data-file-mb}} MB` | `{{v:publish.strict.max-data-file-mb}} MB` |
| Por nível | `{{v:publish.standard.max-level-mb}} MB` | `{{v:publish.strict.max-level-mb}} MB` |

Uma versão para lojas também exige atribuição e hashes, e recusa links arbitrários. Os tamanhos menores não são uma opinião mais rígida. São o que um celular consegue de fato baixar por uma rede móvel

## Um relatório limpo

> [!caution] Cuidado
> Um relatório limpo só com os metadados não significa "pronto". Duas verificações precisam do próprio arquivo do nível: um recurso sem registro e de onde um recurso é obtido. Passar só com os metadados significa "nada de errado no que foi lido"

## Por que os serviços avaliam de forma diferente

As regras de um serviço são um arquivo de dados, não código. Cada serviço faz a mesma dúzia de perguntas, mais ou menos, e responde do próprio jeito:
- quais licenças são aceitáveis
- como os recursos podem ser obtidos
- se uma licença desconhecida é tolerada
- o que precisa ser preenchido
- qual pode ser o tamanho de um nível

Um serviço traz as próprias respostas, outro as substitui. Por isso o mesmo nível pode estar pronto para um serviço e ser recusado por outro

> [!info] Vale saber
> A mesma verificação roda tanto automaticamente no seu computador quanto na moderação manual no servidor. Um cliente sem rede ainda avalia um nível corretamente, porque as regras com que ele foi compilado viajam com ele

A seguir: [[4_resource-record]], [[2_metadata-and-sharing]]
