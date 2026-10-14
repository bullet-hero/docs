---
title: Avatar e movimento
date: 2026-10-14
tags: [advanced_player]
---

# Avatar e movimento

O avatar anda a {{v:avatar.move-speed}} unidades por segundo, e um dash o leva {{v:avatar.dash-distance}} unidades em {{v:avatar.dash-time}} s. A hitbox é um círculo de raio {{v:avatar.hitbox-radius}} unidades, menor que o quadrado desenhado de {{v:avatar.body-size}} unidades

Esta página é a fonte da verdade sobre o avatar. O jogo e os dois bots são feitos com estes números, e o SDK os registra como as constantes `AvatarRules`. Um código que discorda desta página é um bug no código

As distâncias estão em unidades do mundo. A câmera padrão tem exatamente {{v:camera.default-height}} unidades de altura (`ValueRules.DefaultZoom`), então uma unidade é um décimo da altura da tela, e o corpo do avatar tem meia unidade de largura. O zoom da câmera muda quanto você vê, mas não os números abaixo

## Os números

| O quê | Valor | Em palavras simples |
|---|---|---|
| Velocidade de caminhada | `{{v:avatar.move-speed}}` u/s | atravessa a tela de cima a baixo em dois terços de segundo |
| Velocidade do dash | `{{v:avatar.dash-speed}}` u/s | {{v:avatar.dash-to-walk-ratio}} vezes mais rápido que caminhar |
| Duração do dash | `{{v:avatar.dash-time}}` s | |
| Distância do dash | `{{v:avatar.dash-distance}}` unidades | velocidade × duração, três quartos da altura da tela |
| Recarga do dash | `{{v:avatar.dash-cooldown}}` s | contada a partir do início do dash |
| Invulnerabilidade do dash | `{{v:avatar.dash-invulnerability}}` s | também a partir do início, então dura {{v:avatar.dash-invulnerability-margin}} s a mais que o próprio movimento |
| Dash mais curto | `{{v:avatar.arrival-distance}}` unidades | igual à distância de chegada, mais perto que isso você já está sobre o alvo |
| Velocidade do empurrão | `{{v:avatar.knockback-speed}}` u/s | {{v:avatar.knockback-to-walk-ratio}} vezes mais rápido que caminhar, [[7_damage]] |
| Duração do empurrão | `{{v:avatar.knockback-time}}` s | sem controle durante ele |
| Imunidade após dano | `{{v:avatar.damage-timeout}}` s | todo impacto seguinte dentro desse tempo é ignorado |
| Tamanho do corpo | `{{v:avatar.body-size}}` unidades | o quadrado desenhado |
| Hitbox | raio de `{{v:avatar.hitbox-radius}}` unidades | {{v:avatar.hitbox-scale}} do corpo, menor de propósito do que o que você vê |
| Aparecimento e desaparecimento | `{{v:avatar.spawn-time}}` s | cresce e encolhe até virar um ponto |
| Efeito do tamanho do jogador na velocidade | total, `{{v:avatar.size-speed-influence}}` | um avatar maior se move proporcionalmente mais rápido. É a faixa de tamanho do jogador do nível, não o zoom da câmera |
| Velocidade de giro | `{{v:avatar.turn-speed}}` /s | estético: para onde o corpo aponta |
| Distância de chegada | `{{v:avatar.arrival-distance}}` unidades | mais perto do cursor que isso conta como estar sobre ele |

Derivados deles, e são estes que decidem uma esquiva:

| O quê | Valor |
|---|---|
| Dash mais curto: distância | `{{v:avatar.arrival-distance}}` unidades |
| Dash mais curto: duração | bem menos de um quadro |
| Dash mais curto: recarga e invulnerabilidade | bem menos de um quadro, cada uma |
| Dashes mais frequentes | no máximo um a cada dois quadros |
| Distância do empurrão | `{{v:avatar.knockback-distance}}` unidades |

O que acontece em um impacto - [[7_damage]]

## Movimento

Você controla o avatar de um de dois jeitos, e o jogo nunca os mistura:
- **Direção**: WASD, um analógico do gamepad, o giroscópio. O avatar vai para onde você empurra, na velocidade de caminhada. Um analógico empurrado até a metade dá metade da velocidade, e não existe outro "andar devagar"
- **Cursor**: o mouse ou um dedo. O avatar persegue o ponto em vez de se teletransportar para ele. Ele se move na própria velocidade de caminhada e fica para trás de um mouse rápido

O movimento é instantâneo nos dois casos: sem aceleração, deslizamento ou inércia. Você para no mesmo quadro em que para de se mover

## O dash

A invulnerabilidade dura {{v:avatar.dash-invulnerability-margin}} s a mais que o movimento. É essa margem depois da chegada que permite dar dash *através* de um obstáculo

Você continua guiando durante um dash. O dash vai para onde você pede: na direção mantida ou até o ponto de mira, e pode mudar no meio do dash. Um dash sem nenhuma direção mantida não sai do lugar

Com um cursor, o dash vai para onde você aponta e para lá:

| Distância até o cursor | O que acontece |
|---|---|
| mais de {{v:avatar.dash-distance}} unidades | um dash completo na direção dele. Você para antes do cursor |
| de {{v:avatar.arrival-distance}} a {{v:avatar.dash-distance}} unidades | um dash encurtado que termina exatamente no cursor |
| menos de {{v:avatar.arrival-distance}} unidades | nenhum dash |

