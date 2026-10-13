---
title: O que é um nível
date: 2026-10-02
tags: [level_author]
---

# O que é um nível

Um nível é uma pasta comum no disco: o arquivo do nível, os metadados e tudo o que ele usa. Monte-o em Json e passe-o adiante como uma cópia da pasta, não é preciso instalar nada

## O que há na pasta

A pasta não é uma linha em um banco de dados nem um arquivo compactado criptografado

Há dois arquivos principais:
- `level.json` - o nível em si: objetos, quadros-chave, temas, recursos
- `metadata.json` - a capa: nome, descrição, autores, tags, duração

Ao lado deles fica tudo o que o nível usa: a música, as imagens, as fontes.
O jogo não traz nenhuma textura. Tudo o que você vê em um nível é uma forma integrada ou um arquivo desta pasta

A capa é um arquivo separado, para que listar mil níveis não signifique abrir mil níveis

A lista completa de arquivos - [[4_level-folder-and-backups]]

## Json ou Blob

Você escolhe o formato do arquivo ao criar um nível:

| Formato | O que é |
|---|---|
| `Json` | texto simples, abre em qualquer editor e pode ser corrigido à mão |
| `Blob` | um arquivo binário, carrega dezenas de vezes mais rápido e tem um terço do tamanho, não dá para ler a olho |

> [!tip] Recomendação
> Monte o nível em `Json` e converta-o para `Blob` quando estiver terminado. Se o nível deixar de abrir, o `Json` pode ser lido e corrigido à mão. O `Blob` quase não tem conserto: um único byte danificado reprova a verificação de integridade

## Como passar um nível adiante

Um nível viaja por cópia. Compacte a pasta, envie, descompacte, abra.
Nada é instalado, registrado ou importado

No PC isso sempre funciona. No celular - onde o sistema deixar entrar

O que decorre disso:
- um backup de um nível é uma cópia da pasta
- não renomeie arquivos dentro da pasta: os recursos são encontrados pelo nome
- um nível em `Json` que o editor não abre ainda pode ser lido a olho. A aba `{{ui:settings_level-settings_raw}}` só mostra um nível que já está aberto

> [!caution] Cuidado
> Não edite `level.json` em um editor de texto enquanto o nível estiver aberto no jogo. Salvar pelo editor sobrescreve suas edições sem nenhum aviso

## O formato é aberto

O modelo de dados do nível fica em um repositório separado, sob a licença MIT - [bullet-hero/sdk](https://github.com/bullet-hero/sdk).
Por isso um nível pode ser lido sem o jogo, e você pode escrever a própria ferramenta para o formato. Um defeito no formato também fica visível de fora

Mais sobre o formato - [[3_sdk/index]]

A seguir: [[2_first-level]], [[4_level-folder-and-backups]]
