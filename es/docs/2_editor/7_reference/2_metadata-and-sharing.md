---
title: Metadatos y cómo compartir un nivel
date: 2026-10-15
tags: [level_author]
---

# Metadatos y cómo compartir un nivel

Los metadatos son la portada del nivel: nombre, descripción, imagen, autores, clasificación por edad, dificultad y avisos sobre el contenido. Hoy un nivel llega a otra persona como carpeta o a través del Workshop de Steam

> [!warning] Advertencia
> El servidor oficial y el sitio para niveles todavía no existen. Llegan en una actualización posterior a `gv 1.0.0`. Hasta entonces un nivel se comparte como carpeta o, en una build de Steam, a través del Workshop de Steam. Las dos formas se describen al final de la página

## El archivo de metadatos

La portada del nivel vive en su propio archivo. Se lee sin el nivel en sí.
Así un catálogo puede mostrar mil niveles sin abrir ninguno

## Identidad

El nivel tiene un ID estable. Sobrevive a los cambios de nombre y a los traslados de carpeta.
Las puntuaciones y los comentarios se vinculan a él, no al nombre

También hay un número de versión propio del nivel. Súbelo cuando edites. No tiene relación con la versión del formato

## Nombre, descripción y portada

**El nombre y la descripción** se pueden traducir a varios idiomas. No tienen claves: escribes el texto de cada idioma ahí mismo.
El texto se guarda dentro del nivel. En eso se diferencia del texto de la propia interfaz del juego

**La portada** es un archivo junto al nivel, `logo.png` o `logo.jpg`

La portada tiene su propia ficha, como un recurso: licencia, autores, enlace, generación con IA. Se abre con el botón `{{ui:settings_level-settings_metadata-level-logo-metadata}}` bajo la portada.
Una imagen nueva empieza la ficha de cero, y quitar la portada quita también su ficha. Más - [[4_resource-record]]

## Autores

**Los autores** son quienes hicieron el nivel: la colocación, el diseño.
Los autores de los recursos se acreditan por separado, en la ficha de cada recurso.
Tienen ficha las texturas, las fuentes y el audio, y también los temas, los efectos, las formas y los prefabs

> [!caution] Precaución
> Si confundes estas dos listas, el músico se queda sin crédito

## Clasificación por edad

**La clasificación por edad** es un solo número, la edad mínima. Se muestra como "12+". Dos clasificaciones se comparan como números normales

`{{ui:enum_age-rating_unrated}}` es cero. Significa que no se declaró nada, no que el contenido sea seguro

> [!info] Conviene saber
> Hay una sola escala, sin campos separados para ESRB, PEGI y RARS. Los niveles de usuarios no se envían a ningún organismo de clasificación, así que un valor para cada uno sería una suposición

> [!caution] Precaución
> La clasificación es el único aviso de la tarjeta. Si el nivel parpadea o suena fuerte, dilo en la descripción. En un juego de drops y efectos glitch los parpadeos son habituales, y esa línea es todo el aviso que recibe el jugador

## Dificultad

**La dificultad** es un solo número entero: lo difícil que es el nivel. Un número mayor nunca es más fácil

`1` es `{{ui:enum_difficulty-tier_auto}}`, y cada número siguiente es el grado siguiente, hasta `{{v:difficulty.scale-max}}`, `{{ui:enum_difficulty-tier_singularity}}`. El jugador ve solo el nombre del grado y su icono, nunca el número

`{{ui:enum_difficulty-tier_undefined}}` es cero o menos. Es el valor por defecto, y no se dibuja nada para él. Un archivo de metadatos sin dificultad se abre como `{{ui:enum_difficulty-tier_undefined}}`

El valor lo fijas tú, y un moderador que vuelve a publicar el nivel puede sobrescribirlo. Sigue siendo un solo campo: el nivel no guarda el valor del autor y el del moderador por separado

Un valor mayor que `{{v:difficulty.scale-max}}` se guarda tal como está escrito y se muestra como `{{ui:enum_difficulty-tier_singularity}}`. El editor lo cambia solo cuando eliges otro grado.
Por ahora la escala termina ahí. La siguiente se construirá a partir de los niveles que la gente realmente haga

En el archivo de metadatos el campo se llama `difficulty`

Más - [[2_playing-levels#Dificultad]]

## Generación con IA

**`Generación con IA`** indica si el contenido propio del nivel lo generó una IA: el diseño, los objetos, los textos.
Cada recurso y la portada lo indican por sí mismos, en sus propias fichas

| Valor | Significado |
|---|---|
| `{{ui:enum_ai-generation_not-specified}}` | no se declaró nada. Es el valor predeterminado |
| `{{ui:enum_ai-generation_no}}` | declaras que no se usó generación con IA |
| `Generado por IA` | declaras que el contenido lo generó una IA |

`{{ui:enum_ai-generation_not-specified}}` significa "desconocido". No es lo mismo que "no"

La pantalla del nivel en el menú muestra "Incluye contenido generado por IA" si el nivel, su portada o cualquier recurso dice `Generado por IA`

Un asistente de IA pone `{{ui:enum_ai-generation_yes}}` por sí mismo, en el mismo paso de deshacer que su primer lote de cambios en el nivel. Más - [[7_ai-assistant]]

> [!info] Conviene saber
> Igual que la clasificación por edad, es una declaración del propio autor. El juego no la comprueba

## Cómo compartir un nivel hoy

1. Comprime la carpeta del nivel en un zip y envíala
2. La otra persona la descomprime en su propia carpeta `levels`
3. El nivel se abre. No se instala ni se importa nada

> [!warning] Advertencia
> Cada archivo de la carpeta del nivel viaja con ella, incluso uno que no se usa. Límpiala antes de enviarla

## Workshop de Steam

La pestaña `{{ui:settings_level-settings_publication}}` de la configuración del nivel envía el nivel: como archivo comprimido y, en una build de Steam, al Workshop de Steam. Más - [[17_publishing]]

Las builds de Steam también leen el Workshop: muestran los niveles a los que te suscribiste y permiten jugarlos. Más - [[2_playing-levels]]

Antes de publicar, lee [[1_licensing-basics|la sección sobre derechos]]. El informe de la pestaña `{{ui:settings_level-settings_publication}}` evalúa el nivel y la ficha de cada recurso según esas reglas

## Cómo compartir un nivel más adelante

Hay planes para un servidor y un sitio oficiales

Siguiente: [[4_resource-record|La ficha de un recurso]], [[4_level-folder-and-backups|La carpeta del nivel y las copias de seguridad]]
