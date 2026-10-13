---
title: Painéis
date: 2026-10-02
tags: [level_author]
---

# Painéis

A hierarquia, os inspetores e as linhas do tempo ficam acoplados ao redor do viewport. Um clique na alça da borda de um painel o abre ou fecha, um arrasto muda a largura dele

## Três painéis

O viewport fica no meio, e três painéis ficam acoplados ao redor dele:
- o painel esquerdo guarda a hierarquia
- o painel direito guarda os inspetores
- o painel inferior guarda as linhas do tempo

Uma aba do painel direito sem nada para mostrar fica oculta. Mais - [[5_object-properties]]

## Alça do painel

Cada painel tem uma alça na borda:
- um clique abre ou fecha o painel
- um arrasto muda o tamanho dele. Um único movimento pode puxar um painel fechado até qualquer largura

A seta na alça mostra o estado do painel. Em um painel fechado ela aponta para um lado, em um painel aberto ela fica girada meia volta, em qualquer largura. Uma seta girada só em parte significa que um arrasto está em andamento

Um clique abre o painel com uma animação, e os atalhos também: `Ctrl+Left`, `Ctrl+Right` e `Ctrl+Down`. Mais - [[3_speed-and-shortcuts]]

## Largura

Um painel ou está fechado, ou fica em algum ponto entre a largura mínima e a máxima. A largura mínima também é a normal: é o espaço de que o conteúdo do painel precisa

| Painel | Mínima | Máxima |
|---|---|---|
| esquerdo | 25% da tela | 25% da tela |
| direito | 40% da tela | 50% da tela |
| inferior | 35% da altura da tela | 70% da altura da tela |

O painel esquerdo só abre e fecha. O resto do editor é organizado a partir da largura dele

Se você soltar um arrasto abaixo da largura mínima, o painel vai para o que estiver mais perto: a posição fechada ou a largura mínima. Exatamente na metade, ele abre. Assim, um único movimento ainda fecha um painel

Um clique abre o painel na largura em que você o deixou aberto da última vez

> [!info] Vale saber
> Uma largura arrastada não é salva. Ela vive só na sessão atual, por isso um painel alargado não vai continuar largo da próxima vez

## Minimizar e abrir sozinho

`{{ui:cmd_editor_toggle-minimize-panels}}` fecha todos os painéis abertos e deixa só o viewport. Usar de novo abre os painéis que estavam abertos. Se nenhum estava aberto, os três abrem

`{{ui:settings_game-editor_interface-auto-open-panel}}` (configurações, aba `{{ui:settings_game-editor_title}}`, `{{ui:settings_interface_label}}`) abre o painel direito sozinho quando você seleciona algo. Desativado por padrão
