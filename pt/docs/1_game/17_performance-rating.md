---
title: Avaliação de desempenho
date: 2026-10-15
tags: [player, level_author]
---

# Avaliação de desempenho

Antes de jogar, o jogo mostra o quanto um nível pesa para rodar no seu dispositivo. Verde quer dizer que roda bem, amarelo que fica no limite, vermelho que é pesado demais e a taxa de quadros vai cair

A pontuação é um número em que `{{v:performance.score-limit}}` é exatamente o tempo que um quadro pode levar na sua taxa de quadros alvo. A faixa vem da pontuação:

| Faixa | Pontuação |
|---|---|
| `{{ui:level_performance_holds}}` | abaixo de `{{v:performance.score-warning}}` |
| `{{ui:level_performance_tight}}` | de `{{v:performance.score-warning}}` a `{{v:performance.score-limit}}` |
| `{{ui:level_performance_does-not-hold}}` | acima de `{{v:performance.score-limit}}` |
| `{{ui:level_performance_unknown}}` | o nível ou o dispositivo não foi medido |

A pontuação é uma previsão para o momento mais pesado do nível, não para a média. Um nível leve por três minutos que trava por um segundo recebe a pontuação desse segundo

## Onde você vê

- o navegador de níveis: um ponto colorido em cada cartão de nível e o grupo `{{ui:root_level-filters_performance}}` nos filtros
- a página do nível no menu: a faixa e a pontuação
- o editor de níveis, nos metadados do nível: a pontuação no seu dispositivo e nos dispositivos de referência, além dos momentos mais pesados do nível como marcas de tempo

## As duas metades da pontuação

**A metade do nível** é medida quando o nível é salvo no editor e guardada nos metadados. Ela descreve o que o nível pede: quantos objetos estão vivos, quanto da tela eles cobrem, quantos efeitos e passes de pós-processamento rodam. Um nível salvo antes deste recurso não tem esse registro e aparece como `{{ui:level_performance_unknown}}` até ser salvo de novo. O editor o mede ao abrir o nível e guarda o resultado até você fechar o jogo, sem gravá-lo no arquivo

**A metade do dispositivo** diz com que rapidez o seu dispositivo faz cada uma dessas coisas. Até você medir o dispositivo, o jogo usa um dispositivo de referência da sua plataforma. Suas configurações também contam: escala de renderização, anti-aliasing, efeitos e pós-processamento mudam a pontuação sem uma nova medição

## Medir o seu dispositivo

1. No menu principal, abra `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}`
2. Toque em `{{ui:settings_graphics-performance_measure}}`
3. Espere alguns minutos. A tela de configurações some e o jogo roda níveis de teste. Não troque para outro app

No fim, a seção mostra o que limita o seu dispositivo (o processador ou o chip gráfico) e qual predefinição de `{{ui:settings_quick-setup_performance}}` ela sugere

Se a medição ficou instável (o dispositivo esquentou demais, outro app estava ocupado), o jogo a ignora e mantém o dispositivo de referência. Feche outros apps e meça de novo

## Mudar para outro dispositivo

A medição pertence ao dispositivo em que foi feita. A transferência de perfil ([[14_profile-transfer]]) e os salvamentos na nuvem não a levam, então um dispositivo novo começa pelo seu dispositivo de referência até você medi-lo de novo
