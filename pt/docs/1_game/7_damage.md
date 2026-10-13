---
title: Dano e vidas
date: 2026-10-02
tags: [advanced_player]
---

# Dano e vidas

Cada impacto custa uma vida, empurra o avatar por {{v:avatar.knockback-time}} s e dá {{v:avatar.damage-timeout}} s de invulnerabilidade. Por padrão, uma morte volta o nível ao último checkpoint e restaura as vidas

## Um impacto em três etapas

1. **O empurrão, `{{v:avatar.knockback-time}}` s.** O impacto empurra você para longe da origem dele a `{{v:avatar.knockback-speed}}` unidades por segundo. Isso dá cerca de {{v:avatar.knockback-distance}} unidades, um dash inteiro, três quartos da altura da tela padrão. Os comandos não são aceitos durante ele. Não dá para sair do empurrão com um dash: o empurrão se sobrepõe a tudo
2. **O controle volta** depois desses {{v:avatar.knockback-time}} s
3. **Nada pode atingir você** durante `{{v:avatar.damage-timeout}}` s inteiros a partir do momento do impacto. Todo impacto dentro desse segundo é ignorado

Se você estiver exatamente em cima da origem do impacto, não há para onde empurrar. Aí não há empurrão nenhum

Nada atinge você também durante o aparecimento (`{{v:avatar.spawn-time}}` s) e durante os `{{v:avatar.dash-invulnerability}}` s de proteção do dash, [[6_avatar]]

> [!info] Vale saber
> Ficar dentro de uma zona de perigo custa uma vida, não dez. Um empurrão para dentro de uma segunda zona de perigo também dá para sobreviver. Uma rajada densa parece morte instantânea, mas muitas vezes custa menos que um único projétil que chega bem no fim do segundo de proteção

## Vidas

O número de vidas é escolhido na tela do nível: `{{ui:menu_levelview_options-lifes_option-zen}}`, `{{ui:menu_levelview_options-lifes_option-one}}`, `{{ui:menu_levelview_options-lifes_option-three}}` ou `{{ui:menu_levelview_options-lifes_option-custom}}` até 16, [[2_playing-levels]]

Cada impacto custa uma vida. Um impacto que leva a última é uma morte. `{{ui:menu_levelview_options-lifes_option-zen}}` reage aos impactos como qualquer outra partida - o empurrão, o anel de escudo, a explosão de partículas e o segundo de proteção funcionam normalmente, e o impacto conta nas estatísticas - mas nenhuma vida é gasta, então a partida nunca termina

As suas vidas aparecem no anel de pontos em volta do avatar: um ponto aceso é uma vida de reserva, um apagado é uma vida gasta. A janela de resultado mostra `{{ui:game_game-result_hits}}` e `{{ui:game_game-result_lives-left}}`

## O que uma morte faz

Por padrão, uma morte não termina a partida:

1. O relógio do nível para suavemente ao longo de `{{v:checkpoint.rewind-time}}` s de tempo real. A música cai junto com ele
2. O nível volta ao último checkpoint alcançado. As vidas são restauradas
3. O relógio acelera suavemente de volta à velocidade da partida ao longo de mais `{{v:checkpoint.rewind-time}}` s. Nada pode atingir você durante a aceleração, senão um checkpoint ao lado de um ponto perigoso levaria todas as suas vidas no primeiro segundo

A pausa também interrompe essa aceleração

Se `Checkpoints` estiver desativado na tela do nível, a volta é para o início do nível

Para que uma morte abra a janela de resultado, ative `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_open-menu-on-lose}}`. A reprodução então para. Nessa janela, `{{ui:game_game-result_restart-checkpoint}}` começa uma nova tentativa a partir do checkpoint alcançado

## Checkpoints

Os checkpoints são colocados pelo autor do nível. Se eles contam ou não, quem decide é você, com a opção `Checkpoints`

O checkpoint alcançado é o último que está na posição atual do nível ou antes dela. Por isso voltar a ele não desfaz nada, só volta no tempo

O autor pode fazer um checkpoint restaurar a vida. Aí, ao passar por ele, as suas vidas são restauradas uma vez, bem no meio da partida

A barra de progresso na parte de baixo da tela tem uma marca em cada checkpoint. A barra é ativada em `{{ui:settings_interface_label}}` → `{{ui:settings_interface_show-game-progress}}`

Os recordes com e sem checkpoints são guardados separadamente, [[10_statistics]]

## Sem colisão

`{{ui:menu_levelview_options-no-collision_title}}` é uma opção separada de `{{ui:menu_levelview_options-lifes_option-zen}}`, ao lado de `Checkpoints` na tela do nível e no painel de execução do editor. Ative-a e o avatar atravessa tudo: nada mais pode tocá-lo

Uma partida `{{ui:menu_levelview_options-no-collision_title}}` tem recordes próprios, separados de `{{ui:menu_levelview_options-lifes_option-zen}}` e das partidas normais, e a janela de resultado a marca adicionando `· Sem colisão` ao valor de `{{ui:menu_levelview_options-lifes_title}}`, [[10_statistics]]
