---
title: Perfis de publicação
date: 2026-10-01
tags: [developer, level_author]
---

# Perfis de publicação

Um serviço diz quais níveis aceita em um arquivo PublishProfile: licenças, origens de recursos, campos obrigatórios, limites de tamanho. Um serviço novo pede um arquivo, não uma edição do analisador

## Um perfil é dado

Um perfil de publicação (`PublishProfile`) é um modelo serializado como qualquer outra raiz, com a própria geração

Um nível pode ir para a Oficina Steam, para o servidor oficial, para um servidor da comunidade, para o catálogo de uma build de loja. Cada lugar responde às mesmas perguntas do seu jeito. As respostas mudam com os anos, e o código não

O que um perfil decide:

| Campo | Significado |
|---|---|
| `ProfileKey` | que serviço é este, repetido em cada relatório |
| `AllowedLicenses` | os valores de `TypicalLicenseType` que o serviço aceita |
| `AllowedUriTypes` | como os recursos podem ser buscados. Uma lista vazia significa qualquer forma |
| `AllowUnknownLicense`, `AllowPermissionInstead` | se uma licença desconhecida ou uma permissão por escrito basta |
| `RequireResourceMeta`, `RequireResourceUrl`, `RequireAttribution`, `RequireAgeRating`, `RequireLevelAuthors`, `RequireHashes` | o que precisa ser preenchido |
| `MaxResourceBytes`, `MaxDataFileBytes`, `MaxTotalBytes` | limites de tamanho, 0 significa sem limite |
| `Sources`, `UnknownSourceTrust` | uma lista de sites e a classificação para um site que não está nela |

Só o perfil decide quais licenças são aceitáveis. Parece uma propriedade da licença, mas na verdade é uma propriedade do serviço que recebe o nível

## Quatro perfis integrados

| Fábrica | `ProfileKey` | Para quê |
|---|---|---|
| `CreateOpen()` | `local` | um nível no seu dispositivo. Nada é obrigatório |
| `CreateStandard()` | `standard` | um servidor público |
| `CreateWorkshop()` | `workshop` | a Oficina Steam. Qualquer variante CC BY passa, documentos ausentes só geram aviso |
| `CreateStrict()` | `strict` | uma build de loja, com regras mais rígidas do que `standard` |

| O quê | `standard` | `strict` |
|---|---|---|
| licenças | CC0 1.0, CC BY 4.0 e 3.0, CC BY-NC 4.0 e 3.0, SIL OFL 1.1, MIT, Apache 2.0, the Unlicense | como em `standard` |
| de onde vêm os recursos | da pasta do nível, do jogo ou por link direto | sem links |
| atribuição e hashes | - | obrigatórios |
| limite por recurso | 64 MiB | 32 MiB |
| limite por arquivo de dados | 32 MiB | 16 MiB |
| limite por nível | 256 MiB | 128 MiB |

> [!tip] Recomendação
> Não adicione uma fábrica para o seu serviço. Pegue um dos quatro perfis, mude os campos de que precisa e distribua-o como um arquivo JSON

### Por que estas licenças e tamanhos

- licenças da família GPL ficam fora de `standard`. Uma obra GPL distribuída pela App Store entra em conflito com os termos da Apple
- CC BY-SA fica de fora: o ShareAlike obrigaria a mudar a licença do próprio nível
- CC BY-ND fica de fora: o NoDerivatives proíbe a edição sobre a qual o jogo é construído
- os tamanhos rígidos são o que um celular consegue baixar pela rede móvel

## De onde veio um recurso

O campo de licença diz o que o autor afirma. `SourceTrust` diz quanto vale essa afirmação, considerando o site de onde o recurso veio:

| Classificação | Resultado | Exemplos |
|---|---|---|
| `Approved` | publicar | Kenney, ccMixter, Incompetech |
| `PartiallyApproved` | publicar, vale a pena olhar o registro | Pixabay, SoundImage |
| `RequiresLicenseCheck` | conferir a licença na página real | OpenGameArt, Free Music Archive, Wikimedia Commons |
| `RequiresResourceCheck` | primeiro identificar a própria obra | Rawpixel, itch.io |
| `NotAllowed` | recusar | YouTube, SoundCloud, Spotify |
| `Unknown` | sem registro, quem decide é `UnknownSourceTrust` | - |

`TrustedSourceCatalog.CreateDefault()` devolve 25 sites. É uma lista inicial. Espera-se que cada operador a altere. Por isso nada tem o direito de contar com a presença de um registro

Uma lista `Sources` vazia desliga a classificação de origens

As plataformas de streaming estão listadas como `NotAllowed` em vez de ficarem de fora. Um site ausente é classificado por `UnknownSourceTrust`, e em `standard` e `strict` essa classificação pede uma verificação em vez de recusar

O catálogo e [[ugc-licensing-policy]] descrevem a mesma coisa e são editados juntos

## O que fazer com a resposta

A chamada é `ValidationFacade.ValidateForPublish`. Mais - [[6_validation]]

`PublishReadinessReport` tem:
- `HasErrors` - ocorrências no grupo `Error`
- `NeedsManualReview` - ocorrências no grupo `Warning`
- `IsReady`

O perfil não decide o que acontece depois. O cliente bloqueia o envio quando há erros. O servidor coloca o nível em uma fila de revisão em vez de publicá-lo

A mesma verificação pelo lado do autor - [[5_publish-readiness]]
