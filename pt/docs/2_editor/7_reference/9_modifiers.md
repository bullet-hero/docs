---
title: Modificadores
date: 2026-10-12
tags: [level_author]
---

# Modificadores

Um modificador muda o que já está no nível: remove conteúdo, recalcula o fps, achata prefabs, quantiza quadros-chave, ajusta e desloca intervalos. Uma execução se desfaz em um único passo

## Remover conteúdo

Remove o conteúdo do nível que atende às condições indicadas

> [!caution] Cuidado
> O modificador muda o que existe em vez de adicionar. Tudo só pode ser recuperado com um passo de desfazer. Leia os parâmetros antes de executá-lo

Ele atua na janela de quadros da janela de geradores. No modo inverso, ele remove o que não compartilha nenhum quadro com a janela. No modo inverso ou com `{{ui:editor_generators-whole_level}}` ativado, ele pode remover muito mais do que está visível na tela, por isso pede confirmação antes

Mais - [[2_reuse]]

## Remapear taxa de quadros

Recalcula cada número de quadro para outra taxa de quadros.
Os tempos ficam nos mesmos segundos

> [!warning] Aviso
> Os quadros são números inteiros. Tudo o que não se divide exatamente é arredondado. Por isso, depois de dois recálculos, o nível pode não voltar ao original

O formulário mostra a taxa de quadros atual do nível como referência, somente leitura. Qualquer mudança real de taxa de quadros pede confirmação antes. O modificador precisa do nível inteiro, por isso fica indisponível no modo prefab

Mais - [[4_frames-and-time]]

## Achatar prefabs

Transforma cada posicionamento de prefab deste escopo em objetos comuns.
A ligação com o modelo desaparece. Os objetos ficam exatamente onde estavam

> [!info] Vale saber
> O nível fica igual ao que era antes da execução: nada é excluído nem movido. As edições em posicionamentos individuais já estão gravadas nos próprios objetos e não se perdem. Os modelos ficam no nível, a menos que você peça para excluí-los

## Quantizar quadros-chave

Puxa os quadros-chave para um passo regular.
Assim uma animação feita à mão e irregular cai na batida

Atua na seleção e não é executado sem ela

A grade vem da primeira fonte que se aplica:
1. `Use Beat Grid` está ativado (o padrão) e o nível tem uma grade de batidas. As linhas são as batidas dos segmentos dela, cada batida dividida em `Division` partes. O modelo de um prefab não tem grade de batidas
2. `Use Bpm` está ativado (o padrão). Uma linha em cada batida de `Bpm` na taxa de quadros do nível, dividida em `Division` partes
3. `Use Bpm` está desativado. Uma linha a cada `Step Frames` quadros, começando no quadro 1

Cada linha é colocada a partir do tempo exato dela e só depois arredondada para um quadro. Assim a grade fica na batida mesmo onde uma batida não é um número inteiro de quadros: 167 BPM a 60 fps são 21,56 quadros por batida

`Offset Frames` desloca todas as linhas, `Mode` manda um quadro-chave que está entre duas linhas para a mais próxima, a anterior ou a seguinte, `Tracks` escolhe quais faixas são encaixadas. Os rótulos do formulário são os próprios nomes dos parâmetros e não são traduzidos

> [!warning] Aviso
> Um quadro-chave cuja linha já está ocupada por outro quadro-chave da mesma faixa fica onde estava. Por isso uma quantização grossa deixa alguns quadros-chave fora da grade em vez de fundi-los. Um quadro-chave também nunca é movido para antes do início do objeto dele

Mais - [[2_rhythm-and-structure]], a grade de batidas - [[3_timelines#Grade de batidas]]

## Ajustar intervalos

Coloca os intervalos dos filhos dentro do intervalo do pai.
Duas formas: encolher os filhos ou esticar os pais.
As âncoras não mudam em nenhuma delas

> [!info] Vale saber
> Um filho que passa do pai são dados válidos. Ele simplesmente é reproduzido cortado. Ajustar é uma decisão sobre o conteúdo, não a correção de um bug, por isso nunca é executado sozinho

Mais - [[4_frames-and-time]]

## Escalonar

Desloca a seleção no tempo.
Objetos que começavam juntos aparecem um depois do outro

Atua na seleção e não é executado sem ela

Mais - [[2_reuse]]
