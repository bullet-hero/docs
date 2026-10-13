---
title: Bots
date: 2026-10-02
tags: [player, advanced_player]
---

# Bots

Um bot joga um nível por você com os seus próprios controles. Ele observa o que está vindo, procura espaço livre e move o mesmo personagem que você: anda, dá dash, sofre dano e morre

**Um bot não garante a conclusão.** Ele não se cansa, mas pode perder. Se é preciso entrar certo em um padrão um segundo antes de ele chegar, o bot leva o impacto. Quando isso acontece, nada está quebrado

**Um bot pesa no dispositivo.** Procurar espaço livre é trabalho de verdade a cada quadro. Em um dispositivo fraco, conte com quedas de quadros. Em um nível pesado, os primeiros segundos são os piores

Para escolher um bot, use a condição `{{ui:menu_levelview_options-bot}}` na tela do nível: `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}` ou `{{ui:enum_bot-kind_warm}}`. Ele é escolhido para cada partida, como as vidas e a velocidade

> [!info] Vale saber
> Um bot não consegue trapacear, e isso vem de como ele é construído, não de uma promessa. Ele tem os mesmos controles que você e nada além: a mesma velocidade, o mesmo dash, a mesma hitbox, o mesmo dano. Ele não atravessa nada que você não pudesse atravessar

## Um nível venceu o bot?

Os bots melhoram com níveis que eles ainda não viram. Vale a pena mandar um nível assim

Abra uma issue em [bullet-hero/releases](https://github.com/bullet-hero/releases/issues). Escreva qual bot perdeu e onde, e anexe a pasta do nível

## Dois bots

A cada quadro, um bot dá um comando, igual a um teclado, e nada mais. Ele não tem acesso à posição do avatar, à vida dele nem ao estado do nível. Se o bot não responder em algum quadro, quem controla nesse quadro é o seu dispositivo

| | `{{ui:enum_bot-kind_reflex}}` | `{{ui:enum_bot-kind_warm}}` |
|---|---|---|
| O que ele sabe | os próximos 1,5 segundo, recalculados a cada quadro | o nível inteiro, calculado uma vez |
| Quando ele pesa no dispositivo | a cada quadro, enquanto joga | uma vez, antes da partida |
| O que ele consegue | desviar do que vê à frente | seguir um plano que nenhuma previsão encontraria |
| O que o derruba | um padrão em que era preciso entrar um segundo antes | um nível que mudou depois do cálculo |
| Como ele controla | por direção | por alvo |

O bot Warm busca dano zero. Ele paga por isso com uma etapa de carregamento a mais, `{{ui:root_loading_baking}}`. Ela pode durar dezenas de segundos

O `?` ao lado de `{{ui:menu_levelview_options-bot}}` avisa isso de antemão, com um parágrafo por bot. `{{ui:root_loading_cancel}}` interrompe o cálculo e passa a partida para você. A rota do bot Warm depende da semente, [[8_determinism]]

## Onde mais os bots jogam

- **O jogador de teste do editor**: `{{ui:settings_common_title}}` → `{{ui:settings_game-editor_title}}` → `{{ui:settings_game-editor-player_bot}}`. Lá só o bot Reflex joga: ele não precisa de nada preparado de antemão e aguenta o retrocesso. Mais - [[5_bot-playtest]]
- **O fundo do menu principal**: a arena atrás dos botões é um bot Reflex jogando ao vivo, sem previsão nenhuma

O bot faz parte das condições de um recorde. Por isso a partida de um bot nunca substitui o seu melhor resultado, [[10_statistics]]
