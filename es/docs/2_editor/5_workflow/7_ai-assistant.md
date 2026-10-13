---
title: Asistente de IA
date: 2026-10-13
tags: [level_author]
---

# Asistente de IA

Un cliente de IA compatible con MCP puede editar el nivel abierto en el editor mientras lo ves. Cada lote de la IA es un solo paso de deshacer, y la IA no puede publicar, eliminar archivos ni escribir sobre otro nivel

El juego en Windows, Linux y Mac incluye un servidor MCP para esto. La IA edita con las mismas operaciones que tú, así que cada cambio aparece en la vista al instante y entra en el historial como uno tuyo

Sirve cualquier cliente compatible con MCP, como una aplicación de chat o un asistente de programación. Nada en el juego está atado a una sola IA

## Conectar un cliente

1. Abre `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}`
2. Marca `{{ui:settings_game-editor_mcp-enabled}}`. La línea de estado bajo la configuración muestra el puerto en el que escucha el editor
3. Haz clic en `{{ui:settings_game-editor_mcp-copy-config}}`. Ahora el portapapeles contiene la configuración del cliente con las dos rutas ya rellenadas
4. Pégala en la configuración de servidores MCP de tu cliente
5. Abre un nivel en el editor, o pide a la IA que abra ella misma el editor o un nivel

La configuración copiada tiene este aspecto:

```json
{ "mcpServers": { "bullet-hero": { "command": "<path to BH.MCP>", "args": ["--endpoint", "<path to endpoint.json>"] } } }
```

El archivo del servidor `BH.MCP` está junto al juego:

| Sistema | Archivo del servidor |
|---|---|
| Windows | `<game folder>/BH.MCP.exe` |
| Linux | `<game folder>/BH.MCP` |
| Mac | `<game>.app/Contents/Resources/mcp/osx-arm64/BH.MCP`, en Intel `osx-x64` en lugar de `osx-arm64` |

Solo se puede conectar este equipo, y solo un cliente a la vez.
Los teléfonos y las tabletas no tienen la sección MCP: el asistente es solo para escritorio

Pueden ejecutarse varias copias del juego a la vez. La IA trabaja en la última que se inició hasta que le pidas cambiar, y puede listarlas todas. Cada copia sigue admitiendo un solo cliente. Para varias copias, deja `{{ui:settings_game-editor_mcp-port}}` en `0`, ya que dos copias no pueden escuchar en el mismo puerto

## Qué puede y qué no puede hacer la IA

La IA puede hacer casi todo lo que puedes hacer tú:
- leer el nivel: la jerarquía, los objetos, los fotogramas clave, los eventos y los recursos
- crear, cambiar y eliminar objetos, fotogramas clave, marcadores, checkpoints, pistas de audio y la cuadrícula de pulsos
- ejecutar generadores, empaquetar y colocar prefabs, trabajar dentro del modo prefab
- importar al nivel un archivo de textura, fuente o audio
- rellenar el registro de atribución de un archivo de textura, fuente o audio después de importarlo: título, descripción, enlace, orígenes y autores - [[4_resource-record]]
- usar los temas, las fuentes y los sonidos de interfaz predefinidos del propio juego. `resources_list` los marca como del juego, y no hace falta importarlos. El juego no incluye efectos predefinidos: un efecto que coloca la IA es uno que el nivel ya contiene o uno nuevo que ella crea
- dibujar cualquier contorno como forma del nivel a partir de sus esquinas, colorear una forma con un degradado, fijar la fuente y la alineación de un texto, crear y editar los temas del nivel
- deshacer y rehacer, guardar el nivel abierto, abrir otro nivel, crear uno nuevo
- iniciar y pausar la reproducción, como tu botón de reproducir
- llevar el juego a otra pantalla, como el editor, un nivel o la configuración, con los mismos argumentos que acepta un inicio - [[12_launch-arguments]]
- iniciar el juego cuando no está en marcha, si el servidor está junto al juego instalado y MCP ya está activado

