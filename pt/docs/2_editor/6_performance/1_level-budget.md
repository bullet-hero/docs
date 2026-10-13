---
title: Orçamento do nível
date: 2026-10-01
tags: [level_author]
---

# Orçamento do nível

Um celular aguenta com folga cerca de 1000 formas em um quadro, um PC fraco 5000-10000. O overdraw custa mais que a quantidade: coisas translúcidas sobre a tela inteira, camada sobre camada

## Quantas formas um dispositivo aguenta

O que conta são as **formas** vivas ao mesmo tempo em um quadro. Os números são aproximados, mas a ordem de grandeza está certa

| Dispositivo | Com folga | Limite do jogável |
|---|---|---|
| Celular | 1000 | 2000 |
| PC fraco | 5000-10000 | 20000-40000 |
| PC médio (pela pesquisa da Steam) | 50000 | 100000 |

Teste no dispositivo mais fraco que estiver ao seu alcance.
No seu próprio PC tudo vai rodar bem, e isso não quer dizer nada

## Texto e efeitos

Texto e efeitos também são contados em formas

**Texto:** de 2 a 100 formas por objeto de texto. O custo depende da complexidade da fonte, do número de caracteres, do número de estilos e de o texto ser animado ou não

**Efeito:** 10 formas pelo próprio objeto mais 0,1 forma por partícula. Um efeito com mil partículas dá cerca de 110 formas

## Overdraw

**O que custa caro não é a quantidade, mas o overdraw.** É quando o mesmo pixel é pintado de novo e de novo

O que decorre disso:
- um único preenchimento translúcido sobre a tela inteira custa mais que cem projéteis
- camadas de decoração translúcida umas sobre as outras são a coisa mais cara que dá para construir
- se o nível estiver lento, procure o que cobre a tela inteira em vez de contar objetos

> [!info] Vale saber
> Em um chip móvel médio, uma cena de 1000 objetos com 60-70x de sobreposição gasta 95-97 por cento do tempo da GPU pintando pixels. Mil formas pequenas espalhadas pela tela são mais baratas que dez formas translúcidas de tela cheia umas sobre as outras

## Opaco e translúcido

Uma forma tem uma escolha de caminho de desenho: `Auto`, `Opaco`, `Transparente`.
O caminho opaco é mais barato: a GPU descarta com antecedência os pixels cobertos

`Auto` decide sozinho, uma vez no carregamento. A condição rígida dele é nunca mudar a aparência do nível.
Tudo o que não pode ser provado opaco vira translúcido

> [!warning] Aviso
> Defina o caminho à mão só se você sabe exatamente o que está fazendo. Um objeto declarado opaco que não é opaco não vai ficar mais rápido, vai ficar com a aparência errada

## Indicação de capacidade

Ao salvar, o nível registra quantos objetos o quadro mais pesado dele precisou.
Isso é uma indicação para o carregador, não um limite. Um gerador a recalcula

A seguir: [[2_mobile-devices|Dispositivos móveis]], [[3_images-and-fonts|Imagens e fontes]]
