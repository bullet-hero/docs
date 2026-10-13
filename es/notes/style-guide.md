---
title: Guía de estilo
date: 2026-10-13
tags: [contributor]
---

# Guía de estilo

Escribe de forma sencilla: una frase, una idea, números en lugar de adjetivos. Un guion con espacios en lugar de una raya, sin punto y coma, sin punto al final de un párrafo

El texto informa, no vende. Toda emoción se convierte antes en una lista, una tabla o un número.
Una página que suena a marketing, a pose de experto o a asistente simpático ha fracasado, aunque todos sus datos sean correctos

## Primero, la sencillez

Esta regla está por encima de todas las demás

Un texto puede no tener nada de relleno y aun así costar de leer. Cada frase es cierta, pero están encadenadas en un único argumento denso, y el lector tiene que retenerlo todo a la vez

Las páginas para principiantes se escriben para poder leerlas en diagonal. Son las páginas para jugadores, las primeras páginas para autores de niveles, el inicio rápido, las preguntas frecuentes, la ayuda y la página de inicio de cada sección. Las páginas de referencia y del SDK pueden ser más densas, pero sus frases siguen las mismas reglas

1. **Solo lo que el lector necesita ahora.** Antes de cada frase, pregúntate: ¿el lector actuará de otra forma después de leerla? Si no, quítala o pásala a la página detallada. Casos límite, salvedades de plataforma, razones internas, cómo funciona el propio sitio: nada de eso va en una página para principiantes
2. **Una frase, una idea.** Nada de cadenas de oraciones unidas con dos puntos, "porque", "así que", "mientras", nada de paréntesis dentro de paréntesis. Dos frases cortas valen más que una larga. Una frase puede ir en su propia línea dentro de un párrafo: con punto al final, salvo la última. En chino y en japonés, una frase en su propia línea es un párrafo aparte, con una línea en blanco antes
3. **La regla general, no las excepciones.** "Los números suelen coincidir" en lugar de tres frases sobre cuándo difieren. La excepción vive en la página detallada, detrás de `Más - [[page]]` (en inglés `More - [[page]]`, en chino `更多：[[page]]`, en japonés `詳細：[[page]]`, en portugués `Mais - [[page]]`, en francés `Plus - [[page]]`)
4. **Navegación antes que explicación.** Una página de inicio es una introducción corta y una tabla de nombre -> enlace, o líneas como `Todo lo que puedes descargar - [[download]]`. Las columnas descriptivas como "qué es" y "estado" sobran cuando el enlace ya lo dice
5. **Di lo que importa, no cómo funciona.** "Este número importa más que todos los demás" más un enlace, en lugar de describir el mecanismo
6. **El estado, en una palabra.** `En desarrollo`, `No disponible`, `Versión actual - gv 1.0.0`. Nada de "en el momento de escribir esto", nada de "no antes de"
7. **Desarrolla una abreviatura donde aparece por primera vez.** Por ejemplo, una columna `gv` -> `versión del juego`
8. **Habla con el lector.** Una pregunta y una respuesta están bien: `¿No te gusta la documentación? Entonces puedes ayudar a escribirla`. `Puede que quieras...` también está bien
9. **Palabras sencillas.** Un término aparece solo cuando el lector se lo va a encontrar en la interfaz del juego. Entonces va entre comillas invertidas, exactamente como lo muestra el juego

```
Antes (correcto, pero pesado):
Los números no se siguen entre sí. `gv` y `sv` empezaron siendo iguales y ahora pueden divergir libremente: un cambio en el SDK no tiene por qué mover la versión del juego, y una actualización del juego no tiene por qué mover la versión del SDK

Después:
Los números de versión no tienen por qué seguirse entre sí, pero en la mayoría de los casos coinciden.
Las versiones también se suben juntas, y una actualización compartida lleva la misma versión
```

## Puntuación

La puntuación sigue las normas del idioma, con dos excepciones deliberadas. Las dos son obligatorias

**Sin rayas.** La raya y la semirraya no se usan en absoluto. Donde haga falta una raya, escribe un guion con espacios alrededor

```
Antes:    Bullet Hero — menos un juego que un reproductor de animaciones
Después:  Bullet Hero - menos un juego que un reproductor de animaciones
```

