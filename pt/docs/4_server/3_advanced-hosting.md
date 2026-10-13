---
title: Servidor público e como estendê-lo
date: 2026-10-02
tags: [server_advanced]
---

# Servidor público e como estendê-lo

Para um servidor público já existe o SDK aberto: os mesmos modelos e verificações do cliente, sem a Unity. O protocolo, a API do servidor e as ferramentas de moderação ainda não foram decididos

> [!warning] Aviso
> Ainda não há código de servidor nem protocolo. Abaixo está a parte do SDK sobre a qual o servidor vai rodar, e ela já funciona. Endereços, o formato das mensagens e a API do próprio servidor não estão aqui, eles não existem

## O SDK roda em um servidor

O SDK é o modelo de dados aberto do jogo: modelos, serialização para JSON e para um formato binário, regras de validação, geradores. As mesmas fontes que a Unity compila viram uma biblioteca `netstandard2.1` comum, sem o motor. Um servidor ou um utilitário pode referenciá-la:

```bash
dotnet build -c Release BH.SDK.csproj
dotnet pack  -c Release BH.SDK.csproj
```

O pacote se chama `BulletHero.SDK`. O código está em [github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk), sob MIT

A versão do SDK normalmente coincide com a versão do jogo e ainda não promete estabilidade de API. Mais - [[5_versioning]]

**O cliente e o servidor executam as mesmas verificações sobre os mesmos modelos.** Um nível que o editor considera pronto também está pronto para o servidor. Não há um segundo conjunto de regras para manter em acordo

## ValidateForPublish

Uma chamada responde à pergunta "este nível pode ser publicado aqui":

```csharp
new ValidationFacade().ValidateForPublish(meta, profile, level, now, payload)
```

Ela executa três passagens de uma vez:

1. regras declarativas sobre o nível e os metadados dele
2. verificações do grafo do nível
3. as condições do próprio serviço, vindas do `PublishProfile` dele

**Passar o próprio nível é opcional.** `metadata.json` é um arquivo separado para que um catálogo possa avaliar milhares de níveis sem abrir nenhum. Essa passagem barata cobre a maior parte da política

Mas duas verificações precisam de `level.json`: um recurso sem nenhum registro e a forma como os recursos são buscados. Um relatório limpo só com os metadados significa "nenhum erro no que foi lido". `IsReady` continua `false` até o arquivo do nível ser verificado

`payload` carrega os tamanhos medidos: de cada recurso, de `level.json`, de `metadata.json`, do nível inteiro. Sem ele, os limites de tamanho do perfil não podem ser verificados

Nada é corrigido durante a verificação, e isso é de propósito. Editar o conteúdo em silêncio na saída é a última coisa de que um serviço precisa. Mais - [[6_validation]]

## Três veredictos

| Grupo | Significado | O que o servidor faz |
|---|---|---|
| `Error` | o serviço recusa | rejeita o envio (`HasErrors`) |
| `Warning` | pode ser publicado, mas uma pessoa precisa olhar | coloca o nível na fila de moderação (`NeedsManualReview`) |
| `Advice` | anotado | nada |

O cliente bloqueia um envio pelos mesmos erros antes mesmo de ele começar. Um nível que o seu servidor rejeitaria raramente chega até ele

## O seu próprio PublishProfile

A política de um serviço é um arquivo, um modelo serializado do SDK. Um servidor mais rígido ou mais flexível é outro arquivo, não um fork do código

**Um nível que fica no dispositivo do jogador não é verificado de forma alguma.** O perfil só importa no momento em que o nível é oferecido a um serviço. Como um autor prepara um nível para esse momento - [[5_publish-readiness]]

Predefinições:

| Predefinição | Chave | Para quê |
|---|---|---|
| `CreateOpen()` | `local` | níveis no dispositivo, nada é obrigatório |
| `CreateStandard()` | `standard` | um servidor público, a política de [[ugc-licensing-policy]] |
| `CreateStrict()` | `strict` | builds de loja, sem links diretos, um hash em cada recurso |

Os campos principais:

| Campo | O que decide |
|---|---|
| `AllowedLicenses` | quais licenças típicas são aceitas, uma lista vazia aceita todas |
| `AllowedUriTypes` | como os recursos podem ser buscados, uma lista vazia permite todas as formas |
| `AllowUnknownLicense` | se um recurso pode não dizer nada sobre os seus termos |
| `AllowPermissionInstead` | se a permissão do titular dos direitos pode substituir uma licença rejeitada (sempre enviada para revisão) |
| `RequireResourceMeta`, `RequireResourceUrl`, `RequireAttribution` | o que o registro de cada recurso precisa conter |
| `RequireAgeRating`, `RequireLevelAuthors`, `RequireHashes` | o que o nível precisa declarar |
| `MaxResourceBytes`, `MaxDataFileBytes`, `MaxTotalBytes` | limites de tamanho, zero significa sem limite |
| `Sources`, `UnknownSourceTrust` | a lista de sites confiáveis e como é classificado um site fora dela |

