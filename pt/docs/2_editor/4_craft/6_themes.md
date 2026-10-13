---
title: Temas
date: 2026-10-02
tags: [level_author]
---

# Temas

Um tema é uma paleta de 64 cores a que os objetos se referem pelo número do slot. Troque o tema, e tudo o que se refere a ele muda junto

Uma cor do tipo `Tema` não armazena cor própria, só um número de slot. Ela pega o que esse slot contém no tema ativo no quadro atual

Por que isso é melhor que cores digitadas à mão e como manter um nível legível com qualquer tema - [[5_color-and-postprocessing]]

## O que um tema contém

- **Um nome** - aparece nas listas e nos seletores
- **Um ID**, `ThemeId`. Os quadros-chave de tema se referem a um tema por ele, não pelo nome
- **64 cores** em uma grade de 8 por 8, cada uma com transparência
- **Um nome de slot** para cada slot, opcional. Enquanto você não der nome a pelo menos um slot, o arquivo armazena `null` no lugar da lista de nomes

Um tema são dados dentro de `level.json`, não um arquivo separado na pasta do nível (veja [[1_level-needs]]). Um nível pode conter qualquer quantidade de temas

O jogo não atribui papel nenhum a um slot: o próprio tema `Balanced` do jogo simplesmente agrupa as 64 cores dele por matiz

## Como uma cor encontra o valor

Em duas etapas:
1. A faixa `Tema` na linha do tempo de eventos diz qual tema está ativo neste quadro
2. Uma cor do tipo `Tema` indica um slot de 0 a 63 no tema ativo

Entre o que pode se referir a um tema estão, por exemplo, a cor de uma forma (cada canto dela separadamente), a cor de um texto e o fundo do nível

**A posição de um slot é a identidade dele.** Mova uma cor para outro slot, e tudo o que se referia ao antigo muda de cor

## Troca de temas ao longo do tempo

Entre dois quadros-chave de tema, o jogo mistura gradualmente a paleta inteira de um tema para o outro. A suavização vem do quadro-chave posterior (veja [[5_keyframes-and-easing]])

Se não houver nenhum quadro-chave de tema, todos os slots ficam brancos

> [!warning] Aviso
> Um quadro-chave novo recebe `Linear`, então a paleta desliza ao longo de todo o trecho, do quadro-chave de tema anterior até este. Para o tema trocar exatamente no drop, defina `Constant` no quadro-chave do drop

> [!caution] Cuidado
> Um quadro-chave de tema pode sobreviver ao próprio tema. Exclua um tema a que quadros-chave ainda se referem, e todos esses quadros ficam brancos. Os quadros-chave continuam lá. O editor pergunta de novo antes de excluir um tema assim

## Como criar e editar um tema

A aba `Temas` entre os recursos do nível mostra os temas do nível. Ela tem `{{ui:settings_level-settings_resources-themes-add}}` e `{{ui:settings_level-settings_resources-themes-import}}`. Clicar em uma linha abre o `{{ui:settings_level-settings_theme-editor}}`:
- `{{ui:field_common_name}}` do tema
- `ID do tema` e `{{ui:settings_level-settings_theme-editor-regenerate-id}}`
- a grade de 8 por 8. Clicar em uma célula a seleciona, mostra `Cor:` com o número dela e carrega a cor na roda abaixo da grade
- `{{ui:editor_theme-editor_color-name}}` para a célula selecionada

O editor trabalha em uma cópia. Nada chega ao nível até você salvar. O próprio salvamento é um único passo de desfazer

## Como escolher um slot

Mude uma cor para `Tema` e abra `{{ui:editor_select-theme_color}}`

A grade mostra a paleta como ela está misturada no quadro do quadro-chave que está sendo editado, não no indicador de reprodução. Ao lado ficam os dois quadros-chave de tema em volta desse quadro e o que o slot selecionado contém em cada um. Um slot sem nome aparece como `{{ui:editor_search_unnamed}}`

## Como compartilhar e importar

- **A biblioteca do dispositivo.** `{{ui:editor_level-theme-item_export}}` na linha de um tema o salva em `resources/themes` - a biblioteca compartilhada do dispositivo, onde `resources` fica ao lado de `levels` (veja [[4_level-folder-and-backups]]). `{{ui:settings_level-settings_theme-library}}` mostra essa biblioteca e marca o que já está `{{ui:editor_theme-library-item_in-level}}`. `{{ui:editor_library_delete}}` remove um tema da biblioteca. Importar copia o tema para o nível, então o nível nunca depende da sua biblioteca. `{{ui:settings_level-settings_theme-library}}` também mostra os temas das coleções, com etiquetas de origem - [[16_library-and-collections]]
- **Os temas do jogo.** `{{ui:editor_search-title_theme}}` oferece os temas que vêm com o jogo ao lado dos temas do nível

A seguir: [[5_color-and-postprocessing|Cor, temas e pós-processamento]], [[1_readability-and-fairness|Legibilidade e justiça]]
