---
title: Controles
date: 2026-10-02
tags: [player]
---

# Controles

Dá para jogar com mouse, tela sensível ao toque, gamepad ou sensor de movimento. No mouse, segurar o botão esquerdo guia o avatar, e Space, Shift ou o botão direito dão dash

Os comandos são reatribuídos nas configurações de controles, os botões do gamepad não

Para aprender os controles passo a passo ou testar cada modo sem começar um nível - [[13_sandbox]]

## Dispositivos

Todos os controles são configurados em `{{ui:settings_common_title}}` → `{{ui:settings_controls_title}}`, um grupo por dispositivo

| Dispositivo | Modo padrão | Mover | Dash |
|---|---|---|---|
| `{{ui:enum_control-device_keyboard-mouse}}` | `{{ui:enum_control-mode_absolute}}` | segurar o botão esquerdo, o avatar segue o mouse | `Space`, `Shift`, o botão direito do mouse ou um clique duplo (0.3 s) |
| `{{ui:enum_control-device_touchscreen}}` | `{{ui:enum_control-mode_relative}}` | arrastar um dedo em qualquer lugar da tela | um segundo dedo |
| `{{ui:enum_control-device_gamepad}}` | `{{ui:field_common_direction}}` | qualquer um dos analógicos | qualquer botão, exceto `Start` e `Select` |
| `{{ui:enum_control-device_device-gyro}}` | `{{ui:field_common_direction}}` | inclinar o dispositivo em relação à horizontal, velocidade máxima a 20° | um toque em qualquer lugar da tela |

Só o mouse já basta: o botão esquerdo guia o avatar, `{{ui:settings_controls-keyboard-mouse_km-dash-button}}` dá dash. O teclado é opcional

No gamepad, `Start` pausa e retoma. Os botões do gamepad não são reatribuídos: durante o jogo qualquer botão, exceto `Start` e `Select`, dá dash, inclusive o botão frontal da direita. No menu de pausa o botão frontal da direita funciona como "voltar", como em qualquer menu

## Modos de controle

| Modo | O que o seu comando significa |
|---|---|
| `{{ui:enum_control-mode_absolute}}` | uma posição. O cursor salta para lá, o avatar o alcança |
| `{{ui:enum_control-mode_relative}}` | um movimento. O cursor o acumula, o avatar alcança o cursor |
| `{{ui:field_common_direction}}` | uma direção. Não há cursor nenhum |

O movimento é instantâneo em todos os modos: sem aceleração e sem deslizar

Nos modos com cursor, o avatar alcança o cursor na própria velocidade de caminhada. Por isso ele fica para trás de um mouse rápido. Um dash vai na direção do cursor. Se o cursor estiver perto, o dash é mais curto e termina exatamente nele

O que acontece quando você solta o botão de guiar ou levanta o dedo é decidido por uma caixa de seleção - `{{ui:settings_controls-keyboard-mouse_km-cursor-return}}` para o mouse, `{{ui:settings_controls-touchscreen_touch-cursor-return}}` para a tela sensível ao toque:

- ativada - o avatar para onde está, o cursor volta para ele. É o padrão do mouse
- desativada - o cursor fica onde você o deixou, e o avatar caminha até ele. Só o dano pode mover o cursor. É o padrão da tela sensível ao toque

No modo `{{ui:field_common_direction}}`, um analógico empurrado até a metade dá metade da velocidade. Um dash sempre percorre o comprimento inteiro

Na tela sensível ao toque, no modo `{{ui:enum_control-mode_absolute}}`, o cursor fica acima do dedo (`{{ui:settings_controls-touchscreen_touch-finger-offset-y}}`). Assim o dedo não cobre o avatar

Enquanto um dedo guia o avatar, um segundo dedo dá dash onde quer que encoste - também sobre um painel ou um botão. A interface não recebe esse toque, então um dash nunca aperta nada por acidente

Os números exatos - [[6_avatar]]

## Sensor de movimento

O sensor de movimento não tem calibração. O avatar fica parado quando o celular está deitado, com a tela para cima

- incline a borda direita para baixo, e o avatar vai para a direita
- incline a borda superior para baixo, e ele vai para cima
- `{{ui:settings_controls-device_sensitivity}}` 1 dá a velocidade máxima a 20°. Com 2 basta metade da inclinação

O sensor acompanha a tela: gire o celular para a horizontal e de volta, e a direita continua sendo a direita. O sensor tem dois modos, `{{ui:enum_control-mode_absolute}}` e `{{ui:field_common_direction}}`

## Reatribuição

- **Os comandos de jogo** ficam em `{{ui:settings_controls_title}}`: o modo, `{{ui:settings_controls-keyboard-mouse_dash-keys}}`, `{{ui:settings_controls-keyboard-mouse_km-dash-button}}`, sensibilidade, zona morta, amortecimento, inversão, o joystick na tela e o botão de dash. `{{ui:settings_controls_reset}}` devolve todos os dispositivos aos padrões desta plataforma
- **Os atalhos** ficam em `{{ui:settings_keybindings_label}}`. Quase todos são do editor. Fora do editor existem `{{ui:settings_keybindings_window_toggle_fullscreen}}` (`F11` por padrão), `{{ui:settings_keybindings_window_settings_save}}` (`Ctrl+S` com as configurações abertas) e as teclas de navegação. `{{ui:settings_keybindings_reset}}` desfaz todas as reatribuições

Quando o jogo espera uma tecla, ele mostra `Pressione uma tecla para "..."`. Depois vale a regra `{{ui:settings_escape-cancels_backspace}}`

Das teclas, o jogo guarda só o que você reatribuiu. Se uma atribuição padrão melhorar depois, ela chega até você, a não ser que você mesmo tenha mudado essa atribuição. A aba `{{ui:settings_controls_title}}` é guardada inteira, por isso os novos padrões dela não chegam até você

Os atalhos do editor - [[3_speed-and-shortcuts]]

## Vários dispositivos ao mesmo tempo

Um dispositivo guia o avatar - o último que você usou. A troca acontece sozinha, no mesmo quadro, sem menu nenhum

O jogo consulta todos os dispositivos ativos a cada quadro. Um gamepad que ninguém toca envia zeros, e isso não conta como uso

No primeiro quadro nada foi usado ainda, então quem decide é a plataforma: o mouse no computador, a tela sensível ao toque no celular

O dash e a pausa funcionam a partir de qualquer dispositivo ativo, seja qual for o que está guiando. Um botão do gamepad dá dash enquanto o mouse guia. Um dash sozinho não assume o controle do movimento

Um dispositivo só pode guiar o avatar se:

- estiver marcado como ativo
- a plataforma tiver suporte a ele
- estiver conectado agora

`{{ui:settings_controls-active_now}}`, no topo, mostra qual está guiando

> [!tip] Dica
> Um esquema de controle parece não fazer nada? Normalmente outro dispositivo foi tocado depois dele. Olhe primeiro `{{ui:settings_controls-active_now}}`