Una partida iniciada así cuenta en tus estadísticas como cualquier otra, así que la IA solo inicia una cuando se lo pides

No puede:
- publicar en Steam Workshop
- eliminar un nivel ni ningún archivo
- escribir sobre otro nivel u otro archivo. Una importación cuyo nombre de archivo ya está ocupado se rechaza
- abrir un nivel de solo lectura, ni un nivel protegido cuya contraseña no hayas introducido en esta sesión
- abrir otro nivel mientras el abierto tiene cambios sin guardar

**Un lote de la IA es un paso en el historial.** Aparece en la pestaña `{{ui:settings_level-settings_history}}` como `{{ui:op_group_ai-batch}}`, con el título que le puso la IA. Un solo `Ctrl+Z` quita el lote entero. Más sobre el historial - [[10_level-settings#Historial]]

**La IA nunca pone dos objetos en la misma capa mientras los dos se reproducen.** Si un lote lo hiciera, sube el objeto posterior a la siguiente capa libre en el mismo paso y lo indica. El contenido de un prefab es la excepción: puede compartir capas con el resto del nivel

El primer lote de la IA que cambia un nivel pone su `{{ui:settings_level-settings_metadata-level-ai-generated}}` en `{{ui:enum_ai-generation_yes}}`, dentro del mismo paso. Deshacer el lote también lo revierte. Más - [[2_metadata-and-sharing#Generación con IA]]

## Tú tienes prioridad

La IA nunca te disputa el editor:
- mientras arrastras un asa del gizmo o recorres la línea de tiempo con el cabezal, las ediciones de la IA se rechazan, y ella espera y vuelve a intentarlo
- la IA toma el cabezal solo cuando no haces nada: no reproduces, no arrastras, no escribes, no guardas
- el editor empieza a reproducir un nivel al abrirlo, así que la IA puede pausarlo para mirar fotogramas. Un nivel que la IA abre o crea ella misma se queda en pausa. Si estás viendo la reproducción a propósito, la IA pregunta antes de pausar
- si tocas el editor mientras la IA mira un fotograma, la IA se detiene al instante. El cabezal se queda donde lo pusiste
- mientras se recorre el historial, la IA tampoco puede editar

Mientras hay un cliente conectado, la vista muestra `AI` en su esquina superior derecha, bajo los botones de búsqueda. Su color es el estado: verde - conectado, ámbar - la IA está trabajando, rojo - la última llamada de la IA terminó en error.
Después de que el cliente se desconecta, el indicador se mantiene {{v:mcp.badge-hold-seconds}} segundos, para que una IA que se reconecta en cada paso no parpadee. Se oculta junto con las herramientas de la vista.
Pasa el cursor por encima para leer el estado en palabras: `{{ui:editor_agent-badge_connected}}` y, mientras la IA trabaja, el título de lo que está haciendo.
La cruz de al lado desconecta el cliente y lo rechaza, y el indicador desaparece

Una detención no se guarda. Desactivar y volver a activar `{{ui:settings_game-editor_mcp-enabled}}` o reiniciar el juego la anula

## Qué ve la IA

La IA mira el nivel de dos maneras:
- **un esquema.** Una imagen de cualquier fotograma, calculada fuera de la pantalla. No mueve el cabezal. Muestra formas y hitboxes, pero ni textos ni efectos
- **una captura.** Píxeles reales, exactamente como se dibuja el nivel, tomados a través de tu cabezal. Por un momento el cabezal salta a ese fotograma y las superposiciones del editor se ocultan. Después el cabezal vuelve a donde lo dejaste, salvo que `{{ui:settings_game-editor_mcp-follow-ai}}` esté activado. La imagen la encuadra la cámara del nivel, no la cámara del editor. Para ver un detalle de cerca, la IA puede encuadrar en su lugar un rectángulo del mundo. El nivel no cambia

Una imagen fija de un efecto tras un salto se parece a lo que muestra la reproducción continua, pero no siempre es idéntica

La IA no puede oír la música. Convierte la pista en números: tempo, pulsos, compases, secciones, el volumen de cada banda.
Es una estimación con un grado de confianza, y puede equivocarse, por ejemplo dar la mitad o el doble del tempo. La cuadrícula de pulsos que fijaste en el nivel tiene prioridad sobre la estimación de la IA.
Una cuadrícula de pulsos que la IA propone a partir del análisis redondea al número entero un tempo que esté a menos del 0,01 % de él, y su desplazamiento siempre es más corto que un compás. Una propuesta sobre una parte de la pista toma el tempo propio de esa parte, así que una pista cuyo tempo cambia recibe un segmento por cada tempo

Así que, cuando la sincronización importa, la IA puede pedirte que escuches. Reproduce en el editor un fragmento de hasta {{v:mcp.max-play-seconds}} segundos, y eso también mueve el cabezal. Toca el editor y la reproducción se detiene donde esté

Mientras el sonido del editor está silenciado, la IA no reproduce nada y te pide que actives el sonido

Las propias acciones de la IA no hacen sonidos de interfaz: un deshacer, un guardado o un rechazo que ella causa es silencioso. Solo se oye lo que reproduce a propósito

## La carpeta ai

La IA guarda su memoria del nivel en la carpeta `ai`, dentro de la carpeta del nivel. La siguiente sesión, con cualquier cliente, la lee primero y continúa donde se quedó la anterior

Qué hay ahí:
- `CONTEXT.md` - el encargo, la música, el plan de secciones, las decisiones, tus observaciones y las preguntas abiertas
- otros archivos que la IA decida guardar, solo `.md` o `.json`
- `manifest.json` - si la carpeta viaja con el nivel. La IA no puede cambiarlo

La carpeta solo aparece cuando la IA tiene algo que escribir por primera vez. Un archivo admite hasta {{v:mcp.ai-file-max-kb}} KB, la carpeta entera hasta {{v:mcp.ai-folder-max-mb}} MB. Son archivos de texto normales: puedes leerlos, editarlos o eliminarlos tú

> [!warning] Advertencia
> La carpeta `ai` no forma parte del historial del nivel. `Ctrl+Z` no deshace lo que la IA escribió ahí

**La carpeta viaja con el nivel por defecto**: en un archivo comprimido exportado y en una subida a Steam Workshop. Para dejarla en casa, desmarca `{{ui:settings_level-settings_metadata-level-ai-share}}` en la pestaña `{{ui:settings_level-settings_metadata}}` de la configuración del nivel. La casilla aparece cuando la carpeta ya existe. Se guarda en un archivo al instante, así que `Ctrl+Z` tampoco la revierte

Un modo de exportación con contraseña nunca lleva la carpeta, diga lo que diga la casilla. Más - [[13_export-and-protection#Exportar el nivel]]

Una copia del nivel en este dispositivo se lleva la carpeta, porque una copia no es compartir

## Configuración

Todas las opciones están en `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}` y se guardan solo en este dispositivo:
- `{{ui:settings_game-editor_mcp-enabled}}` - si un cliente se puede conectar en absoluto. Desactivado por defecto
- `{{ui:settings_game-editor_mcp-port}}` - el puerto en el que escucha el editor. `0` elige uno libre en cada inicio
- `{{ui:settings_game-editor_mcp-follow-ai}}` - activado: después de una captura, el cabezal se queda en el fotograma que miró la IA, en pausa
- `{{ui:settings_game-editor_mcp-reveal-edits}}` - después de cada edición de la IA, selecciona y localiza lo que creó o cambió
- `{{ui:settings_game-editor_mcp-operation-delay}}` - cuánto espera el editor entre dos operaciones de la IA, para que puedas seguirlas. `0` aplica cada una al instante

Cada opción y su valor predeterminado - [[14_editor-settings#Agente de IA]]

A continuación: [[4_not-losing-work]], [[13_export-and-protection]]
