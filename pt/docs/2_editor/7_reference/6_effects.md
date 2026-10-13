---
title: Efeitos
date: 2026-10-01
tags: [level_author]
---

# Efeitos

Um efeito são partículas do VFX Graph com parâmetros divididos em módulos: quantas partículas, de onde saem, como se movem, que cor e tamanho têm. Você os edita no inspetor ou no editor de efeitos

## Inspetor de efeito

Mostra os parâmetros de um efeito `VFX Graph` em grupos: configuração, principal, forças, forma, ângulo, escala e cor. Todos os grupos ficam visíveis ao mesmo tempo

> [!info] Vale saber
> Os efeitos **recebem a semente do mesmo jeito que todo o resto**: dos números que você edita, não do estado de um gerador. Por isso o nível é reproduzido de forma idêntica em qualquer dispositivo

> [!tip] Dica
> As cores podem fazer referência ao tema do nível em vez de um valor fixo. Os tipos com gradiente abrem o editor de gradientes compartilhado

Mais: [[1_level-budget|O orçamento do nível]]

## Principal - quantas partículas e por quanto tempo

Define quantas partículas existem, quanto tempo vivem e com o que são desenhadas. É tudo o que vale antes da primeira força. A outra metade é [[6_effects#Forças - o que move uma partícula|Forças]]

`Qtd. de partículas` é o principal controle de custo. É exatamente o número que a previsão de capacidade do nível conta

Um emissor custa aproximadamente a quantidade vezes o tempo de vida. Dobrar `Limites do tempo de vida` custa tanto quanto dobrar a quantidade

`Forma` é a silhueta de cada partícula, do mesmo conjunto que os objetos comuns usam. `Textura` é a imagem por cima dela. Os dois campos podem ficar vazios. Uma partícula sem textura é o caso comum e barato

> [!warning] Aviso
> A quantidade tem limite de 1024. Essa é a capacidade do próprio grafo. Um grafo de VFX processa toda a CAPACIDADE dele a cada quadro, não só as partículas vivas. Então um sistema custa o que pediu, mesmo que precise de menos

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve todos os campos ao valor padrão em um único passo de desfazer

Mais: [[1_level-budget|O que cabe em um nível]]

## Configuração - quando o emissor silencia

Define quando o emissor para de gerar partículas. Desativado, ele gera enquanto o objeto vive. Esse é o caso comum: a rajada termina junto com o objeto

`Quadro de parada` conta a partir do início do intervalo próprio do OBJETO, não da linha do tempo do nível. Então um efeito no fim de um nível pode silenciar trezentos quadros próprios depois

As partículas que já estão vivas vivem até o fim. A emissão é cortada, e a imagem desaparece suavemente

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve os dois campos ao valor padrão em um único passo de desfazer

Mais: [[1_level-budget|O que cabe em um nível]]

## Ângulo - rotação da partícula

Define como uma partícula gira ao longo da vida. Há cinco variantes:
- `Valor` - um ângulo fixo
- as duas variantes `Curvas` leem uma curva
- as duas variantes `Aleatório` sorteiam um valor entre A e B para cada partícula

Quais linhas existem depende da escolha. As duas variantes com curva diferem no QUE lê a curva:
- `Curvas ao longo da vida` - o tempo de vida da partícula
- `Curvas por velocidade` - a velocidade da partícula, através da janela de velocidades abaixo

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve o grupo inteiro aos valores padrão, `Tipo` inclusive. A curva ou o par aleatório que você configurou se perde

Mais: [[1_readability-and-fairness|Legibilidade]]

## Cor - cor da partícula

Define como uma partícula é colorida ao longo da vida. Seis variantes: as mesmas cinco de [[6_effects#Ângulo - rotação da partícula|Ângulo]] e [[6_effects#Escala - tamanho da partícula|Escala]], só que com gradientes em vez de curvas, mais um `Gradiente aleatório`:
- `Gradiente ao longo da vida` lê o gradiente pelo tempo de vida da partícula
- `Gradiente por velocidade` lê o gradiente pela velocidade da partícula
- `Gradiente aleatório` pega uma cor do gradiente por partícula em vez de percorrê-lo
- as duas variantes `Aleatório` embaixo sorteiam uma cor entre duas cores

> [!tip] Dica
> Uma cor aqui pode ser uma referência ao tema, como em qualquer outro lugar do nível. Assim o efeito acompanha um nível que muda a paleta no meio do caminho

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve o grupo inteiro aos valores padrão, `Tipo` inclusive. O gradiente ou o par de cores que você configurou se perde

Mais: [[5_color-and-postprocessing|Cor e temas]]

## Escala - tamanho da partícula

Define o tamanho de uma partícula ao longo da vida. As mesmas cinco variantes de [[6_effects#Ângulo - rotação da partícula|Ângulo]]: um tamanho fixo, uma curva ou um sorteio entre dois valores por partícula

Aqui há duas curvas, porque o tamanho tem dois eixos. `Curva X` e `Curva Y` são lidas de forma independente. Uma partícula pode esticar e encolher ao mesmo tempo

> [!warning] Aviso
> A linha abaixo das curvas é REAPROVEITADA. Com `Valor` e as duas variantes `Aleatório`, ela é o próprio tamanho. Com `Curvas por velocidade`, ela é a janela de velocidades. O rótulo ao lado e a ajuda dela dizem o que a linha é no momento

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve o grupo inteiro aos valores padrão, `Tipo` inclusive. As duas curvas e o par aleatório se perdem

Mais: [[1_readability-and-fairness|Legibilidade]]

## Forma - de onde as partículas saem

Define o volume de surgimento: um ponto, um anel, um retângulo, um segmento, um cone ou um toro. Ela decide só onde uma partícula COMEÇA. O que acontece com ela depois é com [[6_effects#Forças - o que move uma partícula|Forças]]

Mudar `Tipo` muda o conjunto de campos abaixo. As linhas são reaproveitadas: a primeira é o raio de um círculo, o raio superior de um cone ou o raio menor de um toro, conforme o que estiver selecionado

`Arco` é quanto da borda é usado, em radianos, no sentido anti-horário a partir do eixo +X. Menos de uma volta completa dá um leque

> [!tip] Dica
> `Abertura` transforma um anel estático em um anel que se move. Ela decide em que ponto da borda cai a próxima partícula: ao acaso, girando em um sentido, em ida e volta ou ao longo de uma senoide. `Loop` é o clássico emissor giratório

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve o grupo inteiro aos valores padrão, `Tipo` inclusive. A forma que você configurou, com os raios e a abertura, se perde

Mais: [[4_composition-and-camera|Composição]]

## Forças - o que move uma partícula

Define tudo o que move uma partícula depois que ela surge. [[6_effects#Forma - de onde as partículas saem|Forma]] decide onde ela começa, e este grupo decide para onde ela voa

Os campos são de dois tipos. Confundi-los é o erro comum:
- os pares de campos iniciais (`inicial` no nome) são sorteados UMA vez quando a partícula nasce, entre o mínimo e o máximo deles. Afaste os valores de um par e uma rajada uniforme vira um leque
- todo o resto atua CONTINUAMENTE durante a vida inteira da partícula

Campos do segundo tipo:
- `Velocidade linear` é vento, não um empurrão
- `Força linear` é uma aceleração, então ela se acumula
- `Velocidade orbital` gira as partículas em torno do centro, não em torno delas mesmas

> [!tip] Dica
> `Velocidade de movimento` multiplica o resultado inteiro. Assim um efeito pronto pode ficar mais lento ou mais rápido sem mexer nos outros campos

> [!info] Vale saber
> A ação **redefinir** ao lado deste botão devolve os onze campos ao valor padrão em um único passo de desfazer

Mais: [[4_composition-and-camera|Composição]]

## Editor de efeitos

Monta um efeito de partículas e o mostra na tela de desenho

> [!info] Vale saber
> Os grupos de parâmetros são os mesmos do inspetor de efeito. Aqui eles são editados como **rascunho**: nada chega ao nível até você salvar

> [!tip] Dica
> Salve o efeito na biblioteca compartilhada do dispositivo para usá-lo em outros níveis

Mais: [[1_level-budget|O orçamento do nível]]
