---
title: Política de licencias de los niveles de usuarios
date: 2026-10-14
tags: [legal]
---

# Política de licencias de los niveles de usuarios

Todo nivel de usuario se distribuye con CC BY-NC: con atribución y solo para uso no comercial. Un recurso externo se permite con una licencia abierta aceptada o con el permiso directo de su autor

> [!warning] Advertencia
> La información de esta página se revisará más adelante - las condiciones, la lista de licencias aceptadas y la forma de registrar un permiso todavía pueden cambiar

Bullet Hero permite a los jugadores crear su propio contenido (UGC, contenido generado por usuarios), y ese contenido necesita una licencia. El enfoque es parecido al de *Geometry Dash*, con una diferencia: donde *Geometry Dash* trata una sola pista de música, esta política cubre **todos** los recursos externos de un nivel

## La licencia del nivel

Todo nivel de usuario se distribuye con **CC BY-NC**:

- **CC** - una licencia Creative Commons
- **BY** - la atribución es obligatoria: se cita a los autores
- **NC** - solo uso no comercial

Esta licencia cubre el contenido original del propio nivel: su disposición, su sincronización y sus fotogramas clave, el código personalizado y el trabajo creativo de reunirlo todo en un nivel terminado. **No cambia la licencia de los recursos externos incluidos en el nivel**

Cada recurso externo conserva su propia licencia o permiso, registrado por separado para cada recurso (ver más abajo). CC BY-NC en el nivel es un envoltorio alrededor de recursos que, cada uno por su cuenta, ya pueden redistribuirse de esta forma

**Un nivel solo puede distribuirse con CC BY-NC si cada recurso externo que contiene cumple la opción A o la opción B.** Si uno solo no la cumple, el nivel no puede distribuirse a través de los servicios web oficiales de Bullet Hero (el servidor oficial, OWS)

No impido la distribución libre de niveles por canales no oficiales. Estoy totalmente en contra del uso comercial de los niveles

## Recursos externos

Los recursos externos abarcan una gran variedad de datos:

- música y audio: `.mp3`, `.wav`, `.ogg`
- texturas e imágenes: `.png`, `.jpg`, `.jpeg`
- fuentes: `.ttf`, `.otf`
- textos y bytes: cualquier dato

Cada recurso externo debe cumplir una de las dos opciones siguientes

### Opción A - una licencia abierta

El recurso está disponible con una licencia igual a CC BY-NC o más permisiva (consulta la lista de licencias aceptadas más abajo). El recurso conserva su **propia** licencia original: no se convierte en CC BY-NC, ya permite la redistribución pública no comercial que exige CC BY-NC, así que incluirlo en un nivel CC BY-NC es coherente

La licencia original y la fuente del recurso deben registrarse en el archivo de metadatos del nivel. La SIL OFL ya lo exige para las fuentes, y aquí el requisito se aplica a todos los recursos, para que cualquiera que descargue el nivel pueda ver en qué condiciones se usó cada parte

### Opción B - el permiso directo del autor

El autor del recurso da permiso para usarlo específicamente en Bullet Hero. Un "claro, adelante" en privado no basta por sí solo: un nivel marcado como CC BY-NC se redistribuye públicamente, así que el permiso debe cubrirlo de forma explícita, no solo tu uso personal. Un permiso válido concede estas tres cosas:

1. El derecho a usar el recurso dentro de un nivel de Bullet Hero
2. El derecho a que el nivel resultante, este recurso incluido, sea redistribuido libremente **sin fines comerciales** por terceros a través de los servicios de Bullet Hero (OWS, Steam Workshop, NOWS), con atribución al autor
3. Solo uso no comercial, indicado de forma explícita

El permiso puede ser cualquier cosa que un moderador pueda comprobar: un correo electrónico, un mensaje directo o una declaración pública (por ejemplo en Twitter/X). Usa la plantilla de abajo como punto de partida y guarda la respuesta del autor como prueba

### Plantilla de solicitud de permiso

Rellena los marcadores y ajusta el tono como haga falta, pero mantén intactos los puntos 1 a 3: son lo que hace válido el permiso para la distribución con CC BY-NC. La plantilla está en inglés, como en la política original. Si el autor habla otro idioma, traduce la plantilla y conserva los tres puntos

```
Subject: Permission to use "<TRACK/RESOURCE NAME>" in a Bullet Hero level

Hi <AUTHOR NAME>,

My name is <YOUR NAME / HANDLE>, I'm creating a level for Bullet Hero (a rhythm/
bullet-hell game - <link to game/project if available>) and I'd love to use your
work "<TRACK/RESOURCE NAME>" (<link to the original>) in it.

Specifically, I'm asking your permission to:
1. Use "<TRACK/RESOURCE NAME>" inside my Bullet Hero level.
2. Allow the level (including your work) to be shared/redistributed for FREE and
   NON-COMMERCIALLY by anyone who downloads it, through Bullet Hero's official and
   unofficial services (including its official server, Steam Workshop, and any
   community-run servers).
3. Credit you as "<HOW YOU WANT TO BE CREDITED>" wherever the level shows attribution.

To be clear, this permission is for non-commercial use only - the level will not be
sold, and no one (including me) will make money from it or from your work through it.

If you're fine with this, a simple reply confirming points 1-3 is all I need - I'll
keep this email/message as proof of permission. If you'd rather I credit you
differently, or you want to set any other condition, just let me know.

Thanks a lot either way!
<YOUR NAME / HANDLE>
```

