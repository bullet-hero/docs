---
title: Jogar níveis
date: 2026-10-11
tags: [player]
---

# Jogar níveis

Escolha um nível na lista de níveis, defina as condições da partida e comece. O nível de outra pessoa é uma pasta comum: copie-a para a pasta de níveis e atualize a lista

## Menu principal

| Botão | O que faz |
|---|---|
| `{{ui:menu_main_levels-btn}}` | a lista de níveis, descrita abaixo |
| `{{ui:menu_main_editor-btn}}` | o editor de níveis, [[2_editor/1_basics/index]] |
| `{{ui:menu_main_sandbox-btn}}` | uma arena sem nível e o tutorial, [[13_sandbox]] |
| `{{ui:settings_common_title}}` | todas as configurações, [[4_settings]] |
| `{{ui:menu_main_story-btn}}` | ainda não funciona |
| `{{ui:menu_main_multiplayer-btn}}` | ainda não funciona |

## A lista de níveis

`{{ui:menu_main_levels-btn}}` no menu principal abre a lista de níveis. Os níveis vêm de três lugares:

- `{{ui:root_level-source_local}}` - a pasta `levels`, [[1_installation]]
- `{{ui:root_level-source_builtin}}` - os níveis que vêm com o jogo
- `Oficina` - só nas versões da Steam. Mostra os níveis das suas inscrições. Coleções de recursos das suas inscrições não são níveis: elas aparecem na biblioteca do editor, [[16_library-and-collections]]

No topo ficam o campo de pesquisa, `{{ui:root_level-browser_sort}}`, `{{ui:root_level-browser_layout}}` (grade ou lista) e `{{ui:root_level-browser_filters}}`. A lista abre como grade. Dá para ordenar por `{{ui:root_level-browser_sort-relevance}}`, `{{ui:root_level-browser_sort-title}}`, `{{ui:root_level-browser_sort-duration}}`, `{{ui:root_level-browser_sort-progress}}` e `{{ui:root_level-browser_sort-recent}}`. A seta ao lado do botão de ordenar (`{{ui:root_level-browser_reverse}}`) inverte a ordem. `{{ui:root_level-browser_sort-relevance}}` não tem direção

A pesquisa olha primeiro os nomes dos níveis, depois os autores, depois as tags

`{{ui:root_level-browser_filters}}` abre uma janela com mais filtros. A lista atrás dela muda conforme você toca:

- `{{ui:root_level-filters_ai}}` - `{{ui:root_level-filters_ai-yes}}`, `{{ui:root_level-filters_ai-no}}` e `{{ui:root_level-filters_ai-unspecified}}`
- `{{ui:root_level-filters_length}}` - o nível mais curto e o mais longo, e se os níveis de duração desconhecida aparecem
- `{{ui:root_level-filters_progress}}` - `{{ui:root_level-filters_progress-unplayed}}`, `{{ui:root_level-filters_progress-started}}`, `{{ui:root_level-filters_progress-cleared}}`, `{{ui:root_level-filters_progress-bot}}`
- `{{ui:root_level-filters_recent}}` - as últimas 24 horas, 7 dias ou 30 dias
- `{{ui:root_level-filters_age}}` - a classificação etária mais alta a mostrar
- `{{ui:root_level-filters_other}}` - ocultar níveis com senha, ocultar níveis de uma versão mais nova do jogo
- `{{ui:root_level-filters_tags}}` - toque em uma tag uma vez para exigi-la, duas vezes para excluí-la

`{{ui:root_level-filters_progress}}` e `{{ui:root_level-filters_recent}}` existem só na lista do menu principal. A lista do editor tem os próprios filtros. O botão mostra quantos filtros estão ativados, e `{{ui:root_level-browser_reset}}` desativa todos. Os filtros continuam valendo até você fechar o jogo

Copiou um nível para a pasta? Toque em `{{ui:root_level-browser_refresh}}` e a lista se atualiza

Um cadeado em um cartão significa que o nível é protegido por senha

Segurar ou clicar com o botão direito em um cartão abre um menu: `{{ui:level_passphrase_open}}` e `{{ui:root_level-browser_delete}}`. `{{ui:root_level-browser_delete}}` em um nível da `Oficina` cancela a sua inscrição no item e exclui os arquivos dele. Para isso a Steam precisa estar aberta: senão a Steam baixa o nível de novo. Níveis inclusos não podem ser excluídos

## Adicionar o nível de outra pessoa

Um nível é uma pasta comum de arquivos. Você pode compactá-la e mandar para um amigo

**Uma pasta.** Copie a pasta do nível para `levels` e toque em `{{ui:root_level-browser_refresh}}`
Copie a própria pasta do nível: a que contém `level.json` (ou `level.blob`) e `metadata.json`

**Um arquivo compactado.** Abra o editor e crie um nível novo com o gerador `{{ui:gen_level_archive}}`
Depois escolha o arquivo com o botão `{{ui:editor_create-level_archive-choose}}`

| Arquivo | Resultado |
|---|---|
| `.zip`, `.tar.gz` | abre |
| `.zip` com senha própria, `.zip.gpg`, `.tar.gz.gpg` | abre depois de `{{ui:editor_create-level_archive-protected}}` |
| `.7z` | recusado por enquanto. Compacte de novo como zip |
| qualquer outro | recusado, [[5_troubleshooting]] |

Um arquivo compactado renomeado abre do mesmo jeito: o jogo reconhece o formato pelos bytes do arquivo. Um arquivo compactado de uma versão mais antiga do jogo é atualizado na importação

Por padrão, um nível importado recebe um id próprio. Assim ele não sobrescreve um nível que já está no dispositivo

Mais - [[6_sharing-by-hand]]