El chino y el japonés no usan ningún tipo de raya: ni `——`, ni `—`, ni siquiera un guion con espacios. Escribe en su lugar una coma, dos puntos o una frase nueva (`，` y `：` en chino, `、` y `：` en japonés)

```
Antes:    Bullet Hero——与其说是游戏，不如说是动画播放器
Después:  Bullet Hero与其说是游戏，不如说是动画播放器

Antes:    Bullet Hero——ゲームというより、アニメーションのプレイヤー
Después:  Bullet Heroはゲームというより、アニメーションのプレイヤー
```

**Sin punto al final de un párrafo.** Los puntos entre frases dentro de un párrafo se mantienen. La última frase de un párrafo, un elemento de lista, una celda de tabla y un encabezado no llevan punto. Los signos de interrogación y de exclamación se mantienen

**Cuidado con los saltos de línea.** Markdown une en un solo párrafo las líneas que no tienen una línea en blanco entre ellas. Una línea sin punto seguida de otra línea se convierte en dos frases pegadas

Por eso en inglés, en ruso, en español, en portugués y en francés, dentro de un párrafo, cada línea seguida de otra línea termina en punto. Pon una línea en blanco antes de cada idea separada

**En chino y en japonés, un párrafo es una sola línea en el texto fuente.** Markdown convierte un salto de línea dentro de un párrafo en un espacio, y ese espacio aparece entre las frases chinas o japonesas y estorba a la búsqueda. Por eso el texto en chino y en japonés nunca se corta a mano, y una frase que debe ir en su propia línea es un párrafo aparte. Cada idea separada lleva una línea en blanco antes

Otros signos:

- **Los dos puntos** son el signo de trabajo para explicar y enumerar, úsalos sin miedo
- **El punto y coma** no se usa nunca. Escribe un punto o un elemento de lista aparte. El chino tampoco usa `；`: escribe dos frases o una `，`. El japonés igual: dos frases o un `、`
- **Los signos de exclamación** son raros, como mucho uno por texto largo
- **Las comillas** en inglés, ruso, español, portugués y francés son solo rectas `"comillas"`, nunca `«»`. El chino usa las de ancho completo `“”`, el japonés `「」`, el coreano rectas como el inglés
- **Los paréntesis** sirven para un comentario breve, una salvedad o un chiste seco

## Chino, japonés, coreano, español y portugués

Las reglas de arriba se aplican a todos los idiomas sin excepción. El chino añade algunos puntos:

- **Trata al lector de `你`,** nunca de `您`. El consejo es `建议`, la opinión del autor es `我`, nunca `开发者` ni `我们`
- **Puntuación de ancho completo** `，。：？！（）` y comillas `“”`. El código, los nombres de archivo y todo lo que va entre comillas invertidas conservan la puntuación ASCII
- **Sin espacio entre hanzi y letras latinas o dígitos,** como lo escribe el propio juego: `在Bullet Hero中`, `60帧`
- **Se quedan en letras latinas:** los nombres de producto y de formato (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), las extensiones de archivo, las teclas, los nombres de campos
- **Los términos salen de `game/zh-glossary.md`.** Cada término tiene una sola grafía, y las filas marcadas `strict` se respetan siempre. Un texto de la interfaz se cita a partir del valor de su clave en `game/zh.yaml`
- **Los títulos de los recuadros** son 建议, 提示, 须知, 警告, 注意 (`> [!tip] 建议`)

El japonés añade estos puntos:

- **Escribe en el registro です/ます.** Al lector no se le nombra con un pronombre, nunca `あなた`: construye la frase para que el sujeto quede claro sin él. El consejo es `〜することをおすすめします` o `推奨`, la opinión del autor es `私`, nunca `開発者` ni `私たち`
- **Puntuación de ancho completo** `、。：？！（）` y comillas angulares `「」`. Una cita dentro de una cita es `『』`. El código, los nombres de archivo y todo lo que va entre comillas invertidas conservan la puntuación ASCII
- **Los préstamos se escriben en katakana,** conservando la `ー` final: `インスペクター`, `レイヤー`. Así los escribe el editor de Unity en japonés
- **Sin espacio entre kana o kanji y letras latinas o dígitos,** como lo escribe el propio juego: `Bullet Heroでは`, `60フレーム`
- **Se quedan en letras latinas:** los nombres de producto y de formato (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), las extensiones de archivo, las teclas, los nombres de campos
- **Los términos salen de `game/ja-glossary.md`.** Cada término tiene una sola grafía, y las filas marcadas `strict` se respetan siempre. Un texto de la interfaz se cita a partir del valor de su clave en `game/ja.yaml`
- **La puntuación va fuera de las marcas de negrita:** escribe `**太字**。本文`, nunca `**太字。**本文`. En la segunda forma Markdown no puede cerrar el `**`, y los asteriscos se imprimen tal cual
- **Los títulos de los recuadros** son 推奨, ヒント, 補足, 警告, 注意 (`> [!tip] 推奨`)

