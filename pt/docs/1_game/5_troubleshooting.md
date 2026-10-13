---
title: Solução de problemas
date: 2026-10-03
tags: [player]
---

# Solução de problemas

Nível copiado à mão aparece após nova busca. Nível mais novo pede atualizar o jogo, e .7z precisa virar zip. Senha esquecida não se recupera. Atividade no Discord: só na versão Steam, com o app aberto

Não achou o seu problema? Onde relatá-lo - [[11_help]]

## Um nível não está na lista

- **Copiado à mão.** A pasta do nível precisa ficar diretamente em `levels`, [[1_installation]]. Depois de copiar, toque em `{{ui:root_level-browser_refresh}}`
- **Um item da Oficina.** A versão da Steam mostra só as suas inscrições. `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general_show-all-found-content}}` adiciona as pastas encontradas no disco. Elas vêm marcadas com `{{ui:root_level-entry_not-listed}}`
- **Não aparece nada.** A pasta de níveis pode estar inacessível. Nesse estado a limpeza do armazenamento em `{{ui:settings_other_title}}` não roda e diz `A busca por níveis não encontrou nada, então esta limpeza foi recusada`

## Um nível não carrega

A tela de carregamento mostra a etapa: `{{ui:root_loading_reading}}`, `{{ui:root_loading_validating}}`, `{{ui:root_loading_resources}}`, `{{ui:root_loading_building}}`

- **Um arquivo em um endereço da web.** Um nível pode pegar um arquivo de um link em vez de guardá-lo na própria pasta. `{{ui:settings_general_title}}` → `{{ui:settings_general_resource-web-timeout}}` é quantos segundos o jogo espera por esse arquivo
- **Um nível danificado.** Um nível em `Json` é texto, dá para lê-lo a olho. Um `Blob` danificado é recusado inteiro. Mais - [[4_level-folder-and-backups]]
- **Uma janela de erro.** Ela tem `{{ui:root_error_copy}}`, `{{ui:root_error_save}}` e `{{ui:root_error_open-reports-folder}}`. O relatório vai para a pasta `reports`. Anexe-o a um relatório de bug em [bullet-hero/releases](https://github.com/bullet-hero/releases/issues), [[11_help]]
- **`O nível precisa de mais objetos por quadro do que este dispositivo permite`.** Isso não é um erro de carregamento. O nível roda, mas parte dele não é desenhada. Mais - [[1_level-budget]]

## "Atualização necessária"

Uma versão mais antiga do jogo não abre arquivos de uma mais nova. Atualize o jogo

| Mensagem | O que fazer |
|---|---|
| `Este nível foi feito em uma versão mais nova do jogo...` | atualizar o jogo |
| `Este arquivo compactado contém um nível de uma versão mais nova do jogo...` | atualizar o jogo |
| `A área de transferência contém conteúdo do editor copiado em uma versão mais nova do jogo...` | atualizar o jogo |
| `Suas configurações ou estatísticas foram salvas por uma versão mais nova do jogo...` | `{{ui:root_update-required_download}}`, `{{ui:root_update-required_keep}}` ou `{{ui:root_update-required_overwrite}}` |

Um cartão marcado com `{{ui:root_level-entry_newer-version}}` ou `{{ui:root_level-entry_newer-file}}` é a mesma recusa. Ela aparece antes mesmo de o nível ser aberto

### Configurações ou estatísticas de uma versão mais nova

Nesse caso o jogo roda com os padrões. Até ser fechado, ele não salva nada próprio, e os arquivos mais novos ficam intactos. Esse é o modo anônimo, [[4_settings]]. Com `--suppress-game-saves` não existe o botão `{{ui:root_update-required_overwrite}}`

As estatísticas de nível de uma versão mais nova não são mostradas. Jogar o nível as sobrescreve, a não ser que os salvamentos estejam desativados

### Por que o jogo recusa

Toda mudança no formato de arquivo recebe um novo número de geração. Uma versão do jogo não lê um arquivo de geração mais nova, para não lê-lo errado

## Um nível protegido

Antes de abrir, o jogo pede uma `{{ui:level_passphrase_password}}`. A senha é pedida uma vez por sessão e fica só na memória

Só o conteúdo é criptografado: objetos, quadros-chave, temas. O título, a capa e as mídias continuam legíveis, por isso o cartão aparece mesmo sem a senha

Excluir um nível protegido não exige a senha

> [!caution] Cuidado
> Uma senha esquecida não pode ser recuperada. A chave não fica guardada em lugar nenhum - nem no jogo, nem no arquivo, nem com ninguém

## Um arquivo compactado é recusado

| Mensagem | Causa |
|---|---|
| `{{ui:editor_create-level_archive-unsupported}}` | é `.7z`. Compacte de novo como `.zip` |
| `{{ui:editor_create-level_archive-wrong-password}}` | a senha não confere |
| `{{ui:editor_create-level_archive-damaged}}` | o arquivo compactado está corrompido, peça para mandarem de novo |
| `{{ui:editor_create-level_archive-not-archive}}` | o arquivo nem é um arquivo compactado de nível |

Um arquivo compactado renomeado não é problema: o jogo reconhece o formato pelos bytes do arquivo. Quais arquivos compactados são aceitos - [[2_playing-levels]]

## O Discord não mostra o que estou jogando

- **Não é uma versão da Steam.** Só as versões da Steam mostram a sua atividade no Discord
- **O Discord está fechado.** O aplicativo de computador do Discord precisa estar aberto no mesmo computador. Abriu depois do jogo? O status aparece na próxima troca de tela
- **A atividade está oculta.** No Discord: `User Settings` -> `Activity Privacy` -> compartilhe as atividades detectadas
- **Um nível próprio não mostra nome.** É de propósito: só um nível da Oficina ou um que vem com o jogo é nomeado, e o editor nunca nomeia o nível dele. Por quê - [[game-privacy-policy#Discord Rich Presence]]
