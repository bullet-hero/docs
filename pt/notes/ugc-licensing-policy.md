---
title: Política de licenciamento dos níveis de usuários
date: 2026-10-01
tags: [legal]
---

# Política de licenciamento dos níveis de usuários

Todo nível de usuário é distribuído sob CC BY-NC: com atribuição e apenas para uso não comercial. Um recurso externo é permitido sob uma licença aberta aceita ou com a permissão direta do autor dele

> [!warning] Aviso
> As informações desta página serão revistas mais tarde - os termos, a lista de licenças aceitas e a forma de registrar uma permissão ainda podem mudar

Bullet Hero permite que os jogadores criem o próprio conteúdo (UGC, conteúdo gerado por usuários), e esse conteúdo precisa ser licenciado. A abordagem é parecida com a de *Geometry Dash*, com uma diferença: onde *Geometry Dash* trata de uma única faixa de música, esta política abrange **todos** os recursos externos de um nível

## A licença do nível

Todo nível de usuário é distribuído sob **CC BY-NC**:

- **CC** - uma licença Creative Commons
- **BY** - a atribuição é obrigatória: os autores são creditados
- **NC** - apenas uso não comercial

Esta licença abrange o conteúdo original do próprio nível: a disposição, a sincronia e os quadros-chave, o código personalizado e o trabalho criativo de organizar tudo em um nível pronto. **Ela não altera a licença dos recursos externos incluídos no nível**

Cada recurso externo mantém a própria licença ou permissão, registrada separadamente para cada recurso (veja abaixo). A CC BY-NC no nível é um invólucro em torno de recursos que, cada um por si, já podem ser redistribuídos dessa forma

**Um nível só pode ser distribuído sob CC BY-NC se cada recurso externo nele atender à opção A ou à opção B.** Se apenas um não atender, o nível não pode ser distribuído pelos serviços web oficiais do Bullet Hero (o servidor oficial, OWS)

Eu não impeço a distribuição livre de níveis por canais não oficiais. Sou categoricamente contra o uso comercial de níveis

## Recursos externos

Os recursos externos abrangem uma grande variedade de dados:

- música e áudio: `.mp3`, `.wav`, `.ogg`
- texturas e imagens: `.png`, `.jpg`, `.jpeg`
- fontes: `.ttf`, `.otf`
- textos e bytes: quaisquer dados

Cada recurso externo precisa atender a uma das duas opções abaixo

### Opção A - uma licença aberta

O recurso está disponível sob uma licença igual à CC BY-NC ou mais permissiva (veja a lista de licenças aceitas abaixo). O recurso mantém a **própria** licença original: ele não é convertido em CC BY-NC, ele já permite a redistribuição pública não comercial que a CC BY-NC exige, então incluí-lo em um nível CC BY-NC é coerente

A licença original e a fonte do recurso precisam ser registradas no arquivo de metadados do nível. A SIL OFL já exige isso para fontes, e aqui a exigência vale para todo recurso, para que qualquer pessoa que baixe o nível possa ver em que termos cada parte foi usada

### Opção B - a permissão direta do autor

O autor do recurso dá permissão para usá-lo especificamente no Bullet Hero. Um "claro, pode usar" em particular não basta por si só: um nível marcado como CC BY-NC é redistribuído publicamente, então a permissão precisa cobrir isso explicitamente, e não só o seu uso pessoal. Uma permissão válida concede as três coisas:

1. O direito de usar o recurso dentro de um nível do Bullet Hero
2. O direito de que o nível resultante, este recurso incluído, seja redistribuído livremente **sem fins comerciais** por terceiros pelos serviços do Bullet Hero (OWS, Oficina Steam, NOWS), com atribuição ao autor
3. Apenas uso não comercial, declarado explicitamente

A permissão pode ser qualquer coisa que um moderador consiga verificar: um e-mail, uma mensagem direta ou uma declaração pública (por exemplo, no Twitter/X). Use o modelo abaixo como ponto de partida e guarde a resposta do autor como prova

### Modelo de pedido de permissão

Preencha os campos e ajuste o tom como for preciso, mas mantenha os pontos 1 a 3 intactos: são eles que tornam a permissão válida para a distribuição sob CC BY-NC. O modelo está em inglês, como na política original. Se o autor fala outro idioma, traduza o modelo e mantenha os três pontos

```
Subject: Permission to use "<TRACK/RESOURCE NAME>" in a Bullet Hero level

Hi <AUTHOR NAME>,

My name is <YOUR NAME / HANDLE>, I'm creating a level for Bullet Hero (a rhythm/
bullet-hell game - <link to game/project if available>) and I'd love to use your
work "<TRACK/RESOURCE NAME>" (<link to the original>) in it.

Specifically, I'm asking your permission to:
1. Use "<TRACK/RESOURCE NAME>" inside my Bullet Hero level.
2. Allow the level (including your work) to be shared/redistributed for FREE and
   NON-COMMERCIALLY by anyone who downloads it, through Bullet Hero's official and
   unofficial services (including its official server, Steam Workshop, and any
   community-run servers).
3. Credit you as "<HOW YOU WANT TO BE CREDITED>" wherever the level shows attribution.

To be clear, this permission is for non-commercial use only - the level will not be
sold, and no one (including me) will make money from it or from your work through it.

If you're fine with this, a simple reply confirming points 1-3 is all I need - I'll
keep this email/message as proof of permission. If you'd rather I credit you
differently, or you want to set any other condition, just let me know.

Thanks a lot either way!
<YOUR NAME / HANDLE>
```

