---
title: Recursos do nível
date: 2026-10-12
tags: [level_author]
---

# Recursos do nível

As texturas, formas, temas, efeitos e prefabs de um nível ficam na pasta dele e viajam com ele. Cada recurso tem um cartão próprio com origem, licença e autores

## Biblioteca

Recursos salvos **neste dispositivo**. Eles são compartilhados por todos os níveis que você abre aqui

Importar copia o recurso *para dentro do nível*. Um nível é uma pasta de arquivos e leva consigo tudo o que precisa. É isso que o mantém portátil

Por isso a biblioteca é uma comodidade para você. Quem joga o seu nível nunca depende dela

A biblioteca mostra três origens, cada uma como um chip: `{{ui:editor_library-source_library}}`, `{{ui:editor_library-source_local}}` e, em uma build da Steam, `{{ui:editor_library-source_workshop}}`. Escolher uma entrada a importa com as dependências dela. Se o nível já tem outra versão, o jogo pergunta qual manter

Mais - [[16_library-and-collections]], [[2_reuse]]

## Texturas

Imagens que este nível carrega. **O jogo em si não traz nenhuma textura.** Cada textura que um nível usa foi adicionada aqui

Um nível é só uma pasta de arquivos. A textura fica nela e viaja com o nível: compacte a pasta, envie, descompacte, jogue

As formas **não** são texturas, são geometria de verdade. Elas não precisam de nada desta aba

Mais - [[3_images-and-fonts]]

## Formas

As formas próprias do nível. Elas se somam às cerca de 500 formas que o jogo gera

Uma forma é **geometria de verdade**, não uma imagem. O retângulo do objeto é a caixa da forma, e os dois tipos de forma se acomodam nela de jeitos diferentes:
- **uma forma embutida mantém as proporções.** O lado mais longo dela ocupa o retângulo, por isso um `Triangle` de tamanho (2, 2) é desenhado com 2 de largura e cerca de 1,73 de altura
- **uma forma definida pelo nível é esticada até o retângulo** do jeito que foi desenhada na caixa dela. Um contorno dado pelo assistente de IA é ajustado à caixa, por isso preenche o retângulo exatamente

> [!tip] Dica
> **Uma forma e uma hitbox são o mesmo tipo de dado.** Um objeto guarda duas referências: uma para o que é desenhado, outra para o que é atingido. Nenhuma deriva da outra. Por isso um feixe de aviso inofensivo, uma hitbox mais simples que o desenho e uma parede invisível são todos conteúdo comum

Mais - [[1_level-needs]]

### Nomes das formas embutidas

O nome de uma forma embutida é montado a partir de partes, sempre nesta ordem. `Circle_S2_T8_I` é a metade direita de um círculo, como um anel com espessura de 1/8 do raio, invertida

| Parte | Significado |
|---|---|
| forma | `Square`, `Circle`, `Triangle`, `RightTriangle` ou um polígono regular: `Pentagon`, `Hexagon` e assim por diante |
| `S2`, `S4`, `S8` | um setor: uma metade, um quarto, um oitavo. Começa reto para cima e segue no sentido horário, por isso `S2` é a metade direita. Sem `S` - a forma inteira |
| `_2` depois de `S4` | o outro quarto: o inferior direito em vez do superior direito. Só existe onde a forma dá uma figura diferente |
| `T2`, `T4`, `T8`, `T16`, `T32` | um anel com espessura de 1/2, 1/4, 1/8, 1/16 ou 1/32 do raio. Sem `T` - preenchida |
| `I` | invertida: a caixa (ou o setor dela) menos a forma |

Uma forma sem outras partes, como `Circle`, é a forma inteira preenchida. Nem toda combinação existe. A metade de um quadrado é só um retângulo, então um tamanho mais estreito resolve isso

## Temas

Um tema é uma **paleta**. As cores do nível podem apontar para ele em vez de guardar valores literais

Trocar o tema ativo muda de uma vez o visual de tudo o que aponta para ele. O tema ativo pode ser animado na linha do tempo de eventos. É assim que um nível muda todo o visual no meio da música

