---
title: Guia de estilo
date: 2026-10-13
tags: [contributor]
---

# Guia de estilo

Escreva de forma simples: uma frase, uma ideia, números em vez de adjetivos. Um hífen com espaços em vez de um travessão, sem ponto e vírgula, sem ponto no fim de um parágrafo

O texto informa, não vende. Toda emoção vira antes uma lista, uma tabela ou um número. Uma página que soa como marketing, pose de especialista ou um assistente simpático fracassou, mesmo quando todos os fatos nela estão certos

## Primeiro, a simplicidade

Esta regra está acima de todas as outras

Um texto pode não ter nenhuma enrolação e ainda assim ser difícil de ler. Cada frase é verdadeira, mas elas estão encadeadas em um único argumento denso, e o leitor precisa segurar tudo isso de uma vez

As páginas para iniciantes são escritas para que possam ser lidas por cima. São as páginas para jogadores, as primeiras páginas para autores de níveis, o início rápido, o FAQ, a ajuda e a página de entrada de cada seção. As páginas de referência e do SDK podem ser mais densas, mas as frases delas seguem as mesmas regras

1. **Só o que o leitor precisa agora.** Antes de cada frase, pergunte: o leitor vai agir de outro jeito depois de lê-la? Se não, corte-a ou leve-a para a página detalhada. Casos-limite, ressalvas de plataforma, motivos internos, como o próprio site funciona - nada disso vai em uma página para iniciantes
2. **Uma frase, uma ideia.** Nada de cadeias de orações ligadas por dois-pontos, "porque", "então", "enquanto", nada de parênteses dentro de parênteses. Duas frases curtas valem mais que uma longa. Uma frase pode ficar na própria linha dentro de um parágrafo: com ponto no fim, exceto a última. Em chinês e japonês, uma frase na própria linha é um parágrafo separado, com uma linha em branco antes
3. **A regra geral, não as exceções.** "Os números costumam coincidir" em vez de três frases sobre quando eles divergem. A exceção mora na página detalhada, atrás de `Mais - [[page]]` (em inglês `More - [[page]]`, em chinês `更多：[[page]]`, em japonês `詳細：[[page]]`, em espanhol `Más - [[page]]`)
4. **Navegação antes de explicação.** Uma página de entrada é uma introdução curta e uma tabela de nome -> link, ou linhas como `Tudo o que você pode baixar - [[download]]`. Colunas descritivas como "o que é" e "status" não são necessárias quando o link já diz isso
5. **Diga o que importa, não como funciona.** "Este número importa mais que todos os outros" mais um link, em vez de descrever o mecanismo
6. **O status em uma palavra.** `Em desenvolvimento`, `Indisponível`, `Versão atual - gv 1.0.0`. Nada de "no momento em que escrevo", nada de "não antes de"
7. **Explique uma abreviação onde ela aparece pela primeira vez.** Por exemplo, uma coluna `gv` -> `versão do jogo`
8. **Fale com o leitor.** Uma pergunta e uma resposta estão ótimas: `Não gosta da documentação? Então você pode ajudar a escrevê-la`. `Talvez você queira...` também está ótimo
9. **Palavras simples.** Um termo aparece só quando o leitor vai encontrá-lo na interface do jogo. Aí ele vai entre crases, exatamente como o jogo o mostra

```
Antes (correto, mas pesado):
Os números não seguem uns aos outros. `gv` e `sv` começaram iguais e agora podem divergir livremente: uma mudança no SDK não precisa mover a versão do jogo, e uma atualização do jogo não precisa mover a versão do SDK

Depois:
Os números de versão não precisam seguir uns aos outros, mas na maioria dos casos coincidem.
As versões também sobem juntas, e uma atualização conjunta leva a mesma versão
```

## Pontuação

A pontuação segue as normas do idioma, com dois desvios deliberados. Os dois são obrigatórios

