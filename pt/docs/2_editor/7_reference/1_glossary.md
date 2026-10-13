---
title: Glossário
date: 2026-10-11
tags: [level_author]
---

# Glossário

A lista principal de termos do projeto. A interface do jogo, esta documentação e qualquer outro texto sobre Bullet Hero usam estas palavras, e um termo novo é adicionado aqui primeiro

## Conteúdo do nível

| Termo | Significado |
|---|---|
| **Nível** | Tudo o que forma uma partida: objetos, áudio, eventos e recursos próprios |
| **Objeto** | Um elemento que o autor cria na linha do tempo, com intervalo, transformação e pai próprios |
| **Objeto vazio** | Um objeto que não desenha nada: uma transformação, um intervalo e filhos. Cada um dos outros tipos adiciona o seu por cima dele |
| **Forma** | Geometria real que um objeto desenha, não uma imagem. O jogo gera cerca de 500 sozinho |
| **Colisor** | Aquilo com que um objeto colide. Pode não coincidir com o que o objeto desenha |
| **Prefab** | Um modelo reutilizável de objetos que se coloca em um nível quantas vezes for preciso |
| **Modo prefab** | Editar o conteúdo próprio de um modelo em vez do nível ao redor |
| **Efeito** | Um emissor: a cada quadro ele cria os próprios objetos a partir de poucos parâmetros |
| **Objeto de quadro** | Um objeto criado por um efeito. O motor cuida dele: não pode ser selecionado nem editado |
| **Tema** | Uma paleta a que o nível se refere por índice: recolorir é uma mudança, não cem |

## Tempo e animação

| Termo | Significado |
|---|---|
| **Quadro** | A unidade de tempo do nível. Um quadro é uma célula, e o tempo é o limite entre duas células |
| **Quadro-chave** | Um valor que o autor fixa em um quadro. Entre dois quadros-chave o valor é interpolado |
| **Faixa** | Uma linha de quadros-chave de uma propriedade animável: posição, rotação, volume |
| **Linha do tempo** | O eixo de quadros sobre o qual o nível é editado: uma aba para cada tipo de conteúdo |
| **Intervalo** | Quando um objeto existe: um quadro inicial e uma duração, mas não um quadro final |
| **Indicador de reprodução** | O quadro mostrado agora |
| **Suavização** | Como o valor passa do quadro-chave anterior para este |
| **Marcador** | Um ponto com nome na régua do nível, para voltar ao lugar exato |
| **Checkpoint** | Para onde uma morte leva o jogador de volta |

## Posicionamento e desenho

| Termo | Significado |
|---|---|
| **Âncora** | Uma borda que segue a borda do pai: se o pai encolhe, o filho se move junto |
| **Camada** | A ordem de desenho, e ela é relativa: a camada do filho se soma à camada do pai |
| **Pivô** | O ponto em torno do qual o objeto gira e escala, dentro do próprio retângulo |
| **Gizmo** | As alças de arrasto desenhadas sobre o objeto selecionado no viewport |
| **Encaixe** | Atrair um arrasto para algo: para o conteúdo com o ímã, para a música com o botão de batida |

## Música

| Termo | Significado |
|---|---|
| **Batida** | A grade própria da música: o autor a define, e nada a lê durante o jogo |
| **Segmento de batida** | Um trecho de andamento constante, com andamento, fase e comprimento de compasso próprios |
| **BPM** | Batidas por minuto - a rapidez com que um segmento de batida avança |
| **Toque** | Um toque enquanto você marca o andamento. Com toques suficientes, um segmento de batida fica descrito |

## Automação e dados

| Termo | Significado |
|---|---|
| **Gerador** | Automação da criação: produz conteúdo do nível a partir de poucos parâmetros |
| **Modificador** | Um gerador que edita ou remove o que já existe em vez de adicionar |
| **Semente** | O número do qual sai cada valor aleatório do nível: uma partida se repete exatamente igual |
| **Dados brutos** | Todo o modelo salvo como uma árvore editável. Aqui nada é validado, e isso é de propósito |
| **Assistente de IA** | Um cliente de IA conectado ao editor por MCP. Ele edita o nível aberto enquanto você assiste, um passo de desfazer por lote |

## Recursos e compartilhamento

| Termo | Significado |
|---|---|
| **Biblioteca** | Recursos no dispositivo para reutilizar entre níveis: sua biblioteca, suas coleções e as coleções que você assinou |
| **Coleção** | Uma pasta de recursos reutilizáveis de até sete tipos. Importar copia o conteúdo dela, então o nível não depende dela |
