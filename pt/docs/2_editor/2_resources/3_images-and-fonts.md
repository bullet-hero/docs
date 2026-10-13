---
title: Imagens e fontes
date: 2026-10-02
tags: [level_author]
---

# Imagens e fontes

Se uma forma resolve, use uma forma: sem arquivo, sem custo de memória, sem questão de direitos. Faça a imagem do tamanho do lugar dela na tela, até {{v:texture.mobile-max-side}} no celular e {{v:texture.desktop-max-side}} no geral

Arredonde o tamanho da imagem para cima até uma potência de dois

## Formatos e tamanho

Carrega tudo o que o motor consegue decodificar a partir dos bytes de um arquivo. Na prática, isso é `png` e `jpg`

O jogo não limita o tamanho do arquivo, o hardware limita:

| Dispositivo | Maior lado |
|---|---|
| Android, garantido | 4096 |
| Android, normalmente | 8192-16384 |
| computador de mesa | até 32768 |

## Memória

**O limite real é a memória.** Na memória, uma imagem é armazenada como pixels brutos, não importa quanto o arquivo pese.
Um `png` ocupa 4 bytes por pixel. Um `jpg` ocupa 3, porque não tem transparência

| Tamanho | Memória (`png`) |
|---|---|
| 512 por 512 | 1 MB |
| 1024 por 1024 | 4 MB |
| 2048 por 2048 | 16 MB |
| 4096 por 4096 | 64 MB |
| 8192 por 8192 | 256 MB |

> [!caution] Cuidado
> Uma textura de 8192 é um quarto de gigabyte para uma única imagem. Em um celular isso não deixa o jogo lento, faz o jogo fechar

## O que o jogador decide

Três itens das configurações de gráficos de cada jogador decidem quanta memória uma imagem ocupa:
- se as imagens são comprimidas ao carregar. A compressão divide os números acima por 4-8
- o maior lado de uma imagem na memória. Metade do lado - um quarto da memória
- se mipmaps são gerados, cópias reduzidas para desenhar em tamanho pequeno

Um celular comprime as imagens e as limita a {{v:texture.mobile-max-side}} por padrão. Um computador de mesa mantém a imagem inteira e a limita a {{v:texture.desktop-max-side}}

**A sua parte são os campos da imagem, antes de tudo o que ela representa.** Eles ficam ao lado da imagem na lista de recursos.
Uma fotografia é o que melhor resiste à redução e à compressão. Um desenho com bordas duras resiste pior

`{{ui:enum_texture-kind_pixel-art}}` nunca recebe mipmaps, não importa o que o dispositivo preferiria. Também começa sem compressão e com pixels nítidos, e os campos `{{ui:level_resources_texture-compression}}` e `{{ui:level_resources_texture-sampling}}` podem mudar isso

## Mipmaps

Os mipmaps impedem que uma imagem pequena cintile. São cópias reduzidas desenhadas no lugar da imagem inteira enquanto ela aparece pequena na tela.
Eles custam um terço a mais de memória

Sem mipmaps, uma imagem reduzida não fica lisa, ela ondula. Um jogador pode desativá-los, e `{{ui:enum_texture-kind_pixel-art}}` nunca os recebe

Uma imagem de 4096 que ocupa 200 pixels na tela custa 256 vezes a memória da mesma imagem reduzida para 256 com antecedência

## Formas antes de imagens

Uma forma é mais barata que uma imagem em tudo: sem arquivo, sem memória, sem questão de direitos.
As formas integradas são geometria de verdade, não uma imagem sobre um retângulo. Elas não têm margens transparentes que são desenhadas e descartadas

Isso aparece no celular. Em um chip móvel intermediário, uma cena de 1000 objetos gasta 95-97% do tempo da GPU sombreando pixels.
Uma forma cobre 29,4% do próprio retângulo. O resto de um quad com textura é desperdício transparente

Uma imagem é necessária quando você precisa exatamente de uma figura: um logotipo, uma fotografia, arte desenhada à mão.
Para uma forma geométrica, use uma forma. Se a que você precisa não existe, desenhe-a no `{{ui:hint_level_shape-editor_header}}`

## Fontes

As fontes carregam como `ttf`, `otf`, `ttc`. Sem fonte própria, o texto é desenhado com o que o sistema tiver, e isso muda de um dispositivo para outro

O `{{ui:settings_level-settings_fontcache}}` é o conjunto de caracteres preparados com antecedência para o desenho. Um gerador o reconstrói a partir do texto que o nível contém.
Execute o gerador quando o texto parar de mudar

A seguir: [[1_level-budget]], [[2_mobile-devices]]
