---
title: Áudio
date: 2026-10-02
tags: [level_author]
---

# Áudio

O som de uma faixa de áudio passa por uma cadeia de efeitos: são 11, da normalização e do compressor ao eco e à reverberação. A cadeia, a velocidade e o volume ficam no inspetor da faixa de áudio

## Inspetor da faixa de áudio

Mostra o clipe da faixa de áudio selecionada, a velocidade dela, o volume do fader e a cadeia de efeitos.
Os efeitos: passa-baixas, passa-altas, eco, reverberação, chorus, alteração de tom, distorção, flanger, compressor, normalização e um equalizador paramétrico

`{{ui:field_common_speed}}` e `{{ui:editor_inspector-audio_volume}}` são controles deslizantes, não campos de entrada. Assim os limites permitidos ficam visíveis

> [!caution] Cuidado
> **O volume aqui é um fader.** O volume com quadros-chave é uma faixa separada na linha do tempo local. Na reprodução os dois se multiplicam

Mais: [[2_preparing-the-track|Preparar a faixa de áudio]]

## Normalizar

Puxa o sinal o tempo todo em direção a um volume-alvo. Assim clipes de fontes diferentes soam igualmente altos sem ajuste manual.
Use-o se as faixas do nível não foram mixadas juntas

Ele atua no volume geral. A dinâmica dentro de uma faixa é alterada pelo [[7_audio#Compressor|Compressor]]

- `Lowest Volume` impede que ele puxe o silêncio e o ruído para cima até virarem chiado
- `Maximum Amp` limita o quanto ele pode amplificar

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve todos os campos ao valor padrão, `{{ui:field_common_mix-level}}` inclusive. O padrão dele é o piso de -80 dB, então a redefinição também desliga o efeito

Mais: [[2_preparing-the-track|Preparar a faixa de áudio]]

## Compressor

Abaixa as partes altas para que as baixas possam soar mais alto. Uma faixa comprimida é ouvida por baixo de todo o resto do nível e não distorce.
Ele costuma ser usado para consertar uma música que se perde atrás dos próprios efeitos

- `Threshold` - onde ele começa a atuar
- `Attack` e `Release` - a rapidez com que ele aperta e solta. Rápido demais e você corta os ataques ou ouve um bombeamento
- `Make Up Gain` devolve o volume que ele tirou

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve todos os campos ao valor padrão, `{{ui:field_common_mix-level}}` inclusive. O padrão dele é o piso de -80 dB, então a redefinição também desliga o efeito

Mais: [[2_preparing-the-track|Preparar a faixa de áudio]]

## Passa-baixas

Deixa passar os graves e corta tudo acima de `Cutoff Freq`. Soa como se viesse de baixo da água ou de trás de uma parede

Abaixe a frequência de corte: a faixa perde primeiro o ar, depois a clareza e, no fim, tudo menos o grave.
No topo da escala o filtro é quase transparente. A faixa soa igual ao arquivo

> [!tip] Dica
> A cadeia de efeitos pertence à **faixa** e não é animada com quadros-chave. Ela não pode mudar suavemente ao longo do tempo. Corte a faixa onde a mudança é necessária e configure as metades de forma diferente

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve todos os campos ao valor padrão, `{{ui:field_common_mix-level}}` inclusive. O padrão dele é o piso de -80 dB, então a redefinição também desliga o efeito

Mais: [[2_preparing-the-track|Preparar a faixa de áudio]]

## Passa-altas

O espelho do passa-baixas: deixa passar os agudos e corta tudo abaixo de `Cutoff Freq`

Aumente a frequência de corte: a faixa afina até soar como um alto-falante minúsculo ou uma ligação telefônica.
Ele costuma ser usado para deixar o som pequeno antes de tudo se abrir

> [!tip] Dica
> A cadeia de efeitos pertence à **faixa** e não é animada com quadros-chave. Ela não pode mudar suavemente ao longo do tempo. Corte a faixa onde a mudança é necessária e configure as metades de forma diferente

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve todos os campos ao valor padrão, `{{ui:field_common_mix-level}}` inclusive. O padrão dele é o piso de -80 dB, então a redefinição também desliga o efeito

Mais: [[2_preparing-the-track|Preparar a faixa de áudio]]

## EQ paramétrico

Uma banda paramétrica: reforça ou corta uma parte escolhida do espectro.
Ao contrário de [[7_audio#Passa-baixas|Passa-baixas]] e [[7_audio#Passa-altas|Passa-altas]], ele também pode adicionar. Por isso é usado para abrir espaço na mixagem, e não para criar um efeito

- `Center Freq` - onde a banda fica
- `Octave Range` - a largura da banda. Estreita para uma correção precisa, larga para colorir o som como um todo
- `Frequency Gain` abaixo de 1 corta, acima de 1 reforça

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve todos os campos ao valor padrão, `{{ui:field_common_mix-level}}` inclusive. O padrão dele é o piso de -80 dB, então a redefinição também desliga o efeito

Mais: [[2_preparing-the-track|Preparar a faixa de áudio]]

## Distorção

Corta a forma de onda. O som se enche de harmônicos que não tinha: sujo, saturado, agressivo.
O efeito mais simples daqui: um único controle, `Level` - o quanto o corte morde

Como efeito colateral, ela achata a dinâmica. Uma faixa muito distorcida perde as partes baixas.
Onde um trecho deve soar implacável, isso é útil. Onde não deve, é destrutivo

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve todos os campos ao valor padrão, `{{ui:field_common_mix-level}}` inclusive. O padrão dele é o piso de -80 dB, então a redefinição também desliga o efeito

Mais: [[2_preparing-the-track|Preparar a faixa de áudio]]

## Eco

Repete o sinal em intervalos de tempo iguais. Cada repetição é mais baixa que a anterior.
Um eco é rítmico, e as repetições podem ser contadas. É isso que o separa da cauda borrada da [[7_audio#Reverberação|Reverberação]]: você ouve cópias separadas, não uma sala

- `Delay` - a distância entre as cópias em milissegundos
- `Decay` - que parte de cada cópia passa para a próxima

Tire o atraso do andamento da música, e o eco vai cair na batida em vez de borrá-la

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve todos os campos ao valor padrão, `{{ui:field_common_mix-level}}` inclusive. O padrão dele é o piso de -80 dB, então a redefinição também desliga o efeito

Mais: [[2_preparing-the-track|Preparar a faixa de áudio]]

## Reverberação

Coloca a faixa em um espaço. Primeiro vêm as primeiras reflexões das paredes próximas, depois uma cauda que se apaga.
É o maior efeito daqui: os campos dele descrevem uma sala, não uma repetição. As repetições são trabalho do [[7_audio#Eco|Eco]]

O som principal é definido por três campos:
- `Decay Time` - o tamanho da sala
- `Room` - quanto dela se ouve
- `Room HF` - corte-o e as paredes soam macias e absorventes

O resto é ajuste fino. Passe a ele quando esses três campos estiverem certos

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve todos os campos ao valor padrão, `{{ui:field_common_mix-level}}` inclusive. O padrão dele é o piso de -80 dB, então a redefinição também desliga o efeito

Mais: [[2_preparing-the-track|Preparar a faixa de áudio]]

## Chorus

Sobrepõe ao sinal três cópias levemente atrasadas com afinação oscilante. Uma única fonte soa como várias.
O resultado é largura e corpo, não uma repetição. Os atrasos são curtos demais para serem ouvidos separadamente

As três cópias o diferenciam do [[7_audio#Flanger|Flanger]], em que uma única cópia varre o espectro

- `Rate` - a velocidade da oscilação
- `Depth` - a amplitude da oscilação
- `Feedback` - aumente-o e o som se aproxima de um flanger

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve todos os campos ao valor padrão, `{{ui:field_common_mix-level}}` inclusive. O padrão dele é o piso de -80 dB, então a redefinição também desliga o efeito

Mais: [[2_preparing-the-track|Preparar a faixa de áudio]]

## Flanger

Mistura ao sinal um atraso muito curto e oscilante dele mesmo. Os dois se anulam em frequências que se movem junto com o atraso.
Esse vale que se arrasta é o zumbido de motor a jato. O efeito vem da anulação, não de uma cópia

Ele é da mesma família do [[7_audio#Chorus|Chorus]]. Mas há uma única cópia e o atraso é mais curto, então você ouve uma varredura, não largura

O vale é mais fundo quando `Dry Mix` e `Wet Mix` têm valores próximos

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve todos os campos ao valor padrão, `{{ui:field_common_mix-level}}` inclusive. O padrão dele é o piso de -80 dB, então a redefinição também desliga o efeito

Mais: [[2_preparing-the-track|Preparar a faixa de áudio]]

## Alteração de tom

Muda a altura da faixa sem mudar a velocidade dela.
Esse é todo o sentido: o tempo do nível está ligado à música. Por isso a faixa não pode simplesmente ser reamostrada, como faz o campo `{{ui:field_common_speed}}` da própria faixa

- `Pitch` - um multiplicador. 1 não muda nada, 2 sobe uma oitava
- `FFT Size` e `Overlap` trocam qualidade por custo

Com uma alteração grande, o som ainda vai ser percebido como processado

> [!tip] Dica
> A cadeia de efeitos pertence à **faixa** e não é animada com quadros-chave. Ela não pode mudar suavemente ao longo do tempo. Corte a faixa onde a mudança é necessária e configure as metades de forma diferente

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve todos os campos ao valor padrão, `{{ui:field_common_mix-level}}` inclusive. O padrão dele é o piso de -80 dB, então a redefinição também desliga o efeito

Mais: [[2_preparing-the-track|Preparar a faixa de áudio]]
