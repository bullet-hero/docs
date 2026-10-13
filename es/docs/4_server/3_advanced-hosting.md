---
title: Servidor público y cómo ampliarlo
date: 2026-10-02
tags: [server_advanced]
---

# Servidor público y cómo ampliarlo

Para un servidor público ya existe el SDK abierto: los mismos modelos y comprobaciones que en el cliente, compilados sin Unity. El protocolo, la API del servidor y las herramientas de moderación todavía no están decididos

> [!warning] Advertencia
> Todavía no hay código de servidor ni protocolo. Abajo está la parte del SDK con la que funcionará el servidor, y esa parte ya funciona. Las direcciones, el formato de los mensajes y la API del propio servidor no están aquí, porque no existen

## El SDK funciona en un servidor

El SDK es el modelo de datos abierto del juego: modelos, serialización a JSON y a un formato binario, reglas de validación, generadores.
Las mismas fuentes que compila Unity se compilan como una biblioteca `netstandard2.1` normal, sin el motor. Un servidor o una utilidad pueden referenciarla:

```bash
dotnet build -c Release BH.SDK.csproj
dotnet pack  -c Release BH.SDK.csproj
```

El paquete se llama `BulletHero.SDK`. El código está en [github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk), bajo MIT

La versión del SDK suele coincidir con la del juego y todavía no promete una API estable. Más - [[5_versioning]]

**El cliente y el servidor ejecutan las mismas comprobaciones sobre los mismos modelos.** Un nivel que el editor considera listo también lo está para el servidor. No hay un segundo conjunto de reglas que mantener de acuerdo

## ValidateForPublish

Una sola llamada responde a la pregunta "¿se puede publicar este nivel aquí?":

```csharp
new ValidationFacade().ValidateForPublish(meta, profile, level, now, payload)
```

Hace tres pasadas a la vez:

1. reglas declarativas sobre el nivel y sus metadatos
2. comprobaciones del grafo del nivel
3. las condiciones propias del servicio, de su `PublishProfile`

**Pasar el propio nivel es opcional.** `metadata.json` es un archivo aparte para que un catálogo pueda evaluar miles de niveles sin abrir ninguno. Esta pasada barata cubre la mayor parte de la política

Pero dos comprobaciones necesitan `level.json`: un recurso sin ningún registro y la forma de obtener los recursos. Un informe limpio solo a partir de los metadatos significa "no hay errores en lo que se ha leído". `IsReady` sigue en `false` hasta que se comprueba el archivo del nivel

`payload` lleva los tamaños medidos: de cada recurso, de `level.json`, de `metadata.json` y del nivel entero. Sin él no se pueden comprobar los límites de tamaño del perfil

Durante la comprobación no se corrige nada, y es a propósito. Editar el contenido en silencio a la salida es lo último que necesita un servicio. Más - [[6_validation]]

## Tres veredictos

| Grupo | Significado | Qué hace el servidor |
|---|---|---|
| `Error` | el servicio lo rechaza | rechaza la subida (`HasErrors`) |
| `Warning` | se puede publicar, pero tiene que mirarlo una persona | pone el nivel en la cola de moderación (`NeedsManualReview`) |
| `Advice` | queda anotado | nada |

El cliente bloquea una subida por los mismos errores antes incluso de que empiece. Un nivel que tu servidor rechazaría rara vez llega a él

## Tu propio PublishProfile

La política de un servicio es un archivo, un modelo del SDK serializado. Un servidor más estricto o más permisivo es otro archivo, no un fork del código

**Un nivel que se queda en el dispositivo del jugador no se comprueba en absoluto.** El perfil solo importa en el momento en que el nivel se ofrece a un servicio. Cómo prepara un autor un nivel para ese momento - [[5_publish-readiness]]

Presets:

| Preset | Clave | Para qué |
|---|---|---|
| `CreateOpen()` | `local` | niveles en el dispositivo, no se exige nada |
| `CreateStandard()` | `standard` | un servidor público, la política de [[ugc-licensing-policy]] |
| `CreateStrict()` | `strict` | compilaciones de tienda, sin enlaces directos, un hash en cada recurso |

Los campos principales:

| Campo | Qué decide |
|---|---|
| `AllowedLicenses` | qué licencias típicas se aceptan, una lista vacía las acepta todas |
| `AllowedUriTypes` | cómo se pueden obtener los recursos, una lista vacía permite todas las formas |
| `AllowUnknownLicense` | si un recurso puede no decir nada sobre sus condiciones |
| `AllowPermissionInstead` | si el permiso del titular de los derechos puede sustituir a una licencia rechazada (siempre se envía a revisión) |
| `RequireResourceMeta`, `RequireResourceUrl`, `RequireAttribution` | qué debe contener el registro de cada recurso |
| `RequireAgeRating`, `RequireLevelAuthors`, `RequireHashes` | qué debe declarar el nivel |
| `MaxResourceBytes`, `MaxDataFileBytes`, `MaxTotalBytes` | límites de tamaño, cero significa sin límite |
| `Sources`, `UnknownSourceTrust` | la lista de sitios de confianza y cómo se valora un sitio que no está en ella |

