---
title: Configurações
date: 2026-10-14
tags: [player]
---

# Configurações

O essencial se configura na primeira execução: o jogo abre sozinho uma configuração rápida com idioma, volume, desempenho e efeitos. Redefinir mexe só nas configurações, os níveis ficam

## As abas

| Aba | O que tem nela |
|---|---|
| `{{ui:settings_general_title}}` | o idioma, cada um com o nome na própria língua, `Русский (ru)`. `Sistema (pt)` segue o dispositivo e mostra qual idioma foi escolhido. Também quantos arquivos de nível carregam ao mesmo tempo, o tempo limite para um arquivo em um endereço da web, `{{ui:settings_general-open_folder}}` |
| `{{ui:field_common_audio}}` | volume: `{{ui:settings_audio_volume}}`, `{{ui:settings_audio_game}}`, `{{ui:settings_audio_ui}}`, `{{ui:settings_audio_editor-ui}}`, `{{ui:settings_audio_editor-game}}` |
| `{{ui:settings_controls_title}}` | os dispositivos e a forma de guiar o avatar, [[3_controls]] |
| `{{ui:settings_keybindings_label}}` | atalhos, principalmente os do editor, [[3_speed-and-shortcuts]] |
| `{{ui:settings_graphics_title}}` | tela, taxa de quadros, antialiasing, `{{ui:settings_graphics-colliders-mode_title}}`, texturas, efeitos, pós-processamento |
| `{{ui:settings_interface_label}}` | a interface durante o jogo, `{{ui:settings_interface_open-menu-on-lose}}`, `{{ui:settings_interface_menu-background}}`, `{{ui:settings_interface_levels-layout}}`, a orientação da tela, a sobreposição de estatísticas |
| `{{ui:settings_game-editor_title}}` | as configurações próprias do editor, incluindo a própria opção `{{ui:settings_interface_levels-layout}}` |
| `{{ui:settings_profile_tab}}` | as suas estatísticas, [[10_statistics]] |
| `{{ui:settings_other_title}}` | limpeza do armazenamento, transferência de perfil e o estado do Steam Cloud ([[14_profile-transfer]]), acesso a pastas no Android, modo anônimo, `{{ui:settings_other_reset}}` |

`{{ui:settings_interface_menu-background}}` escolhe o que aparece atrás dos botões do menu principal: uma arena ao vivo em que um bot se esquiva de ataques, um campo de formas girando ou nada

`{{ui:settings_interface_levels-layout}}` escolhe como a seleção de níveis abre - uma `{{ui:enum_level-browser-layout_grid}}` de capas ou uma `{{ui:enum_level-browser-layout_list}}` de linhas com descrições. Existem duas opções assim: a da aba `{{ui:settings_interface_label}}` é para o menu (`{{ui:enum_level-browser-layout_grid}}` por padrão), a da aba `{{ui:settings_game-editor_title}}` é para o editor (`{{ui:enum_level-browser-layout_list}}` por padrão). O botão ao lado do campo de pesquisa continua alternando a exibição até você sair dessa tela

## Configuração rápida

`{{ui:settings_quick-setup_title}}`, um botão na aba `{{ui:settings_general_title}}` acima de `{{ui:settings_general-open_folder}}`, faz algumas das perguntas mais importantes, uma categoria por página. Na primeiríssima execução ela abre sozinha, antes da oferta do tutorial. Cada resposta tem uma linha sobre o que ela faz. As páginas podem ser abertas em qualquer ordem, `{{ui:settings_quick-setup_next}}` só sugere a próxima

| Página | Pergunta | Respostas | O que muda |
|---|---|---|---|
| `{{ui:settings_quick-setup_page-language}}` | `{{ui:settings_general_language}}` | `{{ui:settings_general_language_system}}` e cada idioma do jogo, com o nome na própria língua | o mesmo que na aba `{{ui:settings_general_title}}` |
| | `{{ui:settings_audio_volume}}` | um controle deslizante | o mesmo que na aba `{{ui:field_common_audio}}` |
| `{{ui:settings_graphics_title}}` | `{{ui:settings_quick-setup_performance}}` | `{{ui:settings_quick-setup_performance-minimum}}`, `{{ui:settings_quick-setup_performance-economy}}`, `{{ui:settings_quick-setup_performance-recommended}}`, `{{ui:settings_quick-setup_performance-max}}` | a escala de renderização (PC), o antialiasing, o tamanho das texturas, a taxa de quadros dos efeitos - mas não o limite da taxa de quadros: toda resposta roda na taxa da tela. `{{ui:settings_quick-setup_performance-minimum}}` também desativa os efeitos de partículas e o pós-processamento e limita as imagens a 512 |
| | `{{ui:settings_quick-setup_comfort}}` | `{{ui:settings_quick-setup_comfort-full}}`, `{{ui:settings_quick-setup_comfort-soft}}`, `{{ui:settings_quick-setup_comfort-minimal}}` | todos os efeitos de pós-processamento e a fragmentação do avatar. `{{ui:settings_quick-setup_comfort-soft}}` desativa glitches, granulação, desfoque, distorção de lente e franjas de cor |
| `{{ui:settings_controls_title}}` | | `{{ui:settings_quick-setup_open-tutorial}}` | nada aqui: o tutorial permite testar cada esquema de controle e escolher o seu. Ele abre pelo menu principal ou pelo sandbox |