**Sem travessões.** O travessão e o meia-risca não são usados em lugar nenhum. Onde for preciso um traço, escreva um hífen com espaços ao redor

```
Antes:   Bullet Hero — menos um jogo do que um player de animações
Depois:  Bullet Hero - menos um jogo do que um player de animações
```

O chinês e o japonês não usam nenhum tipo de traço: nem `——`, nem `—`, nem mesmo um hífen com espaços. Escreva uma vírgula, dois-pontos ou uma frase nova em vez disso (`，` e `：` em chinês, `、` e `：` em japonês)

```
Antes:   Bullet Hero——与其说是游戏，不如说是动画播放器
Depois:  Bullet Hero与其说是游戏，不如说是动画播放器

Antes:   Bullet Hero——ゲームというより、アニメーションのプレイヤー
Depois:  Bullet Heroはゲームというより、アニメーションのプレイヤー
```

**Sem ponto no fim de um parágrafo.** Os pontos entre frases dentro de um parágrafo ficam. A última frase de um parágrafo, um item de lista, uma célula de tabela e um título não levam ponto. Os pontos de interrogação e de exclamação ficam

**Cuidado com as quebras de linha.** O markdown junta em um só parágrafo as linhas que não têm uma linha em branco entre elas. Uma linha sem ponto seguida de outra linha vira duas frases grudadas

Por isso, em inglês, russo, espanhol e português, dentro de um parágrafo, toda linha seguida de outra linha termina com ponto. Coloque uma linha em branco antes de cada ideia separada

**Em chinês e japonês, um parágrafo é uma linha no código-fonte.** O markdown transforma uma quebra de linha dentro de um parágrafo em um espaço, e esse espaço aparece entre frases em chinês ou japonês e atrapalha a pesquisa. Por isso o texto em chinês e japonês nunca é quebrado à mão, e uma frase que precisa ficar na própria linha é um parágrafo separado. Cada ideia separada ganha uma linha em branco antes

Outros sinais:

- **Os dois-pontos** são o sinal de trabalho para explicar e enumerar, use à vontade
- **O ponto e vírgula** nunca é usado. Escreva um ponto ou um item de lista separado em vez dele. O chinês também não usa `；`: escreva duas frases ou uma `，`. O japonês também não: duas frases ou um `、`
- **Os pontos de exclamação** são raros, no máximo um por texto longo
- **As aspas** em inglês, russo, espanhol e português são só retas `"aspas"`, nunca `«»`. O chinês usa as de largura total `“”`, o japonês `「」`, o coreano aspas retas como o inglês
- **Os parênteses** servem para um comentário curto, uma ressalva ou uma piada seca

## Chinês e japonês

As regras acima valem para todos os idiomas, sem exceções. O chinês acrescenta alguns pontos:

- **Trate o leitor por `你`,** nunca `您`. O conselho é `建议`, a opinião do autor é `我`, nunca `开发者` nem `我们`
- **Pontuação de largura total** `，。：？！（）` e aspas `“”`. O código, os nomes de arquivos e tudo o que vai entre crases mantêm a pontuação ASCII
- **Sem espaço entre hanzi e letras latinas ou dígitos,** do jeito que o próprio jogo escreve: `在Bullet Hero中`, `60帧`
- **Ficam em letras latinas:** nomes de produtos e formatos (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), extensões de arquivo, teclas, nomes de campos
- **Os termos vêm de `game/zh-glossary.md`.** Cada termo tem uma só grafia, e as linhas marcadas como `strict` são sempre seguidas. Um rótulo da interface é citado a partir do valor da chave dele em `game/zh.yaml`
- **Os títulos dos destaques** são 建议, 提示, 须知, 警告, 注意 (`> [!tip] 建议`)

O japonês acrescenta estes pontos:

- **Escreva no registro です/ます.** O leitor não é nomeado por um pronome, nunca `あなた`: construa a frase de modo que o sujeito fique claro sem ele. O conselho é `〜することをおすすめします` ou `推奨`, a opinião do autor é `私`, nunca `開発者` nem `私たち`
- **Pontuação de largura total** `、。：？！（）` e aspas angulares `「」`. Uma citação dentro de uma citação é `『』`. O código, os nomes de arquivos e tudo o que vai entre crases mantêm a pontuação ASCII
- **Os empréstimos são escritos em katakana,** com o `ー` final mantido: `インスペクター`, `レイヤー`. É assim que o editor da Unity em japonês os escreve
- **Sem espaço entre kana ou kanji e letras latinas ou dígitos,** do jeito que o próprio jogo escreve: `Bullet Heroでは`, `60フレーム`
- **Ficam em letras latinas:** nomes de produtos e formatos (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), extensões de arquivo, teclas, nomes de campos
- **Os termos vêm de `game/ja-glossary.md`.** Cada termo tem uma só grafia, e as linhas marcadas como `strict` são sempre seguidas. Um rótulo da interface é citado a partir do valor da chave dele em `game/ja.yaml`
- **A pontuação fica fora dos marcadores de negrito:** escreva `**太字**。本文`, nunca `**太字。**本文`. Na segunda forma o markdown não consegue fechar o `**`, e os asteriscos aparecem como estão
- **Os títulos dos destaques** são 推奨, ヒント, 補足, 警告, 注意 (`> [!tip] 推奨`)

O coreano acrescenta estes pontos:

- **Escreva no registro 합니다체** (`-ㅂ니다`/`-습니다`). O leitor não é nomeado por um pronome, nunca `당신`. O conselho é `권장합니다`, a opinião do autor é `저`, nunca `개발자` nem `저희`
- **A pontuação é ASCII e as palavras são separadas por espaços,** como em inglês, então as regras acima sobre o traço, o ponto e as aspas valem como estão escritas
- **Os empréstimos são escritos em Hangul** do jeito que o editor da Unity em coreano os escreve: `레이어`, `인스펙터`
- **Nenhuma partícula solta depois de uma palavra latina, de código ou de um marcador** cujo som final a frase não tem como saber: escreva a forma dupla `을(를)`, `이(가)` ou reformule
- **Ficam em letras latinas:** nomes de produtos e formatos (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), extensões de arquivo, teclas, nomes de campos
- **Os termos vêm de `game/ko-glossary.md`.** Cada termo tem uma só grafia, e as linhas marcadas como `strict` são sempre seguidas. Um rótulo da interface é citado a partir do valor da chave dele em `game/ko.yaml`
- **Pontuação ou código no fim do negrito quebra o negrito quando vem uma partícula depois:** escreva `**이름**을`, nunca `**"이름"**을`
- **Os títulos dos destaques** são 권장, 팁, 참고, 경고, 주의 (`> [!tip] 권장`)

O espanhol acrescenta estes pontos:

- **Espanhol neutro, um só texto para a Espanha e a América Latina.** O leitor é `tú`, no singular, nunca `usted`, `vosotros` ou `ustedes`. O conselho é `se recomienda` ou `conviene`, nunca `te recomendamos`, a opinião do autor é `yo`, nunca `los desarrolladores` nem `nosotros`
- **Um vocabulário que se lê do mesmo jeito dos dois lados do Atlântico:** `archivo`, não `fichero`, `equipo` ou `PC`, não `ordenador` nem `computadora`, `teléfono` ou `móvil`, não `celular`, `hacer clic` na tela e `pulsar` uma tecla
- **Nenhum adjetivo que concorde com o gênero do leitor** (`listo`/`lista`): reformule para evitá-lo
- **Os dois desvios valem sobre a tipografia espanhola:** um hífen com espaços ` - ` em vez da raya (também em incisos e diálogos), aspas retas em vez de `«»`, sem ponto fechando um parágrafo, um item de lista, uma célula de tabela ou um título. Sem `;`
- **`¿…?` e `¡…!` sempre levam os dois sinais**
- **Títulos em sentence case** (`## Cómo funciona el ajuste`), nunca em Title Case. Uma maiúscula mantém o acento (`Á`, `É`)
- **Ficam sem tradução:** nomes de produtos e formatos (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), extensões de arquivo, teclas, nomes de campos
- **Os termos vêm de `game/es-glossary.md`.** Cada termo tem uma só grafia, e as linhas marcadas como `strict` são sempre seguidas. Um rótulo da interface é citado a partir do valor da chave dele em `game/es.yaml`
- **Os títulos dos destaques** são Recomendación, Consejo, Conviene saber, Advertencia, Precaución (`> [!tip] Recomendación`). `More - [[page]]` é escrito `Más - [[page]]`