El coreano añade estos puntos:

- **Escribe en el registro 합니다체** (`-ㅂ니다`/`-습니다`). Al lector no se le nombra con un pronombre, nunca `당신`. El consejo es `권장합니다`, la opinión del autor es `저`, nunca `개발자` ni `저희`
- **La puntuación es ASCII y las palabras se separan con espacios,** como en inglés, así que las reglas de arriba sobre la raya, el punto y las comillas se aplican tal cual
- **Los préstamos se escriben en hangul** como los escribe el editor de Unity en coreano: `레이어`, `인스펙터`
- **Ninguna partícula suelta después de una palabra latina, un código o un marcador** cuyo sonido final la frase no puede conocer: escribe la forma doble `을(를)`, `이(가)` o reformula
- **Se quedan en letras latinas:** los nombres de producto y de formato (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), las extensiones de archivo, las teclas, los nombres de campos
- **Los términos salen de `game/ko-glossary.md`.** Cada término tiene una sola grafía, y las filas marcadas `strict` se respetan siempre. Un texto de la interfaz se cita a partir del valor de su clave en `game/ko.yaml`
- **La puntuación o el código al final de una negrita rompen la negrita cuando sigue una partícula:** escribe `**이름**을`, nunca `**"이름"**을`
- **Los títulos de los recuadros** son 권장, 팁, 참고, 경고, 주의 (`> [!tip] 권장`)

El español añade estos puntos:

- **Español neutro, un solo texto para España y América Latina.** Al lector se le trata de `tú`, en singular, nunca de `usted`, `vosotros` ni `ustedes`. El consejo es `se recomienda` o `conviene`, nunca `te recomendamos`, la opinión del autor es `yo`, nunca `los desarrolladores` ni `nosotros`
- **Vocabulario que se lee igual a los dos lados del Atlántico:** `archivo` y no `fichero`, `equipo` o `PC` y no `ordenador` ni `computadora`, `teléfono` o `móvil` y no `celular`, `hacer clic` en la pantalla y `pulsar` una tecla
- **Ningún adjetivo que concuerde con el género del lector** (`listo`/`lista`): reformula la frase para evitarlo
- **Las dos excepciones se aplican sobre la tipografía española:** un guion con espacios ` - ` en lugar de la raya (también en incisos y diálogos), comillas rectas en lugar de `«»`, sin punto al final de un párrafo, un elemento de lista, una celda de tabla o un encabezado. Sin `;`
- **`¿…?` y `¡…!` llevan siempre los dos signos**
- **Encabezados y títulos con mayúscula solo inicial** (`## Cómo funciona el ajuste`), nunca en Title Case. La mayúscula conserva la tilde (`Á`, `É`)
- **Se quedan sin traducir:** los nombres de producto y de formato (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), las extensiones de archivo, las teclas, los nombres de campos
- **Los términos salen de `game/es-glossary.md`.** Cada término tiene una sola grafía, y las filas marcadas `strict` se respetan siempre. Un texto de la interfaz se cita a partir del valor de su clave en `game/es.yaml`
- **Los títulos de los recuadros** son Recomendación, Consejo, Conviene saber, Advertencia, Precaución (`> [!tip] Recomendación`). `More - [[page]]` se escribe `Más - [[page]]`

El portugués añade estos puntos:

