---
title: Formato de nível
date: 2026-10-02
tags: [developer, level_author]
---

# Formato de nível

Um nível é uma pasta: o conteúdo em level.json ou level.blob, os metadados em metadata.json ou metadata.blob, uma capa e mídia. Backups, recordes e configurações do jogador ficam no dispositivo

## A pasta do nível

Cada nome de arquivo em uma pasta de nível é fixado em `FileNames`:

| Arquivo | Modelo | O que há dentro |
|---|---|---|
| `level.json` ou `level.blob` | `Level` | o conteúdo: configurações, objetos e eventos, áudio, recursos, ajudas |
| `metadata.json` ou `metadata.blob` | `LevelMeta` | título, descrição, autores, licença, um registro para cada recurso, uma referência à capa |
| `logo.png` ou `logo.jpg` | - | a capa |
| música, imagens, fontes | - | arquivos de mídia que o nível referencia |

**A extensão é o formato.** Ela não está escrita em lugar nenhum dentro dos arquivos. O leitor olha qual arquivo existe: `level.json` ou `level.blob`

O nível e os metadados escolhem o formato de forma independente. Por exemplo, o nível integrado `new-zero-demo` guarda `level.blob` ao lado de `metadata.json`

**`metadata.json` é um arquivo separado de propósito.** Um catálogo mostra mil níveis a partir de mil arquivos pequenos de metadados. Nenhum nível é aberto para isso

## Recursos

Um recurso é endereçado por um par de `uri` e `uri_type` (`ResourceUriType`):

| Valor | Tipo | Onde está o arquivo |
|---|---|---|
| 1 | `LevelPath` | dentro da pasta do nível. Só este tipo torna um nível portátil |
| 2 | `AbsolutePath` | em outro lugar deste dispositivo |
| 3 | `DirectUrl` | baixado pela rede |
| 4 | `StreamingAssets` | vem com o jogo, não com o nível |

`AbsolutePath` aparece quando um nível é criado em torno de uma música. Exportar um arquivo compactado copia esse arquivo para dentro. Mais - [[4_archives]]

A capa está disponível por `LevelMeta.LevelLogo`, como qualquer outro recurso. Se ela é `logo.png` ou `logo.jpg` é decidido pelos bytes do próprio arquivo, não pelo nome da imagem de origem

O registro de autoria da capa é um `ResourceMeta` com `resource_type` 9 (`LevelLogo`). Nem `resource_id` nem `resource_guid` são preenchidos nele: um nível tem uma só capa, então o tipo é o endereço inteiro

## Declarações de IA

`LevelMeta` e cada `ResourceMeta` carregam `ai_generated` do tipo `AiGeneration`:

| Valor | Nome | O que significa |
|---|---|---|
| 0 | `NotSpecified` | nada declarado, desconhecido. É o valor padrão, e uma chave ausente é lida assim |
| 1 | `No` | declarado como feito sem geração por IA |
| 2 | `Yes` | declarado como gerado por IA |

Em `LevelMeta` ele cobre só o conteúdo próprio do nível. Cada recurso e a capa se declaram nos próprios registros. Se um nível contém conteúdo de IA não é armazenado: quem responde isso é `LevelMeta.ContainsAiContent()`, e só `Yes` conta

## O que não viaja com um nível

Estes arquivos ficam ao lado da pasta `levels`, nunca dentro de uma pasta de nível. Compactar, enviar ou excluir um nível não mexe neles:

| Pasta ou arquivo | O que é | Por que fica |
|---|---|---|
| `backups/` | salvamentos automáticos do editor, uma pasta por id de nível, `backup_level_<time>.<extension>` | uma cópia dentro da pasta que ela protege seria excluída junto com essa pasta |
| `stats/` | recordes e progresso por `LevelId` e `statistics.json` | um nível que alguém enviou chegaria já concluído |
| `settings.json` | `UserSettings`, as configurações do jogador para o dispositivo inteiro | elas pertencem ao jogador, não ao nível |
| `resources/themes`, `effects`, `shapes`, `prefabs` | as bibliotecas compartilhadas do dispositivo | são compartilhadas por todos os níveis do dispositivo |
| `reports/` | relatórios de diagnóstico | - |

## Chaves JSON

O JSON é sempre gravado compacto, sem indentação. Para lê-lo a olho, formate-o em um editor de texto

**O comprimento de uma chave depende de quantas vezes ela aparece em um nível:**
- uma chave que aparece uma vez por arquivo é escrita com palavras inteiras em `snake_case`: `level_id`, `min_generation`
- uma chave que se repete milhares de vezes é encurtada para poucas letras: `objs`, `f`, `e`, `v`

As chaves ocupam 52% dos bytes de um arquivo de nível, por isso isto é uma regra, não questão de gosto. Todas as chaves são declaradas em `Names.cs`

**Um valor polimórfico é gravado como `[tag, data]`.** Uma string simples é `[0,{"v":"Author"}]`, uma localizada é `[1,{"strs":[...]}]`

Wrappers de identificadores como `ObjectId` são gravados como um número ou uma string sem nada em volta

## Identificadores

**O sinal de um identificador inteiro tem significado.** `0` sempre significa "não definido":

| Identificador | Chave JSON | Positivo | Negativo |
|---|---|---|---|
| `ObjectId` | `id`, e `pid` para o pai | um objeto do nível | um objeto do jogo: `-1` a câmera, `-2` o jogador local, `-3` a raiz de um modelo de prefab |
| identificadores de recursos | `txid`, `fnid`, `auid`, `byid`, `ttid` | um recurso que vem com o jogo | um recurso próprio do nível |
| `AudioId` de uma faixa de áudio | `aid` | uma faixa deste nível | não é usado |

Um `pid` igual a `0` significa que o objeto não tem pai. Números abaixo de `-3` só existem enquanto o jogo está rodando e nunca chegam a um arquivo

**`Marker`, `Checkpoint` e `BeatSegment` não têm identificador.** O endereço deles é um ponto no tempo: para um marcador e um checkpoint é o quadro `f`, para um segmento de batida é o primeiro quadro do intervalo `sp` dele (os segmentos não se sobrepõem). Se um objeto desses é movido, o endereço dele muda

**Uma substituição de prefab nomeia um campo por número, não por chave JSON.** Um posicionamento guarda as substituições dele na lista `mod`. A `key` de cada substituição contém três números:
- `id` - o objeto dentro do modelo, não a cópia dele no nível
- `f` - o número permanente do campo
- `i` - o elemento de um campo de lista, ou `-1` para o campo inteiro

O número fica ligado ao campo para sempre. Renomear a chave JSON desse campo não quebra as substituições já salvas nos níveis

## O "g" externo

Cada raiz de serialização é embrulhada em um envelope com duas chaves:

```json
{"g":2,"v":{"level_id":"18df5f61-3aa4-4812-bf69-d357f2201bc3","vrs":"1.0", ... }}
```

`g` é a geração do modelo (`Names.Generation`), `v` são os dados

Os envelopes se aninham. Dentro de `Level`, cada um de `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources` e `LevelHints` tem o próprio envelope. Como as gerações funcionam - [[5_versioning]]

> [!caution] Cuidado
> `g` e `vrs` são números diferentes. `vrs` é a versão do nível dada pelo autor (`LevelMeta.LevelVersion`), não tem nada a ver com o formato. Não mude `g` à mão: um arquivo com um `g` maior do que a build conhece não é lido de forma alguma
