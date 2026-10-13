---
title: Preparar a faixa de áudio
date: 2026-10-01
tags: [level_author]
---

# Preparar a faixa de áudio

Converta a música para ogg: ela pesa 8-10 vezes menos que wav e, ao contrário do mp3, não adiciona silêncio ao início do arquivo. Além do ogg, só mp3 e wav carregam

## Formatos

`oga`, `mp2`, `aiff`, `flac` e os módulos de tracker `mod`, `xm`, `it`, `s3m` não são aceitos

> [!caution] Cuidado
> `flac` não carrega de jeito nenhum: o motor não o decodifica. Converta antes

> [!warning] Aviso
> Um codificador de `mp3` adiciona alguns milissegundos de silêncio ao início, e codificadores diferentes adicionam quantidades diferentes. Se a música for recodificada por outro codificador, toda a marcação de batidas se desloca

## Deslocamento

Mesmo em `ogg`, uma música quase nunca começa exatamente na primeira batida. É para isso que serve o deslocamento do segmento de batida.
Ele é definido em frações de quadro, por isso é mais fino que um quadro

A ordem é: primeiro o andamento, depois o deslocamento, e só então o conteúdo

## Volume

Normalize a música antes de colocá-la no nível. Uma normalização de pico a -1 dB é um padrão sensato

Um nível bem mais baixo que o seguinte parece um defeito do jogo, não da música

## Duração

A duração do nível e a duração da música são números diferentes, elas não precisam coincidir.
Um nível pode terminar antes da música. Assim dá para fazer um final com fade-out

## Várias faixas de áudio

Pode haver várias faixas de áudio. Cada uma tem a própria posição na linha do tempo, a própria velocidade, o próprio volume e a própria cadeia de efeitos

Efeitos: chorus, compressor, distorção, eco, flanger, filtros, normalização, equalizador, alteração de tom, reverberação

Um efeito em uma faixa de áudio é ouvido em todo lugar onde essa faixa toca, não só onde você queria

A seguir: [[3_where-to-get-resources]], [[2_rhythm-and-structure]]