O português acrescenta estes pontos:

- **Português do Brasil, o código `pt` não carrega região.** O leitor é `você`, com o verbo na terceira pessoa, nunca `tu`, `o senhor` ou `vocês`. O conselho é `recomenda-se` ou `vale a pena`, nunca `recomendamos`, a opinião do autor é `eu`, nunca `os desenvolvedores` nem `nós`
- **Vocabulário brasileiro, nunca europeu:** `arquivo`, não `ficheiro`, `tela`, não `ecrã`, `salvar`, não `guardar`, `mouse`, não `rato`, `celular`, não `telemóvel`, `baixar`, não `transferir`. `estar` + gerúndio (`está carregando`), nunca `estar a` + infinitivo
- **Nenhum adjetivo que concorde com o gênero do leitor** (`pronto`/`pronta`): reformule para evitá-lo
- **Os dois desvios valem sobre a tipografia portuguesa:** um hífen com espaços ` - ` em vez do travessão, aspas retas em vez de `«»` ou `“”`, sem ponto fechando um parágrafo, um item de lista, uma célula de tabela ou um título. Sem `;`
- **Títulos em sentence case** (`## Como funciona o encaixe`), nunca em Title Case. Uma maiúscula mantém o acento (`É`, `Ã`)
- **Ficam sem tradução:** nomes de produtos e formatos (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), extensões de arquivo, teclas, nomes de campos
- **Os termos vêm de `game/pt-glossary.md`.** Cada termo tem uma só grafia, e as linhas marcadas como `strict` são sempre seguidas. Um rótulo da interface é citado a partir do valor da chave dele em `game/pt.yaml`
- **Os títulos dos destaques** são Recomendação, Dica, Vale saber, Aviso, Cuidado (`> [!tip] Recomendação`). `More - [[page]]` é escrito `Mais - [[page]]`

## Layout

- **Parágrafos curtos,** de uma a três linhas
- **Uma lista com marcadores** para qualquer enumeração com mais de dois itens. Listas numeradas só para passos e escolhas
- **Uma tabela** sempre que três ou mais coisas são comparadas em várias propriedades
- **Itálico** (`*text*`) para termos, nomes de produtos e gêneros: *bullet hell musical*, *Geometry Dash*. Não dá para contar com o itálico nas fontes chinesas e japonesas, então nesses idiomas o itálico vai só em nomes de produtos escritos em letras latinas, e a ênfase é em negrito
- **Negrito** para enfatizar uma palavra ou para abrir um parágrafo com o assunto dele
- **Crases** para tudo o que é técnico: arquivos, campos, formatos, valores, teclas, comandos
- **Uma versão é sempre o prefixo mais o número, entre crases:** `gv 1.0.0`, `sv 1.1.0`, `fv 1.0.0`, `bv 1.0.0`, `mg 2`. Nunca um `1.0.0` solto, "versão 1.0.0" ou "SDK 1.0.0" sem o prefixo. As crases não funcionam em `title` e em `# H1`, então ali é `gv 1.0.0` simples. As versões de coisas de terceiros (Unity, pacotes NuGet) não são nossas e são escritas como são
- **Sem emoji**

## Destaques