Um dash encurtado é o mesmo dash em escala menor. Trajeto, invulnerabilidade e recarga encolhem juntos: um dash com metade do comprimento protege por metade do tempo e recarrega duas vezes mais rápido. Ele nunca sai mais barato. Dois meios dashes custam exatamente o mesmo que um dash completo e cobrem a mesma distância

Um dash que não acontece não custa nada: a recarga não começa, nada é gasto. Um jogador no modo direção que não segura nada recebe a mesma resposta - nenhum dash

O corpo fica de um azul mais intenso durante o dash e depois volta à cor normal ao longo dos {{v:avatar.dash-tint-fade}} s seguintes. Nada mais muda a cor do corpo, nem um impacto - um dash é o seu próprio movimento, então só ele faz isso

O rastro do dash e esse azul dependem do comprimento do dash: um dash completo os mostra inteiros, o mais curto a `{{v:avatar.dash-effect-min}}` disso, e tudo o que fica no meio em proporção. Um dash curto lança as partículas mais devagar, então o rastro parece exatamente tão longo quanto o dash

### Dois estilos, um orçamento

- No modo `{{ui:field_common_direction}}`, um dash sempre percorre as {{v:avatar.dash-distance}} unidades inteiras. Uma distância confiável sem mirar, mas também sem parar no meio do caminho
- Com um cursor, você escolhe o comprimento e pode parar exatamente em um ponto. Um dash curto significa proteção mais curta e um quadro vulnerável a mais por dash. Aponte para longe e o dash completo volta

Em linha reta os dois cobrem a mesma distância no mesmo tempo. Nenhum estilo é mais forte: um dá precisão, o outro simplicidade

### Dash atrás de dash

**Um dash segurado não é invulnerabilidade.** A recarga e a proteção têm a mesma duração, então um botão segurado dá uma cadeia contínua de dashes. Mas entre dois dashes sempre existe exatamente um quadro em que algo pode atingir você, em qualquer taxa de quadros, num celular lento do mesmo jeito que num PC rápido
A cadeia mais apertada é um dash no máximo a cada dois quadros

## A hitbox

O anel de pontos no avatar é desenhado exatamente sobre a hitbox. Um projétil raspou no contorno e não fez nada? Isso é de propósito

Enquanto você está invulnerável (em um dash ou logo depois de um impacto), não existe hitbox nenhuma

O mesmo anel mostra as suas vidas: um ponto aceso é uma vida de reserva

A visibilidade do anel é definida em `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_hitbox-ring-opacity}}`. `0` o oculta, mas os níveis são balanceados para quem o vê

O corpo é uma grade de {{v:avatar.grid-cells}} quadrados, {{v:avatar.grid-side}} por 5. Conforme a vida se perde, os quadrados da borda para o centro não somem, e sim desbotam: um quadrado perdido fica como um fantasma pálido, então a grade sempre mostra todos os {{v:avatar.grid-cells}}, e a vida se lê pelo número dos que ainda estão acesos. Os quadrados fantasma são transparentes o bastante para mostrar o anel da hitbox sob o corpo. Com vida zero, exatamente um quadrado fica aceso - o último. Qualquer perda de vida é mostrada ao longo de `{{v:avatar.health-loss-time}}` s, qualquer recuperação ao longo de `{{v:avatar.health-gain-time}}` s, sejam quantas vidas forem. Se você desativar `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics_avatar-render}}`, o corpo vira um único quadrado que desbota. Isso é para dispositivos fracos

Essa é a skin clássica. Uma skin pode mudar a grade, a forma de cada célula e as cores - [[16_skins]]

## Entrada e saída

O avatar cresce no nível ao longo de `{{v:avatar.spawn-time}}` s e encolhe até virar um ponto ao longo de `{{v:avatar.spawn-time}}` s ao morrer. Nos dois casos ele não responde aos comandos, e enquanto aparece não pode ser atingido

## Escala

Um nível pode animar o tamanho e a velocidade do avatar com faixas próprias. Ele também pode tirar o controle por um tempo ou desativar as colisões

- As velocidades de caminhada, de dash e de empurrão são multiplicadas por um mesmo número. Então, com metade da velocidade, o dash também tem metade do comprimento ({{v:avatar.half-speed-dash-distance}} unidades)
- Um avatar maior se move proporcionalmente mais rápido, porque as esquivas dele também cresceram. Tamanho aqui é o tamanho próprio do avatar, da faixa de tamanho do jogador. O zoom da câmera não muda nem a velocidade, nem as distâncias, nem as janelas: o avatar percorre {{v:avatar.move-speed}} unidades por segundo, faça a câmera o que fizer
- A hitbox é uma fração do corpo desenhado, então cresce e encolhe junto com o avatar
- A mira do dash usa a distância atual, não os 7.5 da tabela. Em um nível com metade da velocidade, um cursor a {{v:avatar.half-speed-dash-distance}} unidades já pede um dash completo, e o limiar de {{v:avatar.arrival-distance}} unidades vira {{v:avatar.half-speed-arrival-distance}}, porque o dash acima dele também tem metade do comprimento
- As janelas em segundos não mudam de escala: recarga, invulnerabilidade, imunidade após dano, aparecimento. Só o comprimento do próprio dash muda a escala das duas janelas dele

Os bots seguem as mesmas regras, [[9_bots]]
