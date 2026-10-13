# Spanish term base

The terms `es.yaml` (neutral Spanish) is translated with. Every value in `es.yaml` follows this table: a thing is
named the same way on every screen, in every hint, in every tooltip.

- **`strict`** rows are checked by the game's tests: whenever the English value of a key contains the `en` term (a
  whole word, any case, tags ignored, a plural `s`/`es` included), its Spanish value must contain the `es` term.
- The check is a plain substring match, accents included, so a `strict` cell is the part every form of the term
  shares: `nivel` covers `niveles`. Where the plural moves a word or an accent (`fotogramas clave`, `líneas de
  tiempo`), the cell is the shared part and the note gives the full term; where no such part is a word anyone would
  recognise (`colección`, `colecciones`), the row is `loose`.
- **`loose`** rows are guidance: a common word whose best translation depends on the sentence around it. Follow them
  unless the sentence reads wrong, and never use a `loose` row's `es` for a different concept.
- A row whose `es` is the same Latin text as `en` means "keep it in Latin" - product names, formats, keys.
- Loanwords follow the Spanish Unity documentation and the Spanish-speaking rhythm-game communities (osu!, Geometry
  Dash): a Spanish word where they use one (`capa`, `fotograma clave`, `línea de tiempo`), the English word where
  they keep it (`prefab`, `gizmo`, `checkpoint`, `hitbox`).
- One file for Spain and Latin America: `tú`, a button is an infinitive, sentence case, and a word both sides of the
  Atlantic read the same way (`archivo`, never `fichero`).

The canonical meanings are the [glossary](../en/docs/2_editor/7_reference/1_glossary.md). To propose a change, open an
issue or a pull request that edits this table and every `es.yaml` value that uses the term, in one change.

Punctuation, labels and the rest of the house style for Spanish: `Assets/Addressables/TEXT-STYLE.md`, section 11, in
the game's repository.

