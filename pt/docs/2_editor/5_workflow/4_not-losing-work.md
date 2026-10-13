---
title: Não perder seu trabalho
date: 2026-10-02
tags: [level_author]
---

# Não perder seu trabalho

Seu trabalho é protegido pelo salvamento automático, pelo desfazer e por uma cópia da pasta do nível. Só a cópia da pasta é um retrato completo do nível. Mudar o formato do arquivo e excluir um nível não têm desfazer

Cada proteção cobre o que as outras não cobrem. O salvamento automático e o desfazer não substituem uma cópia da pasta, porque o nível inteiro é uma única pasta

## O hábito

> [!tip] Recomendação
> `Ctrl+S` depois de cada seção terminada. Uma cópia da pasta do nível antes de cada reestruturação. A verificação `{{ui:settings_level-settings_rules}}` antes de considerar o nível terminado

## Salvamento automático

O salvamento automático vem ligado por padrão. Ele funciona assim:
1. Aparece uma edição não salva - começa uma contagem regressiva de `60` segundos
2. O jogo grava uma cópia do nível em `backups/<id do nível>/` na pasta do jogo, fora de `levels`
3. Depois salva o próprio nível, como `Ctrl+S` faria

Um editor aberto sem mudanças não grava nada.
Tudo o que mudou desde o último salvamento, seu ou automático, existe só na memória

São mantidas `25` cópias, e a mais antiga é excluída primeiro.
Uma cópia contém só o arquivo do nível, sem metadados, música nem imagens. Ela sobrevive à exclusão do nível, a menos que você marque `{{ui:root_level-delete_backups}}`.
A cópia de um nível protegido é trancada com a senha do próprio nível

A opção de ligar, o intervalo e a quantidade de cópias ficam em `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}`

**Restauração:** configurações do nível, aba `{{ui:settings_level-settings_dangerous-zone}}`, `{{ui:level_backups_open}}`. As cópias vão da mais nova para a mais antiga, e cada uma tem como nome o momento em que foi feita.
O arquivo atual é copiado antes para `backups`, então uma restauração também pode ser revertida

Também dá para restaurar à mão: copie o backup para a pasta do nível como `level.json` (ou `level.blob`)

## Mudanças não salvas

Uma ação que substituiria o nível aberto ou sairia dele pergunta primeiro o que fazer com as edições não salvas:
- abrir outro nível pela lista de níveis, incluindo copiar um nível e abrir a cópia
- criar um nível
- `{{ui:settings_level-settings_quit}}` nas configurações do editor e nas configurações do nível
- `{{ui:level_backups_open}}`
- em `{{ui:settings_level-settings_dangerous-zone}}`: copiar o nível e abrir a cópia, mudar o formato do arquivo, definir uma senha

A caixa de diálogo tem três respostas:
- `{{ui:editor_save_text}}` - salva o nível e continua a ação
- `{{ui:editor_unsaved-changes_discard}}` - o botão vermelho, a única resposta que perde edições
- `{{ui:editor_cancel_text}}` - não faz nada

Jogar a partir das configurações do nível também pergunta, mas com duas respostas: `{{ui:editor_unsaved-changes_save-play}}` e `{{ui:editor_cancel_text}}`. Aqui as edições não podem ser descartadas, porque, ao voltar do jogo, o nível é lido do disco de novo.
Se não há nada sem salvar, a caixa de diálogo não aparece

## O que o desfazer cobre

O desfazer cobre as edições do nível, e só elas. Toda mudança em objetos, quadros-chave, recursos, temas, prefabs e configurações passa por um único buffer de operações

O que não muda o nível não é desfeito:
- o gizmo escolhido, a ferramenta da linha do tempo, se o encaixe e a grade estão ligados
- a disposição dos painéis, a aba aberta, a posição do indicador de reprodução
- as áreas de transferência
- uma semente de sessão gerada de novo. Recarregar o nível escolhe outra
- **o salvamento**. O desfazer reverte o nível na memória, não o arquivo no disco

## O que não tem desfazer nenhum

Duas ações gravam direto no disco:
- **Mudar o formato do arquivo do nível.** Gravar o nível como `Blob` exclui o `Json` anterior. E um `Blob` não pode ser lido nem consertado a olho
- **Excluir um nível.** Por isso essa ação fica escondida em `{{ui:settings_level-settings_dangerous-zone}}`

## A aba de dados brutos

A aba `{{ui:settings_level-settings_raw}}` mostra o arquivo salvo inteiro como uma árvore de campos. Ela não verifica nada: nem regras, nem limites

É o último recurso. Todas as edições de uma sessão são aplicadas como uma única operação, e ela pode ser desfeita

> [!caution] Cuidado
> Nada verificou o que você escreveu na aba `{{ui:settings_level-settings_raw}}`. Tenha uma cópia da pasta do nível à mão. Mais - [[4_level-folder-and-backups#Backups e recuperação]]

## Regras

A verificação que vale a pena rodar é a aba `{{ui:settings_level-settings_rules}}`. Ela mostra o que a validação encontrou: referências quebradas, ids duplicados, ciclos de pais, prefabs aninhados fundo demais, segmentos de batida sobrepostos

O jogo consegue corrigir algumas ocorrências: uma de cada vez ou todas de uma vez com o botão `{{ui:settings_level-settings_rules-fix-all}}`.
As correções são aplicadas com o botão `{{ui:editor_save_text}}`, como uma única operação que pode ser desfeita. `{{ui:settings_level-settings_raw-discard}}` as descarta.
Ocorrências do grafo não têm correção

O intervalo de um filho que passa do intervalo do pai não é um erro. São dados normais, e se comportam como planejado.
Para ajustar os tempos de vida, rode o modificador `{{ui:mod_span_fit}}`

A seguir: [[4_level-folder-and-backups|A pasta do nível e os backups]], [[1_order-of-work|A ordem de trabalho]]
