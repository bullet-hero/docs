---
title: Avatar y movimiento
date: 2026-10-02
tags: [advanced_player]
---

# Avatar y movimiento

El avatar camina a {{v:avatar.move-speed}} unidades por segundo, y un dash lo lleva {{v:avatar.dash-distance}} unidades en {{v:avatar.dash-time}} s. El hitbox es un círculo de radio {{v:avatar.hitbox-radius}} unidades, más pequeño que el cuadrado dibujado de {{v:avatar.body-size}} unidades

Esta página es la fuente de verdad del avatar. El juego y los dos bots están hechos según estos números, y el SDK los registra como las constantes `AvatarRules`. Un código que no coincide con esta página es un error del código

Las distancias están en unidades del mundo. La cámara predeterminada mide exactamente {{v:camera.default-height}} unidades de alto (`ValueRules.DefaultZoom`), así que una unidad es una décima parte del alto de la pantalla, y el cuerpo del avatar mide media unidad de ancho.
El zoom de la cámara cambia cuánto ves, pero no los números de abajo

## Los números

| Qué | Valor | En palabras sencillas |
|---|---|---|
| Velocidad al caminar | `{{v:avatar.move-speed}}` u/s | cruza la pantalla de arriba abajo en dos tercios de segundo |
| Velocidad del dash | `{{v:avatar.dash-speed}}` u/s | {{v:avatar.dash-to-walk-ratio}} veces más rápido que caminar |
| Duración del dash | `{{v:avatar.dash-time}}` s | |
| Distancia del dash | `{{v:avatar.dash-distance}}` unidades | velocidad × duración, tres cuartas partes del alto de la pantalla |
| Recarga del dash | `{{v:avatar.dash-cooldown}}` s | se cuenta desde el inicio del dash |
| Invulnerabilidad del dash | `{{v:avatar.dash-invulnerability}}` s | también desde el inicio, así que dura {{v:avatar.dash-invulnerability-margin}} s más que el propio movimiento |
| Dash más corto | `{{v:avatar.arrival-distance}}` unidades | lo mismo que la distancia de llegada, más cerca ya estás sobre el objetivo |
| Velocidad del retroceso | `{{v:avatar.knockback-speed}}` u/s | {{v:avatar.knockback-to-walk-ratio}} veces más rápido que caminar, [[7_damage]] |
| Duración del retroceso | `{{v:avatar.knockback-time}}` s | sin control durante ese tiempo |
| Tiempo de inmunidad tras el daño | `{{v:avatar.damage-timeout}}` s | cualquier impacto posterior dentro de ese tiempo se ignora |
| Tamaño del cuerpo | `{{v:avatar.body-size}}` unidades | el cuadrado dibujado |
| Hitbox | radio `{{v:avatar.hitbox-radius}}` unidades | {{v:avatar.hitbox-scale}} del cuerpo, más pequeño a propósito que lo que ves |
| Aparición y desaparición | `{{v:avatar.spawn-time}}` s | crece y se encoge hasta un punto |
| Efecto del tamaño del jugador en la velocidad | total, `{{v:avatar.size-speed-influence}}` | un avatar más grande se mueve proporcionalmente más rápido. Es la pista de tamaño del jugador del nivel, no el zoom de la cámara |
| Velocidad de giro | `{{v:avatar.turn-speed}}` /s | estético: hacia dónde mira el cuerpo |
| Distancia de llegada | `{{v:avatar.arrival-distance}}` unidades | más cerca del cursor que esto cuenta como estar sobre él |

Derivados de ellos, y son los que deciden una esquiva:

| Qué | Valor |
|---|---|
| Dash más corto: distancia | `{{v:avatar.arrival-distance}}` unidades |
| Dash más corto: duración | bastante menos de un fotograma |
| Dash más corto: recarga e invulnerabilidad | bastante menos de un fotograma, cada una |
| Dashes más frecuentes | no más de uno cada dos fotogramas |
| Distancia del retroceso | `{{v:avatar.knockback-distance}}` unidades |

Qué pasa con un impacto - [[7_damage]]

## Moverse

Controlas el avatar de una de dos formas, y el juego nunca las mezcla:
- **Dirección**: WASD, un stick del gamepad, el giroscopio. El avatar se mueve hacia donde empujas, a la velocidad al caminar. Un stick inclinado a medias da la mitad de la velocidad, y no hay otro "paso lento"
- **Cursor**: el ratón o un dedo. El avatar persigue el punto en lugar de teletransportarse a él. Se mueve a su propia velocidad al caminar y se queda atrás con un ratón rápido

El movimiento es instantáneo en los dos casos: sin aceleración, deslizamiento ni inercia. Te detienes en el mismo fotograma en que dejas de moverte

## El dash

La invulnerabilidad dura {{v:avatar.dash-invulnerability-margin}} s más que el movimiento. Ese margen después de aterrizar es lo que permite hacer un dash *a través* de un obstáculo

Durante un dash sigues guiando. El dash va adonde pides: en la dirección mantenida o hacia el punto de mira, y puede cambiar a mitad del dash. Un dash sin ninguna dirección mantenida no se mueve a ningún sitio

Con un cursor, el dash va adonde apuntas y se detiene allí:

| Distancia al cursor | Qué pasa |
|---|---|
| más de {{v:avatar.dash-distance}} unidades | un dash completo hacia él. Te detienes antes de llegar al cursor |
| de {{v:avatar.arrival-distance}} a {{v:avatar.dash-distance}} unidades | un dash acortado que termina justo sobre el cursor |
| menos de {{v:avatar.arrival-distance}} unidades | no hay dash |