- **Portugués de Brasil, el código `pt` no lleva región.** Al lector se le trata de `você` con verbos en tercera persona, nunca de `tu`, `o senhor` ni `vocês`. El consejo es `recomenda-se` o `vale a pena`, nunca `recomendamos`, la opinión del autor es `eu`, nunca `os desenvolvedores` ni `nós`
- **Vocabulario de Brasil, nunca de Europa:** `arquivo` y no `ficheiro`, `tela` y no `ecrã`, `salvar` y no `guardar`, `mouse` y no `rato`, `celular` y no `telemóvel`, `baixar` y no `transferir`. `estar` con gerundio (`está carregando`), nunca `estar a` con infinitivo
- **Ningún adjetivo que concuerde con el género del lector** (`pronto`/`pronta`): reformula la frase para evitarlo
- **Las dos excepciones se aplican sobre la tipografía portuguesa:** un guion con espacios ` - ` en lugar del travessão, comillas rectas en lugar de `«»` o `“”`, sin punto al final de un párrafo, un elemento de lista, una celda de tabla o un encabezado. Sin `;`
- **Encabezados y títulos con mayúscula solo inicial** (`## Como funciona o encaixe`), nunca en Title Case. La mayúscula conserva el acento (`É`, `Ã`)
- **Se quedan sin traducir:** los nombres de producto y de formato (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), las extensiones de archivo, las teclas, los nombres de campos
- **Los términos salen de `game/pt-glossary.md`.** Cada término tiene una sola grafía, y las filas marcadas `strict` se respetan siempre. Un texto de la interfaz se cita a partir del valor de su clave en `game/pt.yaml`
- **Los títulos de los recuadros** son Recomendação, Dica, Vale saber, Aviso, Cuidado (`> [!tip] Recomendação`). `More - [[page]]` se escribe `Mais - [[page]]`

El francés añade estos puntos:

- **Francés tal como se escribe en Francia, que se lee igual en Bélgica, Suiza y Canadá.** Al lector se le trata de `tu`, nunca de `vous`. El consejo es `il vaut mieux` o `mieux vaut`, nunca `nous te recommandons`, la opinión del autor es `je`, nunca `les développeurs` ni `nous`
- **El vocabulario del software en francés:** `fichier`, `paramètres`, `enregistrer`, `souris`, `écran`, `cliquer` en la pantalla y `appuyer sur` una tecla
- **Ningún adjetivo que concuerde con el género del lector** (`prêt`/`prête`): reformula la frase para evitarlo
- **Las dos excepciones se aplican sobre la tipografía francesa:** un guion con espacios ` - ` en lugar del tiret (también en incisos), comillas rectas en lugar de `«»`, el apóstrofo recto `'`, sin punto al final de un párrafo, un elemento de lista, una celda de tabla o un encabezado. Sin `;`
- **Un espacio de no separación (U+00A0) antes de `?`, `!` y `:`,** y antes de `%` tras un número, nunca un espacio normal y nunca sin espacio. El código y todo lo que va entre comillas invertidas conserva su propio texto
- **Encabezados y títulos con mayúscula solo inicial** (`## Comment fonctionne l'aimantation`), nunca en Title Case. La mayúscula conserva el acento (`É`, `À`)
- **Se quedan sin traducir:** los nombres de producto y de formato (`{{ui:root_common_game-name}}`, `JSON`, `BPM`), las extensiones de archivo, las teclas, los nombres de campos
- **Los términos salen de `game/fr-glossary.md`.** Cada término tiene una sola grafía, y las filas marcadas `strict` se respetan siempre. Un texto de la interfaz se cita a partir del valor de su clave en `game/fr.yaml`
- **Los títulos de los recuadros** son Recommandation, Conseil, Bon à savoir, Avertissement, Attention (`> [!tip] Recommandation`). `More - [[page]]` se escribe `Plus - [[page]]`

## Maquetación

