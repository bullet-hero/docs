---
title: Geradores
date: 2026-10-12
tags: [level_author]
---

# Geradores

Um gerador cria conteúdo e o aplica ao nível em uma única operação que se desfaz em um único passo. Todo gerador é executado pela janela "Geradores" da barra de ferramentas

## Geradores

O formulário de um gerador é montado a partir dos próprios campos dele. Não existe uma interface separada para cada gerador

> [!caution] Cuidado
> Tudo o que reescreve ou exclui conteúdo existente pede confirmação antes

> [!info] Vale saber
> Há duas famílias. Os **geradores** (*gen_*) criam conteúdo: ondas de balas, padrões radiais e um cache de fontes. Os **modificadores** (*mod_*) mudam o que já existe: ajustar intervalos, quantizar quadros-chave. Os modificadores são descritos à parte - [[9_modifiers]]

Mais - [[2_reuse]]

## A janela de geradores

Os geradores de conteúdo e os modificadores são executados pela janela `{{ui:editor_generators_text}}` da barra de ferramentas. O bloco `{{ui:editor_generators_base-parameters}}` dela é compartilhado por todos os geradores: `{{ui:editor_generators-start_frame}}`, `{{ui:editor_generators-end_frame}}`, `{{ui:editor_inspector_layer}}` e `{{ui:editor_generators_seed}}`. Eles pertencem à janela, não a um gerador específico

Como o bloco se comporta:
- A janela abre com um segundo a partir do indicador de reprodução e com a semente em 0. `{{ui:editor_generators-seed_random}}` sorteia uma semente nova
- Os quadros ficam dentro da linha do tempo em que você trabalha, do quadro 1 ao último quadro dela. No modo prefab, isso é a duração do modelo
- Editar `{{ui:editor_generators-start_frame}}` empurra `{{ui:editor_generators-end_frame}}` junto. Editar `{{ui:editor_generators-end_frame}}` para em `{{ui:editor_generators-start_frame}}`. Eles nunca se cruzam
- `{{ui:editor_inspector_layer}}` fica dentro dos limites permitidos de camadas
- Cada campo de quadro tem um alfinete que o prende à borda da linha do tempo. `{{ui:editor_generators-whole_level}}` define os dois, e a janela vai do quadro 1 ao último quadro. Os campos continuam editáveis, e digitar em um campo tira o alfinete dessa borda

`{{ui:editor_generators_group}}` e `{{ui:editor_generators-split_layers}}` vêm ativados por padrão. O grupo recebe o nome do gerador. Os dois afetam só os geradores de conteúdo: um modificador não cria nada, então não há nada para agrupar

O conteúdo gerado nunca vai para baixo do objeto selecionado. Ele cai no nível superior do escopo ou no próprio grupo

Antes de você pressionar `{{ui:editor_generators_run}}`, a janela mostra o que uma execução vai adicionar. O botão fica indisponível, e o motivo aparece no lugar da estimativa, se:
- o gerador precisa do nível inteiro e você está no modo prefab. São eles Flash na batida, Cache de fontes, Previsão de capacidade e Remapear taxa de quadros
- o gerador precisa de uma seleção e nada está selecionado
- depois da execução o nível teria mais de 262 144 objetos
- um gerador de conteúdo não adicionaria nada. Um modificador não é recusado por isso

Um gerador que precisa de dados externos (uma faixa de áudio, batidas, uma imagem) não cria nada sem eles, e a estimativa diz isso

`{{ui:editor_generators_run}}` fecha a janela. O conteúdo gerado fica selecionado, no mesmo passo de desfazer

A janela lembra em qual gerador você estava e quais parâmetros você digitou quando ela é fechada e aberta de novo. `{{ui:editor_generators_reset}}` volta aos valores padrão

## Níveis

O assistente de IA não pode executar estes três. Em vez disso, ele começa um nível novo com o próprio `level_create`

### Nível vazio

Limpa o nível por completo. Tudo o que foi criado é excluído.
Serve para recomeçar do zero, não para editar

`Pin Screen Aspect` (ativado por padrão) coloca um quadro-chave com 16:9 fixo na faixa `{{ui:editor_events-timeline_track_screen-limit}}`, no primeiro quadro

Mais - [[2_first-level]]

### Nível a partir de arquivo de áudio

Começa um nível a partir de uma faixa.
Conecta o áudio, ajusta a duração do nível à faixa e deixa você no início de uma linha do tempo vazia

`Pin Screen Aspect` (ativado por padrão) coloca um quadro-chave com 16:9 fixo na faixa `{{ui:editor_events-timeline_track_screen-limit}}`, no primeiro quadro