Os temas podem ser salvos na biblioteca do dispositivo e reutilizados em outros níveis

Mais - [[6_themes]], [[5_color-and-postprocessing]]

## Efeitos

Efeitos de partículas `VFX Graph` que o nível pode posicionar

Os efeitos são um **enriquecimento opcional**. Um nível que nunca usa nenhum é jogado exatamente como foi projetado

Um efeito usa a mesma aleatoriedade com semente que todo o resto do nível. Por isso ele se repete de forma idêntica em qualquer dispositivo. Os efeitos podem ser salvos na biblioteca do dispositivo e reutilizados em outros níveis

**O jogo não traz efeitos predefinidos.** Cada efeito que um nível usa foi criado nele ou tirado da biblioteca

Mais - [[1_level-budget]]

## Prefabs

Grupos reutilizáveis de objetos. Um prefab guarda os próprios objetos de modelo. Posicionar um prefab grava cópias reais deles no nível

Editar o modelo depois se reflete em cada posicionamento. Mesmo assim, um posicionamento pode diferir do modelo por meio de substituições por instância

> [!warning] Aviso
> Os prefabs **não têm predefinições do jogo**, e os efeitos também não. O jogo traz predefinições só para temas, fontes, sons da interface e as formas embutidas. A biblioteca é a única forma de compartilhar um prefab entre níveis: a biblioteca do seu dispositivo ou uma coleção. Mais - [[16_library-and-collections]]

Mais - [[2_reuse]]

## Metadados do recurso

Título, descrição, origens, licença e autores de um recurso

É assim que a atribuição sobrevive. Uma textura, uma fonte ou um arquivo de áudio tirado de algum lugar carrega, dentro do nível, de onde veio e sob quais condições. Esse registro vai para onde o nível for

> [!tip] Recomendação
> Preencha isso ao adicionar o recurso. É o único momento em que você ainda lembra de onde ele veio

Mais - [[4_resource-record]]

## Editor de temas

Os slots de um tema e as cores neles

> [!caution] Cuidado
> O conteúdo do nível aponta para um slot pela posição dele. Por isso **renumerar os slots muda o visual de tudo o que os referencia**

> [!tip] Dica
> Salve um tema pronto na biblioteca do dispositivo. Assim dá para usá-lo em outros níveis

Mais - [[6_themes]], [[5_color-and-postprocessing]]

## Referência a uma cor do tema

Faz esta cor apontar para um **slot do tema do nível** em vez de um valor literal

Quando o tema muda, tudo o que referencia um slot muda de visual de uma vez. Os temas podem ser animados na linha do tempo de eventos. É assim que um nível muda toda a paleta no meio da música sem tocar em um único objeto

> [!tip] Dica
> As amostras mostram a paleta no quadro do quadro-chave que você está editando, nunca no indicador. A janela nomeia os temas de cada lado desse quadro. Para escolher pensando em um visual posterior, edite um quadro-chave que fica mais adiante

Mais - [[6_themes]], [[5_color-and-postprocessing]]

## Editor de formas

Monta uma forma a partir de pontos e das arestas entre eles

Você edita pontos e arestas. **Os triângulos são calculados automaticamente e nunca são editados.** Assim, um canto compartilhado por três triângulos é um único ponto para arrastar, e não três que se separam

> [!warning] Aviso
> As arestas existem só no editor, o formato guarda triângulos. Por isso uma aresta que não fecha nenhum contorno é descartada ao salvar. O editor avisa sobre isso em vez de descartá-la em silêncio

Mais - [[3_images-and-fonts]]

## Licenças

As condições sob as quais este nível e os recursos dele são distribuídos

Um nível carrega todos os arquivos de que precisa: imagens, fontes, áudio. Cada arquivo pode vir com condições próprias. **Essas condições são registradas por recurso**, e não só para o nível como um todo. Assim, um nível feito de partes emprestadas pode dizer exatamente o que foi emprestado e sob quais condições

> [!tip] Recomendação
> Leia as condições antes de reutilizar qualquer coisa do nível de outra pessoa

Mais - [[1_licensing-basics]]
