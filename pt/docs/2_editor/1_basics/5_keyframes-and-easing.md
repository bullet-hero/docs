---
title: Quadros-chave e suavização
date: 2026-10-12
tags: [level_author]
---

# Quadros-chave e suavização

Um quadro-chave é um valor em um quadro de uma faixa, mais a suavização com que se chega a ele. Tudo em um nível que se move, muda de cor ou liga e desliga é uma lista de quadros-chave

As ideias básicas - [[3_how-the-editor-thinks]]. Cada campo do inspetor de quadros-chave - [[5_object-properties]]

## O que pode ser animado

Cada faixa tem os próprios quadros-chave, independentes das outras:

| Dono | Faixas |
|---|---|
| qualquer objeto | posição, rotação, escala, tamanho, âncoras, pivô |
| forma | cor, UV |
| texto | cor, tamanho da fonte, `{{ui:editor_dummy_text-11}}` (quanto do texto está escrito), `{{ui:editor_dummy_text-12}}` (quanto dele está escondido atrás da máscara) |
| câmera | posição, rotação, zoom, pivô, tremor |
| nível | fundo, tema, limite da tela, cada um dos 12 efeitos de pós-processamento |
| jogador | tamanho, velocidade, visibilidade, controle, colisão |

Um quadro-chave de cor de uma forma também pode ser um gradiente sobre o retângulo do objeto. O campo `{{ui:editor_keyframe-color_layout}}` dele escolhe a disposição: `{{ui:enum_color4-x4-key-type_value}}` (uma cor), `{{ui:enum_color4-x4-key-type_vertical}}` (de baixo para cima), `{{ui:enum_color4-x4-key-type_horizontal}}` (da esquerda para a direita) ou `{{ui:enum_color4-x4-key-type_bari-centrical}}` (uma cor em cada canto)

Um quadro-chave de tamanho da fonte é ou um único número, um tamanho fixo em unidades do mundo, ou um par de limites com `{{ui:field_common_auto-size}}` ativado. O texto é desenhado no `{{ui:field_common_max}}` do par e encolhe em direção ao `{{ui:field_common_min}}` até caber no retângulo dele

Os quadros-chave de um objeto são contados a partir do início do intervalo dele. Por isso mover o objeto no tempo leva junto toda a animação

A posição é definida em relação ao pai. Um quadro-chave armazena o próprio valor, não um incremento sobre o quadro-chave anterior

A visibilidade, o controle e a colisão do jogador estão ou ativados ou desativados. Esses quadros-chave não têm suavização: não há nada para misturar

O primeiro quadro-chave em uma faixa vazia do jogador não muda nada na tela: visibilidade, controle e colisão começam ativados, tamanho e velocidade começam nos valores habituais do jogador. Com o controle desativado, ou com o jogador oculto, não dá para controlar o jogador: o cursor some e nenhum clique ou toque é registrado. Um jogador oculto ainda pode ser atingido: só a colisão decide isso

## Texto: preenchimento e aparecimento

Duas faixas de texto escondem caracteres de formas diferentes. As duas recebem uma fração de 0 a 1 e contam os caracteres do texto

**`{{ui:editor_dummy_text-11}}`** é a fração do texto que está escrita: 0 - nada, 1 - tudo. Um caractere que não está escrito não é desenhado, por isso a linha fica mais curta. Uma faixa vazia escreve o texto inteiro. Cada quadro-chave define a direção:
- `{{ui:enum_text-fill-direction_forward}}` (o padrão) - a partir do primeiro caractere, como uma máquina de escrever
- `{{ui:enum_text-fill-direction_backward}}` - a partir do último caractere
- `{{ui:enum_text-fill-direction_from-center}}` - cresce a partir do meio
- `{{ui:enum_text-fill-direction_to-center}}` - cresce a partir das duas pontas e se encontra no meio

**`{{ui:editor_dummy_text-12}}`** é a fração dos caracteres escondidos atrás da máscara: 0 - todos visíveis, 1 - todos mascarados. Um caractere escondido mantém o lugar e é desenhado como um caractere de máscara, `{{v:text.appearing-mask-default}}` por padrão. A máscara é o campo `{{ui:editor_inspector-appearing_mask}}` do objeto de texto, e, com vários caracteres nele, cada caractere escondido pega um deles. Uma faixa vazia não esconde nada. Cada quadro-chave define o modo:
- `{{ui:enum_text-appearing-mode_random}}` (o padrão) - espalhado, mas com o mesmo espalhamento em toda partida. Um caractere escondido em 0,3 continua escondido em 0,6, por isso o texto se revela em vez de piscar
- `{{ui:enum_text-appearing-mode_forward}}` - os caracteres escondidos ficam no fim, o texto aparece a partir do começo
- `{{ui:enum_text-appearing-mode_backward}}` - os caracteres escondidos ficam no começo

