---
title: "Reutilização: prefabs, cópia, geradores"
date: 2026-10-02
tags: [level_author]
---

# Reutilização: prefabs, cópia, geradores

Objetos que depois você vai ter que mudar todos de uma vez viram um prefab, sejam quantos forem. Conteúdo que pode ser descrito por uma regra vira um gerador. Em qualquer outro caso, basta copiar

Um gerador vale a pena até para oito objetos: uma execução de gerador é uma única operação a desfazer.
Oito objetos colocados à mão são oito chances de errar em um deles

## Copiar

Para uma forma que você precisa repetir algumas vezes e não quer mais vincular ao original

Há cinco áreas de transferência, uma por linha do tempo. Clipes copiados em uma linha do tempo não são colados sobre quadros-chave de outra

Copiar e colar seguem caminhos diferentes:
- **Colar** sempre vai para a linha do tempo que você está olhando
- **Copiar** pega o que está selecionado. A linha do tempo aberta tem prioridade se tiver uma seleção própria. Caso contrário, a seleção é copiada onde quer que esteja, então um objeto selecionado com a linha do tempo local aberta também é copiado

Duplicar (`Ctrl+D`) não grava em nenhuma área de transferência. O que você copiou antes não se perde

Duplicar e colar tratam o pai de forma diferente:
- **Uma duplicata** mantém o pai. A cópia fica ao lado do original na hierarquia
- **Colar** descarta o pai, e os objetos colados vão parar no topo da hierarquia. A exceção é um pai `{{ui:editor_search-option_camera}}` ou `{{ui:editor_search-option_local-player}}`: no escopo do nível, ele sobrevive à colagem

Os dois procuram uma camada livre só nos quadros em que cada objeto copiado cai. Colar em um trecho vazio da linha do tempo mantém as camadas que os objetos tinham

O nome de uma cópia é renumerado. Um final de `_` e dígitos é o id do objeto, então `Shape_12` vira `Shape_` com um id novo. Um nome sem esse final não ganha um, e um final que não é só de dígitos (`Wave_2b`) fica como está. Faixas de áudio são renomeadas do mesmo jeito

Objetos copiados no modo prefab são colados de volta no modelo, não no nível

> [!caution] Cuidado
> As áreas de transferência são esvaziadas quando um nível é carregado. Todos os ids e quadros nelas pertencem ao nível que estava aberto

## Prefabs

Para algo que você precisa muitas vezes e quer mudar em todos os lugares de uma vez

Um prefab é um modelo e os posicionamentos dele. Quando você dá um modelo a um posicionamento, o posicionamento recebe cópias reais dos objetos do modelo, com ids permanentes. O arquivo do nível armazena só o próprio posicionamento: o modelo, os ids das cópias e as suas substituições. As cópias são reconstruídas a partir do modelo toda vez que o nível é carregado

Uma edição no modelo se espalha para todos os posicionamentos que fazem referência a ele.
Uma edição em uma cópia de um posicionamento (fora da edição do modelo) é registrada como substituição só daquela instância.
As substituições sobrevivem às edições posteriores do modelo. Por isso um prefab serve também para variações, não só para clones

Prefabs podem ser aninhados uns dentro dos outros. Um modelo aninhado pode ser editado de dentro de outro: os modelos se abrem um por cima do outro e se fecham na ordem inversa

### Um prefab a partir de uma seleção

Selecione objetos e pressione `Ctrl+G` (`{{ui:cmd_editor_pack-prefab}}`). A mesma ação também está:
- na paleta de comandos
- no menu de contexto do viewport, enquanto algo está selecionado
- no menu de uma linha da hierarquia, como `{{ui:editor_context-menu_pack-prefab}}`
- nas configurações do nível, aba `{{ui:editor_library_kind-prefabs}}`, `{{ui:settings_level-settings_resources-prefabs-pack}}`

Os objetos selecionados passam para um modelo novo, um posicionamento dele ocupa o lugar deles, e esse posicionamento fica selecionado. É uma única operação a desfazer.
Um objeto só dá o próprio nome ao modelo. Vários objetos dão um modelo chamado `Prefab`

Um posicionamento e um objeto que pertence a ele não podem ser empacotados de novo. Os menus deles oferecem `{{ui:editor_context-menu_open-prefab}}` no lugar, e o modelo deles se abre.
No modo prefab não é possível empacotar

## Geradores e modificadores

**Geradores** criam conteúdo por uma regra: uma espiral, uma grade, um fractal, uma onda, uma chuva de projéteis, um leque de raios. Você define uma janela de quadros, uma camada e uma semente e recebe objetos. A estimativa do resultado aparece antes de você pressionar qualquer coisa

**Modificadores** funcionam do mesmo jeito, mas com o que já existe: ajustam intervalos, espaçam esses intervalos, quantizam quadros-chave, recalculam a taxa de quadros, excluem o conteúdo de uma janela

## Entre níveis: as bibliotecas compartilhadas do dispositivo

Tudo o que está acima funciona dentro de um nível. De um nível para outro só passam as bibliotecas compartilhadas do dispositivo e as coleções

Temas, efeitos, formas e prefabs são exportados de um nível e importados em outro.
As bibliotecas ficam ao lado da pasta de níveis, então um nível que você envia leva a própria cópia

Uma coleção reúne recursos de qualquer um dos sete tipos, incluindo texturas, fontes e áudio, e viaja como arquivo compactado ou pela Oficina Steam. Mais - [[16_library-and-collections]]

A seguir: [[3_speed-and-shortcuts|Velocidade e atalhos]], [[4_level-folder-and-backups|A pasta do nível e os backups]]
