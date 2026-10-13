---
title: Estatísticas
date: 2026-10-02
tags: [advanced_player]
---

# Estatísticas

O jogo conta tentativas, mortes, impactos e tempo de cada nível e do dispositivo inteiro. Tudo fica salvo localmente na pasta stats. Cada conjunto de condições da partida tem um recorde separado

## Dois arquivos

| Arquivo | O que ele guarda |
|---|---|
| `stats/statistics.json` | tudo sobre você: em todos os níveis e telas |
| `stats/<LevelId>.json` | tudo o que você fez com um nível |

Os arquivos são JSON, os horários estão em UTC. Nada é enviado para lugar nenhum

A pasta `stats` fica ao lado de `levels` na pasta do jogo, [[1_installation]]. Ela nunca fica dentro de um nível. Assim um nível enviado a um amigo não chega já concluído. E o seu progresso sobrevive a excluir o nível e importá-lo de novo

## A aba "Perfil"

`{{ui:settings_common_title}}` → `{{ui:settings_profile_tab}}` mostra o arquivo comum do dispositivo:

| Seção | Linhas |
|---|---|
| `{{ui:settings_profile_section-account}}` | `{{ui:settings_profile_first-played}}`, `{{ui:settings_profile_last-played}}`, `{{ui:settings_profile_launches}}`, `{{ui:settings_profile_app-time}}` |
| `{{ui:field_common_time}}` | `{{ui:settings_profile_menu-time}}`, `{{ui:settings_profile_game-time}}`, `{{ui:settings_profile_editor-time}}`, `{{ui:settings_profile_loading-time}}` |
| `{{ui:settings_profile_section-totals}}` | `{{ui:settings_profile_attempts}}`, `{{ui:settings_profile_clears}}`, `{{ui:settings_profile_deaths}}`, `{{ui:settings_profile_hits}}`, `{{ui:settings_profile_levels-played}}`, `{{ui:settings_profile_levels-cleared}}`, `{{ui:settings_profile_frames}}` |
| `{{ui:settings_profile_section-streaks}}` | `{{ui:settings_profile_streak-current}}`, `{{ui:settings_profile_streak-longest}}` |
| `{{ui:settings_profile_section-avatar}}` | `{{ui:settings_profile_dashes}}`, `{{ui:settings_profile_distance}}` |
| `{{ui:settings_profile_section-tutorial}}` | `{{ui:settings_profile_tutorial-completions}}`, `{{ui:settings_profile_tutorial-first}}`, `{{ui:settings_profile_tutorial-last}}` - uma conclusão só conta quando todos os passos do [[13_sandbox|tutorial do sandbox]] estão feitos |
| `{{ui:settings_profile_section-editor}}` | `{{ui:settings_profile_levels-created}}`, `{{ui:settings_profile_levels-deleted}}`, `{{ui:settings_profile_objects}}`, `{{ui:settings_profile_operations}}`, `{{ui:settings_profile_generators}}`, `{{ui:settings_profile_resources}}` |
| `{{ui:settings_profile_section-devices}}` | `{{ui:settings_profile_device-keyboard}}`, `{{ui:settings_profile_device-touch}}`, `{{ui:settings_profile_device-gamepad}}`, `{{ui:settings_profile_device-gyro}}` |

O tempo é contado em segundos reais, não no tempo do nível. A câmera lenta em um checkpoint e uma partida em meia velocidade contam pelo tempo que realmente duraram

As linhas de dispositivos mostram qual dispositivo controlou o avatar durante o jogo. Um dispositivo que só está conectado não conta

## Por nível

O arquivo de um nível guarda:

- quando você jogou o nível pela primeira e pela última vez
- o tempo real passado no nível e o número de sessões
- tentativas (cada reinício é uma nova), conclusões, mortes, impactos, dashes
- voltas a um checkpoint e partidas abandonadas
- o ponto mais distante alcançado e a primeira conclusão
- onde no nível você morre: pela fração da duração e por checkpoint

## Recordes

Cada conjunto de condições da partida tem o próprio recorde: vidas, velocidade, checkpoints ativados ou desativados, colisão ativada ou desativada, e o bot. A velocidade conta até os centésimos, exatamente como na tela

Zen (0 vidas) continua contando os impactos: cada colisão entra nos números dele, só as vidas e o fim da partida são poupados

Uma partida bate o recorde com as mesmas condições se, nesta ordem:

1. foi mais longe
2. levou menos impactos
3. terminou com mais vidas
4. usou menos dashes

Um recorde também guarda a semente da partida e a versão do nível naquele momento. A versão não faz parte das condições. Por isso um recorde feito antes de o nível ser refeito continua visível, com a versão mostrada ao lado

**Uma partida pelo editor conta, mas não bate recordes.** Ela soma às tentativas, às mortes e aos impactos. Ela não dá recorde, melhor progresso nem primeira conclusão, porque o nível existia só na memória

## Gravar, excluir, congelar

O jogo grava as estatísticas a cada 30 segundos. E na hora no fim de uma partida, numa troca de tela e ao sair. Um travamento custa no máximo 30 segundos de dados

- **Excluir:** `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_other_cache-title}}`. Lá ficam `{{ui:settings_other_cache-orphan-statistics}}` e `{{ui:settings_other_cache-all-statistics}}`
- **Excluir junto com o nível:** excluir um nível oferece `{{ui:root_level-delete_statistics}}`
- **Congelar:** o modo anônimo para toda gravação até o jogo ser fechado, [[4_settings]]
- **Levar para outro dispositivo:** exporte o perfil e importe-o lá. Mesclar guarda o maior valor de cada contador, [[14_profile-transfer]]

> [!warning] Aviso
> Uma pasta de nível copiada à mão mantém o id do nível. O original e a cópia dividem um mesmo arquivo de estatísticas
