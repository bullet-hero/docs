---
title: Biblioteca e coleções
date: 2026-10-02
tags: [level_author]
---

# Biblioteca e coleções

As coleções guardam os recursos que você reutiliza entre níveis. Um nível nunca se refere a uma coleção: importar copia o recurso para dentro, e o nível roda em qualquer lugar

## O que é uma coleção

**Uma coleção** é uma pasta de recursos reutilizáveis. Ela pode guardar recursos de sete tipos:

| Tipo | Como é armazenado |
|---|---|
| prefabs, temas, formas, efeitos | dados, um arquivo por entrada |
| texturas, fontes, áudio | arquivos de mídia |

Uma coleção não está presa a um nível. Ela fica no seu dispositivo e está disponível em qualquer nível que você abrir

## Origens

A biblioteca mostra recursos de três origens. Cada uma é um chip de filtro acima da lista:

| Chip | O que é | Pode ser alterada |
|---|---|---|
| `{{ui:editor_library-source_library}}` | a biblioteca do dispositivo: `resources/prefabs`, `themes`, `shapes`, `effects` | sim |
| `{{ui:editor_library-source_local}}` | as suas coleções, `resources/collections` | sim |
| `{{ui:editor_library-source_workshop}}` | as coleções que você assina na Oficina Steam, lidas no próprio lugar. Só nas builds da Steam | não |

Uma coleção somente leitura é alterada assim: as entradas dela são copiadas para uma coleção sua

## A aba "Biblioteca"

`{{ui:settings_editor-settings_library}}` é a última aba da tela inicial do editor, depois de `{{ui:settings_editor-settings_community}}`

Uma coluna estreita de botões escolhe o tipo:
- `{{ui:editor_library_kind-collections}}`
- `{{ui:editor_library_kind-prefabs}}`, `{{ui:editor_library_kind-themes}}`, `{{ui:editor_library_kind-shapes}}`, `{{ui:editor_library_kind-effects}}`
- `{{ui:editor_library_kind-textures}}`, `{{ui:editor_library_kind-fonts}}`, `{{ui:field_common_audio}}`

À direita dela, o título da página (à esquerda) e os botões dela (à direita) ficam em uma só linha. A lista fica embaixo. Uma lista vazia diz isso no meio dela

Nas páginas dos sete tipos, de `{{ui:editor_library_kind-prefabs}}` a `{{ui:field_common_audio}}`, `{{ui:editor_library_copy-target}}` ocupa uma linha separada de largura total abaixo do título. Os chips de origem ficam na linha abaixo dela

Uma janela da Biblioteca (o cartão de uma coleção, a imagem de uma textura, a janela de compartilhamento) fecha com o X no canto. Não existe botão `{{ui:editor_library_close}}`

Cada linha é um botão. Clicar nela faz a ação principal do tipo dela:

| Tipo | Clicar em uma linha |
|---|---|
| coleção | abre a página dela |
| tema, forma, efeito | abre o editor |
| textura | mostra a imagem e o tamanho dela |
| prefab, fonte, áudio | nada. Uma linha de áudio tem um botão de reprodução próprio |

Os botões pequenos à direita de uma linha são as outras ações, e o ícone de lixeira exclui ou remove

`{{ui:editor_library_open-folder}}` mostra a pasta da página atual no gerenciador de arquivos do sistema. Disponível só no Windows, macOS e Linux

### Coleções

`{{ui:editor_library_open-folder}}` e `{{ui:editor_library_refresh}}` ficam à direita do título da página. `Nova coleção` e `{{ui:editor_library_import-archive}}` ficam em uma linha separada abaixo dele, alinhados à direita

- `Nova coleção` cria uma coleção vazia e abre o cartão dela
- `{{ui:editor_library_import-archive}}` adiciona uma coleção a partir de um arquivo `.zip` ou `.tar.gz` ou de um arquivo compactado protegido por senha: um `.zip` com senha própria, `.zip.gpg` ou `.tar.gz.gpg`. Se essa coleção já está no dispositivo, o jogo pergunta se deve substituí-la

Um arquivo compactado protegido por senha abre a janela `{{ui:editor_library_passphrase-title}}`: `{{ui:editor_library_passphrase-needed}}`. Digite a senha e clique em `{{ui:editor_library_open}}`. Uma senha errada mostra `{{ui:editor_library_passphrase-wrong}}`
- `{{ui:editor_library_open-folder}}` abre `resources/collections`
- `{{ui:editor_library_refresh}}` lê as pastas de novo

