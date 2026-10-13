---
title: Propriedades do objeto
date: 2026-10-12
tags: [level_author]
---

# Propriedades do objeto

O inspetor de objeto edita os campos do objeto selecionado, o inspetor de quadro-chave edita os quadros-chave selecionados, em todas as faixas que a seleção toca ao mesmo tempo

## Inspetor de objeto

Mostra os campos do objeto selecionado. Todos os tipos têm os campos comuns de um objeto vazio. Forma, Efeito, Texto e Prefab adicionam os próprios campos abaixo

`{{ui:field_common_active}}` desliga tanto a renderização *quanto* a colisão. Os filhos herdam isso. Um objeto oculto aqui não pode matar o jogador

> [!caution] Cuidado
> `{{ui:editor_inspector_layer}}` é definida em relação ao pai, não de forma absoluta. Ao lado fica a camada global, somente leitura. É ela que a renderização usa: a sua camada mais as camadas de todos os ancestrais

> [!tip] Dica
> Editar um campo de um objeto vindo de um prefab registra uma **substituição de instância**. A caixa de seleção ao lado mostra a substituição e a desfaz

O botão do pai mostra de quem o objeto depende, `{{ui:editor_inspector-parent_btn}}` inclusive. Ele abre a janela `{{ui:editor_picker_select-parent}}`: todos os objetos do escopo, com opções fixas no topo:
- no nível - `{{ui:editor_inspector-parent_btn}}` e `{{ui:editor_search-option_camera}}`. `{{ui:editor_search-option_camera}}` é a câmera do nível, e o filho dela se move junto com ela
- dentro do modelo de um prefab - uma linha `{{ui:editor_search-option_prefab-root}}`. Ela significa ao mesmo tempo "sem pai" e a raiz do modelo: ali as duas coisas são a mesma. A câmera e o jogador não podem ser pais dentro de um modelo

Um pai reservado aparece com o ID dele: `Câmera (-1)`, `Jogador local (-2)`, `Raiz do prefab (-3)`. O assistente de IA só pode usar a câmera (-1) e, dentro de um modelo, a raiz (-3)

O botão ao lado seleciona o pai. Em um objeto no nível superior de um modelo, ele seleciona a raiz do modelo. Ele fica indisponível quando vários objetos estão selecionados e quando não há nada para selecionar: não há pai, ou o pai é a câmera ou o jogador

Uma aba do painel direito sem nada para mostrar fica oculta. Se a aba aberta fica vazia, o painel passa para a primeira aba que tem algo. Se todas as abas estão vazias, o painel mostra `{{ui:editor_right-panel_placeholder}}`

Mais: [[3_how-the-editor-thinks|Como o editor funciona]]

## Inspetor de quadro-chave

Mostra os quadros-chave selecionados. **Todas as faixas que a seleção toca ficam visíveis ao mesmo tempo**, não só a última em que você clicou.
Uma seleção pode ter quadros-chave de posição e de rotação, quadros-chave de objetos diferentes, e quadros-chave de objetos, de áudio e de eventos juntos

> [!tip] Dica
> A escolha `{{ui:enum_search-domain_ease}}` atua em todas as faixas ao mesmo tempo e ocupa **um único passo de desfazer**. Uma seleção de posição e rotação muda em uma operação, não em duas

> [!info] Vale saber
> O campo `{{ui:editor_frame-key-view_key-frame}}` fica bloqueado quando vários quadros-chave estão selecionados. Em uma faixa, cada quadro é único. Um único número para todos os quadros-chave os fundiria em um só e excluiria o resto sem aviso. Para mover vários quadros-chave de uma vez, arraste-os na linha do tempo

Um valor em branco significa que os quadros-chave selecionados **diferem** nele

Mais: [[3_how-the-editor-thinks|Como o editor funciona]]

## Intervalo

Define quando o objeto existe. O intervalo é semiaberto: o quadro inicial faz parte dele, o quadro final não.
Um objeto que termina em 20 e um objeto que começa em 20 nunca desenham juntos nesse quadro

> [!info] Vale saber
> **O intervalo de um filho precisa ficar dentro do intervalo do pai. Isso é resolvido na leitura e nunca salvo.** Encolha o pai e os filhos são cortados, mas o que está escrito aqui não muda. Estique o pai de volta e tudo retorna. Um objeto raiz além do fim do nível são dados válidos, ele simplesmente não é reproduzido

> [!info] Vale saber
> **As âncoras** significam "esta borda segue a borda do pai", e elas decidem o que é reproduzido. Uma borda com âncora fica na borda do pai, então um filho com âncora se estica junto com um pai que cresce. A animação dele mantém o tempo definido pelo autor

A duração do posicionamento de um prefab vem do modelo por padrão, mas pode ser digitada como qualquer outra. Um valor diferente registra uma substituição deste posicionamento. A caixa de seleção ao lado do intervalo mostra isso e traz de volta a duração do modelo

A raiz do modelo de um prefab não tem bloco de intervalo. No lugar dele há uma linha `{{ui:editor_prefab-mode-frame_length}}`: a duração do modelo inteiro, o mesmo valor de `{{ui:editor_prefab-mode-frame_length}}` na aba `{{ui:field_common_prefab}}`. `{{ui:field_common_active}}` e `{{ui:editor_inspector_layer}}` da raiz são somente leitura, e a raiz não pode ser excluída nem receber um pai

