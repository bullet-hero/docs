---
title: Skins
date: 2026-10-15
tags: [player, advanced_player]
---

# Skins

O corpo do avatar é uma grade de células, e a skin decide o que cada célula desenha: uma forma e uma das cores da skin. Uma skin também pode desligar os olhos, as mãos, a sombra e os efeitos. Monte uma no menu principal, em `{{ui:menu_main_avatar-btn}}`, com formas prontas, uma paleta e um editor de grade, ou escreva o arquivo à mão

Uma skin muda só a aparência. A hitbox, a velocidade e o anel da hitbox são os mesmos para todas as skins

## O hub do avatar

`{{ui:menu_main_avatar-btn}}` no menu principal abre uma tela própria. Seu avatar anda à esquerda, e o painel ocupa a metade direita. `{{ui:menu_avatar_bot}}`, no canto inferior esquerdo, passa o avatar para você, para testar a skin em movimento, e o controle `{{ui:menu_avatar_damage}}` ao lado dele mostra como a skin perde células quando a vida cai. A barra no topo do painel leva a cada seção:

| Seção | O que faz |
|---|---|
| `{{ui:menu_avatar_tab-shapes}}` | formas prontas, desenhadas com os olhos e as mãos que vêm com elas. Um clique coloca a forma na sua skin e mantém suas cores. As formas redondas e poligonais vêm com olhos, as estampadas vêm sem. O primeiro cartão é o avatar clássico: ele é vestido inteiro, com as cores e tudo |
| `{{ui:menu_avatar_tab-colors}}` | as cores do corpo e os olhos. Escolha um alvo e depois uma cor. As mãos, os rastros e o tom do dash seguem suas cores sozinhos |
| `{{ui:menu_avatar_elements}}` | cada botão liga ou desliga uma parte do avatar |
| `{{ui:menu_avatar_editor}}` | a própria grade: o tamanho dela, as peças nas células, a forma, a cor, a rotação, o espelhamento e a escala de cada peça, e formas suas |

`{{ui:menu_avatar_randomize}}`, no canto superior direito, dá à sua skin uma forma e cores aleatórias. Ele fica desativado enquanto você usa o avatar clássico. `{{ui:menu_avatar_tab-skins}}`, ao lado, lista seus arquivos de skin: um clique em um deles faz você vesti-lo, e os botões exportam, excluem, importam e duplicam. `{{ui:menu_avatar_create}}` cria uma skin nova a partir de uma forma aleatória com cores aleatórias. Um arquivo que o jogo não consegue ler ainda pode ser excluído por ali

Toda mudança é salva na hora. A primeira mudança no avatar clássico cria um novo arquivo de skin, e a partir daí você veste esse arquivo

### O editor

1. `{{ui:menu_avatar_paint}}` coloca a peça selecionada numa célula, `{{ui:menu_avatar_erase}}` a esvazia. Arraste pela grade para mudar várias células de uma vez
2. `{{ui:menu_avatar_pieces}}` lista o que as células podem desenhar. `+` copia a peça selecionada, `-` a remove, e as células dela passam para a primeira peça
3. A peça selecionada usa uma forma embutida ou uma das formas próprias da skin. `{{ui:menu_avatar_new-mesh}}` desenha uma nova: coloque pontos e depois ligue três deles num triângulo
4. `{{ui:menu_avatar_columns}}` e `{{ui:menu_avatar_rows}}` mudam o tamanho da grade. As células são quadradas, então uma grade mais alta do que larga dá um corpo alto
5. `{{ui:menu_avatar_rotate-left}}` e `{{ui:menu_avatar_rotate-right}}` giram a skin inteira um quarto de volta: a grade e cada peça junto com ela

O topo de uma skin é a frente dela: o avatar gira para apontar para onde se move

Uma mudança que quebra o corpo - poucas células, ou células em dois pedaços - não é salva. O motivo aparece embaixo da grade até você corrigir

## Onde as skins ficam

Na pasta `skins` dentro da pasta de dados ([[1_installation]]). Uma skin é um arquivo `.json`. O `selection.json` ao lado lembra qual skin você está usando

- no computador, `{{ui:menu_avatar_open-folder}}` abre a pasta
- no celular, use `{{ui:menu_avatar_import}}` e `{{ui:menu_avatar_export}}`: eles abrem o seletor de arquivos do sistema

As skins vão junto com a transferência de perfil e com o Steam Cloud - [[14_profile-transfer]]

## O arquivo

Assim é uma skin exportada, resumida:

