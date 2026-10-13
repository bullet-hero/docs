---
title: Preparación para publicar
date: 2026-10-02
tags: [level_author]
---

# Preparación para publicar

Cada servicio comprueba un nivel con sus propias reglas, así que uno puede aceptarlo y otro rechazarlo. Solo un error bloquea la publicación, una advertencia envía el nivel a moderación

La comprobación se ejecuta sola en la pestaña `{{ui:settings_level-settings_publication}}` de la configuración del nivel, en cualquier compilación. El destino elige el perfil: `{{ui:editor_share_archive}}` se comprueba con `{{ui:editor_publish_profile-local}}`, el más permisivo, y `{{ui:editor_share_steam}}` con el perfil del Workshop. El perfil estándar es el de un servidor público, y el perfil de la compilación para tiendas no se ofrece en el juego, sus límites están más abajo. Más - [[17_publishing]]

## Tres veredictos

| Veredicto | Qué pasa |
|---|---|
| **`Error`** | el servicio lo rechaza, la subida se bloquea antes de empezar |
| **`Warning`** | se puede publicar, pero una persona revisará el nivel. El servidor lo pone en la cola de moderación |
| **`Advice`** | una nota, no bloquea nada |

Un nivel que se queda en tu dispositivo no se evalúa con nada

## El perfil del Workshop

De momento es más permisivo que el estándar, porque la política de licencias todavía se va a reescribir:
- pasa cualquier licencia CC BY, 3.0 y 4.0: BY, BY-SA, BY-NC, BY-NC-SA, BY-ND, BY-NC-ND. También CC0, SIL OFL, MIT, Apache y Unlicense
- se siguen rechazando: todos los derechos reservados, las licencias de la familia GPL y un texto de licencia propio
- solo una advertencia: sin licencia indicada, un recurso sin registro, sin enlace a la página de origen
- la clasificación por edad y los autores del nivel no son obligatorios
- los límites de tamaño son los mismos que en el perfil estándar

> [!caution] Precaución
> La música CC BY-ND se acepta, pero según CC 4.0 la música sincronizada con una imagen en movimiento siempre cuenta como adaptación, y ND prohíbe distribuir adaptaciones. Un nivel montado sobre una canción ND puede retirarse a petición del titular de los derechos. Mejor elige otra canción

## Qué da un error

En el perfil estándar:
- la licencia propia del nivel no se acepta
- no hay clasificación por edad
- no se cita a nadie como autor del nivel
- un recurso no tiene registro
- la licencia de un recurso se rechaza o no está indicada
- un recurso se obtiene de una forma que el servicio no acepta
- un recurso se toma de un sitio no permitido
- algo supera los límites de tamaño

## Qué da una advertencia

- un recurso no tiene enlace a su página de origen. Una obra que hiciste tú no tiene esa página, así que esto nunca bloquea
- un permiso sin alcance o sin prueba
- un permiso caducado
- un sitio con más de un tipo de condiciones

## Qué da una sugerencia

- el registro de un recurso que el nivel ya no tiene

## Por qué y qué hacer

Cada línea del informe nombra su recurso: por el nombre del archivo o por el nombre que le diste. El `?` al final de la línea despliega los detalles: qué licencia tiene el recurso, cuáles acepta el servicio en su lugar, cuánto pesa frente al límite y dónde corregirlo

## Límites de tamaño

| Límite | Perfil estándar | Compilación para tiendas |
|---|---|---|
| Por recurso | `{{v:publish.standard.max-resource-mb}} MB` | `{{v:publish.strict.max-resource-mb}} MB` |
| Por archivo de datos | `{{v:publish.standard.max-data-file-mb}} MB` | `{{v:publish.strict.max-data-file-mb}} MB` |
| Por nivel | `{{v:publish.standard.max-level-mb}} MB` | `{{v:publish.strict.max-level-mb}} MB` |

Una compilación para tiendas además exige atribución y hashes, y rechaza los enlaces arbitrarios.
Los tamaños menores no son una opinión más estricta. Son lo que un teléfono puede descargar de verdad por una red móvil

## Un informe limpio

> [!caution] Precaución
> Un informe limpio solo con los metadatos no significa "preparado". Dos comprobaciones necesitan el propio archivo del nivel: un recurso sin registro y de dónde se obtiene un recurso. Pasar solo con los metadatos significa "no hay nada mal en lo que se leyó"

## Por qué los servicios evalúan distinto

Las reglas de un servicio son un archivo de datos, no código.
Cada servicio hace la misma docena de preguntas y las responde a su manera:
- qué licencias son aceptables
- cómo se pueden obtener los recursos
- si se tolera una licencia desconocida
- qué hay que rellenar
- qué tamaño puede tener un nivel

Un servicio lleva sus propias respuestas, otro las sustituye. Por eso el mismo nivel puede estar preparado para un servicio y ser rechazado por otro

> [!info] Conviene saber
> La misma comprobación se ejecuta tanto automáticamente en tu equipo como en la moderación manual del servidor. Un cliente sin red sigue evaluando bien un nivel, porque las reglas con las que se compiló viajan con él

A continuación: [[4_resource-record]], [[2_metadata-and-sharing]]
