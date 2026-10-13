---
title: Dispositivos móveis
date: 2026-10-02
tags: [level_author]
---

# Dispositivos móveis

No celular o dedo cobre a tela, e o sistema ocupa as bordas. Mantenha o que importa longe das bordas e teste o nível em um celular fraco: a translucidez de tela cheia é o que pesa nele primeiro

Os celulares são um alvo tanto quanto o PC.
Um nível que roda só no PC está feito pela metade

## Um dedo no lugar do mouse

**Um dedo cobre a tela.** Um mouse é um ponto, um dedo é uma mancha que esconde tudo embaixo dela.
Não construa um padrão que exija olhar exatamente onde o jogador está. No PC funciona, no celular é um ponto cego

**O controle é diferente.** No PC, o cursor define o alvo, e o personagem se move até ele. No celular a precisão é menor, e um dedo tem mais inércia.
Uma brecha que com o mouse se passa de primeira vira um teste à parte no celular

**Faça uma brecha estreita ser curta no tempo,** não estreita na largura

## Bordas e formato da tela

> [!caution] Cuidado
> As bordas pertencem ao sistema: o recorte da câmera, os cantos arredondados, os gestos de navegação. A interface do jogo evita a área não segura, o conteúdo do nível não. Mantenha o que importa longe das bordas, principalmente da superior

**Proporção da tela.** Um celular tem cerca de 20:9, bem mais estreito e comprido do que a tela em que você trabalha.
Pelo menos uma vez, veja o nível no simulador de dispositivos nesse formato antes de considerá-lo pronto

> [!caution] Cuidado
> O simulador de dispositivos mostra proporções e recortes, mas não diz nada sobre desempenho. Uma partida em um dispositivo fraco de verdade vale mais que qualquer raciocínio

## O que pesa primeiro no celular

Em ordem:
1. Translucidez de tela cheia em várias camadas
2. Pós-processamento, o Bloom acima de tudo. O custo dele cresce com a resolução, não com o número de objetos
3. Texturas grandes. Uma imagem de 4096 ocupa 64 MB de memória antes de qualquer coisa ser desenhada. Um quarto disso só se as configurações do próprio jogador a comprimirem
4. Efeitos com muitas partículas
5. E só depois o número de formas

## Antialiasing

O antialiasing é uma configuração do jogador, não do nível.
Mas ele explica por que o mesmo nível se comporta de forma diferente em dois celulares parecidos:
- `{{ui:enum_anti-aliasing-type_msaa}}` é calculado por amostra. O custo dele cresce com o overdraw translúcido, exatamente onde um celular fraco já sofre
- `{{ui:enum_anti-aliasing-type_fxaa}}` é uma única passada pela tela, o custo dele não depende de nada

A seguir: [[4_composition-and-camera|Composição e câmera]], [[1_level-budget|Orçamento do nível]]