- **Párrafos cortos,** de una a tres líneas
- **Una lista con viñetas** para cualquier enumeración de más de dos elementos. Las listas numeradas, solo para pasos y opciones
- **Una tabla** siempre que se comparan tres o más cosas en varias propiedades
- **La cursiva** (`*text*`) para términos, nombres de productos y géneros: *musical bullet hell*, *Geometry Dash*. En las fuentes chinas y japonesas no se puede confiar en la cursiva, así que en esos idiomas la cursiva va solo en nombres de productos escritos en letras latinas, y el énfasis va en negrita
- **La negrita** para enfatizar una palabra o para abrir un párrafo con su tema
- **Las comillas invertidas** para todo lo técnico: archivos, campos, formatos, valores, teclas, comandos
- **Una versión es siempre su prefijo más el número, entre comillas invertidas:** `gv 1.0.0`, `sv 1.1.0`, `fv 1.0.0`, `bv 1.0.0`, `mg 2`. Nunca un `1.0.0` suelto, "versión 1.0.0" ni "SDK 1.0.0" sin el prefijo. Las comillas invertidas no funcionan en `title` ni en `# H1`, así que ahí va `gv 1.0.0` sin más. Las versiones de cosas de terceros (Unity, paquetes de NuGet) no son nuestras y se escriben tal cual
- **Sin emoji**

## Recuadros

Un párrafo con un propósito concreto se convierte en un recuadro. Hay exactamente cinco, y el título se escribe en el idioma de la página:

| Recuadro | Título en inglés | Título en ruso | Título en chino | Título en japonés | Título en coreano | Título en español | Título en portugués | Título en francés | Qué introduce |
|---|---|---|---|---|---|---|---|---|---|
| `> [!tip] Recommendation` | Recommendation | Рекомендация | 建议 | 推奨 | 권장 | Recomendación | Recomendação | Recommandation | hazlo así |
| `> [!tip]` | Tip | Подсказка | 提示 | ヒント | 팁 | Consejo | Dica | Conseil | un atajo, un truco, un camino más rápido |
| `> [!info]` | Worth knowing | Интересно | 须知 | 補足 | 참고 | Conviene saber | Vale saber | Bon à savoir | contexto que explica una decisión |
| `> [!warning]` | Warning | Предупреждение | 警告 | 警告 | 경고 | Advertencia | Aviso | Avertissement | esto costará tiempo o calidad |
| `> [!caution]` | Caution | Внимание | 注意 | 注意 | 주의 | Precaución | Cuidado | Attention | esto destruye trabajo o publica un nivel roto |

**Como mucho dos recuadros por página,** porque un tercero deja de leerse como énfasis. Las páginas de referencia pueden tener dos por sección. Una página sobre algo que todavía no existe empieza con un `> [!warning]` sobre su estado, y ese no cuenta para el límite

## Voz

- **Al lector se le trata de "tú"** (en ruso, el "вы" formal en minúscula, en chino `你`, en español `tú`, nunca `usted`, en portugués `você`, en francés `tu`, nunca `vous`). El japonés no nombra al lector con un pronombre y nunca usa `あなた`
- **El proyecto habla de forma impersonal,** nunca como "los desarrolladores" ni "nosotros". El consejo es "se recomienda" (en ruso "рекомендуется", en chino `建议`, en japonés `〜することをおすすめします` o `推奨`, en español también `conviene`, en portugués `recomenda-se` o `vale a pena`, en francés `il vaut mieux` o `mieux vaut`), y un hecho tiene como sujeto la cosa misma: "El juego no incluye ninguna textura"
- **La opinión o la decisión del autor va en primera persona,** "yo recomiendo" (en ruso "я рекомендую", en chino `我建议`, en japonés `私は〜をおすすめします`). El juego lo hace una sola persona, así que aquí "yo" es honesto. Solo para una valoración o una decisión real, no para hechos simples
- **Las notas de `notes/` pueden hablar en primera persona,** porque una nota es el informe de su autor
- **Sin historia en la documentación.** Una página de documentación describe cómo funcionan las cosas ahora. "Antes era X" es una nota
- **Sin afirmaciones de ser mejor.** Una comparación solo se permite cuando ayuda al lector a entender más rápido
- **Di los límites de lo que se sabe.** "Muy probablemente", "todavía no se sabe". La falsa seguridad es peor que no saber
- **Cada valoración va con su razón.** Un adjetivo sin razón es un defecto
- **Números en lugar de adjetivos.** Segundos, fotogramas, megabytes, versiones, cantidades de objetos
- **La ironía es seca y rara,** un comentario breve entre paréntesis. Las páginas de referencia casi no la tienen
- **Sin palabrotas** en ningún idioma, tampoco sustitutos groseros
- **Nunca inventes** una dirección, un número o un dato. Sin fuente, di que no se sabe

## Inicio de la página

