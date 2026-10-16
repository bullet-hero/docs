---
title: Argumentos de inicialização
date: 2026-10-17
tags: [advanced_player, developer]
---

# Argumentos de inicialização

Argumentos de inicialização abrem na hora uma tela, um nível ou uma partida, e interruptores mudam uma só inicialização. Vão após o executável: num atalho, num terminal ou nas opções da Steam

Sem argumentos, o jogo abre o menu principal

Um assistente de IA conectado por MCP pode mandar os mesmos argumentos para um jogo que já está rodando - [[7_ai-assistant]]

## Sintaxe

- todo argumento começa com dois hifens: `--editor`
- um valor vem depois de um espaço ou depois de `=`: `--speed 1.5` e `--speed=1.5` são a mesma coisa
- maiúsculas e minúsculas da chave não importam: `--Editor` também funciona
- os números usam ponto, seja qual for o idioma do sistema: `1.5`, nunca `1,5`
- um valor com espaços vai entre aspas duplas: `--level "D:\My Levels\Volcano"`

**Um argumento que o jogo não consegue usar nunca impede a inicialização.** Ele é descartado, uma linha sobre ele vai para o log, e o jogo abre a tela de sempre. Onde fica o log - [[11_help#Logs]]

**Argumentos desconhecidos são ignorados.** O jogo lê só os próprios argumentos, os que têm dois hifens. Os argumentos da própria Unity, com um hífen, por exemplo `-screen-width`, passam intactos. Defina a resolução e a tela cheia com eles

## Telas

| Argumento | O que abre |
|---|---|
| `--menu` | o menu principal, o mesmo que sem argumentos |
| `--editor` | o editor de níveis |
| `--game` | o nível indicado em `--level`, e a partida começa na hora |
| `--settings` | o menu principal com a tela de configurações por cima |

Passa-se no máximo um argumento de tela. Dois diferentes se anulam, e o menu abre com um aviso no log

`--settings` pode indicar uma aba: `general`, `audio`, `controls`, `keybindings`, `graphics`, `interface`, `game-editor`, `profile`, `other`. Sem nome, as configurações abrem na aba em que você estava da última vez. Um nome desconhecido é descartado, e as configurações abrem mesmo assim

As configurações abrem uma vez por inicialização. Se você voltar ao menu depois, elas não abrem de novo. O que cada aba tem - [[4_settings]]

## Escolher um nível

`--level` indica um nível pelo identificador (`LevelId`) ou pelo caminho da pasta dele. Um título nunca funciona: títulos se repetem, são traduzidos e editados. Um valor que pode ser lido como identificador é sempre tratado como identificador

O nível é procurado entre os que o jogo já mostra na lista. O jogo não encontra uma pasta que não está na lista

| Junto com | O que acontece |
|---|---|
| nada | o menu abre na tela do nível e espera por `{{ui:menu_levelview_play-btn}}` |
| `--editor` | o editor abre com este nível |
| `--game` | a partida começa na hora |

Uma senha nunca é passada como argumento. Um nível protegido pede a senha na tela e abre depois da resposta

## Condições da partida

Estas condições preenchem os controles da tela do nível, e a partida começa como se você tivesse tocado em `{{ui:menu_levelview_play-btn}}`. Elas só funcionam junto com `--game`. Sem ele, são ignoradas, com um aviso no log

| Argumento | Valor | Controle na tela do nível |
|---|---|---|
| `--speed` | acima de `0` e até `2`, arredondado para `0.1` | `{{ui:field_common_speed}}` |
| `--lives` | de `0` a `16`, `0` é `{{ui:menu_levelview_options-lifes_option-zen}}` | `{{ui:menu_levelview_options-lifes_title}}` |
| `--seed` | `0` ou um inteiro positivo, `0` significa uma semente nova a cada partida | `{{ui:level_level-view_seed-value}}` |
| `--bot` | `none`, `reflex`, `warm` | `{{ui:menu_levelview_options-bot}}` |
| `--checkpoints`, `--no-checkpoints` | - | `{{ui:menu_levelview_options-checkpoints_title}}` |
| `--no-collision` | - | `{{ui:menu_levelview_options-no-collision_title}}` |

Uma condição omitida usa o valor padrão: 3 vidas, velocidade `1.0`, checkpoints ativados, sem bot, semente `0`, colisão ativada

Uma partida começada assim é uma partida comum. Ela entra nas estatísticas como qualquer outra, [[10_statistics]]

## Interruptores para a inicialização inteira

Estes três funcionam com qualquer tela e nunca mudam uma configuração salva:

| Argumento | O que faz |
|---|---|
| `--autosave on`, `--autosave off` | ativa ou desativa o salvamento automático do editor nesta inicialização. A aba de configurações `{{ui:settings_game-editor_title}}` mostra o valor forçado e não deixa mudá-lo |
| `--suppress-game-saves` | modo anônimo durante a inicialização inteira. Não dá para desativá-lo dentro do jogo, [[4_settings#Modo anônimo]] |
| `--frame-stats` | grava no log um resumo do tempo de quadro, com o tempo de GPU e de CPU. Serve para medir o desempenho |
| `--frame-stats-windows` | enquanto um nível roda, também grava uma linha a cada {{v:performance.window-hop-seconds}} s de jogo: o quadro do nível e a mediana do tempo de CPU e de GPU. Também liga o `--frame-stats`. Ao fechar o nível, mais uma linha compara cada janela com o que a avaliação previu para ela. Serve para verificar [[17_performance-rating]] |

`--frame-stats` grava uma linha por tela a cada 30 segundos, e também toda vez que muda a janela por cima da tela. Os primeiros 3 segundos de uma tela não contam

## Combinações

| Comando | Resultado |
|---|---|
| nada ou `--menu` | menu |
| `--editor` | o editor sem nenhum nível aberto |
| `--settings` | menu, com as configurações abertas na aba em que você estava da última vez |
| `--settings graphics` | o mesmo, na aba `{{ui:settings_graphics_title}}` |
| `--level X` | menu na tela do nível X, esperando por `{{ui:menu_levelview_play-btn}}` |
| `--level X --game` | o nível X, com uma partida em andamento |
| `--level X --editor` | o editor com o nível X aberto |
| `--game` sem `--level` | menu e um aviso |
| `--menu --editor` | menu e um aviso |
| `--speed 2` sem `--game` | a condição é ignorada, com um aviso |
| `--editor --autosave off` | o editor, com o salvamento automático desativado só nesta inicialização |
| `--autosave maybe` | ignorado com um aviso, quem decide é a sua configuração |
| `--suppress-game-saves` | menu. Nenhum dos salvamentos próprios do jogo desta inicialização chega ao disco |
| `--level X --game --suppress-game-saves` | o nível X, com uma partida em andamento, e nenhuma estatística fica depois dela |
| `--editor --suppress-game-saves` | o editor. Os salvamentos de níveis, o salvamento automático e os backups são gravados, as configurações e as estatísticas não |

## Exemplos

No Windows, por um terminal ou um atalho:

```bash
"Bullet Hero.exe" --editor
"Bullet Hero.exe" --level 5f2b0e6a-1c3d-4b5e-8a9f-0d1e2f3a4b5c --game --lives 1 --speed 1.5
"Bullet Hero.exe" --level "C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero\levels\Volcano" --editor
```

Na Steam, as opções de inicialização do jogo levam só os argumentos, sem o executável: `--editor --autosave off`

## Android

O Android não tem linha de comando. Os argumentos vão no extra de texto `bh` do intent que inicia o jogo e são divididos exatamente como uma linha digitada. A partir de um computador, isso é feito com `adb`:

```bash
adb shell "am start -S -n com.vertoker.BulletHero/com.unity3d.player.UnityPlayerGameActivity -e bh '--frame-stats --editor'"
```

- **As aspas importam.** O `am start` inteiro vai entre aspas duplas, e o valor de `bh` entre aspas simples. Senão o shell do dispositivo divide a linha: só o primeiro argumento chega a `bh`, e o resto vai para o `am` como parâmetros dele
- **`-S` primeiro fecha o jogo que está rodando.** Os argumentos são lidos uma vez, na inicialização. Mandá-los para um jogo que já está rodando não muda nada

O iOS não tem nenhum argumento de inicialização
