---
title: Ritmo e estrutura
date: 2026-10-02
tags: [level_author]
---

# Ritmo e estrutura

Marque a grade de batidas primeiro: o andamento, depois o deslocamento, depois as batidas por compasso. Ponha o pico do nível no pico da música e dê ao jogador um respiro nos breaks

Um jogo de ritmo se apoia em uma única sensação: o jogador não está se movendo ao som da música, ele está tocando a música

## A grade de batidas

A grade de batidas é para você, não para o jogo. A reprodução não a lê. Você a usa para posicionar o conteúdo na música, e os geradores trabalham sobre as mesmas batidas

A grade é feita de segmentos. **Um segmento é um trecho de andamento constante**, e pode haver vários. Entre os segmentos pode haver buracos: uma introdução sem bateria, um break, a cauda depois da última nota

Marque só os trechos que vão levar conteúdo. Uma introdução normalmente não precisa de nada

## Como encontrar o andamento

1. Encontre o andamento
2. Depois o deslocamento
3. Depois as batidas por compasso

Não sabe o andamento? Marque-o com toques junto com a música na janela `{{ui:editor_beat-window_title}}` (`Shift+T`). Arredonde para um número inteiro e faça o ajuste fino com o deslocamento

Uma música quase sempre é composta em um andamento inteiro. Um valor fracionário geralmente significa que o deslocamento está errado, não o andamento

## Som em movimento

**Distribua os instrumentos entre tipos diferentes de conteúdo:**
- o bumbo - sob o que exige ação do jogador
- os golpes secundários - sob o movimento que não exige ação
- pads longos e atmosfera - sob o fundo e a câmera

Assim o nível soa com profundidade, em vez de acertar uma batida só com tudo ao mesmo tempo

**O tamanho de um movimento carrega a força de um som.** Um movimento pequeno é um golpe fraco, um grande é um golpe forte. Um efeito grande sobre uma nota fraca é lido como erro de sincronia, mesmo quando os quadros estão exatos

**A forma de um movimento carrega o acento.** Uma virada brusca acentua uma nota forte, um arco suave acentua uma fraca

**Em 4/4, as batidas se ordenam por peso como 1, 3, 2, 4.** Uma ação na primeira batida é a mais intuitiva. A síncope dá groove. Mas uma síncope frequente ou inconsistente deixa o jogador sem saber onde está

**Uma fórmula de compasso incomum é dividida em grupos que o jogador consegue contar.** Em 7/4, grupos de 4+4+2+2+2 são mais fáceis de acompanhar que 4+4+4+2

## Estrutura

As seções são o que o jogador lembra. Um nível sem elas são quatro minutos da mesma coisa, mesmo que algo novo aconteça a cada cinco segundos

**A repetição ensina.** Um padrão que volta é reconhecido e aprendido mais rápido. Mas repetição demais entedia, e quebrar sem motivo um padrão já estabelecido é lido como descuido, não como variedade

> [!tip] Recomendação
> Coloque marcadores na estrutura da música antes de posicionar o primeiro objeto: intro, verso, refrão, break, drop, outro. Eles aparecem em todas as linhas do tempo e não custam nada

> [!caution] Cuidado
> O pico do nível precisa cair no pico da música, e as pausas são obrigatórias. O break é onde o jogador respira. Um nível sem pausas cansa as pessoas antes de ficar difícil

O final também precisa ser pensado: ou um pico final, ou um desvanecimento calmo. Um nível não deveria simplesmente ser cortado

## Por que segmentos e não quadros-chave

A grade de batidas é uma lista de trechos, não uma faixa de quadros-chave. Uma faixa de quadros-chave não consegue expressar ausência: o último quadro-chave dela se estenderia até o fim do nível. E os segmentos precisam de buracos entre eles

A seguir: [[4_frames-and-time|Quadros, tempo e duração de um nível]], [[3_difficulty-curve|Dificuldade e curva]]
