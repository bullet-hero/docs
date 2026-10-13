---
title: Por que Bullet Hero
date: 2026-10-03
tags: [player, level_author]
---

# Por que Bullet Hero

Bullet Hero é gratuito, roda no Windows e no Android, e o SDK, a documentação e as builds são abertos. O núcleo aguenta milhares de objetos na tela em celulares e é coberto por mais de 8000 testes

## Gratuito

O jogo é gratuito e vai continuar gratuito. Ele não terá compras, anúncios nem conteúdo pago

Não descarto a monetização por meio de doações voluntárias, mas nada além disso

## Disponível em todo lugar, tudo é universal

O jogo está em todos os lugares para onde consegui portá-lo
- Plataformas: Windows, Android (depois iOS, Linux, Mac)
- Lojas: Steam, Google Play (depois App Store)

Tudo no jogo funciona com qualquer controle, os níveis são os mesmos em todo lugar, e cada parte do jogo (o editor, o multiplayer, os servidores) funciona igual em todo lugar

## Um alto grau de código aberto

O SDK, a documentação, as builds e o servidor estão em repositórios abertos. Só o jogo em si e o site são fechados. Todos os repositórios - [[links]]

## O núcleo técnico mais rápido

Milhares de objetos na tela, centenas de efeitos e textos ao mesmo tempo. E tudo isso roda em celulares com a meta de 60 FPS (muitas vezes mais)

## Um núcleo técnico muito estável

O jogo tem muitos mecanismos que mantêm estáveis o jogo e os seus modelos de dados
- Versionamento de tudo (mais aqui - [[5_versioning]])
- Versionamento multimodal e migração de dados, os dados dos níveis não vão quebrar
- Mais de 8k testes no jogo inteiro, literalmente cada aspecto do jogo é coberto por testes

E muitas outras verificações. Junto com o núcleo rápido, isso dá uma relação muito alta entre estabilidade e desempenho

## Multiplayer (em desenvolvimento)

Multiplayer em qualquer forma: no mesmo dispositivo, multiplayer local, por meio de um servidor, e muitas interações interessantes

## Servidores abertos (em desenvolvimento)

Um servidor oficial e servidores da comunidade que qualquer pessoa pode rodar. O código do servidor será aberto. Os catálogos de níveis e a comunicação básica vão chegar junto com o servidor. Mais - [[4_server/index]]

## Muitos idiomas

O jogo pretende suportar de fábrica a maioria dos idiomas do mundo. Acredito que um jogo não deve ter nenhuma barreira de idioma

É claro que ninguém pode saber todos os idiomas do mundo, mas graças aos avanços da IA e à comunidade essa meta é bem alcançável

## Política de licenciamento aberta

Todos os dados do jogo vêm com uma escolha flexível de licenças (principalmente [Creative Commons](https://creativecommons.org/)) para os seus níveis e para os recursos que você usa. Isso torna mais aberta a reutilização de recursos de outras pessoas

Mais - [[ugc-licensing-policy]]

## Integração com todos os serviços possíveis

O jogo tem mais de 10 variantes de build, e cada uma tem as próprias integrações conforme a loja pela qual é distribuída

Mais - [[download]]

## Determinismo e estabilidade

O jogo tem aleatoriedade determinística, e cada fator dela está ligado à semente e aos parâmetros do nível. Isso significa que a aleatoriedade sempre pode ser repetida se você conhece o nível e tem a semente

Mais - [[8_determinism]]

## Editor

O jogo tem um editor de níveis grande e flexível, no qual você pode criar quase qualquer coisa

O editor tem muitas funções únicas: [[8_generators]], depuração e mais

## Formato de nível aberto

O SDK em C# lê e grava níveis do mesmo jeito que o jogo. O jogo e o servidor trabalham por meio dele, e você também pode. Com ele você pode criar os seus próprios níveis ou recursos únicos, ou os seus próprios serviços construídos sobre ele

Mais - [[3_sdk/index]]
