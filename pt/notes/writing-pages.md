---
title: Escrever páginas
date: 2026-10-13
tags: [contributor]
---

# Escrever páginas

As páginas são arquivos markdown no repositório aberto bullet-hero/docs. Uma mudança chega como pull request: um fork, um branch, a mudança em todos os idiomas, uma verificação com o guia de estilo

## Repositórios

Todos os repositórios do projeto ficam na organização [bullet-hero](https://github.com/bullet-hero). Os abertos:

| Repositório | O que contém |
|---|---|
| [bullet-hero/releases](https://github.com/bullet-hero/releases) | as releases contêm cada build pública do jogo, as issues contêm bugs e pedidos dos jogadores sobre o jogo |
| [bullet-hero/sdk](https://github.com/bullet-hero/sdk) | o código do SDK, as issues contêm bugs e pedidos sobre o SDK |
| [bullet-hero/docs](https://github.com/bullet-hero/docs) | estas páginas e as traduções delas |
| [bullet-hero/backend](https://github.com/bullet-hero/backend) | o servidor, vazio por enquanto |

O código do jogo (`bullet-hero/game`) e o do site (`bullet-hero/frontend`) são fechados

Esta página é sobre o bullet-hero/docs

## Como enviar uma mudança

1. Faça um fork de [bullet-hero/docs](https://github.com/bullet-hero/docs) e crie um branch
2. Edite ou adicione páginas no formato descrito abaixo
3. Mude a página em todos os idiomas, ou diga no pull request quais idiomas ainda precisam da mudança. Mais - [[translating]]
4. Confira o texto com o [[style-guide]]
5. Abra um pull request com uma descrição curta do que mudou e por quê

**Os fatos vêm do jogo, do SDK ou da documentação deles.** Números, nomes de campos, nomes de arquivos, atalhos e endereços nunca são adivinhados. Não tem certeza de que algo é verdade? Diga isso no pull request, não na página

Uma mudança aceita aparece em [bullethero.space](https://bullethero.space/) em poucos minutos: cada push para `master` reconstrói o site

> [!tip] Dica
> Você não consegue gerar o site por conta própria, porque o código dele é fechado. A pré-visualização mais próxima é o Obsidian: um link que o Obsidian não encontra também não vai ser encontrado no site

## Como o repositório funciona

- **Só markdown.** Não há build própria nem scripts
- **É um vault do [Obsidian](https://obsidian.md/).** Abra a pasta raiz do repositório como vault, e os links, as incorporações e as pré-visualizações funcionam do mesmo jeito que no site. Qualquer outro editor de markdown também serve
- **É um submódulo do site.** O site inclui o repositório como a pasta `content/`, compila as páginas na build e pré-renderiza cada uma delas. O site é gerado a partir do `master` mais recente deste repositório

## O que vai onde

| Caminho | O que contém | Endereço no site |
|---|---|---|
| `<lang>/docs/1_game/` | para jogadores: instalar, jogar, configurações, as mecânicas | `/docs/game` |
| `<lang>/docs/2_editor/` | para autores de níveis: o guia e a referência do editor | `/docs/editor` |
| `<lang>/docs/3_sdk/` | para desenvolvedores: o SDK aberto e o formato de nível | `/docs/sdk` |
| `<lang>/docs/4_server/` | para quem hospeda servidores: servidores oficiais e da comunidade | `/docs/server` |
| `<lang>/docs/5_changelog/` | o histórico de mudanças, uma página por versão do jogo | `/docs/changelog` |
| `<lang>/notes/` | artigos, comunidade, regras de edição, documentos públicos e políticas, por data | `/notes/<name>` |
| `<lang>/tags/` | páginas de tags | `/tags/<tag>` |
| `<lang>/download.md` | a página de download | `/download` |
| `assets/` | imagens para todos os idiomas | incorporadas nas páginas |

`<lang>` é uma pasta de idioma: `en`, `ru`, `zh`, `zh-Hant`, `ja`, `ko`, `es` ou `pt`. Um arquivo fora de `docs/`, `notes/`, `tags/` e `download.md` não vira uma página

**A documentação descreve como as coisas funcionam agora.** Um histórico de mudanças, uma opinião ou um ensaio é uma nota em `notes/`

## Nomes de arquivos e ordem

- **A ordem na barra lateral é definida por um prefixo `N_`** em cada arquivo e pasta dentro de `docs/`: `1_`, `2_` e assim por diante, até `10_` e além
- **O prefixo nunca chega ao endereço.** `1_game/3_controls.md` abre em `/docs/game/controls`
- **`index.md` não tem prefixo.** É a página de entrada da pasta. Ela assume a posição da pasta e dá o nome ao grupo na barra lateral
- **Para mudar a ordem, renomeie os arquivos.** Ative "Automatically update internal links" no Obsidian, e ele corrige cada link sozinho
- **Um nome sem o prefixo é único dentro de um idioma.** Se dois arquivos se reduzem ao mesmo endereço, a build do site avisa
- **Um nome com prefixo é idêntico em todos os idiomas.** `en/docs/2_editor/4_craft/3_difficulty-curve.md` e `ru/docs/2_editor/4_craft/3_difficulty-curve.md` são a mesma página
- **`notes/` não tem prefixos nem subpastas.** Nunca renomeie `notes/cookie-policy`: o aviso de cookies do site tem um link para ela

## Frontmatter, título e descrição

Toda página começa assim:

```md
---
title: Difficulty and the curve
date: 2026-09-24
tags: [level_author]
---

# Difficulty and the curve

One line that says what the page is, up to 200 characters, no markup
```

- **`title`, o H1 e a descrição são escritos no idioma da página.** O exemplo acima é da versão em inglês
- **O frontmatter é `title`, `date` e `tags`.** Nada mais é lido. `date` no formato `YYYY-MM-DD` é a data da última atualização, não da criação. Quando você editar um arquivo, defina `date` como o dia da edição
- **`# H1` é obrigatório e é igual a `title`.** O site mostra só o corpo da página, então o H1 é o título visível
- **O primeiro parágrafo depois do H1 é a descrição** nas listagens, na pesquisa e nas pré-visualizações de links. Ele é cortado em 200 caracteres. Escreva-o como uma linha, sem links nem formatação. Ele responde brevemente à pergunta da página em vez de descrever o que há nela, [[style-guide#Abertura da página]]
- **As seções são `##`, as subseções `###`.** Elas geram âncoras e o sumário. Níveis mais profundos não são necessários

## Tags de público

Cada página da documentação tem de 1 a 3 tags desta lista. As tags são escritas em `snake_case` sem `#`. O site as mostra na página

| Tag | No site | Quem |
|---|---|---|
| `player` | [[player]] | um jogador comum |
| `advanced_player` | [[advanced_player]] | um jogador interessado nas mecânicas |
| `level_author` | [[level_author]] | faz níveis no editor |
| `developer` | [[developer]] | constrói algo sobre o SDK ou estende o jogo |
| `server_host` | [[server_host]] | roda um servidor para si e para os amigos |
| `server_advanced` | [[server_advanced]] | um grande hospedeiro de servidor, disposto a estender ou escrever um servidor |
| `contributor` | [[contributor]] | edita os textos e as traduções neste repositório |

As notas em `notes/` usam tags de tema em vez disso, atualmente `legal` ([[legal]])

O leitor nunca vê o código da tag. O rótulo vem da página da tag `<lang>/tags/<code>.md`:

- o `title` dela é o rótulo
- o primeiro parágrafo dela descreve o público
- o site adiciona sozinho a lista de páginas com a tag

Uma tag nova precisa de uma página dessas em cada idioma

Para mencionar uma tag no texto, coloque um link para a página dela: `[[level_author]]`. O link mostra o rótulo no idioma do leitor

## Links

| O quê | Como |
|---|---|
| Outra página | `[[3_difficulty-curve]]`, pelo nome completo do arquivo com o prefixo |
| Uma seção de uma página | `[[3_difficulty-curve#Anchor]]` |
| A página de entrada de uma pasta | `[[2_editor/4_craft/index]]`, com o caminho, já que toda página assim se chama `index` |
| Um site externo | `[text](https://…)`, com o endereço completo e o esquema |

Os links levam a um endereço sem idioma, então uma mesma fonte funciona em todos os idiomas. `[[cookie-policy]]` leva um leitor em inglês à página em inglês, um leitor em russo à página em russo, um leitor em chinês à página em chinês, um leitor em japonês à página em japonês, um leitor em coreano à página em coreano, um leitor em espanhol à página em espanhol e um leitor em português à página em português

Coloque links só para páginas que existem. A build do site aponta cada link que não conseguiu resolver

## Imagens

As imagens ficam em `assets/` na raiz do repositório e são incorporadas com `![[file.png]]`

Uma única pasta serve todos os idiomas. O texto desenhado em uma imagem não é traduzido junto com a página

## Destaques

| Sintaxe | Cor | Uso |
|---|---|---|
| `> [!note]`, `> [!info]`, `> [!tip]` | azul | contexto, um atalho, uma recomendação |
| `> [!warning]`, `> [!caution]` | amarelo | custa tempo ou qualidade, destrói trabalho |
| `> [!danger]`, `> [!bug]` | vermelho | renderizados, mas o guia de estilo não os usa |

Qual destaque escolher, o título dele e o limite de dois por página - [[style-guide]]

## Números, versões e rótulos da interface

Um número que o jogo decide - a velocidade do avatar, um padrão das configurações, um limite de tamanho - e a versão atual não são digitados na página. Eles ficam em `values.yaml` na raiz do repositório, e a página escreve um marcador que o site preenche na build:

- `\{{v:avatar.move-speed}}` é um valor de `values.yaml`. O site o escreve do jeito que o idioma da página escreve números, `0.15` em inglês e `0,15` em russo
- `\{{ui:menu_main_sandbox-btn}}` é um rótulo da interface de `game/<lang>.yaml`, no próprio idioma da página
- `\{{` é um par literal de chaves

Uma chave que não existe interrompe a build do site, então um número novo entra primeiro em `values.yaml`. Uma versão citada como um momento da história ("desde `gv 1.0.0`") fica como texto. O Obsidian mostra o marcador do jeito que ele foi escrito

## Código e outras marcações

- **O realce de código** existe só para `ts`, `tsx`, `js`, `json`, `csharp`, `bash`, `yaml`, `css` e `md`. As outras linguagens aparecem como texto simples
- **Tabelas GFM, listas de tarefas, notas de rodapé e `==highlights==`** funcionam
- **Sem MDX e sem JSX.** `{` e `<` aparecem como são
