---
title: Avaliação de desempenho
date: 2026-10-17
tags: [player, level_author]
---

# Avaliação de desempenho

Antes de jogar, o jogo mostra o quanto um nível pesa para rodar no seu dispositivo, com um medidor de cinco barras: quanto mais barras acesas, mais leve o nível. Barras verdes querem dizer que roda bem, amarelas que fica no limite, vermelhas que a taxa de quadros vai cair

A pontuação é um número em que `{{v:performance.score-limit}}` é exatamente o tempo que um quadro pode levar na sua taxa de quadros alvo. A faixa vem da pontuação:

| Barras | Faixa | Pontuação |
|---|---|---|
| 5 | `{{ui:level_performance_holds}}` | abaixo de `{{v:performance.score-warning}}` |
| 4 | `{{ui:level_performance_tight}}` | de `{{v:performance.score-warning}}` a `{{v:performance.score-limit}}` |
| 3 | `{{ui:level_performance_drops}}` | acima de `{{v:performance.score-limit}}`, até `{{v:performance.score-heavy}}` |
| 2 | `{{ui:level_performance_severe-drops}}` | acima de `{{v:performance.score-heavy}}`, até `{{v:performance.score-severe}}` |
| 1 | `{{ui:level_performance_does-not-hold}}` | acima de `{{v:performance.score-severe}}` |
| nenhuma | `{{ui:level_performance_unknown}}` | o nível ou o dispositivo não foi medido |

A pontuação é uma previsão para o momento mais pesado do nível, não para a média. Um nível leve por três minutos que trava por um segundo recebe a pontuação desse segundo

## Onde você vê

- o navegador de níveis: o medidor em cada cartão de nível e o grupo `{{ui:root_level-filters_performance}}` nos filtros
- a página do nível no menu: o medidor, a faixa e a pontuação
- o editor de níveis, nos metadados do nível: a pontuação no seu dispositivo e nos dispositivos de referência, além dos momentos mais pesados do nível como marcas de tempo

## As duas metades da pontuação

**A metade do nível** é medida no editor nos segundos depois de cada salvamento, enquanto você continua trabalhando, e guardada nos metadados. Se você sair do editor antes de terminar, o arquivo mantém a medição anterior. Ela descreve o que o nível pede: quantos objetos estão vivos, quanto da tela eles cobrem, quantos efeitos e passes de pós-processamento rodam. Um nível salvo antes deste recurso não tem esse registro e aparece como `{{ui:level_performance_unknown}}` até ser salvo de novo. O editor o mede ao abrir o nível e guarda o resultado até você sair do editor, sem gravá-lo no arquivo

**A metade do dispositivo** diz com que rapidez o seu dispositivo faz cada uma dessas coisas. Até você medir o dispositivo, o jogo usa um dispositivo de referência da sua plataforma. Suas configurações também contam: escala de renderização, anti-aliasing, efeitos e pós-processamento mudam a pontuação sem uma nova medição

## Medir o seu dispositivo

1. No menu principal, abra `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}`
2. Toque em `{{ui:settings_graphics-performance_measure}}`. Uma janela diz o que ajuda a medição: fechar outros apps e jogos, ligar o celular ou o notebook no carregador, não tocar no dispositivo
3. Toque em `{{ui:settings_graphics-performance_start}}` e espere até {{v:performance.benchmark-max-seconds}} segundos. A tela de configurações some, o jogo roda níveis de teste e mostra nos cantos de cima o que está medindo. Não troque para outro app

`{{ui:settings_graphics-performance_stop}}` encerra a medição antes. Uma medição interrompida ou sem tempo não salva nada, e o resultado anterior continua

No fim, a janela mostra o resultado: o medidor do nível de demonstração no seu dispositivo, o que limita o seu dispositivo (o processador ou o chip gráfico), qual predefinição de `{{ui:settings_quick-setup_performance}}` ela sugere e quantos dos seus níveis caem em cada faixa. `{{ui:settings_graphics-performance_again}}` mede mais uma vez

Se a medição oscilou (o dispositivo esquentou demais, outro app estava ocupado), o jogo a usa mesmo assim, porque ela está mais perto do seu dispositivo do que qualquer referência, e a janela avisa. Feche outros apps e meça de novo para ter uma pontuação mais exata

## Mudar para outro dispositivo

A medição pertence ao dispositivo em que foi feita. A transferência de perfil ([[14_profile-transfer]]) e os salvamentos na nuvem não a levam, então um dispositivo novo começa pelo seu dispositivo de referência até você medi-lo de novo
