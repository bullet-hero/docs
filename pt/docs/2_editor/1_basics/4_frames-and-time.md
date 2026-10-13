---
title: "Quadros, tempo e duração de um nível"
date: 2026-10-12
tags: [level_author]
---

# Quadros, tempo e duração de um nível

Um nível conta o tempo nos próprios quadros, não nos quadros da tela, por isso roda igual em qualquer hardware. Você define a duração do nível, e é melhor deixar o fps no padrão, 60

## Quadros do nível e quadros da tela

Um quadro do nível não tem nada a ver com um quadro da tela.
A tela desenha tantos quadros por segundo quanto o hardware consegue. Um nível conta o tempo nos próprios quadros, e quantos há por segundo fica armazenado no próprio nível. O padrão é `60`

Por isso um nível roda igual a 60 Hz, a 144 Hz e em um celular que caiu para 30. A precisão dos impactos não depende da placa de vídeo

Um quadro é uma célula, não um instante. Se um objeto termina no quadro 100 e outro começa no quadro 100, eles não se sobrepõem

Mais precisamente: os quadros contam a partir de 1, e o quadro f cobre o tempo de (f-1)/fps a f/fps, com a borda esquerda incluída e a direita não. Por isso o quadro 1 começa bem no início da música

## A duração de um nível

Você define a duração do nível. A duração da música vem do arquivo. Elas não precisam coincidir

Conteúdo depois do fim do nível é permitido. Ele simplesmente nunca é reproduzido, e a validação não reclama dele. Um objeto pode passar do fim, mas o assistente de IA não consegue criar um que comece depois dele

Um filho que ultrapassa o intervalo do pai funciona do mesmo jeito. O nível mantém o que você escreveu, e o tempo de vida efetivo é calculado separadamente

Para ajustar os tempos de vida de filhos e pais entre si, use o modificador `{{ui:mod_span_fit}}` em `{{ui:editor_generators_text}}`. Ele ou puxa os filhos para dentro ou alarga os pais

## O fps do nível

Quanto maior o fps, mais precisamente você acerta a batida. E mais quadros ocupa a mesma duração.
Os valores vão de 1 a 1000, o padrão é `60`

> [!tip] Recomendação
> Deixe o fps no padrão. A 60 o ouvido não percebe um deslocamento de um quadro, e o número de quadros-chave cresce com o fps

A linha do tempo tem um limite de `1000000` quadros. Isso dá cerca de 4,6 horas a 60 fps e cerca de 17 minutos a 1000

> [!warning] Aviso
> Mudar o fps de um nível pronto significa recalcular todos os quadros-chave dele. O modificador `{{ui:mod_framerate_remap}}` faz isso, fazer à mão não é realista

A seguir: [[5_keyframes-and-easing]], [[2_rhythm-and-structure]], [[1_order-of-work]]
