---
title: Modo prefab
date: 2026-10-02
tags: [level_author]
---

# Modo prefab

No modo prefab você edita o modelo, e salvar leva a edição a todos os posicionamentos dele. Entre pelo botão "Editar prefab" no inspetor de um posicionamento e volte ao nível com Ctrl+Shift+E

## Modo prefab

> [!caution] Cuidado
> Você está editando o modelo, não um dos posicionamentos dele. Salvar leva a mudança a todos os posicionamentos que referenciam este modelo

Como um posicionamento funciona:
- No momento em que você aponta um posicionamento para um modelo, o posicionamento recebe cópias reais dos objetos dele com ids permanentes. No editor, um filho de prefab é um objeto totalmente comum
- O arquivo do nível guarda só o posicionamento: o modelo, os ids das cópias e as substituições. As cópias são reconstruídas a partir do modelo toda vez que o nível carrega
- Um posicionamento pode diferir do modelo por meio de **substituições por instância**. Elas são registradas quando você edita um objeto assim *fora* do modo prefab
- As edições feitas no modo prefab não registram substituições. Elas mudam o próprio modelo

> [!tip] Dica
> Os modelos se abrem uns sobre os outros. Um posicionamento dentro de um modelo abre o próprio modelo, e `{{ui:editor_prefab-timeline_close}}` traz você de volta. O mesmo modelo não pode estar aberto duas vezes ao mesmo tempo. O limite de aninhamento é de 8 níveis

Mais - [[2_reuse]]

## Entrar e sair

Há duas formas de entrar:
- `{{ui:editor_inspector-prefab_edit}}` no inspetor de um posicionamento
- `{{ui:editor_level-prefab-item_edit}}` na linha de um modelo nas configurações do nível, aba `Prefabs`. Não precisa de posicionamento, por isso também abre um modelo que não está posicionado em lugar nenhum, ou que só está posicionado dentro de outro modelo

`{{ui:editor_context-menu_open-prefab}}` em um menu de contexto e na paleta de comandos faz o mesmo para um posicionamento selecionado, ou para um objeto que um posicionamento trouxe. O objeto correspondente dentro do modelo é selecionado na hora

Há duas formas de sair:
- `{{ui:editor_prefab-timeline_close}}` na linha do tempo do prefab sobe um nível, de volta ao modelo que abriu este
- o status na barra de ferramentas principal (`Editando '...'`) e `Ctrl+Shift+E` saem de todos os modelos abertos de uma vez, de volta ao nível

A seleção é limpa toda vez que você entra ou sai. Voltar um nível restaura o que estava selecionado naquele modelo

Dentro de um modelo, a seleção funciona como no nível: clique, clique com `Ctrl`, seleção retangular, excluir, copiar e recolher. Um clique no viewport não seleciona nada ali: o viewport continua mostrando o nível, e um modelo não tem pré-visualização ao vivo nele

## Dentro de um modelo

Todo objeto de um modelo fica pendurado na **raiz** dele. A raiz:
- cobre o modelo inteiro. A duração dela é `{{ui:editor_prefab-mode-frame_length}}`, o mesmo número no inspetor da raiz e na aba `Prefab`
- não pode ser excluída nem receber um pai
- tem `{{ui:field_common_active}}` e `{{ui:editor_inspector_layer}}` só para leitura. Esses pertencem a cada posicionamento

Um objeto novo vai para baixo do objeto selecionado quando exatamente um está selecionado, a raiz incluída. Caso contrário, vai para o nível superior do modelo, embaixo da raiz. Ele cobre o pai, com âncora nas duas pontas. No nível superior, isso é o modelo inteiro

Os geradores que precisam do nível inteiro não estão disponíveis aqui. Criar um prefab a partir de uma seleção e achatar um posicionamento também são recusados dentro de um modelo

## Criar um prefab a partir de uma seleção

Transforma os objetos selecionados em um modelo novo e coloca um posicionamento dele onde eles estavam. Depois disso, o nível tem a mesma aparência e é jogado do mesmo jeito

Onde encontrar:
- `{{ui:editor_context-menu_pack-prefab}}` no menu de uma linha da hierarquia
- o menu de contexto do viewport
- `{{ui:cmd_editor_pack-prefab}}` na paleta de comandos, `Ctrl+G`
- `{{ui:settings_level-settings_resources-prefabs-pack}}` nas configurações do nível, aba `Prefabs`

Não pede confirmação e é um único passo de desfazer. O posicionamento novo fica selecionado. Um único objeto dá o próprio nome ao modelo. Vários objetos dão um modelo chamado `Prefab`. Renomeie-o nas configurações do nível, aba `Prefabs`

O que é recusado:
- um posicionamento, ou um objeto que um posicionamento trouxe. Para esses, os menus oferecem `{{ui:editor_context-menu_open-prefab}}`
- uma seleção que ficaria aninhada a mais de 15 níveis de profundidade. Nada é gravado, e a mensagem diz isso

## Achatar um posicionamento

Desvincula um posicionamento do modelo: os objetos dele viram objetos comuns do nível e ficam exatamente onde estão

Onde encontrar: `{{ui:editor_inspector-prefab_flatten}}` no inspetor do posicionamento, no menu de uma linha da hierarquia e na paleta de comandos

Sempre pergunta antes. Depois disso, o nível tem a mesma aparência, então um achatamento feito por engano só seria descoberto muito mais tarde, quando uma edição do modelo deixasse de chegar até ele. Vários posicionamentos selecionados dão uma única confirmação e um único passo de desfazer

Um objeto que um posicionamento trouxe não pode ser achatado sozinho. Achate o posicionamento ao qual ele pertence

## Achatar também prefabs aninhados

Decide o que acontece com os prefabs que estão dentro daquele que você achata

**Desativado** - só o posicionamento que você apontou deixa de seguir o modelo. Um prefab posicionado dentro dele continua sendo um posicionamento e mantém o vínculo. Editar esse modelo interno ainda chega ao nível. Este é o valor padrão: é o que "desempacotar este prefab" costuma pedir. O interruptor fica desativado toda vez que a confirmação abre

**Ativado** - tudo o que está aninhado também é achatado. Depois de um único clique, nada no nível fica vinculado a esses modelos internos, em nenhuma profundidade

Em qualquer caso, os próprios modelos continuam no nível. Todo o achatamento é um único passo de desfazer
