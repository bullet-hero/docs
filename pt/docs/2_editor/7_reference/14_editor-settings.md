---
title: Configurações do editor
date: 2026-10-11
tags: [level_author]
---

# Configurações do editor

O salvamento automático, a grade, a seleção, os gizmos e as predefinições de nível novo ficam aqui. O salvamento automático vem ativado e dispara {{v:editor.autosave-delay}} segundos após uma edição

## Editor do jogo

O salvamento automático, a câmera, a seleção e os formatos de arquivo são definidos aqui

| Configuração | O que faz | Padrão |
|---|---|---|
| `{{ui:settings_game-editor_autosave}}` | ativa o salvamento automático | ativado |
| `{{ui:settings_game-editor_autosave-rate}}` | quantos segundos passam de uma edição não salva até o salvamento automático | {{v:editor.autosave-delay}} |
| `{{ui:settings_game-editor_max-autosave-files}}` | quantas cópias são mantidas. Quando o limite é atingido, a mais antiga é excluída | {{v:editor.autosave-copies}} |

O temporizador só corre enquanto há edições não salvas

Um salvamento automático faz duas coisas:
1. Grava uma cópia do nível em `<game folder>/backups/<level id>/`
2. Salva o próprio nível, como faz `Ctrl+S`

Uma cópia guarda só o arquivo do nível. Há duas formas de restaurá-la:
- nas configurações do nível: `{{ui:settings_level-settings_dangerous-zone}}` → `{{ui:level_backups_open}}`
- à mão: copie-a para a pasta do nível com o nome `level.json` (ou `level.blob`)

