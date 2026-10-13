---
title: Dificuldade e curva
date: 2026-10-02
tags: [level_author]
---

# Dificuldade e curva

Projete com base nos números do próprio jogador - todos estão em [[6_avatar]] e [[7_damage]] - e numa reação humana de 12-15 quadros. Mostre cada padrão novo primeiro de forma segura

Você não consegue julgar a própria dificuldade: teste o nível com alguém que o vê pela primeira vez

## O jogador em números

Os valores exatos do avatar estão em [[6_avatar]] e [[7_damage]]. O que eles significam para um nível:

| O quê | O que significa para o design |
|---|---|
| Hitbox do jogador | muito menor que o corpo desenhado, então uma bala que raspa o corpo muitas vezes não acerta |
| Dash | atravessa três quartos da altura da tela quase instantaneamente |
| Invulnerabilidade no dash | dura mais que o próprio dash, então um dash através de um obstáculo fino é seguro |
| Depois de um impacto | um recuo curto sem controle, depois uma janela de tolerância que ignora os impactos seguintes |
| Reação humana | 0,2-0,25 segundo, ou seja, 12-15 quadros a 60 fps |
| Valores ao iniciar | 3 vidas, velocidade 1,0, checkpoints ativados |

Regras práticas que daí decorrem:
- um vão de uma unidade de largura é largo, um vão de 0,6 é apertado
- um dash cobre tanto terreno quanto meio segundo de corrida

## Um impacto não mata na hora

Depois de um impacto, o jogador é empurrado para trás e por um momento fica sem controle. Os impactos seguintes são ignorados por um tempo depois disso ([[7_damage]]). Uma parede de dez projéteis seguidos custa uma vida, não dez

> [!info] Vale saber
> A intuição diz o contrário. Uma rajada densa parece morte instantânea. Na verdade, ela custa menos que um único projétil que chega exatamente quando a invulnerabilidade acabou

## O que o jogador escolhe

Vidas, velocidade de reprodução e checkpoints são escolhidos pelo jogador na tela de início. Os padrões são 3 vidas, velocidade 1,0, checkpoints ativados

Você pode colocar checkpoints, mas não pode obrigar ninguém a usá-los. E não pode proibir jogar na metade da velocidade

Projete com base nos padrões, mas não construa nada sobre o cálculo "é aqui que ele morre". Você está projetando uma sensação, não um castigo

## O loop

O jogador repete um único loop: jogar, morrer, tentar de novo. Um bom nível constrói todo o resto sobre ele, e o loop precisa ser:
- simples no começo, sem mecânicas difíceis logo de cara
- expansível, para que elementos novos cheguem aos poucos e ele não fique repetitivo
- recompensador, porque uma recompensa imediata pela ação certa mantém a motivação

## A curva: ensinar, testar, variar

1. Mostre o padrão de forma segura, em que errar é quase impossível
2. Exija-o de verdade
3. Mude uma variável - velocidade, direção, quantidade - e exija de novo

Se um padrão aparece pela primeira vez já na forma difícil, a culpa fica com o nível. O jogador morre e não entende o que se queria dele

A justiça também tem limite. "Levar pela mão" demais tira a graça tanto quanto a injustiça

## Memorização

Um nível que só pode ser superado de memória é um gênero legítimo. Mas isso precisa ser uma decisão, não um acidente

O limite é simples: depois de morrer, o jogador precisa entender exatamente o que memorizar. Se continua sem ficar claro depois da décima morte, não é memorização, é ruído

## Testar com os olhos de outra pessoa

Você não consegue julgar o próprio nível. Quando você publica, já passou pelo próprio trecho difícil duzentas vezes, e para você ele é fácil

> [!tip] Recomendação
> Dê o nível a alguém que o vê pela primeira vez e observe em silêncio. Não dê dicas. Um trecho em que a pessoa morre três vezes e pergunta o que se queria não é difícil, é confuso

## Comece com algo curto

Faça o primeiro nível com 1-2 minutos. O interesse acaba antes da música. Um nível de quatro minutos é quatro vezes o trabalho e dez vezes os motivos para parar

A seguir: [[1_readability-and-fairness|Legibilidade e justiça]], [[4_composition-and-camera|Composição e câmera]]
