---
title: Legibilidade e justiça
date: 2026-10-01
tags: [level_author]
---

# Legibilidade e justiça

O jogador precisa entender o que o matou. Mostre um perigo antes que ele fique perigoso, dê pelo menos 12 quadros para reagir e faça o perigo se destacar mais que a decoração

Há um único teste de justiça: **ao morrer, o jogador culpa a si mesmo ou o nível?** Tudo nesta página empurra a resposta para "a si mesmo"

## Sinalização antecipada

Um perigo precisa ser visível antes de ficar perigoso

Uma forma e um colisor são dois campos separados de um mesmo objeto. Então avisar é simples: um raio com forma e sem colisor brilha e não acerta. Meio segundo depois aparece outro ao lado, desta vez com colisor

O contrário também é válido: uma parede invisível é um objeto sem forma, mas com um colisor de verdade

> [!caution] Cuidado
> Um perigo invisível só é justo em um caso: o jogador já sabe que ele está lá, porque o nível o mostrou antes

## Tempo de reação

Uma pessoa percebe um perigo e reage em cerca de 0,2-0,25 segundo, no melhor dos casos. A 60 quadros de nível por segundo, isso dá 12-15 quadros

Um perigo que aparece menos de 12 quadros antes do contato (10, por exemplo) não pode ser superado na primeira tentativa. Só pode ser decorado. Quando isso é aceitável - [[3_difficulty-curve#Memorização]]

## Contraste

O que é perigoso precisa se diferenciar do fundo mais do que a decoração. A falha mais comum é um projétil escuro sobre um fundo escuro, exatamente no momento em que o fundo também está mudando

> [!tip] Recomendação
> Tire do tema tanto as cores do fundo quanto as dos projéteis. Assim uma única edição do tema mantém o contraste em todo lugar. Cores digitadas à mão o mantêm só até a primeira edição

## Um perigo, uma aparência

Cada tipo de perigo precisa da própria aparência reconhecível, e do próprio som, se você usa som. Depois que o jogador aprendeu que uma coisa assim acerta, tudo o que parecer igual também precisa acertar

Não contradiga os próprios sinais. Se algo que parece decoração mata em um lugar, o jogador para de confiar em tudo o que parece decoração

## Estrutura vale mais que densidade

Uma tela cheia de movimento é lida como ruído, não como dificuldade. Um jogador não distingue 40 projéteis. Ele distingue uma parede com um buraco, uma onda, uma espiral, um corredor

Oito objetos com estrutura são mais difíceis e mais justos que quarenta sem ela

## Um nível sempre se joga igual

Um nível não tem condições, contadores nem gatilhos que reajam ao jogador. Tudo está escrito na linha do tempo. A aleatoriedade também não muda: o mesmo ponto dá os mesmos números em qualquer dispositivo

Por isso um nível não pode ser reativo. Mas também não pode ficar injusto por acidente, só de propósito

Entre as tentativas muda só o que o jogador escolhe: vidas, velocidade de reprodução e checkpoints. Mais - [[3_difficulty-curve#O que o jogador escolhe]]

A seguir: [[3_difficulty-curve|Dificuldade e curva]], [[5_color-and-postprocessing|Cor, temas e pós-processamento]]