Cómo escribir una solicitud así y qué cuenta como prueba se explica con más detalle en [[6_asking-permission]], y allí también hay una versión rusa de la plantilla

## Servicios externos

El juego puede trabajar con varios servicios externos:

| Servicio | Descripción |
|---|---|
| Official Web Services (OWS) | el servidor predeterminado, disponible en todas las plataformas |
| Steam Workshop | disponible en PC |
| Non-official web services (NOWS) | servicios que cualquiera puede crear y gestionar como quiera |

Está previsto que todas las herramientas para poner en marcha tu propio servidor sean de código abierto con la licencia MIT. Todavía no existe ningún servidor. Más sobre los servidores en [[4_server/index]]

## Licencias aceptadas (opción A)

Un recurso externo aceptado tiene una de estas licencias habituales, igual a la del nivel o más permisiva:

- La familia Creative Commons
  - CC BY-NC (Atribución-NoComercial) - igual que el nivel
  - CC BY (Atribución) - más permisiva que CC BY-NC
  - CC0 (dominio público) - la mejor opción, úsala siempre que puedas
- Apache, MIT - pensadas para texto y código, y más permisivas que CC BY-NC
- GPL - pensada para texto y código, aceptada solo por un servicio cuyo perfil lo permita. El servidor oficial no lo permite, ver más abajo
- SIL OFL (Open Font License) - debe indicarse en el archivo de metadatos

> [!info] Conviene saber
> El perfil de publicación `standard`, sobre el que se construye el servidor oficial, acepta CC0, CC BY, CC BY-NC, SIL OFL, MIT, Apache 2.0 y la Unlicense, pero no la familia GPL. Una obra GPL redistribuida a través de App Store choca con las condiciones de Apple, así que un catálogo con esas obras no podría servirse a iOS más adelante

Licencias habituales que **no** se aceptan:

- Propietaria ("Todos los derechos reservados") - evidentemente no se acepta
- La familia Creative Commons
  - CC BY-SA (Atribución-CompartirIgual) - técnicamente permitida, pero la música sincronizada con un nivel cuenta como una adaptación de ella, y la adaptación de una obra ShareAlike debe llevar la misma licencia. El nivel tendría que pasar a CC BY-SA, que OWS no acepta, así que la respuesta es no
  - CC BY-ND (Atribución-SinDerivadas) - la música sincronizada con un nivel cuenta como una adaptación de ella, y esta licencia prohíbe compartir adaptaciones. Un tema así solo se puede publicar con el permiso de su autor (opción B)
  - CC BY-NC-SA (Atribución-NoComercial-CompartirIgual)
  - CC BY-NC-ND (Atribución-NoComercial-SinDerivadas)

Al publicar un nivel, el juego compara su licencia con las licencias de su música: un tema NoDerivatives sin permiso registrado, una licencia del nivel que un tema ShareAlike no admite y dos temas ShareAlike que exigen licencias distintas aparecen en el informe de publicación

## Dónde encontrar recursos aceptados

### Audio y música

Gratis con garantía:

- [ccMixter](https://ccmixter.org/) - perfecto, contenido con CC BY y CC BY-NC
- [Freesound](https://freesound.org/) - perfecto, todo el contenido con CC0, CC BY y CC BY-NC
- [Incompetech](https://incompetech.com/) - perfecto, todo el contenido con CC BY
- [Teknoaxe](https://teknoaxe.com/) - perfecto, todo el contenido con CC BY
- [Kenney Assets](https://kenney.nl/) - todos los sonidos con CC0

Gratis, pero conviene revisar cada registro:

- [SoundImage](https://soundimage.org/)
- [Pixabay](https://pixabay.com)
- [GoodKid](https://goodkidofficial.com/creators/) - no declara licencia, pero a juzgar por sus preguntas frecuentes es CC BY sin mención del autor. Úsalo como CC BY
- NCS - solo si el nivel mantiene la licencia CC BY-NC predeterminada

Requieren comprobar la licencia a mano:

- [OpenGameArt](https://opengameart.org/) - si no se puede identificar la licencia, el recurso no se puede usar
- [FMA](https://freemusicarchive.org/home) - todo tipo de licencias CC, comprueba cada una con cuidado
- SoundBible

Dudosos:

- Zapsplat
- [Play On Loop](https://www.playonloop.com/music-licensing/) - una condición: el juego no debe ser un proyecto comercial

### Texturas e imágenes

Gratis con garantía:

- [Poly Haven](https://polyhaven.com/)
- [AmbientCG](https://ambientcg.com/)
- [Kenney Assets](https://kenney.nl/)
- [Pexels](https://www.pexels.com/)
- [Unsplash](https://unsplash.com/)

Gratis, pero conviene revisar cada registro:

- [Pixabay](https://pixabay.com)

Requieren comprobar la licencia a mano:

- [OpenGameArt](https://opengameart.org/)
- [Rawpixel](https://www.rawpixel.com/) - solo la "Personal License" y la "Public Domain License", consulta [la página de licencias](https://www.rawpixel.com/services/licenses)
- itch.io
- Wikimedia Commons

### Fuentes

Gratis con garantía:

- Google Fonts

## Palabras finales

Bullet Hero no es un juego grande. Intento mantener un trato humano con la comunidad y te pido que hagas lo mismo. Una buena comunidad se construye entre todos