## A tela do nível

A tela do nível mostra a capa, os autores, a descrição e o autor da música. Ela também tem os botões `{{ui:level_level-view_authors}}` e `{{ui:level_level-view_licenses}}`

O nome do autor e a linha da música abrem o próprio link, se os metadados do nível tiverem um

A classificação etária é definida pelo autor do nível. O jogo não a verifica

"Contém conteúdo gerado por IA" aparece quando o autor declarou que o nível, a capa dele ou um dos recursos foi gerado por IA. Isso também é uma declaração do próprio autor. A falta dessa linha não significa "sem IA": o autor pode simplesmente não ter dito nada

Antes de uma partida, você pode escolher as condições:

| Condição | Opções |
|---|---|
| `{{ui:menu_levelview_options-lifes_title}}` | `{{ui:menu_levelview_options-lifes_option-zen}}` (a partida nunca termina), `{{ui:menu_levelview_options-lifes_option-one}}`, `{{ui:menu_levelview_options-lifes_option-three}}`, `{{ui:menu_levelview_options-lifes_option-custom}}` (um controle deslizante até 16) |
| `{{ui:field_common_speed}}` | `0.5`, `1.0`, `2.0`, `{{ui:menu_levelview_options-lifes_option-custom}}` (um controle deslizante até 2). O nível e a música mudam juntos |
| `Checkpoints` | ativado ou desativado, [[7_damage]] |
| `{{ui:menu_levelview_options-no-collision_title}}` | ativado ou desativado. O avatar atravessa tudo, [[7_damage]] |
| `{{ui:menu_levelview_options-bot}}` | `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}`, `{{ui:enum_bot-kind_warm}}`, [[9_bots]] |
| `{{ui:level_level-view_seed-value}}` | um número, `{{ui:level_level-view_seed-randomize}}`, `{{ui:level_level-view_seed-clear}}`. `0` - uma semente nova a cada partida, [[8_determinism]] |

`Jogar` começa a partida

A pausa tem `{{ui:game_pause-window_continue-btn}}`, `{{ui:game_pause-window_restart-btn}}`, `{{ui:game_game-result_restart-checkpoint}}` (depois de alcançar um checkpoint), `{{ui:settings_common_title}}`, `{{ui:game_game-result_back-to-options}}` e `{{ui:game_game-result_back-to-menu}}`. `{{ui:game_game-result_back-to-options}}` volta para a tela do nível com as condições com que a partida começou, ou para a aba `Jogar` do editor, se a partida começou por lá

## A janela de resultado

A janela mostra `Concluído` ou `{{ui:game_game-result_lose}}` e três seções: `Progresso`, `{{ui:game_game-result_section-damage}}` e `{{ui:game_game-result_section-conditions}}`

- linhas: `Percorrido`, `{{ui:game_game-result_checkpoint}}`, `{{ui:field_common_time}}`, `{{ui:game_game-result_length}}`, `{{ui:game_game-result_hits}}`, `{{ui:game_game-result_lives-left}}`, `{{ui:game_game-result_streak}}`
- condições da partida: `{{ui:field_common_speed}}`, `{{ui:menu_levelview_options-lifes_title}}`, `{{ui:menu_levelview_options-bot}}`, `{{ui:game_game-result_seed}}`, `Checkpoints`. Em uma partida `{{ui:menu_levelview_options-no-collision_title}}`, `{{ui:menu_levelview_options-lifes_title}}` ganha `· Sem colisão`
- botões: `{{ui:game_pause-window_restart-btn}}`, `{{ui:game_game-result_restart-checkpoint}}`, `{{ui:settings_common_title}}`, `{{ui:game_game-result_back-to-options}}`, `{{ui:game_game-result_back-to-menu}}`

Por padrão, a janela não abre em uma derrota. Em vez disso, a partida volta ao último checkpoint. Para mudar isso - `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_open-menu-on-lose}}`

## Recordes

A tela do nível tem um bloco de recorde: `{{ui:menu_levelview_record-best}}`, `{{ui:menu_levelview_record-attempts}}` e `{{ui:menu_levelview_record-clears}}` (ou `{{ui:menu_levelview_record-none}}`)

Cada conjunto de condições tem o próprio recorde: vidas, velocidade, checkpoints, colisões e o bot. O bloco mostra o recorde das condições escolhidas agora. Tentativas e conclusões contam em qualquer partida

Como um recorde é escolhido - [[10_statistics]]

## Marcas nos cartões

| Marca | O que significa |
|---|---|
| `{{ui:root_level-entry_not-listed}}` | a pasta da Oficina está no disco, mas não há inscrição sua nela. Só aparece quando `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general_show-all-found-content}}` está ativado |
| `{{ui:root_level-entry_unverified}}` | a fonte do nível não respondeu |
| `{{ui:root_level-entry_newer-version}}`, `{{ui:root_level-entry_newer-file}}` | esta versão do jogo não abre o nível, [[5_troubleshooting]] |
| `{{ui:root_level-entry_level-missing-badge}}` | a pasta não tem `level.json`, então o nível não pode ser iniciado, [[4_level-folder-and-backups]] |
| `{{ui:root_level-entry_meta-missing-badge}}` | a pasta não tem um `metadata.json` legível. O cartão mostra o nome da pasta, e o nível pode ser jogado, [[4_level-folder-and-backups]] |

## Excluir um nível

Segure ou clique com o botão direito em um cartão → `{{ui:root_level-browser_delete}}`. O jogo pede confirmação antes

Junto com o nível, você pode excluir as estatísticas dele (`{{ui:root_level-delete_statistics}}`) e os backups (`{{ui:root_level-delete_backups}}`)

Excluir um nível protegido não exige senha
