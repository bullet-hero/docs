---
title: "Seu primeiro nível: o caminho"
date: 2026-10-02
tags: [level_author]
---

# Seu primeiro nível: o caminho

Seis passos até o primeiro teste de jogo: criar um nível, adicionar a música, marcar o ritmo, posicionar objetos, fazer um teste de jogo, salvar

## Seis passos

Aqui está só a ordem de trabalho. O que cada campo faz é explicado pela ajuda ao lado do painel dele

**1. Crie o nível.** `{{ui:settings_editor-settings_editor-settings}}` → `{{ui:settings_editor-settings_create-level}}`. Escolha uma predefinição, defina um nome e uma duração. A duração pode ser mudada depois

**2. Adicione a música.** Copie o arquivo de áudio para a pasta do nível e conecte-o. `ogg` funciona melhor, e `flac` não carrega. Mais - [[2_preparing-the-track]]

**3. Marque o ritmo.** A aba `{{ui:editor_inspector-beat_tab}}`: BPM, deslocamento, batidas por compasso. A grade não é para o jogo, é para você: o conteúdo se encaixa nela

Não sabe o andamento? Marque-o com toques junto com a música na janela `{{ui:editor_beat-window_title}}` (`Shift+T`). Marcar com toques não tem tecla padrão

**4. Posicione os primeiros objetos.** Crie um objeto, dê a ele uma forma e coloque dois quadros-chave na posição dele. O jogo leva o valor de um quadro-chave ao outro sozinho

**5. Confira.** Faça um teste de jogo direto do editor. O mais provável é que tudo se mova rápido demais ou devagar demais. Isso é normal: a velocidade só se ajusta de ouvido

**6. Salve.** `Ctrl+S`

O salvamento automático vem ativado por padrão. {{v:editor.autosave-delay}} segundos depois de uma edição não salva, ele salva o nível e coloca uma cópia em `backups/<level id>/`. Mais - [[4_not-losing-work#Salvamento automático]]

## Mantenha o primeiro nível pequeno

> [!tip] Recomendação
> Escolha uma música curta, de 1-2 minutos. Um nível de 4 minutos é quatro vezes mais trabalho e dez vezes mais motivos para abandoná-lo pela metade

Comece pelo padrão mais simples que funciona, não pelo mais difícil que você imaginou.
Jogue o nível de ponta a ponta antes de mostrá-lo a alguém

Deixe geradores, prefabs e modificadores para depois. Eles poupam tempo em um nível grande e atrapalham no primeiro

## A música e os direitos

Uma música para uso próprio não precisa da permissão de ninguém. Os direitos só são verificados quando você publica.
Mais - [[1_licensing-basics]]

As regras completas para publicar no servidor oficial - [[ugc-licensing-policy]]

## Próximos passos

Como o editor funciona - [[3_how-the-editor-thinks]]

Depois do primeiro teste de jogo - o design de níveis: [[2_editor/4_craft/index]]

Quando o nível crescer além de um rascunho - [[1_order-of-work]]
