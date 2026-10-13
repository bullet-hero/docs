---
title: Bots
date: 2026-10-02
tags: [player, advanced_player]
---

# Bots

Un bot juega un nivel por ti con tus mismos controles. Observa lo que viene, busca espacio libre y mueve el mismo personaje que tú: camina, hace dashes, recibe daño y muere

**Un bot no garantiza completar el nivel.** No se cansa, pero puede perder. Si a un patrón hay que entrar bien un segundo antes de que llegue, el bot recibe el impacto. Cuando pasa eso, no hay nada roto

**Un bot carga el dispositivo.** Buscar espacio libre es trabajo real en cada fotograma. En un dispositivo poco potente, cuenta con caídas de fotogramas. En un nivel pesado, los primeros segundos son los peores

Para elegir un bot, usa la condición `{{ui:menu_levelview_options-bot}}` en la pantalla del nivel: `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}` o `{{ui:enum_bot-kind_warm}}`. Se elige en cada partida, como las vidas y la velocidad

> [!info] Conviene saber
> Un bot no puede hacer trampas, y eso es cómo está construido, no una promesa. Tiene los mismos controles que tú y nada más: la misma velocidad, el mismo dash, el mismo hitbox, el mismo daño. No puede atravesar nada que tú no pudieras atravesar

## ¿Un nivel ha vencido al bot?

Los bots mejoran con los niveles que todavía no han visto. Vale la pena enviar un nivel así

Abre una issue en [bullet-hero/releases](https://github.com/bullet-hero/releases/issues). Escribe qué bot perdió y dónde, y adjunta la carpeta del nivel

## Dos bots

En cada fotograma un bot da una entrada, igual que un teclado, y nada más. No tiene acceso a la posición del avatar, a su salud ni al estado del nivel.
Si el bot no responde en algún fotograma, en ese fotograma guía tu dispositivo

| | `{{ui:enum_bot-kind_reflex}}` | `{{ui:enum_bot-kind_warm}}` |
|---|---|---|
| Qué sabe | los próximos 1.5 segundos, recalculados en cada fotograma | todo el nivel, calculado una vez |
| Cuándo carga el dispositivo | en cada fotograma mientras juega | una vez, antes de la partida |
| Qué puede hacer | evitar lo que ve por delante | seguir un plan que ninguna previsión encontraría nunca |
| Qué lo hace fallar | un patrón al que había que entrar un segundo antes | un nivel que cambió después de calcular el plan |
| Cómo guía | por dirección | por objetivo |

El bot Warm busca recibir cero daño. Lo paga con una etapa de carga extra, `{{ui:root_loading_baking}}`. Puede durar decenas de segundos

El `?` junto a `{{ui:menu_levelview_options-bot}}` lo avisa de antemano, con un párrafo por bot. `{{ui:root_loading_cancel}}` detiene el cálculo y te deja la partida a ti.
La ruta del bot Warm depende de la semilla, [[8_determinism]]

## Dónde más juegan los bots

- **El jugador de prueba del editor**: `{{ui:settings_common_title}}` → `{{ui:settings_game-editor_title}}` → `{{ui:settings_game-editor-player_bot}}`. Allí solo juega el bot Reflex: no necesita nada preparado de antemano y sobrevive al rebobinado. Más - [[5_bot-playtest]]
- **El fondo del menú principal**: la arena detrás de los botones es un bot Reflex que juega en vivo sin ninguna previsión

El bot forma parte de las condiciones de un récord. Por eso la partida de un bot nunca sustituye tu mejor resultado, [[10_statistics]]