A resposta marcada com `{{ui:settings_quick-setup_default-badge}}` é aquela com que o jogo começa no seu dispositivo. Uma escolha vale na hora e aparece nas configurações completas. Se as suas configurações não batem com nenhuma resposta, nenhuma fica destacada e uma linha avisa isso - são as suas próprias configurações, e um toque as substitui

## Seções recolhidas

As abas longas são divididas em seções. O que muda com frequência fica aberto, o ajuste fino fica recolhido: uma seção abre pelo título. O botão ao lado do redefinir da aba recolhe ou expande todas as seções de uma vez

Na aba `{{ui:settings_controls_title}}` só fica aberto o dispositivo que está nas suas mãos

## Redefinir

Cada aba tem o próprio redefinir. `{{ui:settings_other_reset}}` em `{{ui:settings_other_title}}` redefine todas as abas de uma vez

Redefinir mexe só nas configurações. Os seus níveis ficam

## A linha de versão

A tela de configurações tem uma linha de versão. Um clique nela a copia

Ela tem este formato: `gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`. É essa linha que vai em um relatório de bug, [[11_help]]

## Gráficos

**Antialiasing.** No PC, o padrão é `{{ui:enum_anti-aliasing-type_msaa}}`. Um celular começa sem antialiasing. Toda forma do jogo é geometria de verdade, e `{{ui:enum_anti-aliasing-type_msaa}}` dá a ela bordas limpas sem desfocar, em todas as plataformas

`{{ui:enum_anti-aliasing-type_fxaa}}` é para celulares fracos. É uma passada sobre a tela inteira, e o custo dela é constante. O custo de `{{ui:enum_anti-aliasing-type_msaa}}` cresce quando muitas formas transparentes são desenhadas umas sobre as outras

TAA não é oferecido de propósito. Ele deixa um rastro atrás de projéteis rápidos, e a vibração dele atrapalha os efeitos de glitch

**Taxa de quadros.** A taxa de quadros alvo é definida manualmente, não pela sincronização vertical. Assim o timing de um nível é o mesmo em uma tela de 60 Hz e em uma de 144 Hz
Enquanto `{{ui:settings_graphics_vsync}}` estiver ativado (só no PC), o limite da taxa de quadros não faz nada

> [!tip] Recomendação
> Em um dispositivo fraco, baixe primeiro a **escala de renderização** para menos de 1. Isso custa só nitidez, e a interface continua em tamanho cheio. Só no PC

Mais - [[2_mobile-devices]]

## Modo só colisores

Um modo para treinar, uma seção recolhida na aba `{{ui:settings_graphics_title}}`. Com `{{ui:settings_graphics-colliders-mode_active}}` ativado, um nível em jogo desenha cada hitbox como um preenchimento liso de uma só cor sobre um fundo simples, e mais nada. Somem: a aparência das próprias formas, as formas sem colisor, os efeitos, os textos, o pós-processamento e o fundo do tema. Não mudam: a música, a colisão, a câmera e o tremor dela, os checkpoints, a interface e as estatísticas - uma partida neste modo conta como qualquer outra. O seu avatar é desenhado normalmente

O modo funciona só ao jogar níveis. O editor, o sandbox e o fundo do menu são desenhados normalmente

| Opção | O que faz |
|---|---|
| `{{ui:settings_graphics-colliders-mode_use-alpha}}` | ativado (o padrão) - os preenchimentos ficam semitransparentes pelo alfa da cor, e obstáculos sobrepostos aparecem mais escuros. O alfa nunca fica abaixo de 0.15. Desativado - todo preenchimento é sólido, e o alfa da cor fica travado |
| `{{ui:settings_graphics-colliders-mode_color}}` | a cor do preenchimento, vermelho com alfa 0.6 por padrão. A exibição de colisores do editor usa o mesmo tom com a própria opacidade |
| `{{ui:settings_graphics-colliders-mode_background}}` | o que é desenhado atrás dos preenchimentos, cinza-escuro por padrão - não preto, para que a borda do quadro da câmera apareça contra as faixas pretas em volta dela |

As duas cores ficam recolhidas sob a própria legenda: expanda a que precisar para ver a roda de cores dela

## Modo anônimo

Ativado em `{{ui:settings_other_title}}` → `{{ui:settings_other_suppress-game-saves}}`

Enquanto o modo está ativado, o jogo não salva nada próprio. `settings.json`, as estatísticas globais e as estatísticas dos níveis continuam intactos no disco. Uma configuração alterada ainda funciona até o jogo ser fechado

O trabalho com níveis é salvo normalmente: salvar, exportar, importar, copiar e excluir. O salvamento automático e os backups do editor também funcionam, eles têm o próprio interruptor

O modo dura até o jogo ser fechado e não é lembrado em lugar nenhum

Se você o desativar, as configurações atuais são salvas. Tudo o que foi jogado nesse tempo é descartado

> [!info] Vale saber
> O modo também é ativado sozinho. O [[12_launch-arguments|argumento de inicialização]] `--suppress-game-saves` o ativa durante toda a execução, e ele não pode ser desativado no jogo. Configurações ou estatísticas de uma versão mais nova do jogo também o ativam. Nesse caso, o jogo pergunta a cada execução se deve mantê-las ou sobrescrevê-las com os padrões
