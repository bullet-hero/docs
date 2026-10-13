---
title: Linhas do tempo
date: 2026-10-02
tags: [level_author]
---

# Linhas do tempo

As linhas do tempo mostram o nível ao longo do tempo: objetos, quadros-chave do objeto selecionado, o modelo de um prefab, áudio e eventos. A grade de batidas ajuda a colocar tudo isso sobre a música

## Linha do tempo do nível

Mostra todos os objetos do nível ao longo do tempo. Cada objeto é um clipe. A linha em que o clipe fica é a **camada** do objeto

Um clipe é um **intervalo** semiaberto. Um objeto nos quadros 10-19 termina exatamente onde começa um objeto que inicia no quadro 20. Os dois nunca desenham juntos em um quadro compartilhado

> [!info] Vale saber
> O intervalo de um filho precisa ficar dentro do intervalo do pai. Isso é **resolvido na leitura e nunca salvo**. Encolha o pai e os filhos são cortados, mas os valores deles não mudam. Estique o pai de volta e tudo retorna. Um objeto raiz além do fim do nível são dados válidos, ele simplesmente não é reproduzido

> [!tip] Dica
> Quatro ferramentas ficam na barra de botões: `{{ui:editor_timeline-tool-selection_tooltip}}` seleciona e move, `Bordas` arrasta uma borda, `Tesoura` corta o clipe sob o cursor, `Seleção retangular` adiciona à seleção cada clipe que o retângulo arrastado toca. O menu abre com um clique direito em um *espaço vazio*. Pressionar um clipe começa um arrasto

O posicionamento de um prefab e os objetos que ele traz são desenhados na cor do prefab

Como as ferramentas tratam um posicionamento:
- A duração vem do modelo por padrão. Uma duração diferente em um posicionamento é registrada como substituição apenas desse posicionamento
- Se você arrastar a borda inicial dele com `Bordas`, o ponto a partir do qual ele lê o modelo se move junto. Assim a imagem dentro dele fica onde estava
- `Tesoura` o corta em dois posicionamentos do mesmo modelo, e cada um reproduz a própria parte. O modelo em si não muda
- Os objetos que um posicionamento trouxe não podem ser cortados. Corte o próprio posicionamento ou corte esses objetos no modo prefab

Mais: [[3_how-the-editor-thinks|Como o editor funciona]], [[4_composition-and-camera|Composição e câmera]]

## Linha do tempo local

Mostra os quadros-chave do **objeto selecionado**. Cada propriedade animável tem a própria faixa: posição, rotação, escala, tamanho, âncoras, pivô, cor, UV, tamanho da fonte

Aqui os quadros contam **a partir do início do intervalo do objeto**. Mova o objeto e toda a animação dele se move junto

> [!info] Vale saber
> **Uma faixa vazia são dados válidos**, não uma lacuna. Uma faixa sem quadros-chave usa o valor padrão. Por isso um objeto novo não anima nada até você colocar um quadro-chave

Um valor só se mistura entre quadros-chave vizinhos. O intervalo decide quais quadros existem, mas não como os valores se misturam

Em um objeto vindo de um prefab, uma faixa que ainda coincide com o modelo é desenhada na cor do prefab. Adicione, mova ou edite um quadro-chave nela e a cor some: a faixa agora guarda uma substituição

No modo prefab, com a raiz do modelo selecionada, esta linha do tempo tem a duração do modelo inteiro

Mais: [[3_how-the-editor-thinks|Como o editor funciona]]

## Linha do tempo do prefab

A linha do tempo própria do modo prefab. Mostra os objetos do **modelo**

> [!info] Vale saber
> A duração dela é a duração própria do modelo, não o intervalo de um dos posicionamentos. Um modelo é editado como um pequeno nível independente. Ele pode ser posicionado muitas vezes e em momentos diferentes