As suas coleções têm `{{ui:editor_library_edit}}` e o ícone de lixeira. A lixeira pergunta antes e depois exclui a coleção com todos os arquivos dela

### O cartão de uma coleção

`{{ui:editor_library_edit}}` abre uma janela com o cartão da coleção:
- `{{ui:editor_library_field-name}}`, `{{ui:field_common_description}}`
- `{{ui:editor_library_field-authors}}`, separados por vírgula
- `{{ui:editor_library_field-license}}`: `{{ui:editor_library_license-unspecified}}` ou uma das licenças típicas
- `{{ui:editor_library_set-cover}}` escolhe uma imagem png. A linha ao lado diz se há uma capa

`{{ui:editor_save_text}}` grava o cartão. `{{ui:editor_cancel_text}}`, o X ou um clique fora da janela descarta as alterações

### A página de uma coleção

| Elemento | O que faz |
|---|---|
| `{{ui:settings_common_back}}` | volta para a lista |
| `{{ui:editor_library_edit}}` | abre o cartão. Só para as suas coleções |
| `{{ui:editor_share_share}}` | abre a janela de compartilhamento: `{{ui:editor_share_archive}}` como `.zip` ou `.tar.gz`, com ou sem senha, e na build da Steam também `{{ui:editor_share_steam}}` para uma coleção sua |
| `{{ui:editor_library_open-folder}}` | abre a pasta própria da coleção |
| `{{ui:editor_library_delete}}` | exclui a coleção, perguntando antes |

Abaixo fica o conteúdo. Uma linha abre a entrada do mesmo jeito que a página do tipo dela, e o ícone de lixeira remove a entrada da coleção

Uma coleção somente leitura diz `{{ui:editor_library_read-only}}`

Mais sobre `{{ui:editor_share_share}}` - [[17_publishing]]

### Prefabs, temas, formas, efeitos

Cada uma destas páginas mostra todas as entradas de todas as origens. Os chips estreitam a lista

`{{ui:editor_library_copy-target}}` escolhe uma das suas coleções. Por padrão é `{{ui:editor_library_copy-target-none}}`. Depois que um destino é escolhido, toda linha vinda de outro lugar ganha `{{ui:editor_library_copy-to}}`

Um tema, uma forma ou um efeito abre no mesmo editor das configurações do nível. `{{ui:editor_save_text}}` grava a alteração onde a entrada vive: em `{{ui:editor_library-source_library}}` ou na sua coleção. Uma entrada da Oficina abre somente leitura, e `{{ui:editor_save_text}}` fica desativado. Para alterá-la, copie-a para uma coleção sua

`{{ui:editor_library_new-entry}}` cria um tema, uma forma ou um efeito novo no editor. A entrada é salva na coleção de destino, ou em `{{ui:editor_library-source_library}}` se nenhum destino foi escolhido. Os prefabs são criados em um nível e não têm `{{ui:editor_library_new-entry}}`

As entradas que você pode alterar têm o ícone de lixeira, e ele pergunta antes

Toda linha tem `{{ui:editor_share_share}}`. O botão empacota a entrada com tudo de que ela precisa (por exemplo, as formas, texturas e prefabs aninhados de um prefab) em um `.zip` ou `.tar.gz`, com ou sem senha, como uma coleção de uma única entrada. Quem recebe importa esse arquivo por `{{ui:editor_library_import-archive}}`, como qualquer coleção

`{{ui:editor_library_open-folder}}` abre a pasta da biblioteca do dispositivo para aquele tipo, por exemplo `resources/themes`

### Texturas, fontes, áudio

Estas páginas mostram os arquivos de todas as coleções. Não existe biblioteca pessoal para arquivos, por isso esses tipos vivem só em coleções

- uma linha de textura mostra a imagem
- uma linha de áudio tem um botão de reprodução. Toca uma faixa por vez, e ela para quando você sai da página
- uma linha de fonte não tem pré-visualização

`{{ui:editor_library_add-file}}` coloca um arquivo do dispositivo na coleção de destino, por isso sem destino o botão fica desativado. Uma textura é png ou jpg, uma fonte ttf ou otf, um áudio mp3, wav ou ogg. Se a coleção já tem um arquivo com os mesmos bytes, nada é adicionado, e o jogo avisa

As linhas têm `{{ui:editor_library_copy-to}}` e o ícone de lixeira

### O que uma cópia leva junto

Uma cópia leva tudo de que a entrada precisa: as formas, texturas, fontes e prefabs aninhados de um prefab, a forma das partículas de um efeito. As informações de autoria desses recursos também vão junto com eles

