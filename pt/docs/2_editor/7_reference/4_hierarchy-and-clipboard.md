---
title: Hierarquia e área de transferência
date: 2026-10-02
tags: [level_author]
---

# Hierarquia e área de transferência

A hierarquia é uma árvore dos objetos do quadro atual, por pai. Cada linha do tempo tem o próprio buffer de área de transferência, e a paleta de comandos encontra qualquer ação do editor pelo nome

## Hierarquia

Mostra todos os objetos vivos no **quadro atual**, aninhados pelo pai

Um objeto aparece aqui só enquanto o indicador de reprodução está dentro do intervalo dele. Por isso a lista muda enquanto você arrasta o indicador.
Uma hierarquia vazia geralmente significa que o indicador está depois do fim do conteúdo

> [!info] Vale saber
> **Um pai** passa a transformação dele para os filhos. As camadas se somam ao longo da cadeia: a ordem de desenho de um filho é a camada própria dele mais as camadas de todos os ancestrais. Por isso trocar o pai move o objeto na ordem de desenho. Isso também muda os valores aleatórios dele: a aleatoriedade está ligada à camada resultante

> [!tip] Dica
> Clique com o botão direito em uma linha para abrir as ações dela. Em uma tela sensível ao toque, segurar abre o mesmo menu

Segurar uma linha também abre o menu com o mouse. Os clipes nas linhas do tempo não têm menu ao segurar

Arraste uma linha sobre outra para tornar o objeto filho dela. Solto no espaço vazio abaixo das linhas, o objeto perde o pai. A soltura é recusada:
- sobre o próprio objeto ou sobre o pai que ele já tem
- sobre um dos próprios filhos
- se a cadeia ficasse com mais de 15 níveis de profundidade

A linha `{{ui:editor_search-option_camera}}` fica fixa no fim da lista. Uma linha solta sobre ela torna o objeto filho da câmera do nível. Dentro do modelo de um prefab a câmera não aceita filhos, mas a raiz do modelo aceita

Mais: [[3_how-the-editor-thinks|Como o editor funciona]]

## Selecionar vários objetos

Um clique com `Ctrl` adiciona um objeto à seleção ou o remove dela. Funciona igual na hierarquia, nas linhas do tempo e no viewport. `Ctrl` é a única tecla desse tipo: um clique com `Shift` na hierarquia não faz nada, não existe seleção em sequência. A tecla pode ser reatribuída

Um clique com `Ctrl`, ou um retângulo que pega mais de um item, ativa o **modo de seleção múltipla**. Enquanto ele está ativo, o que um clique simples faz depende de `{{ui:settings_game-editor-multi-select-requires_hold}}` - veja [[14_editor-settings]]

O item de seleção na barra de ferramentas mostra `{{ui:editor_multi-select_status}}` ou `Selecionados (N)`. Ele funciona enquanto algo está selecionado:
- um clique limpa a seleção inteira
- um clique duplo ou um clique com `Shift` ativa o modo de seleção múltipla em vez disso. Ativado assim, o modo ignora `{{ui:settings_game-editor-multi-select-requires_hold}}`, e cada clique simples adiciona. É assim que um dedo, que não tem `Ctrl`, monta uma seleção

O mesmo item aparece nos menus de contexto enquanto algo está selecionado. Ali um clique limpa a seleção

O modo se desativa sozinho quando nada está selecionado, e com `Escape` se nenhum campo de texto está recebendo digitação

## Área de transferência

Leva uma seleção de um nível para outro e de um dispositivo para outro. Cada linha do tempo tem o próprio buffer e a própria linha de status

`{{ui:editor_clipboard-serialize_copy}}` grava todos os buffers na área de transferência do sistema como texto.
`{{ui:editor_clipboard-deserialize_paste}}` lê o texto de volta para os buffers - e **para por aí**

> [!info] Vale saber
> A parada é proposital. Ler o texto e colar são duas decisões diferentes. Onde o conteúdo é colado depende do indicador de reprodução e do escopo ativo. O conteúdo só aparece quando você o **cola na linha do tempo que escolheu**

Se a área de transferência do sistema guarda um texto alheio, o editor informa um erro e não trava. Ela guarda o que você copiou por último em qualquer lugar

Não existe a ação "colar todos os buffers de uma vez". Depois de `{{ui:editor_clipboard-deserialize_paste}}`, cole em cada linha do tempo por conta própria

Os quadros-chave colados caem no indicador de reprodução. Para cada dono, o quadro-chave colado mais antigo dele é colocado no indicador, contado dentro do intervalo desse dono. Os quadros-chave de eventos se deslocam na mesma medida, então um movimento de câmera e o efeito que o acompanhava continuam à mesma distância

Um quadro-chave é ignorado se cairia fora da linha do tempo do dono ou em um quadro já ocupado na faixa dele. Os quadros-chave ignorados são contados e informados em uma única mensagem

Uma cópia ou uma colagem bem-sucedida não escreve nada no console. Só os problemas são informados

Mais: [[2_reuse|Reutilização: prefabs, cópia, geradores]]

## Paleta de comandos

Encontra qualquer ação do editor pelo nome

Ela lista comandos, não conteúdo. São as mesmas ações que a barra de ferramentas e os menus de contexto executam

> [!tip] Dica
> A pesquisa de conteúdo (`Ctrl+F`) é a gêmea dela. Ela procura em todos os objetos do escopo atual e em todas as faixas de áudio. Os recursos não estão nela: cada um é escolhido pelo campo que precisa dele

Mais: [[3_speed-and-shortcuts|Velocidade e atalhos]]