```json
{"g":3,"v":{
  "id":"9b2f0d64-1c3a-4e8b-8f21-6a0c5d7e9f13",
  "name":"Hex knight",
  "size":1.0,
  "columns":5,"rows":5,
  "mask":60651675406,
  "cells":[0,0,0,0,1,1,1,0,0,1,2,1,0,0,1,1,1,0,0,0,0],
  "parts":[
    {"shape":"00000000-0000-0000-0000-000000016000","color":0},
    {"shape":"00000000-0000-0000-0000-000000001000","color":1,"scale":0.9},
    {"shape":"4d1f6c2a-7b3e-4f10-9a55-2c8e01b7d001","color":2,"rotation":90.0,"mirror":true}
  ],
  "colors":[[0,{"r":0.51,"g":0.76,"b":0.96,"a":1.0}],[0,{"r":0.2,"g":0.4,"b":0.9,"a":1.0}],[0,{"r":1.0,"g":1.0,"b":1.0,"a":1.0}]],
  "meshes":[{"id":"4d1f6c2a-7b3e-4f10-9a55-2c8e01b7d001","vts":[[0,{"x":-0.5,"y":-0.5}],[0,{"x":0.5,"y":-0.5}],[0,{"x":0.0,"y":0.5}]],"idxs":[0,1,2]}],
  "elements":125
}}
```

`g` é a geração do formato do arquivo, `v` guarda a skin. O mais fácil é exportar uma skin e editar a cópia

| Chave | O que é |
|---|---|
| `id` | quem a skin é: um GUID próprio. O jogo dá ao arquivo o nome dele, mas encontra a skin por essa chave, então o nome do arquivo não importa |
| `name` | o nome mostrado na lista |
| `size` | o tamanho em que o corpo é desenhado, de `{{v:skin.size-min}}` a `{{v:skin.size-max}}` do clássico. A hitbox não muda |
| `columns`, `rows` | a largura e a altura da grade, de `{{v:skin.grid-min}}` a `{{v:skin.grid-max}}`. As células são quadradas: o lado mais longo cobre o corpo todo |
| `mask` | quais células estão preenchidas, como um único número de 64 bits: a célula na coluna `x` e na linha `y` é o bit `y * 8 + x`, com a linha 0 embaixo. A linha tem sempre 8 bits de largura, seja qual for o valor de `columns` |
| `cells` | a peça que cada célula preenchida desenha, um índice em `parts`, na ordem dos bits a partir do mais baixo. Se ficar vazio, toda célula desenha a peça 0 |
| `parts` | o que uma célula desenha: `shape` (o id de uma forma embutida ou o `id` de uma das `meshes` da skin), `color` (um índice em `colors`), `rotation` (graus), `mirror` e `scale` (de `{{v:skin.part-scale-min}}` a `{{v:skin.part-scale-max}}` da célula) |
| `colors` | as cores do corpo, de 1 a `{{v:skin.colors-max}}`. Uma cor se escreve `[0,{"r":…,"g":…,"b":…,"a":…}]`, cada canal de 0 a 1 |
| `meshes` | até `{{v:skin.meshes-max}}` formas próprias da skin: um `id` (qualquer GUID que não seja de uma forma embutida), pontos `vts` dentro da caixa de -0.5 a 0.5 e triângulos `idxs`, de três pontos cada |
| `elements` | quais partes do avatar são desenhadas, como a soma de: olhos 1, mãos 2, sombra 4, rastro 8, rastro do dash 16, brilho do golpe 32, tom do dash 64. 127 desenha tudo, uma skin nova começa em 125: tudo menos as mãos. A grade é sempre desenhada |
| `eyes`, `hands`, `shadow`, `move_effect`, `dash_effect`, `damage_effect`, `dash_body` | as cores do resto do avatar, na mesma forma que `colors`. Uma parte desligada em `elements` mantém sua cor |

Uma chave omitida fica com o valor do avatar clássico. O id de uma forma embutida é mais fácil de copiar de uma skin exportada: as formas prontas estampadas em `{{ui:menu_avatar_tab-shapes}}` usam só formas embutidas. Um arquivo escrito à mão pode omitir o `id` - `{{ui:menu_avatar_import}}` dá um a ele

## O que uma skin precisa seguir

- `columns` e `rows` vão de `{{v:skin.grid-min}}` a `{{v:skin.grid-max}}`, e `mask` não preenche nenhuma célula fora deles
- pelo menos `{{v:skin.filled-min}}` células estão preenchidas, e todas se tocam por um lado: o corpo é uma peça só
- `cells` está vazio ou tem exatamente uma peça para cada célula preenchida
- no máximo `{{v:skin.parts-max}}` peças, e a forma e a cor de cada peça existem
- o corpo e a sombra são desenhados com opacidade de pelo menos `{{v:skin.body-alpha-min}}`

Uma skin que quebra uma regra aparece em cinza em `{{ui:menu_avatar_tab-skins}}` com o motivo, e não pode ser vestida. O mesmo vale para um segundo arquivo com o mesmo `id`. Se a skin em uso quebrar, o avatar clássico é desenhado e sua escolha é mantida. Uma skin escrita por uma versão mais nova do jogo mostra `{{ui:menu_avatar_newer}}`

## Vida

A vida é mostrada só pelas células preenchidas. As células perdidas ficam como fantasmas escuros, da borda para o centro, e a última célula aguenta enquanto restar alguma vida. Com menos células preenchidas, cada uma vale mais vida - [[7_damage]]
