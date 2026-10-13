---
title: Como o editor funciona
date: 2026-10-12
tags: [level_author]
---

# Como o editor funciona

Objeto, quadro, intervalo, camada, pai, quadro-chave - as seis ideias em que todo o editor se apoia

Quando essas seis ideias ficam claras, o resto do editor se explica sozinho:

| Ideia | Em resumo |
|---|---|
| Objeto | uma forma (o que você vê) e um colisor (o que atinge), dois campos separados |
| Quadro | uma célula de tempo, não um instante |
| Intervalo | o tempo de vida de um objeto: um início e uma duração, sem incluir o fim |
| Camada | ordem de desenho, somada às camadas de todos os pais |
| Pai | passa aos filhos a própria transformação, o estado ativo e o tempo de vida |
| Quadro-chave | o valor de um campo em um quadro, o jogo leva o valor de um quadro-chave ao outro sozinho |

Uma palavra desconhecida - [[1_glossary]]

## Objeto

Um objeto é aquilo que é desenhado e aquilo que atinge. São dois campos diferentes: uma forma (o que você vê) e um colisor (o que atinge).
Um feixe que brilha mas nunca toca você é um objeto com forma e sem colisor. Uma parede invisível é o contrário

## Quadro e intervalo

Um quadro é uma célula de tempo, não um instante. O quadro 30 ocupa um trecho, não um ponto.
A linha do tempo conta a partir de um. Um nível de 900 quadros contém os quadros de 1 a 900. O número 901 é o limite final, não um quadro

Um intervalo é o tempo de vida de um objeto: um início e uma duração. O fim não faz parte do intervalo.
Por isso dois objetos colocados um logo após o outro não se sobrepõem em um quadro compartilhado

Mais - [[4_frames-and-time]]

## Camada e pai

Uma camada é a ordem de desenho. Ela é relativa: a camada de um objeto é somada às camadas de todos os pais dele

Uma camada mais alta é desenhada na frente. De duas formas na mesma camada resultante, a mais nova (o id mais alto) é desenhada atrás. Por isso a forma que precisa ficar por cima recebe uma camada mais alta

> [!caution] Cuidado
> Arrastar um objeto para baixo de outro pai muda a ordem de desenho dele mesmo que você nunca tenha mexido no número

Um pai passa aos filhos a própria transformação, o estado ativo e o tempo de vida.
O intervalo de um filho precisa ficar dentro do intervalo do pai

O editor nunca corta o que você escreveu. Ele mantém o seu valor e calcula o valor efetivo separadamente.
É por isso que encolher um pai é reversível: alargue-o de novo e o filho volta

## Quadro-chave

Um quadro-chave é o valor de um campo em um quadro. O jogo leva o valor de um quadro-chave ao outro sozinho.
Cada campo tem o próprio conjunto de quadros-chave: posição, rotação, escala, tamanho, âncoras e pivô

> [!info] Vale saber
> Um campo sem quadros-chave não está quebrado, ele assume o valor padrão. Não é preciso pôr quadros-chave em tudo só por organização

O que um quadro-chave armazena e como o valor viaja entre quadros-chave - [[5_keyframes-and-easing]]

## Coordenadas

Posições, tamanhos e distâncias ficam em unidades do mundo. O ponto (0, 0) é o centro da tela enquanto a câmera não tem quadros-chave próprios. O x cresce para a direita, o y cresce para cima

O zoom da câmera é a altura da área visível em unidades, {{v:camera.default-height}} por padrão. Por isso uma tela 16:9 mostra x de cerca de -{{v:camera.default-half-width}} a {{v:camera.default-half-width}} e y de -{{v:camera.default-half-height}} a {{v:camera.default-half-height}}. Uma tela mais larga ou mais estreita muda só a largura

Um quadro-chave de posição é relativo ao pai. É o deslocamento do pivô do objeto em relação ao ponto de âncora do pai, e ele gira e escala junto com o pai. Um objeto sem pai é posicionado em coordenadas do mundo. Um filho da câmera se move com a câmera

- **pivô** - o ponto do próprio retângulo do objeto que a posição coloca no lugar e em torno do qual a rotação e a escala agem. `(0.5, 0.5)`, o centro, por padrão
- **âncoras** - o ponto do retângulo do pai a partir do qual a posição é contada, de `(0, 0)` (canto inferior esquerdo) a `(1, 1)` (canto superior direito). O centro por padrão. Duas âncoras diferentes esticam o filho junto com o pai

A rotação gira no sentido anti-horário. O arquivo a armazena em radianos, e o assistente de IA também escreve radianos. O inspetor mostra graus por padrão, e a configuração do editor `{{ui:settings_game-editor_interface-rotation-unit}}` muda para radianos

A seguir: [[4_frames-and-time]], [[5_keyframes-and-easing]], [[1_readability-and-fairness]]