Los dos presets públicos:

| | `standard` | `strict` |
|---|---|---|
| Enlaces directos a recursos | permitidos | prohibidos |
| Crédito del autor en cada recurso | no se exige | se exige |
| Hash del contenido en cada registro | no se exige | se exige |
| Recurso más grande | {{v:publish.standard.max-resource-mb}} MB | {{v:publish.strict.max-resource-mb}} MB |
| `level.json` o `metadata.json` más grande | {{v:publish.standard.max-data-file-mb}} MB | {{v:publish.strict.max-data-file-mb}} MB |
| Nivel más grande | {{v:publish.standard.max-level-mb}} MB | {{v:publish.strict.max-level-mb}} MB |
| Un sitio que no está en la lista | `RequiresLicenseCheck` | `RequiresResourceCheck` |

Todos los presets y campos - [[7_publish-profiles]]

### Por qué standard no tiene GPL

Las licencias de la familia GPL quedan fuera de `standard` a propósito. Una obra GPL distribuida a través de la App Store choca con las condiciones de Apple. Un catálogo que las admitiera no podría llevarse después a iOS

> [!info] Conviene saber
> La lista de sitios de confianza que incluye el SDK es solo un punto de partida. Los sitios cambian sus condiciones, así que cada dueño de servidor debería sustituirla en su propio perfil. Nada puede dar por hecho que un sitio concreto esté en la lista

## Moderación

Lo que el servidor oficial piensa añadir encima de la comprobación. Muy probablemente un servidor público también lo necesitará:

- **Una cola de moderación.** La llenan las incidencias `Warning`
- **Denuncias y bloqueo** de niveles y usuarios. Las reglas de Google Play y App Store exigen las dos cosas para cualquier contenido que vean otras personas
- **Retirada por hash.** El registro de un recurso puede guardar los hashes del contenido de sus archivos como `sha256:<hex>`. Una reclamación nombra una obra, y con hashes cada nivel que la contiene se encuentra buscando, no adivinando por los títulos. El editor registra el hash al importar un recurso
- **Condiciones de uso.** Cubren lo que la licencia no cubre: la declaración del autor de que tiene los derechos, el derecho del dueño del servidor a retirar un nivel, el derecho a mostrar su título y su portada en las listas

**El Workshop de Steam funciona de otra manera.** Valve almacena los archivos, y no hay cola de moderación por parte de Bullet Hero. El juego comprueba un nivel o una colección antes de subirlo, y un error bloquea la subida - [[17_publishing]]. Después de la publicación el juego solo decide qué descargar de ello

## Formatos de archivo comprimido

Un nivel es una carpeta de archivos, y un archivo comprimido lo hace portátil. Lo que el SDK lee y escribe:

| Formato | Lectura | Escritura | Nota |
|---|---|---|---|
| `.tar.gz` | sí | sí | el predeterminado |
| `.zip` | sí | sí | se puede cifrar por entrada con AES-256 |
| `.tar.gz.gpg`, `.zip.gpg` | sí | sí | un mensaje OpenPGP protegido con contraseña, la única protección disponible para `.tar.gz` |
| `level.json.gpg` | sí | sí | un único archivo de nivel protegido |
| `.7z` | no | no | se reconoce para poder rechazarlo con un nombre claro |

El formato se detecta por los primeros bytes del archivo, no por su extensión. El nombre es la única parte de un archivo que cualquiera puede cambiar

`tar -xzf`, `gpg -d` y cualquier compresor zip abren todos los formatos que se escriben. No hace falta el juego para descomprimir un nivel. Más - [[4_archives]]

## Qué no está decidido

- el protocolo entre el juego y un servidor, y si será el mismo para OWS y NOWS
- la API del servidor: subida, catálogo, búsqueda, cuentas
- cómo indicarle al juego un servidor comunitario
- cómo se amplía el propio servidor y en qué lenguaje
- el juego en compañía en un servidor: transporte, autoridad, sincronización del nivel y salas

Para el juego en compañía solo hay una cosa resuelta: cómo aparece y desaparece el avatar de un jugador con un mensaje de red

La publicación de niveles en cualquier servicio llegará como pronto en la actualización posterior a `gv 1.0.0`. Los datos en los que se apoya la comprobación tienen que entrar en los niveles antes de que se publiquen

## La licencia de los niveles y cualquier servidor

De forma predeterminada un nivel se distribuye bajo *CC BY-NC*, y el autor puede elegir otra licencia en los metadatos del nivel. El permiso para compartir un nivel va de su autor directamente a cada destinatario. Por eso ningún servidor, oficial o comunitario, puede alojar con fines comerciales un nivel bajo *CC BY-NC*

Un servidor con otro código bajo otra licencia no cambia nada en los derechos sobre el contenido. Las reglas completas para autores - [[ugc-licensing-policy]]
