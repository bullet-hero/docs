---
title: Como um bot joga seu nível
date: 2026-10-02
tags: [level_author]
---

# Como um bot joga seu nível

Um bot joga o nível com os mesmos controles que você e verifica a legibilidade, não a dificuldade. Ele não garante que o nível possa ser concluído

Ele observa o que está voando, procura espaço livre e move o mesmo personagem que você.
Ele anda, dá dash, sofre dano e morre

O bot é escolhido antes de o nível começar, junto das vidas e da velocidade

## Um bot no editor

No editor, um bot controla o jogador de pré-visualização:
1. Abra `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_player_title}}`
2. Marque `{{ui:settings_game-editor-player_bot}}`
3. Ligue o jogador de pré-visualização na barra de ferramentas

O jogador de pré-visualização não tem escolha de bot, é sempre `{{ui:enum_bot-kind_reflex}}`. Só esse bot não precisa de nada preparado com antecedência.
Ele continua funcionando enquanto você edita o nível, em qualquer velocidade de reprodução, inclusive de trás para frente

Logo depois de você arrastar o indicador de reprodução, o bot joga pior por um momento: ele está aprendendo de novo o que vem pela frente

Enquanto você arrasta uma alça do gizmo ou digita em um campo de texto, o jogador de pré-visualização não obedece aos seus controles

**`{{ui:settings_game-editor-player_bot-debug}}`**, nas mesmas configurações, desenha sobre o nível. Vem desligado por padrão, e as três partes dele vêm ligadas, então assim que você o liga vê a imagem completa de uma vez:
- `{{ui:settings_game-editor-player_bot-debug-grid}}` - quanto espaço livre o bot acha que cada parte da tela tem. Vermelho é onde ele espera um impacto, e a cor desbota conforme o espaço aumenta. Nada é desenhado onde ele se considera seguro
- `{{ui:settings_game-editor-player_bot-debug-target}}` - o ponto para onde ele está indo. Um alvo que não se move significa que o bot está satisfeito, não travado
- `{{ui:settings_game-editor-player_bot-debug-reach}}` - até onde ele espera chegar: o anel interno andando, o externo com um dash. Ele nunca escolhe um alvo fora deles

Só `{{ui:enum_bot-kind_reflex}}` é desenhado. Ligue com a reprodução pausada, quando a imagem fica parada

**Uma partida completa com qualquer bot.** Nas configurações do nível, na aba `{{ui:settings_level-settings_play}}`, há a mesma lista `{{ui:settings_level-settings_bot}}` da tela do nível no menu: `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}`, `{{ui:enum_bot-kind_warm}}`. Isso inicia uma partida de verdade do nível, não o jogador de pré-visualização

## Como ler o resultado

Um bot verifica a legibilidade, não a dificuldade:
- o bot passa com calma por um trecho que é difícil para você. Então o trecho é bem legível, e o que falta para você é prática
- o bot é atingido no mesmo lugar várias vezes. Olhe esse lugar: normalmente é um perigo que não deixa espaço para escapar. Uma pessoa não vai lê-lo melhor

## O que um bot promete e o que não promete

**Um bot não garante que o nível possa ser concluído.** Ele é um jogador que não se cansa, não um jogador que não perde.
Se um trecho exige entrar certo em um padrão um segundo antes dele, o bot vai ser atingido. Isso não é um bug

> [!info] Vale saber
> Um bot não consegue trapacear, ele foi construído assim. Ele tem os mesmos controles que um jogador e nada além: a mesma velocidade, o mesmo dash, a mesma hitbox, o mesmo dano. Onde um jogador não consegue passar, o bot também não consegue

**Um bot pesa no dispositivo.** Ele procura espaço livre em cada quadro.
Em um dispositivo fraco, espere quedas na taxa de quadros. Em um nível pesado, os primeiros segundos vão ser os piores

## Um nível que venceu o bot

Os bots só melhoram em níveis que ainda não viram. Níveis que um bot já conclui não ensinam nada a ele

Seu nível venceu o bot? Envie:
1. Abra uma issue em [bullet-hero/releases](https://github.com/bullet-hero/releases/issues)
2. Escreva qual bot perdeu e onde
3. Anexe a pasta do nível

A seguir: [[1_readability-and-fairness|Legibilidade e justiça]], [[3_difficulty-curve|Dificuldade]]
