---
title: Servidor para amigos
date: 2026-10-01
tags: [server_host]
---

# Servidor para amigos

Você vai precisar das ferramentas abertas de servidor, da build completa para cada jogador e de um arquivo PublishProfile. Moderar e respeitar as licenças dos níveis cabe ao dono do servidor

> [!warning] Aviso
> As ferramentas de servidor não foram lançadas, o protocolo não foi projetado. Esta página contém só o que já foi decidido

## O que você vai precisar

- **Ferramentas de servidor.** Elas serão abertas, sob MIT. É o mesmo código em que o servidor oficial roda. Você pode construir o seu servidor sobre essas ferramentas ou sobre qualquer coisa baseada nelas
- **A build completa do jogo para todos que se conectam.** As builds do Google Play e da App Store não se conectam a servidores da comunidade. A build completa está no [GitHub](https://github.com/bullet-hero/releases) e no site do projeto
- **Um perfil de publicação.** O arquivo `PublishProfile` decide quais níveis o seu servidor aceita. Mais - [[7_publish-profiles]]
- **Uma máquina para o servidor.** Requisitos de sistema, runtime, portas e a forma de iniciá-lo ainda não são conhecidos

## Perfil de publicação

O perfil define quais licenças são aceitas, de onde um nível pode buscar arquivos e qual é o limite de tamanho dele. Nenhum código precisa mudar para isso

O servidor oficial roda com a predefinição `standard`, definida na configuração do servidor. Comece por ela e afrouxe ou aperte do jeito que lhe convier

## O que você assume

- **Moderação.** O Bullet Hero não modera servidores da comunidade. O EULA da build completa diz isso a cada jogador
- **Nada de comércio.** Por padrão, um nível é distribuído sob *CC BY-NC*, e o autor pode escolher outra licença. Respeite a licença de cada nível. Um nível sob *CC BY-NC* pode ser hospedado e compartilhado de graça, mas você não pode cobrar dinheiro por ele nem lucrar com ele de nenhuma outra forma
- **Direitos sobre os recursos.** Um nível pode conter música e gráficos de outras pessoas. O rigor dessa verificação é decidido pelo seu perfil. Mas uma reclamação sobre a obra de outra pessoa vai chegar a você. As regras do servidor oficial - [[ugc-licensing-policy]]

A permissão para distribuição não comercial é dada pelo autor de cada nível, não pelo jogo. Por isso só o autor pode abrir uma exceção

## O que não se sabe

- como o jogo encontra um servidor e se conecta a ele
- se um servidor da comunidade terá contas
- como os níveis são enviados e entram na lista
- se um servidor para poucas pessoas será configurado de forma diferente de um público

O que já existe para um servidor grande - [[3_advanced-hosting]]