As duas predefinições públicas:

| | `standard` | `strict` |
|---|---|---|
| Links diretos para recursos | permitidos | proibidos |
| Crédito do autor em cada recurso | não obrigatório | obrigatório |
| Hash do conteúdo em cada registro | não obrigatório | obrigatório |
| Maior recurso | {{v:publish.standard.max-resource-mb}} MB | {{v:publish.strict.max-resource-mb}} MB |
| Maior `level.json` ou `metadata.json` | {{v:publish.standard.max-data-file-mb}} MB | {{v:publish.strict.max-data-file-mb}} MB |
| Maior nível | {{v:publish.standard.max-level-mb}} MB | {{v:publish.strict.max-level-mb}} MB |
| Um site fora da lista | `RequiresLicenseCheck` | `RequiresResourceCheck` |

Todas as predefinições e campos - [[7_publish-profiles]]

### Por que standard não tem GPL

As licenças da família GPL ficam fora de `standard` de propósito. Uma obra GPL distribuída pela App Store entra em conflito com os termos da Apple. Um catálogo que as permitisse não poderia ser lançado no iOS depois

> [!info] Vale saber
> A lista de sites confiáveis que vem com o SDK é só um ponto de partida. Os sites mudam os seus termos, por isso cada dono de servidor deve substituí-la no próprio perfil. Nada pode contar com a presença de um site específico na lista

## Moderação

O que o servidor oficial planeja acrescentar por cima da verificação. Um servidor público muito provavelmente também vai precisar disso:

- **Uma fila de moderação.** Ela é preenchida pelas ocorrências `Warning`
- **Denúncias e bloqueio** de níveis e usuários. As regras do Google Play e da App Store exigem os dois para qualquer conteúdo que outras pessoas veem
- **Remoção por hash.** Um registro de recurso pode armazenar os hashes de conteúdo dos arquivos dele como `sha256:<hex>`. Uma denúncia nomeia uma obra, e com os hashes cada nível que a contém é encontrado por busca, não por palpite a partir de títulos. O editor registra o hash quando um recurso é importado
- **Termos de uso.** Eles cobrem o que a licença não cobre: a declaração do autor de que detém os direitos, o direito do dono do servidor de remover um nível, o direito de mostrar o título e a capa dele nas listas

**A Oficina Steam funciona de outro jeito.** A Valve guarda os arquivos, e não há fila de moderação do lado do Bullet Hero. O jogo verifica um nível ou uma coleção antes do envio, e um erro bloqueia o envio - [[17_publishing]]. Depois da publicação, o jogo só decide o que baixar dali

## Formatos de arquivo compactado

Um nível é uma pasta de arquivos, e um arquivo compactado o torna portátil. O que o SDK lê e grava:

| Formato | Leitura | Gravação | Observação |
|---|---|---|---|
| `.tar.gz` | sim | sim | o padrão |
| `.zip` | sim | sim | pode ser criptografado por entrada com AES-256 |
| `.tar.gz.gpg`, `.zip.gpg` | sim | sim | uma mensagem OpenPGP protegida por senha, a única proteção disponível para `.tar.gz` |
| `level.json.gpg` | sim | sim | um único arquivo de nível protegido |
| `.7z` | não | não | detectado para poder ser recusado com um nome claro |

O formato é detectado pelos primeiros bytes do arquivo, não pela extensão. O nome é a única parte de um arquivo que qualquer um pode mudar

`tar -xzf`, `gpg -d` e qualquer compactador zip abrem todo formato que é gravado. O jogo não é necessário para descompactar um nível. Mais - [[4_archives]]

## O que não foi decidido

- o protocolo entre o jogo e um servidor, e se ele será o mesmo para OWS e NOWS
- a API do servidor: envio, catálogo, pesquisa, contas
- como apontar o jogo para um servidor da comunidade
- como o próprio servidor é estendido e em que linguagem
- jogar junto em um servidor: transporte, autoridade, sincronização de níveis e lobbies

Para o jogo em conjunto, só uma coisa foi resolvida: como o avatar de um jogador aparece e desaparece com uma mensagem de rede

A publicação de níveis em qualquer serviço vai aparecer não antes da atualização posterior ao `gv 1.0.0`. Os dados em que a verificação se apoia precisam entrar nos níveis antes de eles serem publicados

## Licença do nível e qualquer servidor

Por padrão, um nível é distribuído sob *CC BY-NC*, e o autor pode escolher outra licença nos metadados do nível. A permissão para compartilhar um nível vai do autor diretamente para cada destinatário. Por isso nenhum servidor, oficial ou da comunidade, pode hospedar um nível sob *CC BY-NC* com fins comerciais

Um servidor com outro código sob outra licença não muda nada nos direitos sobre o conteúdo. As regras completas para autores - [[ugc-licensing-policy]]
