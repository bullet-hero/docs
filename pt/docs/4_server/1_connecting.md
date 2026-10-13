---
title: Como se conectar a um servidor
date: 2026-10-01
tags: [player]
---

# Como se conectar a um servidor

O jogo terá o servidor oficial OWS para todas as builds e servidores da comunidade NOWS só na build completa. O Bullet Hero não modera os da comunidade: conecte-se aos de donos que você conhece

> [!warning] Aviso
> Ainda não há servidores, e o jogo não consegue se conectar a eles. Não há formato de endereço, nem tela de conexão, nem contas

## Quais servidores haverá

| | OWS | NOWS |
|---|---|---|
| Nome completo | Official Web Services | Non-official web services |
| Quem roda | Bullet Hero | qualquer pessoa |
| Quem modera | Bullet Hero | o dono do servidor |
| Quais builds se conectam | todas | só a build completa |

**O OWS é o servidor padrão.** Toda build do jogo em qualquer plataforma o conhece, não é preciso configurar nada

**Os NOWS são servidores da comunidade.** O Bullet Hero não os controla nem os modera

**A Oficina Steam é um terceiro canal de níveis no PC.** As builds da Steam listam e iniciam os itens que você assinou e publicam níveis e coleções lá a partir do editor - [[17_publishing]]

## Quais builds se conectam

| Build | De onde | OWS | NOWS |
|---|---|---|---|
| Build de loja | Google Play, App Store | sim | não |
| Build completa | [GitHub](https://github.com/bullet-hero/releases) e o site do projeto | sim | sim |

Uma build de loja não consegue se conectar a um servidor da comunidade de jeito nenhum. O suporte a NOWS é removido dela na compilação, não escondido atrás de uma configuração

O motivo são as regras das lojas. Uma loja julga o que um programa consegue fazer, não quais botões ele mostra. E o conteúdo que outras pessoas veem precisa ser moderado conforme as regras dela

Está planejado que a build completa receba um application id próprio, para que no Android possa ser instalada ao lado da versão da loja. Hoje todas as builds para Android compartilham um id, `com.vertoker.BulletHero`

## O que o OWS terá

- contas e termos de uso
- uma verificação de cada nível antes da publicação: um nível com erro é rejeitado, um nível com aviso vai para um moderador
- denúncias de níveis e usuários, e bloqueio deles

O que uma conta guarda ainda não foi decidido. O servidor terá a própria política de privacidade, que vai aparecer junto com o servidor. Ela vai descrever a conta e explicar como excluí-la. As políticas do jogo e do site não cobrem o servidor - [[game-privacy-policy]], [[privacy-policy]]

## Quando

A publicação na Oficina Steam já funciona nas builds da Steam. Para o resto não há datas. A ordem é: OWS, depois a build do Google Play, depois a build da App Store

Ainda não dá para jogar junto em um servidor, isso não foi projetado

## Riscos dos servidores de outras pessoas

Um servidor da comunidade é rodado por uma pessoa que muito provavelmente você não conhece. O Bullet Hero não controla nem modera esses servidores. O EULA da build completa diz isso diretamente

| Risco | Por quê |
|---|---|
| Níveis com direitos não verificados | o dono decide o que verificar e pode não verificar nada. Um nível pode conter música que o autor não tinha o direito de compartilhar |
| Ninguém modera o conteúdo | não há garantia de que alguém olhe o que é enviado |
| Arquivos de outros sites | a política padrão permite que um nível busque um arquivo por link direto. Quando você abre um nível desses, o jogo baixa o arquivo de um site escolhido pelo autor do nível. Por isso as builds de loja proíbem isso |
| O dono vê o seu tráfego | ainda não há protocolo, então não se sabe o que exatamente o servidor vai receber. Parta do princípio de que o dono vê tudo o que você envia |
| O servidor pode sumir | um nível que existe só naquele servidor some junto com ele |

Por padrão, um nível é distribuído sob *CC BY-NC*, e o autor pode escolher outra licença nos metadados do nível. Um servidor precisa respeitar a licença de cada nível. Sob *CC BY-NC*, ninguém pode hospedar um nível com fins comerciais, um servidor da comunidade inclusive, e um servidor que cobra dinheiro por esses níveis viola a licença de cada um dos autores deles

> [!tip] Recomendação
> Conecte-se só a servidores de donos que você conhece. Guarde a sua própria cópia de cada nível que importa para você: um nível é uma pasta de arquivos, e a cópia no seu disco não depende de nenhum servidor

## EULA

O build completa vem com um EULA. Ele diz: os servidores da comunidade são serviços de terceiros, e o Bullet Hero não os controla nem os modera

As builds de loja vão pedir que você aceite um EULA antes de publicar um nível

Nenhum desses textos foi escrito ainda

## O que ler a seguir

- [[ugc-licensing-policy]] - quais regras um nível precisa cumprir para ser publicado
- [[2_hosting]] - se você quer rodar um servidor por conta própria
