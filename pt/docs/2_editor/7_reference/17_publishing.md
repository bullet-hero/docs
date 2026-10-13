---
title: Publicação
date: 2026-10-11
tags: [level_author]
---

# Publicação

Um nível só é enviado pela aba "Publicação" das configurações do nível: como arquivo compactado ou para a Oficina Steam. O relatório verifica o nível sozinho, e os erros nele bloqueiam o envio

## A aba "Publicação"

`Publicação` é uma aba das configurações do nível. É o único lugar de onde um nível é enviado para algum destino

No topo, `{{ui:editor_share_destination}}` mostra a forma de envio escolhida. Clicar nele abre `{{ui:editor_share_pick-title}}`: as formas que esta build oferece neste dispositivo, cada uma com uma descrição de uma linha. `{{ui:editor_share_archive}}` vem escolhido por padrão. A última escolha é lembrada até o jogo ser fechado

Abaixo dele:
- as configurações próprias da forma
- o relatório dela
- o botão que a executa: `{{ui:editor_share_export}}` ou `Publicar`

Se esta build não tem nenhuma forma neste dispositivo, a aba mostra `{{ui:editor_share_none}}`

## O relatório

O relatório verifica sozinho: quando uma forma abre e quando qualquer configuração dela muda. Não há botão para isso. Ele começa com a linha `Erros: N, avisos: N, sugestões: N`, seguida de uma linha por ocorrência

Os erros bloqueiam o envio. Avisos e sugestões ficam a seu critério

A forma decide as regras pelas quais o nível é julgado. `{{ui:editor_share_archive}}` verifica pelo conjunto `{{ui:editor_publish_profile-local}}`, `{{ui:editor_share_steam}}` pelas regras da Oficina. O que cada conjunto exige e o que cada veredito significa - [[5_publish-readiness]]

## Formas de envio

| Forma | Onde existe | O que envia |
|---|---|---|
| `{{ui:editor_share_archive}}` | em qualquer dispositivo com uma janela de salvar. Não no iOS | um nível, uma coleção ou um recurso, como arquivo |
| `{{ui:editor_share_steam}}` | só na build da Steam | um nível ou uma coleção sua |

Uma forma que esta build ou este dispositivo não tem simplesmente não aparece na lista

## Arquivo compactado

Para um nível:

| Elemento | O que faz |
|---|---|
| `{{ui:editor_share_format}}` | um de sete modos de exportação, de uma pasta simples a um arquivo compactado protegido por senha |
| `{{ui:editor_share_passphrase}}` | visível só nos modos protegidos. Um modo protegido com senha vazia não executa |
| `{{ui:editor_share_export}}` | grava o nível onde você indicar |

