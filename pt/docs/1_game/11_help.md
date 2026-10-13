---
title: Ajuda e relatórios de bugs
date: 2026-10-02
tags: [player, level_author]
---

# Ajuda e relatórios de bugs

Bugs do jogo vão para as issues do releases, perguntas vão para o Discord. Anexe a linha de versão das configurações e os passos depois dos quais o bug aparece

Confira primeiro [[5_troubleshooting]]. Um nível sumido, "o jogo precisa ser atualizado" e um arquivo compactado recusado estão explicados lá

## Onde escrever

| O quê | Onde |
|---|---|
| um bug no jogo ou no editor, um pedido para o jogo | [bullet-hero/releases](https://github.com/bullet-hero/releases/issues) |
| um bug no SDK ou no código dele | [bullet-hero/sdk](https://github.com/bullet-hero/sdk/issues) |
| um erro ou um dado desatualizado na documentação | [bullet-hero/docs](https://github.com/bullet-hero/docs), [[community]] |
| uma pergunta, ajuda com um nível, uma discussão | [Discord](https://discord.gg/gkHQrp9NgS) |

As mensagens no GitHub são públicas. Qualquer pessoa pode lê-las e complementá-las. Você pode enviar uma issue ou um pull request para a documentação

Não tem certeza de que é um bug? Pergunte primeiro no Discord

Todos os links do projeto - [[links]]

## O que colocar em um relatório de bug

Um bug que pode ser reproduzido é corrigido. "Travou" normalmente não tem como ser corrigido: ninguém sabe o que repetir

1. **A linha de versão.** Clique na linha de versão na tela de configurações e ela é copiada sozinha. Ela tem este formato: `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`, [[4_settings]]
2. **Plataforma e dispositivo:** o sistema e, no caso de um celular, o modelo
3. **Passos:** o que você fez, o que esperava e o que aconteceu
4. **O nível,** se o bug estiver ligado a ele: a pasta dele em um arquivo compactado, ou o arquivo compactado que você abriu. Se o nível for protegido, avise
5. **O relatório de erro,** se apareceu uma janela de erro. `{{ui:root_error_save}}` o grava na pasta `reports`, `{{ui:root_error_open-reports-folder}}` abre a pasta, [[1_installation]]

> [!tip] Dica
> Anexe os arquivos à mensagem em vez de colá-los no texto. Um log é longo e, dentro do texto, fica difícil de ler

## Logs

O jogo grava um log enquanto está rodando. Ele ajuda quando nem apareceu uma janela de erro

- **Windows:** `Player.log` na pasta de dados do jogo, `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` (o local padrão da Unity)
- **Android:** o log vai para o logcat. Com o dispositivo conectado a um computador, `adb logcat -s Unity` o exibe
- **Outros sistemas:** ainda não descritos