Mais - [[4_not-losing-work#Salvamento automático]]

`{{ui:settings_game-editor_camera-min-size}}` e `{{ui:settings_game-editor_camera-max-size}}` limitam o quanto o viewport do editor pode aproximar e afastar o zoom

`{{ui:settings_game-editor-multi-select-requires_hold}}` e `{{ui:settings_game-editor-pick-invisible_aabb}}` mudam o que um clique no viewport significa. Confira essas opções se a seleção de repente se comportar de um jeito diferente do habitual

`{{ui:settings_game-editor-level-serialize_mode}}` e `{{ui:settings_game-editor-resources-serialize_mode}}` definem o formato padrão para gravar no disco

`{{ui:settings_game-editor_publish-language}}` escolhe o idioma em que o título e a descrição de um item da Oficina são publicados primeiro: `{{ui:enum_publish-language_english}}` (o padrão) ou `{{ui:enum_publish-language_system}}`, o idioma do dispositivo

Mais - [[3_speed-and-shortcuts]]

## Grade

A grade do viewport é desenhada atrás do nível e ajuda a posicionar objetos

| Configuração | O que faz | Padrão |
|---|---|---|
| `{{ui:settings_game-editor_grid-active-default}}` | se a grade está ativada quando o editor abre. É só o estado inicial | desativado |
| `{{ui:settings_game-editor-grid_size}}` | o lado de uma célula, em unidades do mundo | 1 |
| `{{ui:settings_game-editor-grid_opacity}}` | o quanto as linhas são visíveis, de 0 a 1 | 0.25 |

O botão da grade na barra de ferramentas a ativa e desativa. Esse estado não é salvo entre sessões

Como a grade aparece:
- Ela não tem borda. A célula muda em passos de 10 conforme o zoom, e a grade mais fina surge aos poucos
- Se um patamar da grade precisasse de linhas demais, esse patamar é desligado em vez de ficar mais ralo
- A cor das linhas é sempre o inverso do fundo da câmera no quadro atual, por isso a grade continua visível quando o fundo muda. Você define só a opacidade

Com o encaixe ativado, arrastar uma posição gruda em meia célula: nos cruzamentos e nos centros das células. Ele usa a grade que você vê. Com a grade desativada, a posição gruda em um passo fixo

## Seleção

| Configuração | O que faz | Padrão |
|---|---|---|
| `{{ui:settings_game-editor-multi-select-requires_hold}}` | ativado: no modo de seleção múltipla, um clique só adiciona enquanto `Ctrl` está pressionado, e um clique simples substitui a seleção. Desativado: enquanto o modo está ligado, todo clique adiciona | ativado |
| `{{ui:settings_game-editor-preview-collider-on_select}}` | desenha a hitbox de cada objeto selecionado como um preenchimento translúcido | desativado |
| `{{ui:settings_game-editor-pick-invisible_aabb}}` | um clique seleciona um objeto pelo retângulo inteiro dele, não pelo que ele desenha | desativado |
| `{{ui:settings_game-editor_selection-long-press-delay}}` | quanto tempo um toque mantido dura antes de um menu abrir, em segundos | 0.5 |
| `{{ui:settings_game-editor_selection-long-press-threshold}}` | o quanto o cursor pode se mover durante o toque mantido antes de virar um arrasto | 8 |
| `{{ui:settings_game-editor_selection-collider-opacity}}` | o quanto a hitbox de um objeto selecionado é desenhada sólida | 0.5 |
| `{{ui:settings_game-editor_selection-collider-opacity-view}}` | o mesmo para a vista de todas as hitboxes, mais fraca porque ali centenas delas se sobrepõem | 0.25 |

Soltar `Ctrl` no modo de seleção múltipla não limpa nada e não sai do modo. Só o próximo clique simples substitui a seleção. Mais sobre o modo - [[4_hierarchy-and-clipboard]]

O botão de colisores na barra de ferramentas mostra as hitboxes de tudo o que está no quadro, incluindo o círculo do jogador. Esse estado não é salvo entre sessões. Se houver hitboxes demais na tela, a vista se desliga sozinha com uma mensagem em vez de desenhar só algumas delas

Um objeto sem colisor não desenha hitbox em nenhuma das duas vistas, e um objeto inativo também não

A cor de preenchimento das duas vistas é `Configurações > Gráficos > Modo só colisores > Cor de preenchimento`, compartilhada com o modo "Só colisores" do jogo ([[4_settings]]). As duas opacidades acima continuam sendo configurações próprias do editor

## Gizmos

| Configuração | O que faz | Padrão |
|---|---|---|
| `{{ui:settings_game-editor_gizmos-scale}}` | o tamanho das alças de arrasto no viewport, de 0.1 a 10. Uma alça feita para o mouse é difícil de acertar com o dedo | 1 |

As alças mantêm o mesmo tamanho na tela em qualquer zoom

## Agente de IA

`{{ui:settings_game-editor_mcp_title}}` permite que um cliente de IA que fala MCP edite o nível aberto. Só no Windows, Linux e Mac: celulares e tablets não mostram esta seção

| Configuração | O que faz | Padrão |
|---|---|---|
| `{{ui:settings_game-editor_mcp-enabled}}` | permite que um cliente se conecte. Só este computador pode se conectar, um cliente por vez | desativado |
| `{{ui:settings_game-editor_mcp-port}}` | a porta em que o editor escuta. `0` escolhe uma livre a cada início, senão de {{v:mcp.port-min}} a {{v:mcp.port-max}}. Qualquer outro número é revertido | 0 |
| `{{ui:settings_game-editor_mcp-follow-ai}}` | para onde o indicador vai depois que a IA olha um quadro. Desativado: volta para onde você o deixou. Ativado: fica naquele quadro, em pausa | ativado |
| `{{ui:settings_game-editor_mcp-reveal-edits}}` | depois de cada edição da IA, seleciona e localiza o que ela criou ou mudou. Nunca enquanto você arrasta, digita ou reproduz | ativado |
| `{{ui:settings_game-editor_mcp-operation-delay}}` | quantos segundos o editor espera entre duas operações da IA, de 0 a {{v:mcp.operation-delay-max}}. `0` aplica cada uma na hora. Reproduzir, pausar e mover o indicador nunca sofrem atraso, nem nada que a IA apenas lê | {{v:mcp.operation-delay}} |

`{{ui:settings_game-editor_mcp-copy-config}}` copia a configuração que um cliente MCP recebe, com o caminho até o servidor e até o arquivo de conexão do jogo já preenchidos

A linha abaixo das configurações diz o que o editor está fazendo: desligado, escutando em uma porta, conectado ou parado pelo selo de IA no editor

Essas configurações ficam só neste dispositivo

Mais - [[7_ai-assistant]]

## Criar um nível

`{{ui:settings_editor-settings_level-presets}}` definem com o que um nível novo começa: vazio ou com uma pequena estrutura inicial. Sem uma predefinição, você teria que montar essa estrutura à mão toda vez

> [!caution] Cuidado
> `{{ui:settings_editor-settings_parameters}}` definem o que é chato de mudar depois: a duração em quadros e a taxa de quadros

> [!tip] Dica
> As listas `{{ui:settings_editor-settings_quot-level-quot-file-format}}` e `{{ui:settings_editor-settings_quot-metadata-quot-file-format}}` escolhem o formato em que o nível e os metadados dele são gravados no disco. Os dois podem ser mudados depois em `{{ui:settings_level-settings_dangerous-zone}}` do nível

Mais - [[2_first-level]]

## Biblioteca

`{{ui:settings_editor-settings_library}}` é a última aba, depois de `{{ui:settings_editor-settings_community}}`. Ela guarda os recursos que você reutiliza entre níveis: a biblioteca do dispositivo, as suas coleções e, na build da Steam, as coleções que você assinou na Oficina Steam

A coluna à esquerda escolhe o tipo: `{{ui:settings_level-settings_collections}}`, depois prefabs, temas, formas e efeitos, depois texturas, fontes e áudio. Aqui você cria e edita coleções, copia entradas entre elas, importa e exporta coleções e, na build da Steam, publica as suas

Mais - [[16_library-and-collections]]

## Usar o trabalho de outras pessoas

Cada recurso externo de um nível (música, imagens, fontes, textos) precisa se enquadrar em uma de duas opções:
- uma licença pelo menos tão livre quanto `CC BY-NC`
- a permissão do próprio detentor dos direitos para distribuição pública não comercial

> [!caution] Cuidado
> Um "claro, sem problema" em particular não basta. Um nível sob `CC BY-NC` é distribuído publicamente. A permissão precisa cobrir exatamente isso, não só o seu uso pessoal

Um nível que fica no seu dispositivo não é verificado. As regras valem em um momento: quando o nível é entregue a um serviço

As regras completas, a lista de licenças aceitas, o modelo de pedido e onde procurar recursos:
- [[2_legal-resource-paths]]
- [[6_asking-permission]]
- [[3_where-to-get-resources]]
