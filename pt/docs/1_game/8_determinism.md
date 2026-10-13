---
title: Determinismo
date: 2026-10-02
tags: [advanced_player]
---

# Determinismo

Um nível com a mesma semente roda igual em qualquer dispositivo e em qualquer taxa de quadros. A aleatoriedade dele é calculada a partir da semente, e as suas ações não afetam o nível

## Um nível é uma função do tempo

Um nível é construído sobre uma linha do tempo. Cada objeto vive em um intervalo de quadros e se move ao longo de quadros-chave

O nível não lê as suas ações. Por isso o quadro 1200 é igual quer você siga na partida, tenha morrido, esteja no meio de um dash ou tenha um bot jogando no seu lugar

A influência vai em um só sentido. Um nível pode mudar o tamanho do avatar, deixá-lo mais lento, tirar o controle ou desativar as colisões. Não existe canal de volta do avatar para o nível

Não existem gatilhos. Eles estão em discussão para versões futuras, mas nada foi decidido

Um nível roda em tempo real. A taxa de quadros só define com que frequência a tela é redesenhada. A mesma partida roda igual a 30 e a 144 quadros por segundo

## A semente

A semente é tirada do primeiro lugar em que está definida:

1. `{{ui:level_level-view_seed-value}}` na tela do nível (`{{ui:level_level-view_seed-randomize}}` escolhe uma nova, `{{ui:level_level-view_seed-clear}}` a remove)
2. a semente própria do nível, definida pelo autor
3. uma semente nova para esta partida

`0` significa "não definida". Por isso um nível comum pega uma semente nova a cada carregamento

A janela de resultado mostra a semente da partida, e o recorde a guarda. Assim uma partida de sorte pode ser repetida

## Como a aleatoriedade funciona

Um valor aleatório em um nível não vem de um gerador que lembra o próprio estado. Ele é calculado a partir do endereço dele:

`Hash(seed, keyframe frame, layer, start frame, track, channel)`

O mesmo endereço sempre dá o mesmo número. Em qualquer dispositivo e em qualquer ordem de cálculo. Cada parte do endereço é algo que o autor edita. Por isso a mesma disposição repete a mesma partida

## O que isso garante a você

- **O bot Warm** planeja um caminho pelo nível inteiro antes de a partida começar. Isso é possível porque é exatamente o nível para o qual ele planejou que vai rodar
- **O bot Reflex** constrói quadros à frente do atual e se esquiva com base neles
- **Voltar a um checkpoint** constrói de novo o quadro necessário em vez de desfazer qualquer coisa
- **O editor** constrói qualquer quadro do zero, por isso o arrasto pela linha do tempo é instantâneo
- **Recordes e estatísticas** significam a mesma coisa em qualquer dispositivo

## Limites conhecidos

O lado do nível é determinístico. O lado do avatar tem defeitos conhecidos que ainda não foram corrigidos:

- dois obstáculos atingem o avatar no mesmo quadro. Qual deles define a direção do empurrão pode variar entre partidas
- o relógio do avatar não é zerado quando o nível começa. Um dash pode durar um quadro a mais ou a menos, dependendo de quanto tempo o nível levou para carregar

Repetir a mesma partida de bot em uma mesma versão do jogo bateu até o último dígito quando foi medido. Então esses defeitos não aparecem em todo nível. Por causa deles, uma partida é reproduzível na prática, mas não garantida
