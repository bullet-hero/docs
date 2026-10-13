---
title: Exportação de vídeo
date: 2026-10-03
tags: [level_author]
---

# Exportação de vídeo

O editor renderiza o nível aberto em um arquivo de vídeo pelo ffmpeg do seu computador. A renderização é offline, um quadro por vez, por isso o vídeo sai exato por mais lenta que seja a máquina

A exportação funciona no Windows, macOS e Linux. Ela não está disponível em celulares

## Onde encontrar

- `{{ui:editor_video-export_open}}` na coluna lateral das configurações do nível
- o comando `{{ui:cmd_editor_export-video}}` na paleta de comandos

A janela abre por cima do editor. Se foi aberta pelas configurações do nível, ela volta para elas ao fechar. Enquanto um vídeo renderiza, a janela não pode ser fechada: `{{ui:editor_video-export_stop}}` encerra a renderização

## Instalar o ffmpeg

O ffmpeg não faz parte do jogo. Instale-o uma vez, e a janela o encontra sozinha. É necessária a versão `{{v:ffmpeg.min-version}}` ou mais nova. Uma mais antiga é recusada, e a janela informa a versão que encontrou

| Sistema | Comando de instalação |
|---|---|
| Windows | `winget install ffmpeg` |
| macOS | `brew install ffmpeg` |
| Linux | o pacote da sua distribuição, por exemplo `sudo apt install ffmpeg` |

> [!warning] Aviso
> Algumas distribuições Linux trazem um ffmpeg mais antigo que `{{v:ffmpeg.min-version}}` (o Ubuntu 24.04 traz o 6.1). Nesse caso, instale uma build mais nova do site do ffmpeg e indique-a na janela

A janela procura o ffmpeg nesta ordem:
1. o arquivo que você escolheu com `{{ui:editor_video-export_ffmpeg_choose}}`. Então nada mais é procurado
2. o caminho na variável de ambiente `BH_FFMPEG`
3. `tools/ffmpeg` dentro da pasta de dados do jogo
4. cada pasta em `PATH`
5. as pastas em que os instaladores comuns gravam

`{{ui:editor_video-export_ffmpeg_auto}}` esquece o arquivo escolhido e procura de novo. `{{ui:editor_video-export_ffmpeg_check}}` repete a verificação, por exemplo logo depois de instalar

O seu ffmpeg pode conter codificadores de hardware (NVIDIA, AMD, Intel, Apple). A janela testa cada um em um décimo de segundo de preto e usa só os que de fato funcionam neste computador

## Opções da janela

| Opção | O que faz |
|---|---|
| `{{ui:editor_video-export_container}}`, `{{ui:editor_video-export_codec}}` | o tipo de arquivo e como ele é comprimido, veja os formatos abaixo |
| `{{ui:editor_video-export_resolution}}` | o tamanho do vídeo. Largura e altura são números pares de `{{v:video-export.min-size}}` a `{{v:video-export.max-size}}` |
| `{{ui:editor_video-export_fps}}` | quadros por segundo do vídeo, até `{{v:video-export.max-fps}}`. Não depende da taxa de quadros do próprio nível. Abaixo de `{{v:video-export.min-simulation-rate}}`, cada quadro é simulado em vários passos, para que o bot jogue como joga no jogo |
| `{{ui:editor_video-export_range}}` | o nível inteiro, o trecho de loop da linha do tempo ou um quadro inicial e final seus |
| `{{ui:editor_video-export_quality}}` | quanto espaço o vídeo ocupa. Fica oculta nos formatos que já são sem perdas |
| `{{ui:editor_video-export_full-chroma}}` | cor para cada pixel em vez de um pixel sim, outro não. Linhas finas coloridas mais nítidas, um arquivo maior |
| `{{ui:editor_video-export_seed}}` | a semente da aleatoriedade do nível. `0` mantém a semente que o editor está usando |
| `{{ui:editor_video-export_preroll}}` | quantos segundos antes do início são reproduzidos, mas não gravados, para que os efeitos já tenham o seu histórico. `{{v:video-export.default-preroll}}` por padrão, até `{{v:video-export.max-preroll}}` |
| `{{ui:editor_video-export_bot}}` | `{{ui:enum_bot-kind_reflex}}` por padrão, `{{ui:enum_bot-kind_warm}}` ou `{{ui:enum_bot-kind_none}}` para um vídeo sem avatar. Os impactos não fazem nada durante uma exportação |
| `{{ui:editor_video-export_post-processing}}`, `{{ui:editor_video-export_effects}}` | os mesmos interruptores do editor, só para o vídeo |
| `{{ui:editor_video-export_audio}}` | as faixas do nível no vídeo |

Cada opção tem o seu próprio `?` na janela