Mais: [[4_frames-and-time|Quadros, tempo e duração de um nível]]

## Suavização

Define como o valor chega a este quadro-chave a partir do anterior

> [!info] Vale saber
> A suavização pertence ao lado de **entrada** de um quadro-chave. Ela define o trecho do quadro-chave anterior até este, e é exatamente assim que a reprodução a lê. Por isso, no primeiro quadro-chave de uma faixa, a suavização não tem efeito

> [!tip] Dica
> Se vários quadros-chave estão selecionados, a escolha se aplica a todos ao mesmo tempo em **um único passo de desfazer**. Mesmo que os quadros-chave estejam em faixas diferentes e pertençam a objetos diferentes. Uma escolha em branco significa que os quadros-chave selecionados diferem

Mais: [[5_keyframes-and-easing]]

## Camada

Define a ordem de desenho **em relação ao pai**, não de forma absoluta. Uma camada resultante mais alta é desenhada na frente. De duas formas na mesma camada resultante, a mais nova (o ID mais alto) é desenhada atrás

> [!caution] Cuidado
> A renderização usa este número mais as camadas de todos os ancestrais. A soma aparece, somente leitura, no campo `{{ui:editor_inspector-global_layer}}` abaixo. Por isso a mesma camada significa coisas diferentes sob pais diferentes. Trocar o pai muda onde o objeto é desenhado

> [!info] Vale saber
> A camada também participa da aleatoriedade. Um valor aleatório está ligado à camada resultante, então mover um objeto na hierarquia muda os números que ele sorteou. Dois objetos com a mesma camada resultante E o mesmo quadro inicial recebem os mesmos números

Mais: [[3_how-the-editor-thinks|Como o editor funciona]]

## Forma

Define o que o objeto **desenha**

> [!info] Vale saber
> Uma forma é geometria real, não uma imagem. Ela é ajustada ao próprio retângulo, e o lado maior dela mede exatamente 1. Por isso o retângulo do objeto é exatamente o que se vê na tela

> [!info] Vale saber
> O jogo gera cerca de 500 formas ao longo de quatro eixos: figura, setor, espessura e inversão. Um nível pode adicionar as próprias. Um valor vazio é válido: um objeto sem imagem, mas com hitbox, é uma parede invisível

Mais: [[1_readability-and-fairness|Legibilidade e justiça]]

## Colisor

Define com o que o objeto **colide**. É uma escolha separada e não depende do que o objeto desenha

> [!info] Vale saber
> Um não é derivado do outro de propósito. Um raio de aviso inofensivo, uma hitbox mais simples que a imagem e uma parede invisível são conteúdo comum, não truques

> [!tip] Dica
> Os dois campos escolhem das mesmas duas coleções. Uma forma que o nível criou serve para qualquer um dos dois

Nos modos de exibição de hitbox, um objeto sem colisor não desenha nada, e um objeto inativo também não. É assim que a decoração se distingue do perigo. Como eles são desenhados é definido em [[14_editor-settings]]

Mais: [[1_readability-and-fairness|Legibilidade e justiça]]

## Tipo de shader

Define por qual caminho o objeto é renderizado

> [!caution] Cuidado
> `{{ui:enum_shader-type_auto}}` decide uma única vez, quando o nível carrega. A regra é rígida: a aparência do nível não pode mudar. Tudo o que não pode ser provado opaco vira transparente. A geometria não é considerada, só o alfa

> [!tip] Dica
> O rótulo ao lado mostra no que `{{ui:enum_shader-type_auto}}` realmente se resolveu. Ele é lido direto dos dados de renderização, não é calculado de novo. Assim o rótulo não pode discordar do que está na tela

Mais: [[1_level-budget|O orçamento do nível]]

## Valores atuais

Mostra o que os objetos selecionados **são** no quadro atual, não o que você escreveu neles. Cada número é lido da simulação em execução. Por isso ele coincide com o que se vê no viewport

O quadrado no fim de uma linha é o estado de quadro-chave desse campo:
- azul - há um quadro-chave neste quadro. Clicar no quadrado o seleciona
- âmbar - o quadro está entre dois quadros-chave, o valor é interpolado
- cinza - a faixa tem quadros-chave, mas o quadro está fora deles. O valor é mantido
- vazado - a faixa está vazia, o campo usa o valor padrão do motor

As setas movem o indicador de reprodução para o quadro-chave anterior ou o próximo dessa faixa

Uma linha UV é lida como dois pares: primeiro o mosaico, depois o deslocamento

Abaixo da linha vêm os valores compostos: a camada somada, a atividade herdada e a transformação com os pais levados em conta. Nenhum quadro-chave os define, então eles não têm esse sinal

> [!info] Vale saber
> Uma faixa de quadros-chave vazia são dados válidos, não dados que faltam. Significa que o objeto usa o valor padrão desse campo

> [!info] Vale saber
> No modo prefab esta seção fica oculta. Um modelo não reproduz os próprios quadros, então não há nada para mostrar em um quadro
