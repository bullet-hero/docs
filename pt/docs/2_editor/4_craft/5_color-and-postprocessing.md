---
title: "Cor, temas e pós-processamento"
date: 2026-10-02
tags: [level_author]
---

# Cor, temas e pós-processamento

Passe a cor do conteúdo por uma referência ao tema e deixe as cores literais para o que é realmente único. Ative o pós-processamento em um pico e desative de novo, senão os projéteis perdem as bordas

## Referências ao tema e cores literais

Uma cor pode ser definida de dois jeitos:
- **uma cor literal** - um valor digitado direto no objeto
- **uma referência ao tema** - "pegue tal slot do tema ativo". Qual tema está ativo é definido por uma faixa de quadros-chave

A diferença aparece na segunda passada. Com referências, mudar a paleta é uma edição no tema. Com literais, é uma edição em cada objeto

O fundo também pega a cor do tema. Como funcionam os slots e os quadros-chave de tema - [[6_themes]]

> [!caution] Cuidado
> Verifique o contraste em cada tema, não só naquele em que você trabalhou. Um nível que troca de tema no drop precisa continuar legível nos dois. Projéteis escuros que se leem perfeitamente em um tema claro somem em um escuro

## Pós-processamento

O conjunto padrão do URP mais dois efeitos de glitch. Tudo funciona por quadros-chave, então cada parâmetro pode ser animado

> [!caution] Cuidado
> Este é o caminho mais rápido para um nível que ninguém consegue jogar. Bloom no limite transforma qualquer objeto claro em uma mancha, e o projétil perde a borda. A aberração cromática separa as bordas. Um glitch mais longo que um compasso é interferência, não estilo. O bloom não tem limiar: cada pixel brilha, então um fundo escuro clareia em direção ao cinza à medida que a intensidade sobe

Três regras mantêm o pós-processamento do lado do estilo:
- ative um efeito em um pico e desative de novo, não o deixe como pano de fundo
- não ative um efeito que prejudique a legibilidade dos projéteis onde é preciso desviar deles
- precisou apertar os olhos depois de ativar um efeito? Desative. O jogador não vai apertar os olhos, ele vai desistir

## Antialiasing

O antialiasing é uma configuração do jogador, não sua. Um nível que só fica certo em um modo não fica certo para todos

| Modo | O que faz |
|---|---|
| `{{ui:enum_anti-aliasing-type_msaa}}` | o padrão. Alisa exatamente as bordas da geometria, e cada forma é geometria real |
| `{{ui:enum_anti-aliasing-type_fxaa}}` | custa uma passada sobre a tela, não importa o quanto o nível desenhe sobre si mesmo |
| `TAA`, `STP` | não são oferecidos: deixam um rastro atrás de objetos rápidos, e um rastro atrás de um projétil torna o nível mais difícil de ler |

A seguir: [[1_readability-and-fairness|Legibilidade e justiça]], [[1_level-budget|Orçamento do nível]]
