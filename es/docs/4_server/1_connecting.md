---
title: Conectarse a un servidor
date: 2026-10-01
tags: [player]
---

# Conectarse a un servidor

El juego tendrá el servidor oficial OWS para todas las compilaciones y servidores comunitarios NOWS solo para la compilación completa. Bullet Hero no modera los servidores comunitarios, así que conéctate a aquellos cuyo dueño conozcas

> [!warning] Advertencia
> Todavía no hay servidores, y el juego no sabe conectarse a ellos. No hay formato de dirección, ni pantalla de conexión, ni cuentas

## Qué servidores habrá

| | OWS | NOWS |
|---|---|---|
| Nombre completo | Official Web Services | Non-official web services |
| Quién lo pone en marcha | Bullet Hero | cualquiera |
| Quién lo modera | Bullet Hero | el dueño del servidor |
| Qué compilaciones se conectan | todas | solo la compilación completa |

**OWS es el servidor predeterminado.** Lo conoce cada compilación del juego en todas las plataformas, no hace falta configurar nada

**NOWS son los servidores comunitarios.** Bullet Hero no los controla ni los modera

**El Workshop de Steam es un tercer canal para niveles en PC.** Las compilaciones de Steam muestran y abren los artículos a los que te suscribiste, y publican allí niveles y colecciones desde el editor - [[17_publishing]]

## Qué compilaciones se conectan

| Compilación | De dónde | OWS | NOWS |
|---|---|---|---|
| Compilación de tienda | Google Play, App Store | sí | no |
| Compilación completa | [GitHub](https://github.com/bullet-hero/releases) y el sitio web del proyecto | sí | sí |

Una compilación de tienda no puede conectarse a un servidor comunitario de ninguna manera.
La compatibilidad con NOWS se elimina de ella al compilar, no se esconde detrás de una opción de configuración

El motivo son las reglas de las tiendas. Una tienda juzga lo que un programa puede hacer, no qué botones muestra. Y el contenido que ven otras personas tiene que estar moderado según sus reglas

Está previsto dar a la compilación completa su propio identificador de aplicación, para que en Android pueda instalarse junto a la versión de la tienda. Ahora mismo todas las compilaciones de Android comparten un identificador, `com.vertoker.BulletHero`

## Qué tendrá OWS

- cuentas y condiciones de uso
- una revisión de cada nivel antes de publicarlo: un nivel con un error se rechaza, un nivel con una advertencia pasa a un moderador
- denuncias de niveles y usuarios, y su bloqueo

Todavía no está decidido qué guarda una cuenta. El servidor tendrá su propia política de privacidad, que aparecerá junto con el servidor. Describirá la cuenta y explicará cómo eliminarla. Las políticas del juego y del sitio no cubren el servidor - [[game-privacy-policy]], [[privacy-policy]]

## Cuándo

La publicación en el Workshop de Steam ya funciona en las compilaciones de Steam. Para lo demás no hay fechas. El orden es: OWS, después la compilación de Google Play, después la de App Store

Todavía no se puede jugar en compañía en un servidor, no está diseñado

## Riesgos de los servidores ajenos

Un servidor comunitario lo pone en marcha una persona que muy probablemente no conoces.
Bullet Hero no controla ni modera esos servidores. El EULA de la compilación completa lo dice directamente

| Riesgo | Por qué |
|---|---|
| Niveles con derechos sin comprobar | el dueño decide qué comprobar y puede no comprobar nada. Un nivel puede contener música que su autor no tenía derecho a compartir |
| Nadie modera el contenido | no hay garantía de que alguien mire lo que se sube |
| Archivos de otros sitios | la política estándar permite que un nivel obtenga un archivo por un enlace directo. Al abrir un nivel así, el juego descarga el archivo de un sitio que eligió el autor del nivel. Por eso las compilaciones de tienda lo prohíben |
| El dueño ve tu tráfico | todavía no hay protocolo, así que no se sabe qué recibirá exactamente el servidor. Cuenta con que el dueño ve todo lo que envías |
| El servidor puede desaparecer | un nivel que solo existe en ese servidor desaparece con él |

De forma predeterminada un nivel se distribuye bajo *CC BY-NC*, y el autor puede elegir otra licencia en los metadatos del nivel. Un servidor tiene que respetar la licencia de cada nivel. Bajo *CC BY-NC* nadie puede alojar un nivel con fines comerciales, tampoco un servidor comunitario, y un servidor que cobra por esos niveles infringe la licencia de cada uno de sus autores

> [!tip] Recomendación
> Conéctate solo a servidores cuyo dueño conozcas. Guarda tu propia copia de cada nivel que te importe: un nivel es una carpeta de archivos, y la copia en tu disco no depende de ningún servidor

## EULA

La compilación completa incluye un EULA. Dice: los servidores comunitarios son servicios de terceros, Bullet Hero no los controla ni los modera

Las compilaciones de tienda pedirán aceptar un EULA antes de publicar un nivel

Ninguno de estos textos está escrito todavía

## Qué leer después

- [[ugc-licensing-policy]] - qué reglas debe cumplir un nivel para publicarse
- [[2_hosting]] - si quieres poner en marcha un servidor por tu cuenta