A interface do editor, a grade, os gizmos, a seleção e os limites da câmera nunca entram no vídeo. A câmera do nível enquadra a imagem, e barras pretas preenchem o que a proporção dela não cobre

## Velocidade de renderização

O vídeo não depende da velocidade do seu computador. O tempo do nível e o bot avançam exatamente um quadro do vídeo por quadro renderizado, por isso uma máquina lenta renderiza o mesmo vídeo, só que mais tarde

`{{ui:enum_bot-kind_warm}}` calcula a rota inteira antes do primeiro quadro, e a janela mostra até onde ele chegou. Se ele não encontrar uma rota, a exportação para e pede outro bot

## Formatos

Um formato são duas escolhas: `{{ui:editor_video-export_container}}` e `{{ui:editor_video-export_codec}}`. Só aparecem os pares que o seu ffmpeg consegue gerar. A linha abaixo deles diz qual som acompanha o par e que arquivo você recebe

| `{{ui:editor_video-export_container}}` | `{{ui:editor_video-export_codec}}` | Som | Bom para |
|---|---|---|---|
| `{{ui:editor_video-export_container_mp4}}` | H.264, HEVC, AV1 | `{{ui:editor_video-export_audio-codec_aac}}` | enviar e publicar em qualquer lugar |
| `{{ui:editor_video-export_container_mkv}}` | H.264, HEVC, AV1, VP9, FFV1 | `{{ui:editor_video-export_audio-codec_flac}}` | arquivamento, FFV1 sem nenhuma perda |
| `{{ui:editor_video-export_container_mov}}` | H.264, HEVC, ProRes | `{{ui:editor_video-export_audio-codec_pcm}}` | edição no Premiere, DaVinci Resolve, Final Cut |
| `{{ui:editor_video-export_container_webm}}` | VP9, AV1 | `{{ui:editor_video-export_audio-codec_opus}}` | a web |
| `{{ui:editor_video-export_container_gif}}`, `{{ui:editor_video-export_container_webp}}`, `{{ui:editor_video-export_container_apng}}` | - | sem som | clipes curtos em loop para chats e páginas |
| `{{ui:editor_video-export_container_sequence}}` | PNG, JPEG, WebP, TIFF | `audio.wav` ao lado dos quadros | qualquer editor importa |
| `{{ui:editor_video-export_container_audio}}` | WAV, FLAC, MP3, Opus | o próprio formato | só o som do nível, nada é renderizado |

O GIF usa uma única paleta de 256 cores para o clipe inteiro. Mantenha-o curto e pequeno: um GIF de um nível inteiro pesa muito mais que um MP4 do mesmo nível

## Para onde o vídeo vai

Por padrão, o vídeo vai para `recordings/<level id>/` na pasta de dados do jogo, com o nome do nível e a hora da exportação. `{{ui:editor_video-export_output_folder}}` abre essa pasta. `{{ui:editor_video-export_output_choose}}` salva o próximo vídeo em qualquer outro lugar

As gravações ficam quando você exclui o nível. Elas não fazem parte de uma transferência de perfil, a menos que você marque `{{ui:settings_profile-transfer_category-recordings}}`

## Som

O som do vídeo não é gravado dos alto-falantes, e você não ouve nada durante uma exportação

Com `{{ui:editor_video-export_engine-audio}}` ativado (o padrão) e efeitos nas faixas, o som do nível toca em tempo real enquanto os quadros renderizam, e o próprio som do jogo é gravado, efeitos incluídos. A exportação dura pelo menos a duração do trecho: um computador rápido espera o som terminar. Desativado, as faixas são mixadas à parte, com os quadros-chave de volume e pan, mas sem os efeitos. `{{ui:editor_video-export_container_audio}}` sempre mixa à parte

Abaixo da pré-visualização, a janela mostra duas linhas do tempo, `{{ui:editor_video-export_track_frames}}` e `{{ui:editor_video-export_track_sound}}`: elas andam de forma independente. Em um nível pesado, o som em paralelo pode engasgar. Nesse caso, ative `{{ui:editor_video-export_sound-after-frames}}`: o som é gravado depois do último quadro, e a exportação demora mais pela duração do trecho

> [!warning] Aviso
> Não feche o jogo enquanto um vídeo renderiza. A janela avisa isso durante toda a execução

## O que não entra no vídeo

- os efeitos nas faixas de áudio, mas só com `{{ui:editor_video-export_engine-audio}}` desativado ou em `{{ui:editor_video-export_container_audio}}`. A janela avisa quando o nível tem esses efeitos
- um fundo transparente
- uma gravação de como você jogou: só o bot pode jogar no vídeo

Leia a seguir: [[13_export-and-protection]], [[7_audio]]