Para digitar uma linha letra por letra, anime `{{ui:editor_dummy_text-11}}` de 0 a 1. Para fazê-la surgir do ruído, anime `{{ui:editor_dummy_text-12}}` de 1 a 0

## Conselhos

- Coloque quadros-chave só no que se move. Uma faixa sem quadros-chave assume o valor padrão
- Para uma mudança exatamente na batida, use `Constant`, por exemplo uma troca de tema no drop
- A rotação não se limita a uma volta: um quadro-chave em 0 grau e outro em 720 giram o objeto duas vezes. Em radianos, como o arquivo e o assistente de IA escrevem, isso é 0 e 12,566

## Entre dois quadros-chave

Antes do primeiro quadro-chave e depois do último, o valor fica parado.
Entre dois quadros-chave, o jogo pega a fração de tempo que passou, aplica a suavização a ela e mistura os dois valores

A fração é contada em tempo, não em quadros desenhados. Por isso a curva é a mesma a 30 e a 144 fps

**A suavização pertence ao quadro-chave posterior do par.** A suavização de um quadro-chave define o trecho que chega a ele vindo do anterior.
Por isso a suavização do primeiro quadro-chave de uma faixa nunca aparece. Um quadro-chave novo recebe `Linear`

O campo `{{ui:hint_editor_inspector_ease_header}}` abre a janela `{{ui:editor_search-title_ease}}`, onde cada suavização é desenhada como uma curva própria.
Você pode selecionar vários quadros-chave, mesmo em faixas diferentes, e mudá-los em um único passo de desfazer

## 29 suavizações

`Linear` é uma linha reta. `Constant` mantém o valor anterior e salta no quadro-chave

As outras 27 são nove famílias de três: `In`, `Out` e `InOut`. Por exemplo, `InSine`, `OutSine`, `InOutSine`

| Família | Forma |
|---|---|
| `Sine` | a curva mais suave |
| `Quad`, `Cubic`, `Quart`, `Quint` | potências 2, 3, 4 e 5 |
| `Expo` | exponencial |
| `Circ` | um quarto de círculo |
| `Back` | passa dos limites e volta |
| `Elastic` | oscila em torno do valor |

`In` começa devagar e termina rápido. `Out` começa rápido e se acomoda. `InOut` é lento nas duas pontas.
De `Sine` a `Expo`, cada família é mais acentuada que a anterior

> [!caution] Cuidado
> `Back` e `Elastic` saem dos limites: `Out` ultrapassa o alvo, `In` recua além do início. O colisor se move com o objeto. Por isso um projétil que deveria parar na borda de uma zona segura entra nela por alguns quadros

## Valores aleatórios

Um valor em um quadro-chave não precisa ser um único número:
- um número: `{{ui:field_common_value}}`, `{{ui:enum_color-type_random-min-max}}`, `{{ui:enum_float-type_random-min-max-step}}`
- um vetor (posição, escala e afins): `{{ui:field_common_value}}`, `{{ui:enum_vector-type_random-rect}}`, `{{ui:enum_vector-type_random-rect-step}}`, `{{ui:enum_vector-type_random-circle}}`, `{{ui:enum_color-type_random-lerp}}`, `{{ui:enum_vector-type_random-lerp-step}}`
- uma cor: `{{ui:field_common_value}}`, `{{ui:editor_events-timeline_track_theme}}`, `{{ui:enum_color-type_random-min-max}}`, `{{ui:enum_color-type_random-lerp}}`

`{{ui:enum_vector-type_random-rect}}` escolhe cada eixo separadamente. `{{ui:enum_color-type_random-lerp}}` escolhe um único número para todos os eixos, por isso o ponto cai na linha entre A e B.
As formas com passo arredondam o resultado para baixo até um múltiplo do passo. Um passo de 0 desliga a grade, e o valor se comporta como a forma sem passo.
Depois disso o quadro-chave é misturado como qualquer outro

A mesma semente dá o mesmo nível. O número aleatório é calculado a partir da semente, do quadro do quadro-chave, da camada, do quadro inicial do objeto, da faixa e do canal. Mais - [[8_determinism]]

A seguir: [[2_rhythm-and-structure|Ritmo e estrutura]], [[6_themes|Temas]]
