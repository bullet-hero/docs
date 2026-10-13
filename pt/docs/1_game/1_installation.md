---
title: Instalação
date: 2026-10-02
tags: [player]
---

# Instalação

O jogo guarda níveis, configurações e estatísticas em uma única pasta de dados. Atualizar é seguro: a versão nova lê todos os dados antigos. No Android, desinstalar o jogo apaga também os níveis

Baixe aqui - [[download]]

## Onde ficam os seus arquivos

| Sistema | Pasta |
|---|---|
| Windows | `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` |
| Android | `/storage/emulated/0/Android/data/com.vertoker.BulletHero/files` |

O jeito mais rápido de abri-la é pelo jogo: `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general-open_folder}}`

O que tem dentro:

| Pasta | O que guarda |
|---|---|
| `levels` | os seus níveis, cada um na própria pasta |
| `backups` | os salvamentos automáticos do editor |
| `stats` | as estatísticas |
| `settings.json` | as configurações |
| `reports` | os relatórios de erro |

## Desinstalação

No Windows, no Linux e no Mac a versão gratuita traz um desinstalador ao lado do jogo: `unins000.exe` no Windows, `unins000` no Linux e `unins000` ao lado de `Bullet Hero.app` no Mac. Execute-o e ele remove o jogo sozinho, sem fazer nenhuma pergunta. Os seus níveis, configurações e estatísticas continuam na pasta de dados

Ele remove só os arquivos do próprio jogo. O que você mesmo colocou na pasta do jogo continua lá, e a pasta só some quando fica vazia. Se o jogo estiver aberto, o desinstalador primeiro o fecha, como o botão de fechar faria, e junto com ele o servidor MCP da IA. Um nível com alterações não salvas as perde, por isso salve-o antes de desinstalar

Se o jogo foi instalado pelo instalador do Windows, ele é removido como qualquer outro programa, nas Configurações do Windows, em Aplicativos

Uma versão de loja é removida pela própria loja

## Atualização

Uma versão nova do jogo lê todos os dados antigos sem problemas, seja qual for a atualização e o que quer que tenha mudado

Uma versão antiga não abre níveis de uma mais nova. Se o jogo pedir para atualizar, atualize

Na versão do Google Play, o menu principal oferece uma atualização nova, que é baixada em segundo plano. Quando ela está pronta, o menu principal mostra `{{ui:menu_update-ready_text}}` - toque em `{{ui:menu_update-ready_install-btn}}`. Depois de concluir um nível, ela pode pedir que você avalie o jogo

> [!caution] Cuidado
> No Android, desinstalar o jogo também exclui todos os seus níveis. Exporte o perfil antes de desinstalar - [[14_profile-transfer]]