Mais - [[2_preparing-the-track]]

### Importar arquivo compactado do nível

Monta um nível a partir de um arquivo compactado criado por este jogo.
Formatos: `.tar.gz` e `.zip`. Os dois podem ter senha

O tipo de arquivo é detectado pelo conteúdo, não pelo nome. Um arquivo compactado renomeado abre do mesmo jeito.
O jogo reconhece `7z`, mas ainda não o lê e o recusa

> [!tip] Dica
> Um arquivo compactado de uma build antiga abre sem preparação. O próprio jogo o converte para o formato atual na importação

> [!warning] Aviso
> Por padrão, um nível importado recebe um ID novo. Assim ele não sobrescreve um nível que já está neste dispositivo. Desmarque esta caixa só para restaurar um nível que já esteve neste dispositivo

## Balas

Mais sobre todos os geradores de balas - [[1_readability-and-fairness]]

> [!caution] Cuidado
> O `Collider` de um gerador de balas vem vazio por padrão. As balas dele desenham um quadrado e não podem ferir o jogador até você escolher um colisor, por exemplo a mesma forma de `Shape`. Os outros geradores que colocam formas, os de geometria e Forma de onda do áudio, têm o mesmo campo com o mesmo padrão

### Onda de balas

Uma fileira de balas que se movem juntas.
O padrão básico, e é por ele que vale a pena começar. Os parâmetros dele se repetem nos outros geradores de balas

### Espiral de balas

As balas saem ao longo de um raio que gira. O resultado é a clássica parede em espiral

### Chuva de balas

As balas caem sobre uma área ao longo de um tempo definido.
A densidade e a dispersão são ajustáveis.
O lugar onde cada bala cai vem da `{{ui:editor_generators_seed}}` da janela, não da semente do nível. A mesma semente repete uma execução exatamente, e uma semente diferente dá outra distribuição. O assistente de IA passa a própria semente, `0` a menos que ele indique outra, então duas execuções que devem ser diferentes precisam de duas sementes

### Balas teleguiadas

As balas fazem uma curva em direção ao lugar onde se espera que o jogador esteja.
A trajetória é calculada antes, não durante o jogo. Por isso o resultado é o mesmo em qualquer dispositivo

### Varredura de laser

Um raio atravessa o campo.
O aviso e a fase que causa dano são objetos diferentes. Assim o aviso pode ser mostrado sem matar.
O raio de aviso nunca colide. O raio que dispara só fere com um `Collider` escolhido

## Geometria

Mais sobre todos os geradores de geometria - [[2_reuse]]

### Polígono

Coloca formas nos vértices ou nas arestas de um polígono regular

### Radial

Coloca cópias ao redor de um círculo. A base da maioria dos padrões simétricos

### Espiral

Coloca cópias ao longo de uma espiral. O raio e o ângulo crescem juntos

### Grade

Preenche um retângulo com cópias de uma forma a distâncias iguais

### Fractal

Repete uma forma dentro dela mesma, menor a cada vez.
A quantidade de objetos cresce exponencialmente com a profundidade. Aumente a profundidade um passo de cada vez

## Áudio e efeitos

### Forma de onda do áudio

Monta objetos a partir da forma de uma faixa de áudio. O nível acompanha visivelmente o que se ouve

Mais - [[2_reuse]]

### Flash na batida

Coloca um flash em cada batida.
As batidas vêm do mapa de batidas do nível. Se não há mapa, vêm dos marcadores.
Assim pisca exatamente o que você vê na grade

Mais - [[2_rhythm-and-structure]]

## Recursos e utilitários

### Objetos da textura

Transforma uma imagem em objetos, um por célula.
A imagem vira conteúdo do nível e é animada como todo o resto

Mais - [[3_images-and-fonts]]

### Cache de fontes

Reúne todos os caracteres que o texto do nível usa e os prepara com antecedência.
Assim nenhum caractere é preparado no momento em que aparece pela primeira vez

> [!tip] Recomendação
> Execute-o quando o texto estiver terminado. Um caractere adicionado depois sem preparar de novo causa um travamento na primeira vez que aparece

Mais - [[3_images-and-fonts]]

### Previsão de capacidade

Registra os limites recomendados do nível: quantos objetos e efeitos ele precisa ao mesmo tempo

> [!info] Vale saber
> Isso não afeta o que é mostrado. O jogo reserva buffers para esses limites com antecedência. Sem isso, os buffers cresceriam no meio do nível, e isso causaria um travamento

Mais - [[1_level-budget]]
