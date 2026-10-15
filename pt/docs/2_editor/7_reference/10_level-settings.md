---
title: Configurações do nível
date: 2026-10-15
tags: [level_author]
---

# Configurações do nível

Aqui se define tudo o que pertence ao próprio nível: duração, fps, semente, orientação, metadados, publicação. Daqui também o nível é iniciado, verificado pelas regras e restaurado de uma cópia

## Jogar

As opções de início valem **só para esta partida**. Nada daqui é salvo no nível

`{{ui:settings_level-settings_life-text}}`, `{{ui:field_common_speed}}`, `{{ui:settings_level-settings_checkpoints-toggle}}` e o nível automático permitem ensaiar um trecho sem editá-lo

> [!tip] Dica
> A `{{ui:settings_level-settings_seed}}` daqui tem prioridade sobre a semente do próprio nível. É a prioridade mais alta das três. Use-a para repetir exatamente a partida que você acabou de ver. `0` significa usar a semente do próprio nível, ou uma nova a cada partida

Mais - [[3_difficulty-curve]]

## Núcleo

Duração em quadros, taxa de quadros e as duas sementes do nível

`{{ui:settings_level-settings_core-seed-value}}` é a semente do próprio nível. Ela faz parte do conteúdo, e alterá-la pode ser desfeito. `0` significa "uma semente nova a cada partida". É o valor padrão, por isso um nível comum é jogado de um jeito diferente a cada vez

> [!tip] Dica
> `{{ui:settings_level-settings_core-runtime-seed-value}}` só mostra qual semente esta sessão do editor resolveu. `{{ui:settings_level-settings_core-runtime-seed-regenerate}}` sorteia uma nova só para a sessão: nada é gravado e nada entra no histórico de desfazer. Ao recarregar o nível, a semente é resolvida de novo

> [!info] Vale saber
> **Um quadro é uma célula, e o tempo é um limite.** Os quadros contam a partir de 1. O quadro *f* cobre o tempo de (*f*-1)/fps até *f*/fps, sem incluir este último. Um nível de N quadros contém os quadros de 1 a N. N+1 é o limite final, não um quadro

Mais - [[4_frames-and-time]]

## Orientação do nível

Em que posição o aparelho é segurado durante este nível

`{{ui:enum_level-orientation_horizontal}}` e `{{ui:enum_level-orientation_vertical}}` giram o aparelho do jogador enquanto o nível dura. Essa escolha tem prioridade sobre a configuração do jogador. Um monitor não pode ser girado. Por isso, no computador, um nível vertical é jogado com barras nas laterais, e é assim que deve ficar

`{{ui:enum_level-orientation_not-specified}}` deixa a escolha para o jogador. Não é um valor padrão, e sim uma afirmação sobre o seu nível: ele fica legível nas **duas** orientações. O jogo não ajusta nada para isso: nada é deslocado, cortado ou escalado. O conteúdo além das bordas horizontais fica fora da tela em uma orientação e visível na outra. Escolha essa opção só depois de conferir o nível das duas formas

## Zona de perigo

Ações que excluem ou reescrevem arquivos, e não conteúdo

> [!caution] Cuidado
> As listas `{{ui:settings_level-settings_quot-level-quot-file-format}}` e `{{ui:settings_level-settings_quot-metadata-quot-file-format}}` reescrevem o nível e os metadados dele no disco. Trocar o formato **exclui o arquivo no formato antigo**. Nada mais acontece: não há recarga nem nova simulação, a seleção e o histórico de desfazer continuam. O que é gravado é exatamente o que já está na memória

> [!caution] Cuidado
> `{{ui:settings_level-settings_delete-level-open}}` remove a pasta do nível do disco. Isso não pode ser desfeito

Mais - [[4_not-losing-work]]

## Regras

Problemas que a validação encontrou neste nível:
- referências quebradas
- ids duplicados
- ciclos de pais
- prefabs aninhados fundo demais
- segmentos de batida sobrepostos

> [!info] Vale saber
> **Algumas ocorrências podem ser corrigidas, uma de cada vez ou com `{{ui:settings_level-settings_rules-fix-all}}`.** As correções vão para um rascunho: `{{ui:editor_save_text}}` as aplica como uma única operação que pode ser desfeita, `{{ui:settings_level-settings_raw-discard}}` as descarta. As ocorrências do grafo (ids, pais, aninhamento de prefabs) não têm correção, e isso é de propósito: cada uma é uma decisão sobre o conteúdo que só você pode tomar, e uma correção automática escolheria em silêncio uma entre várias respostas válidas

> [!tip] Dica
> Um filho que ultrapassa o intervalo do pai **não** é apontado. São dados válidos que se comportam como previsto. Se você quiser ajustar os tempos de vida, rode o modificador `{{ui:mod_span_fit}}` nos geradores. Ele encolhe os filhos para dentro ou estende os pais para fora

Mais - [[4_not-losing-work]]

## Metadados