| en | es | kind | note |
|---|---|---|---|
| Level | nivel | strict | Todo lo que forma una partida: objetos, audio, eventos y recursos propios. El "level" del sonido es otra cosa: "volumen" o "nivel de señal" |
| Object | objeto | strict | Lo que el autor crea en la línea de tiempo, con su propio tramo, transformación y padre |
| Rect | objeto vacío | loose | Objeto que no dibuja nada: solo transformación, tramo e hijos. Como en ru, dos palabras: el tipo es "objeto vacío", la forma geométrica es "rectángulo" |
| Shape | forma | loose | Geometría real que dibuja un objeto, no una imagen. El juego genera unas 500 por sí mismo |
| Collider | colisionador | strict | Con lo que choca un objeto. Puede no coincidir con lo que dibuja. Plural "colisionadores" |
| Prefab | prefab | strict | Plantilla reutilizable de objetos que se coloca en un nivel tantas veces como haga falta. En inglés, como en Unity. Plural "prefabs" |
| Prefab Mode | modo prefab | strict | Editar el contenido propio de una plantilla en lugar del nivel que la rodea |
| Effect | efecto | loose | Objeto que cada fotograma crea sus propios objetos a partir de unos pocos parámetros. Bloom, Vignette, etc. son "efectos de posprocesado", nunca "efecto" a secas |
| Inframe Object | objeto de fotograma | loose | Objeto creado por un efecto. Lo gestiona el motor: no se puede seleccionar ni editar |
| Theme | tema | strict | Paleta a la que el nivel se refiere por índice: recolorear es un cambio, no cien. Una canción nunca es "tema" aquí, es "canción" |
| Frame | fotograma | strict | Unidad de tiempo del nivel. El fotograma es una celda y el tiempo es el límite entre dos celdas. Nunca "cuadro" |
| Keyframe | clave | strict | Término completo "fotograma clave", plural "fotogramas clave": la celda es "clave" porque las dos formas la comparten y porque distingue Keyframe de Frame. Valor fijado por el autor en un fotograma, entre dos se interpola |
| Key | fotograma clave | loose | Abreviatura de keyframe: "fotograma clave". La tecla del teclado es "tecla", la clave de localización es "clave" |
| Track | pista | strict | Fila de fotogramas clave de una propiedad animable: posición, rotación, volumen. Audio Track es "pista de audio" |
| Timeline | de tiempo | strict | Término completo "línea de tiempo", plural "líneas de tiempo": la celda es "de tiempo" porque las dos formas la comparten. Eje de fotogramas sobre el que se edita el nivel, una pestaña por tipo de contenido |
| Span | tramo | loose | Cuándo existe un objeto: fotograma inicial y duración, no fotograma final. El verbo span ("abarcar") no se traduce como "tramo" |
| Playhead | cabezal | strict | El fotograma que se muestra ahora. Forma larga "cabezal de reproducción" donde cabe |
| Ease | suavizado | strict | Cómo pasa el valor del fotograma clave anterior a este. No es Curve ("curva") ni el antialiasing |
| Marker | marcador | strict | Punto con nombre en la regla del nivel, para volver al sitio exacto |
| Checkpoint | checkpoint | strict | Adonde una muerte devuelve al jugador. En inglés, como en la comunidad de Geometry Dash y como en ru, que también usa el préstamo. Plural "checkpoints" |
| Anchor | ancla | strict | Borde que sigue al borde del padre: si el padre se encoge, el hijo se mueve con él. "ancla" también está en "anclaje" y "anclado" |
| Layer | capa | strict | Orden de dibujo relativo al padre: la capa del hijo se suma a la del padre |
| Pivot | pivote | loose | Punto sobre el que el objeto gira y escala, dentro de su propio recuadro |
| Gizmo | gizmo | strict | Asas de arrastre dibujadas sobre el objeto seleccionado en la vista. En inglés, como en Unity |
| Snapping | ajuste | strict | Atraer un arrastre hacia algo: hacia el contenido con el imán, hacia la música con el interruptor de pulso. Por eso Settings es "configuración", nunca "ajustes" |
| Snap | ajust | strict | Igual que Snapping. La celda es la raíz "ajust", que comparten "ajuste" y "ajustar". Fit es "encajar", nunca "ajustar" |
| Beat | pulso | strict | La rejilla propia de la música: la fija el autor y nada la lee durante el juego. No "tiempo", que choca con la línea de tiempo y con el tiempo del nivel |
| Beat Segment | segmento | strict | Término completo "segmento de pulso". Parte de tempo constante con su propio tempo, fase y longitud de compás. No "tramo", que es Span |
| BPM | BPM | strict | Pulsos por minuto. En latín, como en las comunidades de juegos de ritmo |
| Tap | toque | loose | Una pulsación al marcar el tempo. En la pantalla táctil también "toque" |
| Generator | generador | strict | Automatización de la creación: produce contenido del nivel a partir de unos pocos parámetros |
| Modifier | modificador | strict | Generador que edita o elimina lo que ya existe en lugar de añadir. La tecla del teclado es Modifier Key |
| Seed | semilla | strict | El número del que sale cada valor aleatorio del nivel: la misma semilla reproduce exactamente lo mismo |
| Raw Data | datos sin procesar | strict | Todo el modelo guardado como un árbol editable. Aquí no se valida nada, a propósito |
| Recommendation | Recomendación | strict | Una de las cinco etiquetas: `<b>Recomendación:</b>`, y la frase que sigue empieza en minúscula |
| Tip | Consejo | strict | Una de las cinco etiquetas: `<b>Consejo:</b>`, y la frase que sigue empieza en minúscula |
| Worth knowing | Conviene saber | strict | Una de las cinco etiquetas: `<b>Conviene saber:</b>`, y la frase que sigue empieza en minúscula |
| Warning | Advertencia | strict | Una de las cinco etiquetas: `<b>Advertencia:</b>`, y la frase que sigue empieza en minúscula |
| Caution | Precaución | strict | Una de las cinco etiquetas: `<b>Precaución:</b>`, y la frase que sigue empieza en minúscula |
| More | Más | loose | La última línea de enlaces de una ayuda, `More:`, es `Más:` |
| Bullet Hero | Bullet Hero | strict | Nombre del producto. No se traduce |
| Steam | Steam | loose |  |
| JSON | JSON | strict | Nombre de formato. No se traduce |
| MSAA | MSAA | strict | Sigla técnica. No se traduce |
| FXAA | FXAA | strict | Sigla técnica. No se traduce |
| HDR | HDR | loose |  |
| VFX | VFX | loose |  |
| URL | URL | loose |  |
| Ctrl | Ctrl | loose | Las teclas van en latín |
| Shift | Shift | loose | En latín, no "Mayús" |
| Enter | Enter | loose | En latín, no "Intro" |
| Hierarchy | jerarquía | strict | Panel del editor que lista los objetos por relación padre-hijo. La ventana Hierarchy de Unity es "Jerarquía" |
| Inspector | inspector | strict | Panel del editor con las propiedades de lo seleccionado. Como en Unity |
| Viewport | vista | strict | Zona del editor que muestra la pantalla del nivel. La categoría de comandos View es "Ver", no "Vista" |
| Command Palette | paleta de comandos | strict | Ventana que busca y ejecuta un comando por su nombre. Como en VS Code en español |
| Command | comando | loose |  |
| Selection | selección | loose |  |
| Select | seleccionar | loose |  |
| Marquee | selección rectangular | strict | Seleccionar arrastrando un rectángulo |
| Apply | aplicar | loose |  |
| Reset | restablecer | loose |  |
| Cancel | cancelar | loose |  |
| Confirm | confirmar | loose |  |
| OK | Aceptar | loose | El botón OK de una interfaz en español es "Aceptar" |
| Save | guardar | loose |  |
| Load | cargar | loose |  |
| Open | abrir | loose |  |
| Close | cerrar | loose |  |
| Exit | salir | loose |  |
| Create | crear | loose |  |
| Add | añadir | loose | "añadir", no "agregar": un solo verbo en todo el archivo |
| Remove | quitar | loose | Distinto de Delete ("eliminar"): Remove saca algo de una lista, Delete lo borra |
| Delete | eliminar | loose |  |
| Duplicate | duplicar | loose |  |
| Copy | copiar | loose |  |
| Paste | pegar | loose |  |
| Cut | cortar | loose |  |
| Undo | deshacer | loose |  |
| Redo | rehacer | loose |  |
| History | historial | loose | Distinto de Story ("historia") |
| Edit | editar | loose | Como categoría de menú, "Edición" |
| Rename | cambiar nombre | loose |  |
| Move | mover | loose |  |
| Import | importar | loose |  |
| Export | exportar | loose |  |
| Archive | archivo comprimido | loose | Contenedor portátil de un nivel o de una colección. Nunca "archivo" a secas, que es File |
| Folder | carpeta | loose |  |
| File | archivo | loose | "archivo", nunca "fichero" |
| Search | buscar | loose | Como sustantivo, "búsqueda" |
| Filter | filtrar | loose | Como sustantivo, "filtro" |
| Refresh | actualizar | loose |  |
| Toggle | alternar | loose | Un interruptor de mostrar y ocultar puede decir "Mostrar/ocultar" |
| Show | mostrar | loose |  |
| Hide | ocultar | loose |  |
| Hidden | oculto | loose |  |
| Visible | visible | loose |  |
| Enabled | activado | loose |  |
| Disabled | desactivado | loose |  |
| On | activado | loose | Estado de un interruptor |
| Off | desactivado | loose |  |
| None | ninguno | loose | Concuerda con el sustantivo al que se refiere ("ninguna" para una forma) |
| Auto | automático | loose |  |
| Custom | personalizado | loose |  |
| Default | predeterminado | loose |  |
| All | todo | loose |  |
| Nothing | nada | loose |  |
| Current | actual | loose |  |
| Active | activo | loose |  |
| Global | global | loose |  |
| Local | local | loose |  |
| Parent | padre | loose |  |
| Child | hijo | loose |  |
| Root | raíz | loose |  |
| Fold | contraer | loose |  |
| Unfold | expandir | loose |  |
| Flatten | aplanar | loose |  |
| Transform | transformación | loose |  |
| Position | posición | loose |  |
| Rotation | rotación | loose |  |
| Scale | escala | loose |  |
| Size | tamaño | loose |  |
| Offset | desplazamiento | loose |  |
| Angle | ángulo | loose |  |
| Radius | radio | loose |  |
| Width | ancho | loose |  |
| Height | alto | loose |  |
| Min | mín. | loose |  |
| Max | máx. | loose |  |
| Step | paso | loose |  |
| Random | aleatorio | loose |  |
| Rnd | aleat. | loose | Abreviatura de "aleatorio" en etiquetas cortas |
| From | desde | loose |  |
| To | hasta | loose |  |
| Value | valor | loose |  |
| Type | tipo | loose |  |
| Name | nombre | loose |  |
| Mode | modo | loose |  |
| Count | cantidad | loose |  |
| Speed | velocidad | loose |  |
| Velocity | velocidad | loose |  |
| Gravity | gravedad | loose |  |
| Particle | partícula | loose |  |
| Orbital | orbital | loose |  |
| Lifetime | tiempo de vida | loose |  |
| Color | color | loose |  |
| Alpha | alfa | loose |  |
| Opacity | opacidad | loose |  |
| Opaque | opaco | loose |  |
| Transparent | transparente | loose |  |
| Gradient | degradado | loose |  |
| Texture | textura | loose |  |
| Font | fuente | loose |  |
| Text | texto | loose |  |
| Localized Text | texto localizado | loose |  |
| Language | idioma | loose |  |
| Audio | audio | loose |  |
| Audio Track | pista de audio | loose |  |
| Volume | volumen | loose |  |
| Music | música | loose |  |
| Sound | sonido | loose |  |
| Resource | recurso | loose |  |
| Resources | recursos | loose |  |
| Metadata | metadatos | loose |  |
| Meta | meta | loose |  |
| License | licencia | loose |  |
| Author | autor | loose |  |
| Artist | artista | loose |  |
| Settings | configuración | loose | Nunca "ajustes", que es Snapping |
| Editor | editor | loose |  |
| Game | juego | loose |  |
| Player | jugador | loose |  |
| Avatar | avatar | loose |  |
| Dash | dash | loose | En inglés, como en la comunidad de Geometry Dash. "impulso" contiene "pulso" (Beat) |
| Hitbox | hitbox | loose |  |
| Damage | daño | loose |  |
| Health | salud | loose |  |
| Death | muerte | loose |  |
| Camera | cámara | loose |  |
| Zoom | zoom | loose |  |
| Pan | paneo | loose |  |
| Shake | sacudida | loose |  |
| Grid | cuadrícula | loose |  |
| Ruler | regla | loose |  |
| Loop | bucle | loose |  |
| Play | reproducir | loose | Reproducir en el editor es "reproducir", jugar el nivel es "jugar" |
| Pause | pausar | loose | Como sustantivo, "pausa" |
| Stop | detener | loose |  |
| Preview | vista previa | loose |  |
| Render | renderizado | loose |  |
| Post-processing | posprocesado | loose |  |
| Post | posprocesado | loose | Abreviatura de post-processing |
| Bloom | bloom | loose |  |
| Vignette | viñeta | loose |  |
| Chromatic Aberration | aberración cromática | loose |  |
| Lens Distortion | distorsión de lente | loose |  |
| Film Grain | grano de película | loose |  |
| Grain | grano | loose |  |
| Motion Blur | desenfoque de movimiento | loose |  |
| Blur | desenfoque | loose |  |
| Color Curves | curvas de color | loose |  |
| Curve | curva | loose | No es Ease ("suavizado") |
| Lift Gamma Gain | Lift/Gamma/Gain | loose | Controles de la corrección de color, en inglés |
| Shadows Midtones Highlights | sombras/medios tonos/luces | loose |  |
| White Balance | balance de blancos | loose |  |
| Analog Glitch | glitch analógico | loose |  |
| Digital Glitch | glitch digital | loose |  |
| Glitch | glitch | loose |  |
| Gamma | gamma | loose |  |
| Background | fondo | loose |  |
| Framerate | frecuencia de fotogramas | loose |  |
| Fixed Framerate | frecuencia fija de simulación | loose | Como en ru, dos sentidos: en la configuración, la frecuencia de actualización de la simulación; en otros sitios, "frecuencia de fotogramas fija" |
| Collision | colisión | loose |  |
| Screen Limit | límite de pantalla | loose |  |
| Cursor | cursor | loose |  |
| Control | control | loose |  |
| Controls | controles | loose |  |
| Keybinding | asignación de teclas | loose |  |
| Shortcut | atajo | loose |  |
| Button | botón | loose |  |
| Interface | interfaz | loose |  |
| Screen | pantalla | loose |  |
| Window | ventana | loose |  |
| Panel | panel | loose |  |
| Tab | pestaña | loose |  |
| Menu | menú | loose |  |
| Tool | herramienta | loose |  |
| Library | biblioteca | loose |  |
| Bot | bot | loose |  |
| Tutorial | tutorial | loose |  |
| Sandbox | sandbox | loose |  |
| Hint | ayuda | loose | El texto de ayuda de un campo o de una ventana. Nunca "pista" (Track) ni "consejo" (Tip) |
| Glossary | glosario | loose |  |
| Validation | validación | loose |  |
| Rules | reglas | loose |  |
| Format | formato | loose |  |
| Version | versión | loose |  |
| Desktop | escritorio | loose |  |
| Mobile | móvil | loose |  |
| Alignment | alineación | loose | Distinto de Placement ("colocación") |
| Align | alinear | loose |  |
| Center | centro | loose |  |
| Left | izquierda | loose |  |
| Right | derecha | loose |  |
| Top | arriba | loose |  |
| Bottom | abajo | loose |  |
| Horizontal | horizontal | loose |  |
| Vertical | vertical | loose |  |
| Linear | lineal | loose |  |
| Appearing | aparición | loose |  |
| Scissors | tijeras | loose |  |
| Edges | bordes | loose | Como en ru, dos sentidos: la herramienta que mueve los bordes de un tramo es "bordes", las aristas de una forma son "aristas" |
| Point | punto | loose |  |
| Continue | continuar | loose |  |
| Next | siguiente | loose |  |
| Back | atrás | loose |  |
| Loading | cargando | loose |  |
| Progress | progreso | loose |  |
| Statistics | estadísticas | loose |  |
| Preset | preset | loose | En inglés: "preajuste" contiene "ajuste" (Snapping) |
| Clipboard | portapapeles | loose |  |
| Console | consola | loose |  |
| Ping | localizar | loose | Mostrar algo en la vista, la línea de tiempo y la jerarquía |
| Override | sobrescritura | loose |  |
| Placement | colocación | loose |  |
| Template | plantilla | loose |  |
| Clip | clip | loose |  |
| Slip | deslizar contenido | loose | Como en ru: mover el contenido dentro de su tramo sin mover el tramo |
| Slot | ranura | loose |  |
| Beat Grid | cuadrícula de pulsos | loose |  |
| Bar | compás | loose | En música. La barra de progreso es "barra" |
| Tempo | tempo | loose |  |
| Tap Tempo | tempo por toques | loose |  |
| Stereo Pan | paneo estéreo | loose |  |
| Font Size | tamaño de fuente | loose |  |
| Word Wrap | salto de línea automático | loose |  |
| Backup | copia de seguridad | loose |  |
| Branch | rama | loose |  |
| Fit | encajar | loose | Nunca "ajustar", que es Snap |
| Finding | incidencia | loose | Lo que la validación encuentra en un nivel |
| Fix | corregir | loose |  |
| Group | grupo | loose |  |
| Id | ID | loose |  |
| Mipmap | mipmap | loose |  |
| Sampling | muestreo | loose |  |
| Tiling | mosaico | loose |  |
| Wrapping | fuera de los bordes | loose | Qué muestra una textura más allá de sus bordes, como en ru |
| Pixel art | pixel art | loose |  |
| Drawing | dibujo | loose |  |
| Emission Shape | forma de emisión | loose |  |
| Over Lifetime | durante la vida | loose |  |
| Forces | fuerzas | loose |  |
| Scatter | dispersión | loose |  |
| Spread | apertura | loose |  |
| Tangent | tangente | loose |  |
| Clamp | limitar | loose |  |
| Ping Pong | ida y vuelta | loose |  |
| Temperature | temperatura | loose |  |
| Tint | tinte | loose |  |
| Modifier Key | tecla modificadora | loose |  |
| Dead Zone | zona muerta | loose |  |
| Sensitivity | sensibilidad | loose |  |
| Stick | stick | loose |  |
| Shoulder | botón superior | loose |  |
| Gamepad | gamepad | loose | Ni "mando" ni "control": cada lado del Atlántico usa uno |
| Touchscreen | pantalla táctil | loose |  |
| Motion Sensor | sensor de movimiento | loose |  |
| Handedness | mano dominante | loose |  |
| Double Tap | doble toque | loose |  |
| Workshop | Workshop | loose | Como en Steam en español |
| Story | historia | loose |  |
| Wave | oleada | loose |  |
| Immortal | inmortal | loose |  |
| Dodge | esquiva | loose |  |
| Zen | zen | loose |  |
| Clears | completados | loose | Cuántas veces se ha superado un nivel |
| Hits | impactos | loose |  |
| Profile | perfil | loose |  |
| Frame Hierarchy | jerarquía del fotograma | loose | Sigue a Hierarchy ("jerarquía") y a Frame ("fotograma"), los dos strict |
| Stop Frame | fotograma de parada | loose |  |
| Runtime Seed | semilla de ejecución | loose |  |
| Level Logo | portada del nivel | loose | La imagen que se muestra en la lista de niveles |
| Post-processing effect | efecto de posprocesado | loose |  |
| Audio effect | efecto de audio | loose | "efecto" a secas es solo el objeto Effect |
| Chorus | chorus | loose |  |
| Compressor | compresor | loose |  |
| Distortion | distorsión | loose |  |
| Echo | eco | loose |  |
| Flange | flanger | loose |  |
| Highpass | paso alto | loose |  |
| Lowpass | paso bajo | loose |  |
| Normalize | normalizar | loose |  |
| Param EQ | EQ paramétrico | loose |  |
| Pitch Shifter | cambio de tono | loose |  |
| Reverb | reverberación | loose |  |
| Emitter | emisor | loose |  |
| Variant | variante | loose |  |
| Fader | fader | loose |  |
| Signal level | nivel de señal | loose | El "level" de las ayudas de efectos de audio. LocalizationGlossaryTests lo excluye |
| Swatch | muestra | loose |  |
| Device library | biblioteca compartida del dispositivo | loose |  |
| Collection | colección | loose | Carpeta de recursos reutilizables: prefabs, temas, formas, efectos, texturas, fuentes, audio. Nada que ver con las colecciones de Steam. Es loose porque "colecciones" pierde la tilde y no contiene "colección". La collection de las reglas de validación (una estructura de datos) no tiene por qué ser "colección", y LocalizationGlossaryTests excluye esas claves |
| Anti-aliasing | antialiasing | loose | En inglés. Nunca "suavizado", que es Ease |
| Overlay | superposición | loose |  |
| Scrub | arrastre | loose |  |
| Gradient stop | parada de color | loose |  |
| Link to a docs page | título de la página | loose | Un enlace a la documentación lleva el título en español de la página enlazada |
