---
title: Conquistas
date: 2026-10-17
tags: [player]
---

# Conquistas

As conquistas são desbloqueadas sozinhas a partir das suas estatísticas. Só contam níveis feitos por outras pessoas e só partidas jogadas de forma justa. A lista fica no menu principal, em `{{ui:menu_main_achievements-btn}}`

## A lista

`{{ui:menu_main_achievements-btn}}` no menu principal abre todas as conquistas da sua versão, em grupos. Uma bloqueada mostra quanto falta, uma desbloqueada mostra o dia em que foi desbloqueada. Uma conquista secreta aparece como `{{ui:menu_achievements_hidden_name}}` até ser desbloqueada

## O que conta

**Uma partida justa** é aquela em que:

- nenhum bot joga
- as colisões estão ligadas
- a velocidade é `{{v:achievements.fair-min-speed}}` ou maior
- você tem vidas: uma partida em `{{ui:menu_levelview_options-lifes_option-zen}}` só conta onde uma conquista pede isso

Checkpoints são permitidos. Uma partida iniciada pelo editor nunca conta, ela também não define recorde - [[10_statistics]]

**Não ser o seu próprio nível.** Um nível que você abriu no editor neste dispositivo é seu. Concluí-lo só conta para a conquista de testar o seu próprio nível. Níveis incluídos, níveis do Workshop e níveis de amigos contam

## Onde fica salvo

`stats/achievements.json`, ao lado das estatísticas. O arquivo só lembra quando cada conquista foi desbloqueada. Se uma conquista está desbloqueada é decidido toda vez a partir das estatísticas, então o arquivo não pode ser perdido: apague-o e, na próxima vez que abrir o jogo, tudo o que você conquistou volta, com a data daquele dia

Limpar as estatísticas nas configurações mantém as suas conquistas. A transferência de perfil e o Steam Cloud levam o arquivo: dois dispositivos ficam com todas as conquistas desbloqueadas em qualquer um deles - [[14_profile-transfer]]

## Steam

Numa versão Steam cada conquista também é desbloqueada no Steam, e o Steam mostra a própria notificação. O registro do Steam vence: uma conquista que o Steam tem é desbloqueada no jogo com a data do Steam. Uma que o jogo tem e o Steam não é desbloqueada de novo se as suas estatísticas ainda a justificarem

## Google Play

Na versão do Google Play cada conquista também é desbloqueada no Google Play Games quando você entra na sua conta, e o Google Play Games mostra a própria notificação. O registro dele vence do mesmo jeito que o do Steam. Sem entrar na conta, as conquistas ficam só no jogo

As outras versões, e a do Google Play sem entrar na conta, mostram a notificação do próprio jogo no topo da tela