## A aba "Coleções"

`{{ui:editor_library_kind-collections}}` é uma aba das configurações do nível, logo depois de `{{ui:editor_library_kind-prefabs}}`. No topo há dois modos: `Importar` e `{{ui:editor_collections_mode-build}}`

### Importar

1. A aba mostra uma lista de coleções. Clique na que você precisa
2. Marque as entradas de que precisa. `{{ui:editor_collections_select-all}}` e `{{ui:editor_collections_select-none}}` marcam tudo ou limpam todas as marcações
3. A linha `Selecionados: N, dependências adicionadas: M` mostra o que vai entrar no nível. As dependências são adicionadas sozinhas
4. Clique em `Importar`

Toda a importação é um único passo de desfazer

Texturas, fontes e áudio recebem ids novos no nível, e os arquivos deles são copiados para a pasta do nível com um nome único. Um arquivo que o nível já tem byte a byte não é copiado uma segunda vez: a importação usa a textura, a fonte ou a faixa que o próprio nível já tem

### Criar uma coleção

1. `{{ui:editor_collections_target}}` escolhe `Nova coleção` ou uma das suas. Uma coleção nova recebe o nome do campo `{{ui:editor_library_field-name}}`
2. Marque os recursos do nível, de qualquer um dos sete tipos
3. Clique em `{{ui:editor_collections_build}}`

Uma coleção nova recebe os autores do nível

Não é possível criar uma coleção a partir de um nível protegido. Mais - [[13_export-and-protection]]

## Escolha de recursos e pesquisa

A pesquisa e as janelas de escolha de recursos têm uma seção `{{ui:settings_editor-settings_library}}` para prefabs, temas, formas e efeitos. Ela mostra todas as origens. As janelas de escolha são os campos de forma, colisor, efeito e tema e `{{ui:cmd_editor_place-prefab}}`

Escolher uma entrada da biblioteca a importa para o nível com as dependências dela e a atribui. Um conflito faz a mesma pergunta que na aba "Coleções"

Os navegadores da biblioteca dentro das abas de recursos do nível funcionam do mesmo jeito e mostram os chips de origem. Mais - [[11_level-resources]]

## Conflitos

Uma entrada importada pode já estar no nível com o mesmo id:
- o mesmo conteúdo - não é preciso fazer nada
- conteúdo diferente - a janela `{{ui:editor_resource-conflict_title}}` abre

A janela lista cada conflito, cada um com um interruptor `{{ui:editor_resource-conflict_copy}}`:

| Escolha | Resultado |
|---|---|
| manter (interruptor desativado) | a versão do nível fica e é usada |
| `{{ui:editor_resource-conflict_copy}}` | a versão da coleção é adicionada com um id novo. Tudo o que foi importado junto com ela se refere à cópia |

`{{ui:editor_resource-conflict_all-keep}}` e `{{ui:editor_resource-conflict_all-copy}}` definem todos os interruptores de uma vez. `Importar` aplica a escolha, `{{ui:editor_cancel_text}}` não importa nada

Nenhuma versão vence em silêncio. Todo conflito com conteúdo diferente é decidido nesta janela

## Autoria

Os registros sobre os recursos de um nível cobrem temas, efeitos, formas e prefabs, além de texturas, fontes e áudio. Importar copia os registros necessários para o nível, por isso a autoria chega junto com o recurso

Mais - [[4_resource-record]]

## No disco

As coleções vivem em `resources/collections/<collection-guid>/` na pasta de dados do jogo. É a mesma pasta `resources` ao lado de `levels` onde vive a biblioteca do dispositivo. Mais - [[4_level-folder-and-backups]]

| Caminho | O que guarda |
|---|---|
| `collection.json` ou `collection.blob` | o manifesto: nome, descrição, autores, licença, as entradas de textura, fonte e áudio e as informações de autoria de tudo o que está dentro |
| `cover.png` | a capa, opcional |
| `prefabs/`, `themes/`, `shapes/`, `effects/` | um `<guid>.json` ou `<guid>.blob` por entrada, os mesmos arquivos da biblioteca do dispositivo |
| `media/` | arquivos de textura, fonte e áudio |

Uma coleção é repassada como arquivo compactado: `{{ui:editor_share_share}}` na página dela, `{{ui:editor_library_import-archive}}` na lista. Um arquivo compactado que não é uma coleção é recusado

A seguir: [[17_publishing]], [[2_reuse]], [[4_resource-record]]
