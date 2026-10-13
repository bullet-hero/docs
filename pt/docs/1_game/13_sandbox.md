---
title: Sandbox e tutorial
date: 2026-10-02
tags: [player]
---

# Sandbox e tutorial

O sandbox é uma arena do menu principal onde você pode mover o avatar, lançar contra si mesmo qualquer um dos seis ataques e fazer o tutorial de seis passos. Não é preciso nenhum nível

Na primeira execução, o jogo oferece o tutorial uma vez: `{{ui:menu_tutorial-offer_confirm}}` abre o sandbox no tutorial, `{{ui:menu_tutorial-offer_cancel}}` fecha a oferta de vez. O sandbox em si continua no menu de qualquer jeito

## O painel

O sandbox tem um painel à esquerda. Clique na alça dele para recolher o painel, ou arraste a alça para deixar o painel mais largo ou mais estreito. O painel tem cinco abas:

| Aba | O que faz |
|---|---|
| `{{ui:sandbox_tab_home}}` | o que é o sandbox e o que cada aba faz |
| `{{ui:sandbox_tab_tutorial}}` | os passos do tutorial e o que fazer agora |
| `{{ui:sandbox_tab_controls}}` | o modo do dispositivo com que você está controlando agora, o interruptor do sensor de movimento e um caminho para todas as configurações de controle |
| `{{ui:sandbox_tab_attacks}}` | lança qualquer um dos seis ataques à mão ou deixa as ondas virem sozinhas |
| `{{ui:sandbox_tab_game}}` | as vidas, a velocidade dos ataques, o bot e a câmera livre |

`{{ui:settings_common_title}}` abre as configurações do jogo por cima do sandbox. `{{ui:sandbox_panel_exit}}` volta para o menu principal

## Pausa

O botão de pausa fica no canto superior direito da tela. `Esc` também abre a pausa em vez de sair do sandbox. A pausa para tudo, como em um nível: o avatar, os ataques e o tutorial. A janela de pausa tem `{{ui:root_error_continue}}`, `{{ui:settings_common_title}}` e `{{ui:game_game-result_back-to-menu}}`

## Tutorial

Seis passos, em ordem:

1. `{{ui:sandbox_tutorial_move_title}}` - percorra mais ou menos a largura da tela
2. `{{ui:sandbox_tutorial_dash_title}}` - dê dash três vezes
3. `{{ui:sandbox_tutorial_dodge_title}}` - aguente 10 segundos sob rajadas desaceleradas sem levar um impacto. Um impacto recomeça a contagem
4. `{{ui:sandbox_tutorial_dash-through_title}}` - o anel cresce além das bordas da tela, então a única saída é um dash através da borda dele. É preciso passar por dois anéis - um anel que falhou não anula um que já foi passado. Nada atinge você durante um dash
5. `{{ui:sandbox_tutorial_choose-mode_title}}` - experimente os modos na aba `{{ui:sandbox_tab_controls}}` e toque em `{{ui:sandbox_tutorial_confirm-mode}}`
6. `{{ui:sandbox_tutorial_done_title}}` - `{{ui:sandbox_tutorial_play-level}}` começa o nível do tutorial

Enquanto um passo é jogado na arena, o painel se recolhe e o passo aparece como um cartão pequeno no topo da tela. Os toques atravessam o cartão. A alça continua abrindo o painel. Nos passos `{{ui:sandbox_tutorial_choose-mode_title}}` e `{{ui:sandbox_tutorial_done_title}}`, o painel abre sozinho, na aba `{{ui:sandbox_tab_tutorial}}`

Um impacto ou uma morte reinicia só o passo em que aconteceu, não o tutorial inteiro, e o passo fica vermelho até ser concluído. Os passos concluídos ficam verdes

Clicar em um passo da lista começa esse passo, mesmo um já concluído. Depois que um passo é concluído, o tutorial segue para o próximo ainda não concluído. O tutorial só conta como concluído quando todos os passos são concluídos - é aí também que ele é gravado nas estatísticas. `{{ui:sandbox_tutorial_restart}}`, na mesma aba, recomeça o tutorial a qualquer momento

> [!warning] Aviso
> Com `{{ui:sandbox_game_immortal}}` na aba `{{ui:sandbox_tab_game}}`, os impactos não são contados de jeito nenhum, então os passos `{{ui:sandbox_tutorial_dodge_title}}` e `{{ui:sandbox_tutorial_dash-through_title}}` também não os veem. Deixe algumas vidas enquanto faz o tutorial

## Controles

Os modos mudam para o dispositivo que está controlando agora e são salvos na hora. O sensor de movimento não tem o modo `{{ui:enum_control-mode_relative}}`. O que cada modo significa - [[3_controls#Modos de controle]]

## Ataques e jogo

- `{{ui:sandbox_attacks_auto}}` lança ondas aleatórias com um intervalo de `{{ui:sandbox_attacks_gap}}`, como o fundo do menu principal
- `{{ui:sandbox_attacks_clear}}` tira todos os ataques da tela
- `{{ui:sandbox_game_speed}}` desacelera ou acelera só os ataques. O avatar sempre se move na própria velocidade
- Vidas: `{{ui:sandbox_game_immortal}}`, 1, 3 ou 5. Quando elas acabam, voltam, e o sandbox não termina
- `{{ui:sandbox_game_bot}}` passa o avatar para o mesmo bot que joga no fundo do menu principal
- `{{ui:sandbox_game_free-camera}}` deixa você olhar além das bordas da tela: mova a vista com o botão do meio do mouse ou com dois dedos, e dê zoom com a roda ou com um movimento de pinça. A moldura azul mostra o que a câmera do nível vê, e `{{ui:sandbox_camera_back}}` leva a vista de volta para ela. Os controles, o dash e os ataques funcionam do mesmo jeito que sem ela
- Uma morte acontece como em um nível: os ataques desaceleram e somem, e o avatar aparece no centro com todas as vidas
