---
title: Velocidade e atalhos
date: 2026-10-02
tags: [level_author]
---

# Velocidade e atalhos

A paleta de comandos (Ctrl+Shift+P), a pesquisa de conteúdo (Ctrl+F), o botão Localizar e as setas em uma linha do tempo são o que mais poupa tempo. Qualquer tecla pode ser reatribuída nas configurações

## Os quatro maiores poupadores de tempo

- **`{{ui:editor_search-title_command}}`** (`Ctrl+Shift+P`) - tudo o que o editor sabe fazer, com pesquisa por nome. É mais rápido do que lembrar em que painel fica um botão
- **`Pesquisar conteúdo`** (`Ctrl+F`) - pula para um objeto ou uma faixa de áudio pelo nome. O indicador de reprodução vai junto
- **`{{ui:cmd_editor_ping}}`** - o viewport enquadra a seleção, e a linha do tempo e a hierarquia rolam até ela, tudo de uma vez. Pressionar de novo passa para o próximo objeto de uma seleção múltipla
- **Setas em uma linha do tempo** - movem por direção, não pela posição em uma lista. Dá para passar de um quadro-chave para o vizinho sem o mouse

## Os padrões

Os grupos e nomes abaixo são os que `{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}` mostra

### Reprodução

| Tecla | Nome nas configurações | Ação |
|---|---|---|
| `Space` | `{{ui:settings_keybindings_editor_play_pause}}` | reproduzir e pausar |

### Editar

| Tecla | Nome nas configurações | Ação |
|---|---|---|
| `Ctrl+Z` | `{{ui:cmd_editor_undo}}` | desfazer |
| `Ctrl+Y` ou `Ctrl+Shift+Z` | `{{ui:cmd_editor_redo}}` | refazer |
| `Ctrl+S` | `{{ui:settings_keybindings_editor_save}}` | salvar |
| `Ctrl+C` | `{{ui:cmd_editor_copy}}` | copiar |
| `Ctrl+V` | `{{ui:cmd_editor_paste}}` | colar |
| `Ctrl+D` | `{{ui:cmd_editor_duplicate}}` | duplicar |
| `Ctrl+G` | `{{ui:cmd_editor_pack-prefab}}` | criar um prefab a partir da seleção |

### Seleção

| Tecla | Nome nas configurações | Ação |
|---|---|---|
| `Del` | `{{ui:settings_keybindings_editor_delete}}` | excluir a seleção |
| segurar `Ctrl` | `{{ui:settings_keybindings_editor_multi_select}}` | seleção múltipla |
| `Ctrl+Shift+A` | `{{ui:settings_keybindings_editor_deselect}}` | limpar todas as seleções de uma vez: objetos, quadros-chave, áudio e batidas |
| `Ctrl+Shift+E` | `{{ui:cmd_editor_exit-prefab}}` | sair do modo prefab e voltar ao nível |

### Exibir

