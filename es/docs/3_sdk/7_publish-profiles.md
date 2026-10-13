---
title: Perfiles de publicación
date: 2026-10-01
tags: [developer, level_author]
---

# Perfiles de publicación

Un servicio describe qué niveles acepta con un archivo PublishProfile: licencias, orígenes de los recursos, campos obligatorios, límites de tamaño. Añadir un servicio significa escribir un archivo, no editar el analizador

## Un perfil son datos

Un perfil de publicación (`PublishProfile`) es un modelo que se serializa como cualquier otra raíz, con su propia generación

Un nivel puede ir a Steam Workshop, al servidor oficial, a un servidor de la comunidad o al catálogo de una compilación para tiendas. Cada lugar responde a las mismas preguntas a su manera. Las respuestas cambian con los años, y el código no

Lo que decide un perfil:

| Campo | Significado |
|---|---|
| `ProfileKey` | qué servicio es, se repite en cada informe |
| `AllowedLicenses` | los valores de `TypicalLicenseType` que acepta el servicio |
| `AllowedUriTypes` | cómo se pueden obtener los recursos. Una lista vacía significa de cualquier forma |
| `AllowUnknownLicense`, `AllowPermissionInstead` | si basta con una licencia desconocida o con un permiso por escrito |
| `RequireResourceMeta`, `RequireResourceUrl`, `RequireAttribution`, `RequireAgeRating`, `RequireLevelAuthors`, `RequireHashes` | qué hay que rellenar |
| `MaxResourceBytes`, `MaxDataFileBytes`, `MaxTotalBytes` | límites de tamaño, 0 significa sin límite |
| `Sources`, `UnknownSourceTrust` | una lista de sitios y la valoración para un sitio que no está en ella |

Qué licencias son aceptables lo decide solo el perfil. Parece una propiedad de la licencia, pero en realidad es una propiedad del servicio que recibe el nivel

## Cuatro perfiles integrados

| Fábrica | `ProfileKey` | Para qué |
|---|---|---|
| `CreateOpen()` | `local` | un nivel en tu dispositivo. No se exige nada |
| `CreateStandard()` | `standard` | un servidor público |
| `CreateWorkshop()` | `workshop` | Steam Workshop. Pasa cualquier variante de CC BY, y la falta de documentos solo genera advertencias |
| `CreateStrict()` | `strict` | una compilación para tiendas, más estricta que `standard` |

| Qué | `standard` | `strict` |
|---|---|---|
| licencias | CC0 1.0, CC BY 4.0 y 3.0, CC BY-NC 4.0 y 3.0, SIL OFL 1.1, MIT, Apache 2.0, the Unlicense | como en `standard` |
| de dónde vienen los recursos | de la carpeta del nivel, del juego o por enlace directo | sin enlaces |
| atribución y hashes | - | obligatorios |
| límite por recurso | 64 MiB | 32 MiB |
| límite por archivo de datos | 32 MiB | 16 MiB |
| límite por nivel | 256 MiB | 128 MiB |

> [!tip] Recomendación
> No añadas una fábrica para tu servicio. Toma uno de los cuatro perfiles, cambia los campos que necesites y distribúyelo como archivo JSON

### Por qué estas licencias y tamaños

- las licencias de la familia GPL están excluidas de `standard`. Una obra GPL distribuida a través de la App Store entra en conflicto con las condiciones de Apple
- CC BY-SA está excluida: ShareAlike obligaría a cambiar la licencia del propio nivel
- CC BY-ND está excluida: NoDerivatives prohíbe la edición sobre la que se construye el juego
- los tamaños estrictos son lo que un teléfono puede descargar por una red móvil

## De dónde vino un recurso

El campo de licencia dice lo que afirma el autor. `SourceTrust` dice cuánto vale esa afirmación según el sitio del que vino el recurso:

| Valoración | Resultado | Ejemplos |
|---|---|---|
| `Approved` | publicar | Kenney, ccMixter, Incompetech |
| `PartiallyApproved` | publicar, conviene revisar el registro | Pixabay, SoundImage |
| `RequiresLicenseCheck` | contrastar la licencia con la página real | OpenGameArt, Free Music Archive, Wikimedia Commons |
| `RequiresResourceCheck` | identificar primero la propia obra | Rawpixel, itch.io |
| `NotAllowed` | rechazar | YouTube, SoundCloud, Spotify |
| `Unknown` | no hay registro, decide `UnknownSourceTrust` | - |

`TrustedSourceCatalog.CreateDefault()` devuelve 25 sitios. Es una lista de partida. Se espera que cada operador la cambie. Por eso nada puede dar por hecho que un registro esté ahí

Una lista `Sources` vacía desactiva la valoración de orígenes

Las plataformas de streaming figuran como `NotAllowed` en lugar de quedar fuera de la lista. Un sitio ausente se valora mediante `UnknownSourceTrust`, y en `standard` y `strict` esa valoración pide una comprobación en lugar de rechazar

El catálogo y [[ugc-licensing-policy]] describen lo mismo y se editan juntos

## Qué hacer con la respuesta

La llamada es `ValidationFacade.ValidateForPublish`. Más - [[6_validation]]

`PublishReadinessReport` tiene:
- `HasErrors` - incidencias del grupo `Error`
- `NeedsManualReview` - incidencias del grupo `Warning`
- `IsReady`

El perfil no decide qué pasa después. El cliente bloquea la subida si hay errores. El servidor pone el nivel en una cola de revisión en lugar de publicarlo

La misma comprobación desde el lado del autor - [[5_publish-readiness]]