**El inicio responde, no anuncia.** No describe la página ("qué es X, cómo funciona Y y dónde está Z"), da una respuesta breve a la pregunta por la que existe la página. Un inicio así es útil por sí solo, aunque el lector no siga leyendo

**Lo esencial va en el primer párrafo.** También es la descripción en listados, búsqueda y vistas previas de enlaces: se corta a los 200 caracteres, sin enlaces ni formato. La respuesta puede continuar en el segundo y el tercer párrafo

**No dividas una página corta.** Si hay poco contenido, el inicio se funde con el cuerpo en lugar de repetirlo como una línea aparte arriba

```
Antes:
Dónde informar de un bug o hacer una pregunta, y qué escribir para que el bug se pueda reproducir

Después:
Los bugs del juego van a los issues de releases, las preguntas a Discord. Adjunta la línea de versión de la configuración y los pasos que llevan al bug
```

## Estructura de una página

1. `# H1` y un inicio que responde a la pregunta de la página
2. El cuerpo no repite el inicio, da los detalles, los casos y los pasos
3. Secciones `##`, un tema cada una: la afirmación, después el mecanismo o los pasos, después la conclusión
4. Donde encaje, consejos concretos o enlaces de "qué leer después" al final
5. El final nunca vuelve a contar la página

Una página de guía se lee en 2 a 4 minutos, unos 2000 a 3500 caracteres. Una página de referencia puede ser más larga, pero cada sección se sostiene por sí sola

## Qué delata un texto ajeno

- una raya, un punto al final de un párrafo, un punto y coma
- "No es solo X, es todo un Y"
- floreos de tres: "más rápido, más barato, más fiable"
- arranques vacíos: "en el mundo actual", "vamos a sumergirnos", "no es ningún secreto que"
- un párrafo final que repite lo ya dicho
- adjetivos entusiastas sin razón: "increíble", "asombroso", "una herramienta potente"
- relleno cortés y disculpas al lector
- frases simétricas escritas por el ritmo y no por el sentido
- consejos genéricos que nadie comprobó en este juego

## Antes y después

**Un párrafo inicial**

```
Antes:
En el mundo actual del diseño de niveles, el editor de Bullet Hero ocupa un lugar especial — no es solo
una herramienta, es todo un ecosistema. Vamos a sumergirnos y ver por qué.

Después:
El editor construye un nivel a partir de objetos que viven en un tramo de tiempo y se mueven siguiendo fotogramas clave. Abajo se explica cómo está organizado y en qué orden trabajar con él
```

**Una valoración**

```
Antes:
El formato Blob es una solución asombrosa que acelera drásticamente la carga y hace tu flujo de trabajo más productivo.

Después:
`Blob` carga más rápido que `Json`, pero no se puede leer a simple vista ni comparar en git. Mantén un nivel en `Json` mientras trabajas en él y conviértelo a `Blob` antes de publicarlo
```

**Algo que todavía no existe**

```
Antes:
El servidor oficial ofrecerá una forma cómoda de compartir tus niveles con todo el mundo.

Después:
Todavía no hay servidor oficial. El protocolo con el que el juego se comunicará con él no está diseñado, así que esta página describe solo lo que ya está decidido
```

## Lista de comprobación antes de un pull request

1. La página se puede leer en diagonal: una idea por frase, los detalles más abajo o en su propia página
2. Sin rayas ni semirrayas (el chino y el japonés no usan ningún tipo de raya)
3. Ningún párrafo, elemento de lista ni encabezado termina en punto
4. Sin líneas pegadas: cada idea separada es su propio párrafo o va separada por un punto dentro de la línea. Un párrafo en chino o en japonés es una sola línea en el texto fuente
5. Sin punto y coma, sin emoji, como mucho un signo de exclamación
6. Sin palabrotas
7. Las comas, los dos puntos y la concordancia siguen la norma, sin erratas
8. Cada valoración tiene su razón al lado
9. Los números, los nombres de campos y los enlaces salen de una fuente
10. Sin "los desarrolladores" ni "nosotros" en `docs/`: el consejo es impersonal, "yo" solo para la opinión o la decisión del autor
11. Como mucho dos recuadros
12. El inicio después del H1 responde a la pregunta de la página (lo esencial en los primeros 200 caracteres), no describe la página y no se repite más abajo
13. El final no vuelve a contar la página