| Tecla | Nome nas configurações | Ação |
|---|---|---|
| `Ctrl+F` | `Pesquisar conteúdo` | pesquisar conteúdo |
| `Ctrl+Shift+P` | `{{ui:editor_search-title_command}}` | executar um comando |
| `Ctrl+Left` | `{{ui:settings_keybindings_editor_panel_left}}` | mostrar ou ocultar o painel esquerdo |
| `Ctrl+Right` | `{{ui:settings_keybindings_editor_panel_right}}` | mostrar ou ocultar o painel direito |
| `Ctrl+Down` | `{{ui:settings_keybindings_editor_panel_bottom}}` | mostrar ou ocultar o painel inferior |
| `Ctrl+Up` | `{{ui:settings_keybindings_editor_viewport_tools}}` | mostrar ou ocultar os grupos de ferramentas sobre o viewport |
| segurar `` ` `` | `{{ui:settings_keybindings_editor_preview}}` | pré-visualização: a interface do editor fica oculta enquanto a tecla está pressionada |

### Linha do tempo

| Tecla | Nome nas configurações | Ação |
|---|---|---|
| `Z` | `{{ui:settings_keybindings_editor_expansion_cycle}}` | alternar o recolhimento: todas as subárvores, só os tipos escolhidos, nada |
| `X` | `{{ui:settings_keybindings_editor_tool_snap}}` | ligar ou desligar o encaixe |
| `C` | `{{ui:settings_keybindings_editor_tool_selection}}` | a ferramenta de seleção |
| `V` | `{{ui:settings_keybindings_editor_tool_marquee}}` | a ferramenta de seleção retangular |
| `B` | `{{ui:settings_keybindings_editor_tool_scissors}}` | a ferramenta tesoura |
| `N` | `{{ui:settings_keybindings_editor_tool_edges}}` | a ferramenta de bordas |
| `Ctrl+E` | `{{ui:settings_keybindings_editor_fold}}` | recolher os objetos selecionados na linha do tempo |
| `Q` | `{{ui:settings_keybindings_editor_tab_timeline_level}}` | abrir a linha do tempo do nível |
| `W` | `{{ui:settings_keybindings_editor_tab_timeline_local}}` | abrir a linha do tempo local |
| `E` | `{{ui:settings_keybindings_editor_tab_timeline_audio}}` | abrir a linha do tempo de áudio |
| `R` | `{{ui:settings_keybindings_editor_tab_timeline_events}}` | abrir a linha do tempo de eventos |
| `T` | `{{ui:settings_keybindings_editor_tab_timeline_prefab}}` | abrir a linha do tempo do prefab |
| `Shift+T` | `{{ui:settings_keybindings_editor_beat_window}}` | a janela da grade de batidas, onde o andamento é marcado por toques. `{{ui:settings_keybindings_editor_beat_tap}}` em si não tem tecla padrão, atribua uma se precisar |
| segurar `Ctrl` e girar a roda | `{{ui:settings_keybindings_timeline_pan_modifier}}` | panorâmica |
| segurar `Shift` e girar a roda | `{{ui:settings_keybindings_timeline_zoom_modifier}}` | zoom |

`Z X C V B N` seguem a barra de ferramentas da linha do tempo da esquerda para a direita, e `Q W E R T` seguem a fileira de abas. Uma linha do tempo com menos ferramentas perde as da direita: a linha do tempo local tem só `Z X C V`. Uma letra para a qual a linha do tempo aberta não tem ferramenta não faz nada

### Gizmos

| Tecla | Nome nas configurações | Ação |
|---|---|---|
| `1` | `{{ui:settings_keybindings_editor_gizmo_none}}` | seleção |
| `2` | `{{ui:settings_keybindings_editor_gizmo_position}}` | posição |
| `3` | `{{ui:settings_keybindings_editor_gizmo_rotation}}` | rotação |
| `4` | `{{ui:settings_keybindings_editor_gizmo_scale}}` | escala |
| `5` | `{{ui:settings_keybindings_editor_gizmo_size}}` | tamanho |
| `6` | `{{ui:settings_keybindings_editor_gizmo_anchors}}` | âncoras |
| `7` | `{{ui:settings_keybindings_editor_gizmo_pivot}}` | pivô |
| `0` | `{{ui:settings_keybindings_editor_gizmo_hidden}}` | oculto: a seleção continua, mas nem as alças nem a borda são desenhadas |

### Janela

| Tecla | Nome nas configurações | Ação |
|---|---|---|
| `F11` | `{{ui:settings_keybindings_window_toggle_fullscreen}}` | ligar ou desligar a tela cheia. Funciona em qualquer tela, só no computador |
| `Ctrl+S` | `{{ui:settings_keybindings_window_settings_save}}` | gravar as configurações no disco agora, enquanto as configurações estão abertas. No editor, `Ctrl+S` salva o nível em vez disso |

### Navegação

| Tecla | Nome nas configurações | Ação |
|---|---|---|
| `Up` | `{{ui:settings_keybindings_nav_up}}` | mover para cima na superfície em que você clicou por último |
| `Down` | `{{ui:settings_keybindings_nav_down}}` | mover para baixo na superfície em que você clicou por último |
| `Left` | `{{ui:settings_keybindings_nav_left}}` | mover para a esquerda na superfície em que você clicou por último |
| `Right` | `{{ui:settings_keybindings_nav_right}}` | mover para a direita na superfície em que você clicou por último |

Teclas sem modificador, como os dígitos dos gizmos, as letras da linha do tempo e `Space`, não fazem nada enquanto você digita em um campo de texto. Um `2` em um campo de quadro não troca o gizmo

## Setas em uma linha do tempo

Uma seta escolhe o item mais próximo naquela direção na tela. O mesmo toque na tecla encontra o mesmo item com qualquer zoom

- A partir de uma seleção múltipla, a seta começa no item mais distante na direção pressionada. Ela nunca volta para dentro do bloco que você selecionou
- Um movimento com seta sempre substitui a seleção. Nunca a amplia
- A linha do tempo rola só o necessário para mostrar o item novo. Clicar no mostrador do indicador de reprodução continua centralizando a vista
- Enquanto o jogador de teste está ligado, as setas controlam o jogador, não a linha do tempo. A hierarquia e a aba `{{ui:settings_level-settings_raw}}` mantêm as próprias setas depois que você clica nelas

## Vendo o nível

**Pré-visualização.** Segure `` ` `` para ocultar a interface do editor e ver só o nível. É uma tecla de segurar, não um interruptor: solte a tecla e tudo volta. O nível, as barras do letterbox, o jogador e os limites da câmera continuam visíveis.
Não há botão nem configuração para isso. A tecla pode ser reatribuída como `{{ui:settings_keybindings_editor_preview}}`

