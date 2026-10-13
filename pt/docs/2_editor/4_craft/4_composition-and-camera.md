---
title: Composição e câmera
date: 2026-10-02
tags: [level_author]
---

# Composição e câmera

Mantenha o conteúdo importante longe da borda: outras telas a põem em outro lugar, e o recorte do celular pode cobrir um projétil. Tremor serve para um compasso, giro rápido e zoom brusco dão enjoo

## Cada tela é diferente

O nível é montado em um monitor 16:9. Em um celular 20:9 ele mostra mais na largura e menos na altura, em um tablet 4:3 é o contrário. Um objeto que ficava exatamente na borda acaba ou bem dentro do enquadramento, ou fora dele

**A faixa `{{ui:editor_events-timeline_track_screen-limit}}`** define como a área visível é limitada:
- de jeito nenhum
- uma proporção fixa
- uma gama de proporções

A fixa é a mais previsível. Todo mundo vê exatamente o que você viu, mas outras telas ganham barras nas bordas. Escolha de propósito. "De jeito nenhum" também é uma escolha, e significa que você não sabe o que o jogador vai ver. Um nível novo vazio ou um nível criado a partir de um arquivo de áudio já começa com um quadro-chave fixo de 16:9 no primeiro quadro, a menos que você desmarque `Pin Screen Aspect` ao criá-lo

> [!caution] Cuidado
> A interface do jogo se afasta da área insegura da tela, o conteúdo do nível não. A câmera enquadra o nível em relação à tela inteira, então o recorte de um celular pode cobrir um projétil. Mantenha o conteúdo importante longe da borda

## A câmera é uma ferramenta

A câmera não é um pano de fundo. Ela tem faixas de quadros-chave: `{{ui:editor_dummy_text-15}}`, `{{ui:editor_dummy_text-16}}`, `{{ui:editor_dummy_text-17}}`, `{{ui:editor_dummy_text-18}}`, `{{ui:editor_dummy_text-19}}`

Uma rotação de 15 graus torna difícil um padrão simples sem um único objeto novo. Ela quebra todas as direções a que o jogador tinha se acostumado

Esse poder também joga contra você. A câmera pode tornar um nível impossível de passar, e você não vai notar, porque sabe para onde olhar

> [!warning] Aviso
> Giro rápido, tremor constante e zoom brusco tornam um nível fisicamente impossível de terminar. Não pela dificuldade, mas por como o jogador se sente. Tremor serve para um compasso em um drop e é insuportável por um minuto

## Camadas

A ordem de desenho é relativa: a camada de um objeto é somada às camadas de todos os pais dele. Se você arrastar um objeto para outro pai, muda o que é desenhado sobre o quê. Mesmo que o número da camada nunca tenha sido mexido

Reserve números de camada diferentes para a decoração e para o perigo. Assim a decoração não vai cobrir um projétil por acidente

## Legibilidade vale mais que beleza

Um jogador que não viu um projétil por causa da decoração é erro seu, não dele. Quando precisar escolher, corte a decoração

A seguir: [[2_mobile-devices|Dispositivos móveis]], [[1_readability-and-fairness|Legibilidade e justiça]]
