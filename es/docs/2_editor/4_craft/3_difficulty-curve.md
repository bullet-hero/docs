---
title: La dificultad y la curva
date: 2026-10-02
tags: [level_author]
---

# La dificultad y la curva

Diseña según los números del propio jugador - todos están en [[6_avatar]] y [[7_damage]] - y una reacción humana de 12-15 fotogramas. Muestra primero cada patrón nuevo en una forma segura

No puedes juzgar tu propia dificultad: prueba el nivel con alguien que lo vea por primera vez

## El jugador en números

Los valores exactos del avatar están en [[6_avatar]] y [[7_damage]]. Lo que significan para un nivel:

| Qué | Qué significa para el diseño |
|---|---|
| Hitbox del jugador | mucho menor que el cuerpo dibujado, así que una bala que roza el cuerpo a menudo no impacta |
| Dash | cruza tres cuartos de la altura de la pantalla casi al instante |
| Invulnerabilidad durante el dash | dura más que el propio dash, así que un dash a través de un obstáculo fino es seguro |
| Tras un impacto | un breve retroceso sin control, y luego una ventana de gracia que ignora los impactos siguientes |
| Reacción humana | 0.2-0.25 segundos, es decir, 12-15 fotogramas a 60 fps |
| Valores al iniciar | 3 vidas, velocidad 1.0, checkpoints activados |

Reglas prácticas que se deducen:
- un hueco de una unidad de ancho es amplio, un hueco de 0.6 es estrecho
- un dash cubre tanto terreno como medio segundo de carrera

## Un impacto no mata de inmediato

Tras un impacto, el jugador sale despedido hacia atrás y durante un momento no tiene control.
Durante un tiempo después se ignoran los impactos siguientes ([[7_damage]]). Un muro de diez proyectiles seguidos cuesta una vida, no diez

> [!info] Conviene saber
> La intuición dice lo contrario. Una ráfaga densa parece una muerte instantánea. En realidad cuesta menos que un solo proyectil que llega justo cuando se acabó la invulnerabilidad

## Lo que elige el jugador

Las vidas, la velocidad de reproducción y los checkpoints los elige el jugador en la pantalla de inicio.
Los valores predeterminados son 3 vidas, velocidad 1.0, checkpoints activados

Puedes colocar checkpoints, pero no puedes obligar a nadie a usarlos. Y no puedes prohibir jugar a media velocidad

Diseña según los valores predeterminados, pero no construyas nada sobre el cálculo "aquí es donde muere".
Estás diseñando una sensación, no un castigo

## El bucle

El jugador repite un único bucle: jugar, morir, volver a intentarlo. Un buen nivel construye todo lo demás encima de él, y el bucle tiene que ser:
- sencillo al principio, sin mecánicas difíciles de entrada
- ampliable, para que los elementos nuevos lleguen poco a poco y no se vuelva repetitivo
- gratificante, porque una recompensa inmediata por la acción correcta mantiene la motivación

## La curva: enseñar, poner a prueba, dar un giro

1. Muestra el patrón en una forma segura donde equivocarse es casi imposible
2. Exígelo de verdad
3. Cambia una variable - velocidad, dirección, cantidad - y vuelve a exigirlo

Si un patrón aparece por primera vez directamente en su forma difícil, la culpa es del nivel.
El jugador muere y no entiende qué se esperaba de él

La justicia también tiene un límite. Llevar al jugador "de la mano" en exceso quita la diversión igual que la injusticia

## Memorización

Un nivel que solo se puede superar de memoria es un género legítimo. Pero tiene que ser una decisión, no un accidente

El límite es sencillo: tras morir, el jugador tiene que entender qué exactamente debe recordar.
Si sigue sin estar claro tras la décima muerte, no es memorización, es ruido

## Probar con otros ojos

No puedes juzgar tu propio nivel.
Para cuando publicas, has superado tu propio punto difícil doscientas veces, y para ti es fácil

> [!tip] Recomendación
> Dale el nivel a alguien que lo vea por primera vez y observa en silencio. No des indicaciones. Un punto donde alguien muere tres veces y pregunta qué se esperaba no es difícil, es confuso

## Empieza por algo corto

Haz que el primer nivel dure 1-2 minutos.
El interés se acaba antes que la canción. Un nivel de cuatro minutos es cuatro veces más trabajo y diez veces más motivos para dejarlo

A continuación: [[1_readability-and-fairness|Legibilidad y justicia]], [[4_composition-and-camera|Composición y cámara]]