**A grade do viewport** é ligada pelo botão dela na barra de ferramentas ou pelo comando `{{ui:cmd_editor_viewport-grid}}`. Ela começa desligada. Isso se muda em `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_grid-active-default}}`, e o fato de você ter ligado a grade não é lembrado entre sessões

**O ímã do gizmo** encaixa na grade o que um gizmo arrasta. Ele vem ligado por padrão e não depende do modo do gizmo. É alternado pelo botão dele na barra de ferramentas e pelo comando `{{ui:cmd_editor_gizmo-magnet}}`

**Pausado é o estado normal para observar.** A grade, os colisores, a sobreposição do bot, as alças do gizmo e a borda da seleção continuam sendo desenhados com a reprodução pausada. Pegar uma alça do gizmo pausa a reprodução

## Reatribuição

Qualquer tecla pode ser reatribuída: `{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`

Só as teclas que você mudou são armazenadas. O resto vem dos padrões.
Assim, um padrão melhorado chega até você se você não mexeu naquela tecla.
`{{ui:settings_keybindings_reset}}` simplesmente remove as suas mudanças, e todas as teclas voltam aos padrões

> [!tip] Dica
> Os rótulos das teclas não são fixos na interface. Depois de uma reatribuição, a paleta de comandos e todos os menus de contexto mostram a tecla nova na hora

## Teclas pressionadas e seguradas

Uma tecla pressionada só dispara se os modificadores dela batem exatamente.
`Ctrl+Shift+P` não dispara também como `Ctrl+P`, e um `T` sozinho não dispara enquanto `Ctrl` está pressionado

Uma tecla segurada dispara se os modificadores dela estão entre os que estão pressionados. Ela refina um gesto que já está em andamento

> [!info] Vale saber
> Por isso duas teclas seguradas podem dividir um botão de propósito. A seleção múltipla e a panorâmica da linha do tempo ficam ambas em `Ctrl` e não atrapalham uma à outra

A seguir: [[1_order-of-work|A ordem de trabalho]], [[2_reuse|Reutilização: prefabs, cópia, geradores]]
