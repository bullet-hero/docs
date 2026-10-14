---
title: Transferência de perfil
date: 2026-10-14
tags: [player]
---

# Transferência de perfil

O seu perfil inteiro cabe em um único arquivo zip: níveis, estatísticas, configurações e a biblioteca. Exporte-o antes de reinstalar ou de passar para outro dispositivo, depois importe-o lá

Os botões ficam em `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_profile-transfer_title}}`. Funciona no Windows, Mac, Linux e Android. Não está disponível no iOS

## O que entra no arquivo

| Parte | Na pasta de dados | Marcada por padrão |
|---|---|---|
| `{{ui:settings_profile-transfer_category-levels}}` | `levels` | sim |
| `{{ui:settings_profile-transfer_category-statistics}}` | `stats` | sim |
| `{{ui:settings_profile-transfer_category-settings}}` | `settings.json` | sim |
| `{{ui:settings_profile-transfer_category-library}}` | `resources` | sim |
| `{{ui:settings_profile-transfer_category-backups}}` | `backups` | não |
| `{{ui:settings_profile-transfer_category-reports}}` | `reports` | não |
| `{{ui:settings_profile-transfer_category-recordings}}` | `recordings` | não |

O arquivo é um zip comum e abre em qualquer programa de compactação. Dentro estão as mesmas pastas da pasta de dados ([[1_installation]]), mais `profile.json`, que descreve o arquivo

## Exportar

1. Toque em `{{ui:settings_profile-transfer_export}}`
2. Marque as partes de que você precisa
3. Escolha onde salvar o arquivo

Exportar funciona em qualquer lugar onde as configurações abrem: no menu principal, em uma partida pausada e no editor. Antes, as estatísticas são gravadas no disco, então o arquivo sai atualizado

## Importar

1. Abra as configurações pelo menu principal e toque em `{{ui:settings_profile-transfer_import}}`
2. Escolha o arquivo zip
3. Marque as partes e escolha o modo
4. Confirme

Importar só funciona pelo menu principal. Um nível em andamento ou um editor aberto está usando os próprios arquivos, e eles não podem ser substituídos por baixo dele

| Modo | O que acontece |
|---|---|
| `{{ui:settings_profile-transfer_mode-replace}}` | cada parte marcada é esvaziada e preenchida a partir do arquivo |
| `{{ui:settings_profile-transfer_mode-merge}}` | os níveis são adicionados. Um nível que existe dos dois lados é substituído por inteiro pela cópia mais nova. As estatísticas guardam o maior valor de cada contador e o melhor recorde. Os arquivos da biblioteca, os salvamentos automáticos e os relatórios só são adicionados, os seus continuam |

Toda importação pergunta mais uma vez antes de gravar qualquer coisa. Substituir diz quais partes vai esvaziar, mesclar diz quantos níveis vai adicionar, substituir e manter

**Configurações de outro tipo de dispositivo.** Um perfil de um celular importado em um computador (ou o contrário) mantém os seus próprios controles e gráficos. Todo o resto vem do arquivo

O jogo recusa um arquivo de uma versão mais nova do jogo - atualize o jogo antes. Ele também recusa um arquivo que não é zip, um zip que não é um perfil, um zip protegido por senha e um arquivo danificado. Em nenhum desses casos nada é alterado

## Backup

Antes de qualquer importação, o jogo salva em um único backup as partes que está prestes a substituir. Ele fica na pasta `profile-backups`, dentro da pasta de dados. Existe só um: a próxima importação o sobrescreve

- `{{ui:settings_profile-transfer_backup-restore}}` coloca o backup de volta. O que ele substitui vira o novo backup, então uma restauração também pode ser desfeita
- `{{ui:settings_profile-transfer_backup-save-as}}` salva uma cópia onde você escolher
- `{{ui:settings_profile-transfer_backup-delete}}` exclui o backup
- `{{ui:settings_profile-transfer_clear-cache}}` exclui a pasta `profile-backups` inteira: o backup e o que uma transferência interrompida tiver deixado para trás

`{{ui:settings_profile-transfer_backup-to-folder}}` vem marcado por padrão durante uma importação: o jogo pergunta na hora onde guardar uma cópia fora do jogo

> [!caution] Cuidado
> No Android, o backup fica na pasta de dados do jogo e é apagado junto com o jogo. Antes de desinstalar, exporte o perfil ou salve o backup em outro lugar

Se o jogo fechar no meio de uma importação, a próxima inicialização devolve o perfil ao estado em que estava

## Steam Cloud

Na versão da Steam, seu perfil acompanha sua conta Steam sozinho. Não há botão: o jogo sincroniza uma vez ao iniciar, envia o que muda enquanto você joga e sincroniza uma última vez ao fechar

O interruptor é da Steam: a caixa Steam Cloud nas propriedades do jogo na Steam. Se ela está ligada e quando foi a última sincronização aparece em `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_cloud_title}}`

| Parte | Quando os dois dispositivos a mudaram |
|---|---|
| `{{ui:settings_profile-transfer_category-statistics}}` | cada contador fica com o maior valor e o melhor recorde, nada se perde |
| `{{ui:settings_profile-transfer_category-settings}}` | a cópia mais nova vence. `{{ui:settings_graphics_title}}` e `{{ui:settings_controls_title}}` continuam sempre sendo os de cada dispositivo |
| `{{ui:settings_profile-transfer_category-levels}}` | a cópia mais nova de um nível vence inteira. A outra vai para os backups do editor no dispositivo que perdeu |
| `{{ui:settings_profile-transfer_category-library}}` | a cópia mais nova de cada arquivo vence |

- Um nível excluído em um dispositivo é excluído nos outros também. Cada um guarda o último estado dele nos backups do editor
- As estatísticas excluídas em um dispositivo são excluídas nos outros também. Se outro dispositivo jogou depois da última sincronização, o progresso dele é mantido
- Um nível maior que o espaço que a Steam deixa para o jogo fica só no dispositivo dele
- `{{ui:settings_profile-transfer_category-backups}}`, `{{ui:settings_profile-transfer_category-reports}}` e `{{ui:settings_profile-transfer_category-recordings}}` não são sincronizados
- Uma cópia na nuvem escrita por uma versão mais nova do jogo não é tocada até você atualizar o jogo neste dispositivo
- O nível aberto no editor não é substituído: ele sincroniza no próximo início
- Com `{{ui:settings_other_suppress-game-saves}}` ligado, nada é sincronizado

## Trocar de versão no Android

Uma cópia do jogo instalada a partir de um arquivo (itch.io e parecidos) não pode ser atualizada pelo Google Play, e vice-versa. As versões são assinadas de jeitos diferentes, por isso o Android recusa a atualização. Para trocar:

1. Exporte o perfil e salve o arquivo fora do jogo
2. Desinstale o jogo
3. Instale a outra versão
4. Importe o perfil
