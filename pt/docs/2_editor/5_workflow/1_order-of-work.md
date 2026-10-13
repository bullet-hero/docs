---
title: A ordem de trabalho
date: 2026-10-12
tags: [level_author]
---

# A ordem de trabalho

Primeiro a música, o fps, o mapa de batidas e os marcadores, depois um esqueleto de formas simples e o playtest dele. Decoração, tema e efeitos ficam por último

Os passos vão do mais caro ao mais barato.
Quanto mais cedo o passo, mais custa refazê-lo quando tudo já foi construído em cima dele

## A base

1. **A música pronta.** Convertida, normalizada, cortada. Todo o resto é medido a partir dela. Trocar a música depois desloca cada quadro do nível
2. **FPS e duração do nível.** Os dois podem ser mudados, mas o caro é o fps: depois da mudança, todos os quadros-chave são recalculados. O padrão é `60`, e normalmente não há motivo para mudá-lo
3. **O mapa de batidas.** Segmentos, andamento, deslocamento, fórmula de compasso. Enquanto o mapa de batidas estiver errado, nada se encaixa direito nas batidas. Tudo o que for colocado antes dele terá que ser movido depois
4. **Marcadores sobre a estrutura.** Intro, verso, refrão, break, drop, outro. São dez minutos de trabalho, e os marcadores aparecem em todas as linhas do tempo

## O esqueleto e o playtest dele

5. **O esqueleto.** Os padrões principais em formas simples. Sem decoração, sem tema, sem efeitos
6. **Playtest do esqueleto.** Antes da decoração: depois que uma seção é decorada, você não vai querer excluí-la

> [!caution] Cuidado
> O esqueleto é a etapa em que o nível é de fato projetado. E é a etapa pulada com mais frequência. Um esqueleto que não é divertido de jogar não fica divertido com decoração. Ele vira um nível decorado que não é divertido de jogar

## Completando o nível

7. **Conteúdo.** Complete os padrões e adicione os objetos que até agora estavam só subentendidos
8. **Temas e cor.** Desde o início, defina as cores como referências ao tema, não como valores fixos
9. **Efeitos e pós-processamento.** Por último. São os mais fáceis de exagerar, e é difícil avaliá-los enquanto o nível ainda está mudando
10. **Metadados.** Nome, descrição, autores, classificação etária. Preencha a ficha de um recurso assim que adicionar o recurso, não neste passo

## Três hábitos que poupam trabalho

Vale o mesmo quando quem monta o nível é você ou o assistente de IA:
- **Tudo o que se repete é um prefab.** Edite o modelo uma vez e todas as cópias acompanham - [[2_reuse]]
- **Um contorno que nenhuma forma embutida oferece é uma forma do nível**, desenhada no editor de formas ou dada pela IA como polígono. Ela desenha e causa dano como um único objeto, ao contrário de uma pilha de retângulos
- **Use o enquadramento 16:9 inteiro.** Uma margem vazia grande é tela que o jogador vê e o nível desperdiça. Mantenha o perigo longe da borda em si, a decoração pode chegar até ela - [[4_composition-and-camera]]

## O que é barato e o que é caro mudar

**Barato de mudar no final:** as cores pelo tema, a decoração, o pós-processamento, a descrição do nível

**Caro:** o fps, a música, o mapa de batidas e a hierarquia

> [!warning] Aviso
> Mudar o pai de um objeto muda de uma vez a transformação, o tempo de vida e a ordem de desenho dele. Por isso reestruturar um nível pronto raramente se resolve com uma única edição

Salve a cada passo. O que o salvamento automático e o desfazer cobrem - [[4_not-losing-work]]

A seguir: [[2_reuse|Reutilização: prefabs, cópia, geradores]], [[4_not-losing-work|Não perder seu trabalho]]