Um parágrafo com um propósito concreto vira um destaque. Há exatamente cinco, e o título é escrito no idioma da página:

| Destaque | Título em inglês | Título em russo | Título em chinês | Título em japonês | Título em coreano | Título em espanhol | Título em português | O que ele abre |
|---|---|---|---|---| --- |---|---|---|
| `> [!tip] Recommendation` | Recommendation | Рекомендация | 建议 | 推奨 | 권장 | Recomendación | Recomendação | faça deste jeito |
| `> [!tip]` | Tip | Подсказка | 提示 | ヒント | 팁 | Consejo | Dica | um atalho, um truque, um caminho mais rápido |
| `> [!info]` | Worth knowing | Интересно | 须知 | 補足 | 참고 | Conviene saber | Vale saber | contexto que explica uma decisão |
| `> [!warning]` | Warning | Предупреждение | 警告 | 警告 | 경고 | Advertencia | Aviso | isto vai custar tempo ou qualidade |
| `> [!caution]` | Caution | Внимание | 注意 | 注意 | 주의 | Precaución | Cuidado | isto destrói trabalho ou publica um nível quebrado |

**No máximo dois destaques por página,** porque um terceiro deixa de ser lido como ênfase. As páginas de referência podem ter dois por seção. Uma página sobre algo que ainda não existe abre com um `> [!warning]` sobre o status, e esse não conta para o limite

## Voz

- **Trate o leitor por "você"** (em russo, o "вы" formal em minúscula, em chinês `你`, em espanhol `tú`, nunca `usted`, em português `você`). O japonês não nomeia o leitor por um pronome e nunca usa `あなた`
- **O projeto fala de forma impessoal,** nunca como "os desenvolvedores" ou "nós". O conselho é "recomenda-se" (em russo "рекомендуется", em chinês `建议`, em japonês `〜することをおすすめします` ou `推奨`, em espanhol `se recomienda` ou `conviene`, em português também `vale a pena`), e um fato tem a própria coisa como sujeito: "O jogo não traz nenhuma textura"
- **A opinião ou a decisão do autor fica na primeira pessoa,** "eu recomendo" (em russo "я рекомендую", em chinês `我建议`, em japonês `私は〜をおすすめします`). O jogo é feito por uma pessoa só, então "eu" é honesto aqui. Só para um julgamento ou uma decisão real, não para fatos simples
- **As notas em `notes/` podem falar na primeira pessoa,** porque uma nota é o relato do autor dela
- **Sem histórico na documentação.** Uma página da documentação descreve como as coisas funcionam agora. "Antes era X" é uma nota
- **Sem alegações de ser melhor.** Uma comparação só é permitida quando ajuda o leitor a entender mais rápido
- **Declare os limites do que se sabe.** "Muito provavelmente", "ainda não se sabe". A falsa certeza é pior do que não saber
- **Todo julgamento vem com o motivo.** Um adjetivo sem motivo é um defeito
- **Números em vez de adjetivos.** Segundos, quadros, megabytes, versões, quantidades de objetos
- **A ironia é seca e rara,** um comentário curto entre parênteses. As páginas de referência quase não têm
- **Sem palavrões** em nenhum idioma, incluindo substitutos grosseiros
- **Nunca invente** um endereço, um número ou um fato. Sem fonte, diga que não se sabe

## Abertura da página

**A abertura responde, ela não anuncia.** Ela não descreve a página ("o que é X, como Y funciona e onde fica Z"), ela dá uma resposta curta à pergunta para a qual a página existe. Uma abertura assim é útil sozinha, mesmo que o leitor não vá adiante

**O essencial vai no primeiro parágrafo.** Ele também é a descrição nas listagens, na pesquisa e nas pré-visualizações de links: cortado em 200 caracteres, sem links nem formatação. A resposta pode continuar no segundo e no terceiro parágrafos

**Não divida uma página curta.** Se há pouco conteúdo, a abertura se junta ao corpo em vez de se repetir como uma linha separada no topo

