---
title: Perguntas frequentes
date: 2026-10-02
tags: [player, level_author]
---

# Perguntas frequentes

Bullet Hero é um híbrido gratuito de jogo de ritmo e bullet hell. Não exige conta, e ainda não há servidor. Os jogadores criam níveis no editor integrado e os trocam como pasta ou arquivo compactado

## O jogo

### O que é Bullet Hero?

Um híbrido de *jogo de ritmo* e *bullet hell*. Um nível é música e formas que se movem com ela. Você controla um pequeno quadrado, e ele precisa sobreviver até o fim da música

Bullet Hero é construído como um motor para o gênero. Por isso a maioria dos níveis é feita pelos jogadores no editor integrado.
Mais - [[1_game/index]]

### O jogo é gratuito?

Sim. O jogo não tem compras, anúncios nem conteúdo pago.
Mais - [[1_licensing-basics]]

### Onde conseguir o jogo?

Todos os builds e lojas - [[download]]

O jogo já foi lançado, versão `gv {{v:version.gv}}`. Os builds não são assinados

### Precisa de conta ou de internet?

Não. Não há contas nem servidor, e o jogo não envia nada para lugar nenhum

A internet só é necessária para um tipo de nível: aquele que carrega um arquivo do endereço web do autor.
Mais - [[1_installation]]

### Onde os níveis ficam armazenados?

Na pasta `levels`, dentro da pasta de dados do jogo. Para abri-la: `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general-open_folder}}`.
Mais - [[1_installation]]

## Jogando níveis

### Como jogar um nível que alguém enviou para você?

Coloque a pasta em `levels` e clique em `{{ui:root_level-browser_refresh}}` na lista de níveis.
Um arquivo compactado (`.zip`, `.tar.gz`) é aberto pelo editor, com o gerador `{{ui:gen_level_archive}}`.
Mais - [[2_playing-levels]]

### O jogo diz que o nível é de uma versão mais nova. E agora?

Atualize o jogo. Uma versão antiga não abre arquivos de uma versão mais nova, para nunca lê-los de forma errada.
Mais - [[5_troubleshooting]]

### Dá para recuperar a senha esquecida de um nível?

Não. A chave não fica armazenada em lugar nenhum: nem no jogo, nem no arquivo, nem com ninguém.
Mais - [[5_troubleshooting]]

### O jogo consegue jogar um nível sozinho?

Sim, com a condição `{{ui:menu_levelview_options-bot}}` na tela do nível: `{{ui:enum_bot-kind_reflex}}` ou `{{ui:enum_bot-kind_warm}}`. Um bot tem os mesmos controles que você, e também pode perder.
Mais - [[9_bots]]

## Criando níveis

### Como criar o primeiro nível?

`{{ui:menu_main_editor-btn}}` no menu principal, depois `{{ui:settings_editor-settings_editor-settings}}`, depois `{{ui:settings_editor-settings_create-level}}`.
Copie uma música para a pasta do nível, defina o andamento (bpm), coloque um objeto com dois quadros-chave e faça um teste de jogo.
Mais - [[2_first-level]]

### Quais arquivos de música funcionam?

`ogg`, `mp3` e `wav`, nada mais. `flac`, `aiff` e módulos de tracker não carregam

`ogg` é a melhor escolha. Ele é 8-10 vezes menor que `wav` e, ao contrário do `mp3`, não adiciona silêncio ao início.
Mais - [[2_preparing-the-track]]

### Posso usar qualquer música?

Nada é verificado no seu próprio disco. A licença da música importa quando um nível é oferecido a um serviço, e ainda não existem serviços assim.
Mais - [[1_licensing-basics]]

### Como compartilhar um nível?

À mão, como pasta ou arquivo compactado. Um build da Steam também pode publicar um nível na Oficina Steam. Ainda não há servidor oficial.
Mais - [[6_sharing-by-hand]], [[17_publishing]]

## O projeto

### Existem rankings online ou um catálogo de níveis?

Ainda não. O servidor oficial e os servidores da comunidade estão em desenvolvimento.
Mais - [[4_server/index]]

### Por que o código do jogo é fechado?

Tenho motivos pessoais para isso.
Quando o desenvolvimento parar de vez, todos os repositórios vão se tornar abertos, e a organização [bullet-hero](https://github.com/bullet-hero) talvez passe para as mãos de outra pessoa

O SDK, a documentação e o futuro servidor já são abertos. Mais - [[index]]

### Encontrou um bug?

Relate bugs do jogo em [bullet-hero/releases](https://github.com/bullet-hero/releases/issues). Leve as perguntas para o [Discord](https://discord.gg/gkHQrp9NgS).
Onde escrever e o que anexar - [[11_help]]

Todos os links do projeto - [[links]]