Tudo sobre o nível que não é o próprio nível: nome, descrição, capa, licença, classificação etária, dificuldade e autores

O nome e a descrição são escritos para cada idioma, aqui mesmo. Um jogador cujo idioma você não preencheu recebe o primeiro que você preencheu

> [!info] Vale saber
> Aqui não são necessárias chaves de tradução. Um nível é conteúdo, não parte da interface do jogo

A licença e os autores acompanham o nível onde quer que ele seja compartilhado. É assim que o crédito sobrevive a um novo envio

`{{ui:settings_level-settings_difficulty}}` mostra um ícone grande do grau e um botão com o número salvo e o nome do grau, por exemplo `3 · {{ui:enum_difficulty-tier_rain}}`. O botão abre um menu com todos os graus, cada um com o número e o ícone: `0` é `{{ui:enum_difficulty-tier_undefined}}`, de `1` a `{{v:difficulty.scale-max}}` são os graus de `{{ui:enum_difficulty-tier_auto}}` a `{{ui:enum_difficulty-tier_singularity}}`

O padrão é `{{ui:enum_difficulty-tier_undefined}}`: nesse caso o jogador não vê nenhum ícone. Um moderador que republica o nível pode sobrescrever o grau. Continua sendo um só valor, não dois. Um valor acima de `{{v:difficulty.scale-max}}` aparece no botão com o próprio número, ao lado de `{{ui:enum_difficulty-tier_singularity}}`, e fica como foi escrito até você escolher outro grau

Mais - [[2_metadata-and-sharing]]

## Tags do nível

As tags são palavras suas. Elas aparecem exatamente como foram escritas e nunca são traduzidas. O jogador filtra os níveis por elas no navegador de níveis

Escreva as tags separadas por vírgula. Mantenha-as curtas e gerais: um gênero, um clima, uma mecânica. Uma tag só ajuda se outros níveis também a usam. Uma tag que mais ninguém vai digitar não filtra nada

## Coleções

Traz recursos de uma coleção para o nível ou monta uma coleção com os recursos do próprio nível. A aba fica logo depois de `{{ui:editor_library_kind-prefabs}}`

- `Importar` - abra uma coleção, marque as entradas e clique em `Importar`. As dependências vêm junto, e toda a importação é um único passo de desfazer
- `{{ui:editor_collections_mode-build}}` - marque os recursos do nível e clique em `{{ui:editor_collections_build}}`, em `{{ui:editor_collections_target-new}}` ou em uma coleção sua

Uma entrada que o nível já tem em outra versão abre `{{ui:editor_resource-conflict_title}}`. Nada é sobrescrito em silêncio

Mais - [[16_library-and-collections]]

## Publicação

O único lugar de onde um nível é enviado para algum destino: como arquivo compactado ou para a Oficina Steam

`{{ui:editor_share_destination}}` escolhe o destino. Abaixo ficam os controles próprios desse destino, o relatório dele e o botão que o executa. O relatório verifica o nível sozinho, sem botão para apertar. Os erros bloqueiam o envio, os avisos e as sugestões não

Mais - [[17_publishing]]

## Histórico

Cada edição desta sessão é uma linha aqui. As mais recentes ficam em cima, como em um `git log`

A coluna mais à esquerda é a linha principal. Uma coluna própria é um ramo. É uma linha que você deixou para trás quando desfez uma edição e seguiu outro caminho

O anel marca onde você está. O círculo verde marca o último salvamento

Clicar em uma linha leva o nível de volta exatamente àquele estado. O percurso aplica uma operação por quadro. Assim você vê o nível mudar em vez de esperar diante de uma tela congelada

> [!warning] Aviso
> Enquanto um percurso está em andamento, o editor fica só para leitura. Ainda dá para mover a câmera e arrastar o indicador, mas não editar. Cancelar para o percurso onde ele estiver, e esse é sempre um estado real do nível

> [!tip] Dica
> O histórico vive só na sessão atual. Ele nunca é gravado no disco, e reabrir o nível o começa do zero. O tamanho dele é limitado: primeiro saem os ramos abandonados mais antigos, depois as edições mais antigas

## Dados brutos

Todo o modelo salvo do nível como uma árvore de campos. É o próprio arquivo, antes de o editor processá-lo

> [!caution] Cuidado
> **Nada aqui é validado.** Esta é a saída de emergência para o que nenhuma outra tela cobre ainda. Ela grava um valor que o resto do editor considera impossível

Um ponto cheio ao lado de um campo significa que você o alterou nesta sessão. Um ponto vazado significa que algo dentro dele mudou. Sem ele, uma mudança três níveis abaixo em um ramo recolhido ficaria invisível

O botão `{{ui:settings_level-settings_raw-apply}}` fica oculto, e não desativado, quando não há nada para aplicar. Uma aplicação vazia colocaria uma troca do nível na pilha de desfazer sem motivo

Mais - [[4_not-losing-work]]