O que cada modo grava e com o que abrir - [[13_export-and-protection#Exportar o nível]]

Para uma coleção ou um recurso, `{{ui:editor_share_format}}` oferece cinco desses modos, e todos são arquivos compactados. Não há modos de pasta:

| `{{ui:editor_share_format}}` | O que você recebe | Com o que abrir |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_zip}}` | um único arquivo | um clique duplo no Explorador de Arquivos do Windows, sem instalar nada |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | um zip com criptografia AES-256 embutida | 7-Zip ou outro compactador, que pede a senha |
| `{{ui:settings_level-settings_export-mode_zip-protected}}` | o zip inteiro envolto em OpenPGP | gpg |
| `{{ui:settings_level-settings_export-mode_targz}}` | um único arquivo | qualquer compactador |
| `{{ui:settings_level-settings_export-mode_targz-protected}}` | um tar.gz envolto em OpenPGP | gpg |

`{{ui:editor_share_passphrase}}` aparece nos três modos com senha. Com a senha vazia, nada é exportado. Vale a verificação de coleção descrita abaixo, pelas mesmas regras de `{{ui:editor_publish_profile-local}}`

## Oficina Steam

Só nas builds da Steam. Os elementos:

| Elemento | O que faz |
|---|---|
| `{{ui:editor_publish_visibility}}` | quem vê o item: `{{ui:editor_publish_visibility-public}}`, `{{ui:editor_publish_visibility-friends-only}}` ou `{{ui:editor_publish_visibility-private}}`. Por padrão, `{{ui:editor_publish_visibility-private}}` |
| `{{ui:editor_publish_changelog}}` | a nota de alterações deste envio. Um campo de várias linhas, com o rótulo em uma linha própria |
| `O título e a descrição são enviados em` | o idioma do qual o texto do item é tirado (veja abaixo) |
| `{{ui:editor_share_steam-descriptors}}` | cinco caixas de seleção, os descritores de conteúdo da própria Steam (veja abaixo) |
| `Publicar` | envia o nível |

O nível é sempre verificado pelas regras da Oficina. Aqui não há escolha de regras

O item da Oficina é preenchido a partir do nível:
- o título e a descrição são o nome e a descrição do nível, em um idioma
- a pré-visualização é a capa do nível, png ou jpg, de no máximo 1 MB. Qualquer outra capa é ignorada, e o item é enviado sem imagem
- o jogo define as tags sozinho, veja "Tags da Oficina" abaixo

O primeiro clique em `Publicar` cria o item. Os seguintes atualizam o mesmo item. O jogo o encontra pelo id do próprio nível entre os itens que você publicou, por isso nada é guardado no nível

Um nível protegido não pode ser publicado. Mais - [[13_export-and-protection]]

O envio leva a pasta `ai` do nível, onde um assistente de IA guarda as anotações dele sobre o nível, a menos que `{{ui:settings_level-settings_metadata-level-ai-share}}` esteja desmarcado nos metadados do nível. Todo mundo que assina recebe essa pasta com o nível. Mais - [[7_ai-assistant#A pasta ai]]

> [!warning] Aviso
> Se você não aceitou o contrato legal da Oficina Steam, o item é enviado, mas fica oculto. Aceite o contrato na página do item. O jogo abre essa página na sobreposição da Steam

### Idioma do título

A Steam mostra um título e uma descrição por item. O jogo pega o primeiro idioma que encontrar, nesta ordem:
1. `{{ui:settings_game-editor_publish-language}}` nas configurações `{{ui:settings_game-editor_title}}`: `{{ui:enum_publish-language_english}}` (o padrão) ou `{{ui:enum_publish-language_system}}`, o idioma do dispositivo. Mais - [[14_editor-settings]]
2. o seu idioma, ou seja, o idioma da interface do jogo
3. inglês
4. o primeiro idioma em que o texto foi escrito

A descrição é procurada primeiro no idioma do título, para que os dois combinem. Um nome que não é localizado (texto simples) é enviado exatamente como foi escrito, e a linha diz `{{ui:editor_share_steam-language-as-written}}`

### Descritores de conteúdo

`{{ui:editor_share_steam-descriptors}}` tem cinco caixas de seleção, os descritores de conteúdo da própria Steam:
- `{{ui:editor_share_steam-descriptor-mature}}`
- `{{ui:editor_share_steam-descriptor-violence}}`
- `{{ui:editor_share_steam-descriptor-some-nudity}}`
- `{{ui:editor_share_steam-descriptor-frequent-nudity}}`
- `{{ui:editor_share_steam-descriptor-adult-only}}`

Eles são enviados a cada publicação e nunca são guardados no nível. Cada publicação envia o conjunto inteiro, por isso uma caixa desmarcada também remove o descritor de um item que já foi publicado. Eles são enviados em uma segunda atualização logo depois do envio. Se essa parte falhar, o item continua publicado, e o resultado diz que os descritores não foram definidos

### Depois de publicar

Em caso de sucesso, o formulário mostra qual item foi criado ou atualizado e um botão `{{ui:editor_publish_open-item}}`. Ele abre a página do item na Steam

Em caso de falha, o formulário mostra:
- o motivo em palavras simples, `Falha ao publicar: ...`
- `O que foi enviado e o que a Steam respondeu: ...` - uma linha técnica em inglês. Vale a pena citá-la ao desenvolvedor quando você relatar um problema
- um `?` que explica por que a Steam recusa desse jeito, e três links: `{{ui:editor_publish_help-docs}}` (esta página), `{{ui:editor_publish_help-steam-support}}` e `{{ui:editor_publish_help-agreement}}`

As linhas do próprio log do jogo sobre a publicação estão sempre em inglês, seja qual for o idioma da interface

| Motivo | O que fazer |
|---|---|
| `{{ui:enum_workshop-failure_steam-not-running}}` | inicie a Steam e reinicie o jogo pela Steam |
| `{{ui:enum_workshop-failure_not-owner}}` | publique a partir dessa conta, ou faça uma cópia do nível, que então é enviada como item novo |
| `{{ui:enum_workshop-failure_access-denied}}` | a conta não possui o jogo, a conta é limitada (ainda sem compras na Steam) ou a Oficina está fechada para ela |
| `{{ui:enum_workshop-failure_invalid-param}}` | a Oficina do jogo não está configurada para envios, ou a Steam está rodando com o id de outro jogo. Reinicie a Steam e o jogo |
| `{{ui:enum_workshop-failure_limit-exceeded}}` | exclua itens antigos nos seus arquivos da Oficina |
| `{{ui:enum_workshop-failure_connection}}` | confira a conexão e o status da Steam |
| `{{ui:enum_workshop-failure_invalid-request}}` | um título de até 128 caracteres, uma descrição de até 8000, uma pré-visualização png ou jpg de até 1 MB |
| `{{ui:enum_workshop-failure_staging}}` | confira o espaço livre no disco e se os arquivos do nível não estão abertos em outro programa |

Se um item novo é criado, mas o envio dele é rejeitado, o jogo exclui esse item vazio, para que nenhum item abandonado fique na Oficina

## Builds sem Steam

Uma build sem Steam não mostra `{{ui:editor_share_steam}}` na lista. `{{ui:editor_share_archive}}` continua

## Como compartilhar uma coleção

Uma coleção é compartilhada pela página dela na aba "Biblioteca". `{{ui:editor_share_share}}` abre o mesmo painel em uma janela: `{{ui:editor_share_archive}}` e, na build da Steam, também `{{ui:editor_share_steam}}` para uma coleção sua

A verificação da coleção:
- ela tem um nome
- ela tem uma licença informada
- ela não está vazia
- todo arquivo que ela cita está nela
- todo recurso a que as entradas dela se referem está incluído nela

A falta de licença depende da forma. Para `{{ui:editor_share_archive}}` é um aviso, e a exportação acontece. Para `{{ui:editor_share_steam}}` é um erro. Os erros bloqueiam o envio. Mais sobre coleções - [[16_library-and-collections]]

## Como compartilhar um recurso

Toda linha de tema, forma, efeito e prefab na Biblioteca também tem um botão `{{ui:editor_share_share}}`. Ele empacota o recurso com tudo de que ele precisa (por exemplo, as formas, texturas e prefabs aninhados de um prefab) como uma coleção de uma única entrada

Só `{{ui:editor_share_archive}}` está disponível, com os mesmos cinco formatos de uma coleção, inclusive os com senha. Quem recebe importa o arquivo por `{{ui:editor_library_import-archive}}`, como qualquer coleção

## Tags da Oficina

O jogo define as tags sozinho:

| Item | Tags |
|---|---|
| nível | `level` |
| coleção | `collection` e uma para cada tipo dentro dela: `prefabs`, `themes`, `shapes`, `effects` |

Texturas, fontes e áudio não recebem tags e não vão para a Oficina sozinhos. Eles vão dentro de uma coleção como aquilo que os prefabs, temas, formas e efeitos dela usam. Uma coleção só de mídia é recusada com uma linha que diz o motivo, e é melhor compartilhar uma coleção assim como arquivo compactado

> [!info] Vale saber
> As "Coleções" da própria Steam são listas curadas de itens da Oficina, um recurso da Valve. Elas não têm nada a ver com as coleções do Bullet Hero

## Assinaturas

A build da Steam lê o que você assina:
- os níveis aparecem na lista de níveis em `{{ui:editor_library-source_workshop}}`, [[2_playing-levels]]
- as coleções aparecem na biblioteca do editor no chip `{{ui:editor_library-source_workshop}}`, somente leitura

A seguir: [[5_publish-readiness]], [[1_licensing-basics]], [[16_library-and-collections]]