Uma das linhas é a **raiz** do modelo, e ela ocupa a duração do modelo inteiro. Todos os outros objetos do modelo ficam pendurados nela:
- a linha da raiz pode ser selecionada. O inspetor e a linha do tempo local passam a mostrar a raiz
- ela não pode ser arrastada, esticada nem cortada
- ela se recolhe como qualquer pai. Uma raiz recolhida oculta o modelo inteiro nesta linha do tempo

> [!warning] Aviso
> A seleção não é compartilhada com o resto do editor. Não há pré-visualização ao vivo de um posicionamento específico. As edições mudam o modelo e se espalham para todos os posicionamentos que fazem referência a ele

Mais: [[2_reuse|Reutilização: prefabs, cópia, geradores]]

## Linha do tempo de áudio

Mostra as faixas de áudio do nível com a forma de onda. Isso facilita alinhar o conteúdo com o que se ouve

> [!tip] Dica
> `{{ui:editor_inspector-audio-span_fit}}` no inspetor ajusta a faixa à duração real do clipe. O botão fica indisponível se não há clipe ou se a velocidade é 0: uma faixa congelada não tem duração
> `{{ui:editor_inspector-audio-span_fit-level}}` também aumenta a duração do nível até o clipe inteiro caber. Os dois botões pedem confirmação antes

> [!caution] Cuidado
> O controle deslizante `{{ui:editor_inspector-audio_volume}}` no inspetor é o fader da faixa. O volume com quadros-chave é uma faixa Volume separada na linha do tempo local. Na reprodução os dois se multiplicam

Mais: [[2_preparing-the-track|Preparar a faixa de áudio]]

## Linha do tempo de eventos

Mostra os quadros-chave do nível que não pertencem a nenhum objeto:
- posição, rotação, zoom, pivô e tremor da câmera
- marcadores e checkpoints
- o limite da tela
- o fundo e o tema
- todos os efeitos de pós-processamento
- a visibilidade, o controle, a colisão, o tamanho e a velocidade do jogador

> [!info] Vale saber
> A faixa **Batida** é a exceção aqui. Os itens dela têm intervalo, e ela é a única faixa em que `Bordas` e `Tesoura` atuam

> [!tip] Dica
> Uma cor pode fazer referência ao tema do nível em vez de um valor fixo. Então mudar o tema recolore de uma vez tudo o que faz referência a ele

Mais: [[4_composition-and-camera|Composição e câmera]], [[6_themes]]

## Grade de batidas

Ajuda a colocar o conteúdo sobre a música. Os geradores trabalham com as mesmas batidas que você vê

São metadados de criação, não uma mecânica. **A reprodução não lê a grade**

A grade é uma lista de **segmentos**. Cada um tem andamento constante: BPM, deslocamento de fase, batidas por compasso.
Os segmentos não se sobrepõem. As lacunas entre eles são necessárias: uma introdução sem bateria, uma pausa, o final depois da música. Uma única faixa de andamento não conseguiria expressar isso

> [!tip] Dica
> `TOCAR` registra toques no indicador de reprodução. `{{ui:editor_beat-tap_commit}}` transforma os toques em um segmento do primeiro toque ao último. As batidas sempre são contadas a partir do início do segmento e não se acumulam, então o erro fica abaixo de meio quadro

Mais: [[2_rhythm-and-structure|Ritmo e estrutura]]

## Segmento de batida

Um trecho de andamento constante: BPM, deslocamento de fase em quadros fracionários, batidas por compasso, um nome e uma cor

Exatamente um segmento é mostrado, mesmo que vários estejam selecionados. Todos os campos, exceto o nome, são únicos de cada segmento. Editá-los juntos fundiria os segmentos uns nos outros

> [!caution] Cuidado
> Um segmento é identificado pelo quadro inicial. Por isso **movê-lo muda a identidade dele**. Depois de mover, selecione o segmento de novo no novo início

> [!tip] Dica
> Aqui os toques refazem a fase do segmento selecionado em vez de criar um novo. O BPM e o deslocamento mudam em um único passo de desfazer

Mais: [[2_rhythm-and-structure|Ritmo e estrutura]]
