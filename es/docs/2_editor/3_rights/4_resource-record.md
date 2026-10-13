---
title: El registro del recurso
date: 2026-10-02
tags: [level_author]
---

# El registro del recurso

El registro anota de dónde viene un recurso y en qué condiciones: el enlace, la licencia, los permisos, los autores. Un campo de licencia vacío significa "nadie lo comprobó", y ese recurso se rechaza

> [!tip] Recomendación
> Rellena el registro en cuanto añadas el recurso. Es el único momento en que todavía recuerdas de dónde salió

## Qué contiene el registro

Cada recurso tuyo en un nivel tiene su propio registro. Se guarda dentro del nivel y viaja con él.
Así la atribución no se pierde: vaya donde vaya el nivel, el archivo lleva consigo de dónde viene y en qué condiciones

Los campos del registro:
- **Título** y **descripción** de la obra original, ambos se pueden traducir a otros idiomas
- **Url** - la página de la obra: la publicación o la página del autor, una página de tienda
- **Licencia** - las condiciones en que se distribuye la obra
- **Permisos** - [[2_legal-resource-paths|opción B]], una entrada por titular de derechos, con alcance, fechas y prueba
- **Autores** - todas las personas a las que hay que citar por este recurso, aparte de los autores del propio nivel
- **Orígenes** - texto libre sobre la procedencia, para lo que un enlace no puede expresar
- **Hashes** - las sumas de comprobación del contenido de los archivos del recurso
- **Generación con IA** - si la obra la generó una IA: `{{ui:enum_ai-generation_not-specified}}`, `{{ui:enum_ai-generation_no}}` o `{{ui:enum_ai-generation_yes}}`

**El enlace apunta a la página con las condiciones, no a una descarga directa.** Un moderador necesita la página, no el archivo

## Un campo vacío significa "desconocido"

> [!caution] Precaución
> Un campo de licencia vacío es `NoSpecifiedLicense`, y ese recurso se rechaza. No significa "las condiciones están bien". Significa "nadie lo comprobó"

Todo el modelo funciona así: un valor vacío significa "no se declaró nada", no "todo está permitido".
Una clasificación por edad `Unrated`, un alcance de permiso `Undefined` y una generación con IA `{{ui:enum_ai-generation_not-specified}}` funcionan igual

`NoSpecifiedLicense` puede indicar además de dónde se sacó el archivo: YouTube, SoundCloud, Spotify.
El veredicto no cambia por eso. El moderador simplemente ve qué conversación le espera

## Hashes

Rellena los hashes desde el primer día, incluso donde no se exigen.
La reclamación de un titular de derechos nombra una obra. Para responderla, hay que encontrar todos los niveles que tienen esa obra.
Por el nombre es adivinar, por el hash es una búsqueda exacta

## Registros obsoletos

El registro de un recurso que el nivel ya no tiene da una sugerencia, no un error.
No bloquea nada, pero aun así conviene eliminarlo

## Un recurso en la tarjeta del nivel

El registro de un recurso se puede marcar para que aparezca en la tarjeta del nivel. Está pensado para la música.
Entonces bajo los autores del nivel aparece una línea con ese recurso. Todo lo demás queda en los créditos completos

## El registro de la portada

La portada del nivel también tiene registro. La portada no es un recurso del nivel, así que su registro se abre junto a la portada en la pestaña de metadatos, con el botón `{{ui:settings_level-settings_metadata-level-logo-metadata}}`

- Una imagen nueva empieza el registro de cero, y solo contiene el hash del archivo. Otra imagen es otra obra, y se citaría mal a los autores anteriores
- El mismo archivo elegido de nuevo deja el registro como está
- Quitar la portada quita también su registro. Deshacer recupera ambos

Un recurso o una portada con `{{ui:enum_ai-generation_yes}}` hace que la pantalla del nivel muestre la línea "Incluye contenido generado por IA"

A continuación: [[5_publish-readiness]], [[2_metadata-and-sharing]]