```
Antes:
Onde relatar um bug ou fazer uma pergunta, e o que escrever para que o bug possa ser reproduzido

Depois:
Os bugs do jogo vão para as issues de releases, as perguntas para o Discord. Anexe a linha de versão das configurações e os passos que levam ao bug
```

## Estrutura de uma página

1. `# H1` e uma abertura que responde à pergunta da página
2. O corpo não repete a abertura, ele dá os detalhes, os casos e os passos
3. Seções `##`, um tema cada: a afirmação, depois o mecanismo ou os passos, depois a conclusão
4. Onde couber, conselhos concretos ou links de "leia a seguir" no fim
5. O final nunca reconta a página

Uma página de guia leva de 2 a 4 minutos para ser lida, cerca de 2000 a 3500 caracteres. Uma página de referência pode ser mais longa, mas cada seção se sustenta sozinha

## O que denuncia o texto de outra pessoa

- um travessão, um ponto no fim de um parágrafo, um ponto e vírgula
- "Não é só X, é um Y inteiro"
- floreios em três tempos: "mais rápido, mais barato, mais confiável"
- aberturas vazias: "no mundo de hoje", "vamos mergulhar", "não é segredo que"
- um parágrafo final que repete o que já foi dito
- adjetivos entusiasmados sem motivo: "incrível", "fantástico", "uma ferramenta poderosa"
- enrolação educada e pedidos de desculpa ao leitor
- frases simétricas escritas pelo ritmo em vez do sentido
- conselhos genéricos que ninguém conferiu com este jogo

## Antes e depois

**Um parágrafo de abertura**

```
Antes:
No mundo atual do design de níveis, o editor do Bullet Hero ocupa um lugar especial — não é só uma
ferramenta, é um ecossistema inteiro. Vamos mergulhar e ver por quê.

Depois:
O editor monta um nível a partir de objetos que vivem em um trecho de tempo e se movem seguindo quadros-chave. Abaixo está como ele é organizado e em que ordem trabalhar com ele
```

**Um julgamento**

```
Antes:
O formato Blob é uma solução incrível que acelera drasticamente o carregamento e deixa o seu fluxo de trabalho mais produtivo.

Depois:
`Blob` carrega mais rápido que `Json`, mas não pode ser lido a olho nem comparado no git. Mantenha um nível em `Json` enquanto trabalha nele e converta-o para `Blob` antes de publicar
```

**Algo que ainda não existe**

```
Antes:
O servidor oficial vai oferecer um jeito prático de compartilhar os seus níveis com o mundo inteiro.

Depois:
Ainda não há servidor oficial. O protocolo que o jogo vai usar para falar com ele não foi projetado, então esta página descreve só o que já foi decidido
```

## Checklist antes de um pull request

1. A página pode ser lida por cima: uma ideia por frase, os detalhes mais abaixo na página ou numa página própria
2. Nenhum travessão e nenhum meia-risca (o chinês e o japonês não usam traço nenhum)
3. Nenhum parágrafo, item de lista ou título termina com ponto
4. Nenhuma linha grudada: cada ideia separada é um parágrafo próprio ou está separada por um ponto dentro da linha. Um parágrafo em chinês ou japonês é uma linha no código-fonte
5. Nenhum ponto e vírgula, nenhum emoji, no máximo um ponto de exclamação
6. Nenhum palavrão
7. Vírgulas, dois-pontos e concordância seguem a norma, sem erros de digitação
8. Todo julgamento tem o motivo ao lado
9. Números, nomes de campos e links vêm de uma fonte
10. Nada de "os desenvolvedores" ou "nós" em `docs/`: o conselho é impessoal, "eu" só para a opinião ou a decisão do autor
11. No máximo dois destaques
12. A abertura depois do H1 responde à pergunta da página (o essencial nos primeiros 200 caracteres), não descreve a página e não se repete abaixo
13. O final não reconta a página