Un dash acortado es el mismo dash a menor escala. El recorrido, la invulnerabilidad y la recarga se reducen juntos: un dash de la mitad de largo protege la mitad de tiempo y se recarga el doble de rápido. Nunca sale más barato. Dos medios dashes cuestan exactamente lo mismo que un dash completo y cubren la misma distancia

Un dash que no ocurre no cuesta nada: la recarga no empieza, no se gasta nada. Un jugador en modo dirección que no mantiene nada recibe la misma respuesta: no hay dash

El cuerpo se vuelve de un azul más intenso durante el dash y luego recupera su color normal en los siguientes {{v:avatar.dash-tint-fade}} s. Nada más cambia el color del cuerpo, ni siquiera un impacto: un dash es tu propio movimiento, así que solo él lo hace

La estela del dash y ese azul dependen de la longitud del dash: un dash completo los muestra enteros, el más corto a `{{v:avatar.dash-effect-min}}` de eso, y todo lo intermedio en proporción. Un dash corto lanza sus partículas más despacio, así que la estela parece exactamente tan larga como el dash

### Dos estilos, un mismo presupuesto

- En el modo `{{ui:field_common_direction}}`, un dash siempre recorre las {{v:avatar.dash-distance}} unidades completas. Una distancia fiable sin apuntar, pero tampoco se puede parar a mitad de camino
- Con un cursor eliges la longitud y puedes detenerte justo en un punto. Un dash corto significa menos protección y un fotograma vulnerable más por dash. Apunta lejos y vuelve el dash completo

En línea recta los dos cubren la misma distancia en el mismo tiempo. Ningún estilo es más fuerte: uno da precisión, el otro sencillez

### Dash tras dash

**Un dash mantenido no es invulnerabilidad.** La recarga y la protección duran lo mismo, así que un botón mantenido da una cadena continua de dashes. Pero entre dos dashes siempre hay exactamente un fotograma en el que pueden alcanzarte, a cualquier frecuencia de fotogramas, en un teléfono lento igual que en un PC rápido.
La cadena más ajustada es un dash no más de una vez cada dos fotogramas

## El hitbox

El anillo de puntos del avatar se dibuja exactamente sobre el hitbox. ¿Una bala rozó el contorno y no hizo nada? Es intencionado

Mientras eres invulnerable (durante un dash o justo después de un impacto), no hay hitbox en absoluto

El mismo anillo muestra tus vidas: un punto encendido es una vida en reserva

La visibilidad del anillo se fija en `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_hitbox-ring-opacity}}`. `0` lo oculta, pero los niveles están equilibrados para quien lo ve

El cuerpo es una cuadrícula de {{v:avatar.grid-cells}} cuadrados, {{v:avatar.grid-side}} por 5. Al perder salud, los cuadrados del borde al centro no desaparecen, sino que se apagan: un cuadrado perdido se queda como un fantasma pálido, así que la cuadrícula siempre muestra los {{v:avatar.grid-cells}}, y la salud se lee por el número de los que siguen encendidos.
Los cuadrados fantasma son lo bastante transparentes para que se vea el anillo del hitbox bajo el cuerpo.
Con salud cero queda encendido exactamente un cuadrado, el último.
Cualquier pérdida de salud se muestra a lo largo de `{{v:avatar.health-loss-time}}` s, cualquier recuperación a lo largo de `{{v:avatar.health-gain-time}}` s, sean cuantas sean las vidas.
Si desactivas `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics_avatar-render}}`, el cuerpo se convierte en un solo cuadrado que se apaga. Esto es para dispositivos poco potentes

## Aparecer y desaparecer

El avatar crece dentro del nivel a lo largo de `{{v:avatar.spawn-time}}` s y se encoge hasta un punto a lo largo de `{{v:avatar.spawn-time}}` s al morir. En los dos casos no responde a la entrada, y mientras aparece no pueden alcanzarlo

## Escalado

Un nivel puede animar el tamaño y la velocidad del avatar con sus propias pistas. También puede quitarte el control durante un rato o desactivar las colisiones

- Las velocidades al caminar, del dash y del retroceso se multiplican por un mismo número. Así, a media velocidad el dash también mide la mitad ({{v:avatar.half-speed-dash-distance}} unidades)
- Un avatar más grande se mueve proporcionalmente más rápido, porque sus esquivas también crecieron. El tamaño aquí es el tamaño propio del avatar, de la pista de tamaño del jugador. El zoom de la cámara no cambia ni la velocidad, ni las distancias, ni las ventanas de tiempo: el avatar recorre {{v:avatar.move-speed}} unidades por segundo haga lo que haga la cámara
- El hitbox es una fracción del cuerpo dibujado, así que crece y se encoge con el avatar
- La puntería del dash usa la distancia actual, no los 7.5 de la tabla. En un nivel a media velocidad, un cursor a {{v:avatar.half-speed-dash-distance}} unidades ya pide un dash completo, y el umbral de {{v:avatar.arrival-distance}} unidades pasa a ser {{v:avatar.half-speed-arrival-distance}}, porque el dash por encima de él también mide la mitad
- Las ventanas en segundos no se escalan: recarga, invulnerabilidad, inmunidad tras el daño, aparición. Solo la longitud del propio dash escala sus dos ventanas propias

Los bots siguen las mismas reglas, [[9_bots]]