Como escrever um pedido assim e o que conta como prova está explicado com mais detalhes em [[6_asking-permission]], e lá também há uma versão do modelo em russo

## Serviços externos

O jogo pode funcionar com vários serviços externos:

| Serviço | Descrição |
|---|---|
| Official Web Services (OWS) | o servidor padrão, disponível em todas as plataformas |
| Oficina Steam | disponível no PC |
| Non-official web services (NOWS) | serviços que qualquer pessoa pode criar e operar como achar melhor |

Está previsto que todas as ferramentas para rodar o seu próprio servidor sejam de código aberto sob a licença MIT. Ainda não existe nenhum servidor. Mais sobre os servidores em [[4_server/index]]

## Licenças aceitas (opção A)

Um recurso externo aceito tem uma destas licenças típicas, igual à do nível ou mais permissiva:

- A família Creative Commons
  - CC BY-NC (Atribuição-NãoComercial) - igual à do nível
  - CC BY (Atribuição) - mais permissiva que a CC BY-NC
  - CC0 (domínio público) - a melhor opção, use sempre que puder
- Apache, MIT - feitas para texto e código, e mais permissivas que a CC BY-NC
- GPL - feita para texto e código, aceita apenas por um serviço cujo perfil permita. O servidor oficial não permite, veja abaixo
- SIL OFL (Open Font License) - precisa ser indicada no arquivo de metadados

> [!info] Vale saber
> O perfil de publicação `standard`, sobre o qual o servidor oficial é construído, aceita CC0, CC BY, CC BY-NC, SIL OFL, MIT, Apache 2.0 e a Unlicense, mas não a família GPL. Uma obra GPL redistribuída pela App Store entra em conflito com os termos da Apple, então um catálogo com essas obras não poderia ser servido ao iOS mais tarde

Licenças típicas que **não** são aceitas:

- Proprietária ("Todos os direitos reservados") - obviamente não é aceita
- A família Creative Commons
  - CC BY-SA (Atribuição-CompartilhaIgual) - tecnicamente permitida, mas exige que a licença do nível mude para CC BY-NC-SA, que o OWS não aceita, então a resposta é não
  - CC BY-ND (Atribuição-SemDerivações) - tecnicamente permitida, mas exige que o nível seja protegido contra modificações, o que o jogo não suporta, então a resposta é não
  - CC BY-NC-SA (Atribuição-NãoComercial-CompartilhaIgual)
  - CC BY-NC-ND (Atribuição-NãoComercial-SemDerivações)

## Onde encontrar recursos aceitos

### Áudio e música

Gratuitos com garantia:

- [ccMixter](https://ccmixter.org/) - perfeito, conteúdo sob CC BY e CC BY-NC
- [Freesound](https://freesound.org/) - perfeito, todo o conteúdo sob CC0, CC BY e CC BY-NC
- [Incompetech](https://incompetech.com/) - perfeito, todo o conteúdo sob CC BY
- [Teknoaxe](https://teknoaxe.com/) - perfeito, todo o conteúdo sob CC BY
- [Kenney Assets](https://kenney.nl/) - todos os sons sob CC0

Gratuitos, mas vale a pena conferir cada registro:

- [SoundImage](https://soundimage.org/)
- [Pixabay](https://pixabay.com)
- [GoodKid](https://goodkidofficial.com/creators/) - nenhuma licença é declarada, mas a julgar pelo FAQ deles é CC BY sem menção ao autor. Use como CC BY
- NCS - apenas se o nível mantiver a licença padrão CC BY-NC

Exigem verificação manual da licença:

- [OpenGameArt](https://opengameart.org/) - se a licença não puder ser identificada, o recurso não pode ser usado
- [FMA](https://freemusicarchive.org/home) - todo tipo de licença CC, verifique cada uma com cuidado
- SoundBible

Duvidosos:

- Zapsplat
- [Play On Loop](https://www.playonloop.com/music-licensing/) - uma condição: o jogo não pode ser um projeto comercial

### Texturas e imagens

Gratuitos com garantia:

- [Poly Haven](https://polyhaven.com/)
- [AmbientCG](https://ambientcg.com/)
- [Kenney Assets](https://kenney.nl/)
- [Pexels](https://www.pexels.com/)
- [Unsplash](https://unsplash.com/)

Gratuitos, mas vale a pena conferir cada registro:

- [Pixabay](https://pixabay.com)

Exigem verificação manual da licença:

- [OpenGameArt](https://opengameart.org/)
- [Rawpixel](https://www.rawpixel.com/) - apenas a "Personal License" e a "Public Domain License", veja [a página de licenças](https://www.rawpixel.com/services/licenses)
- itch.io
- Wikimedia Commons

### Fontes

Gratuitos com garantia:

- Google Fonts

## Palavras finais

Bullet Hero não é um jogo grande. Eu tento manter uma relação humana com a comunidade e peço que você faça o mesmo. Uma boa comunidade se constrói em conjunto
