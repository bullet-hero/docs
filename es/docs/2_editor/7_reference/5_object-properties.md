---
title: Propiedades del objeto
date: 2026-10-12
tags: [level_author]
---

# Propiedades del objeto

El inspector de objeto edita los campos del objeto seleccionado, el inspector de fotograma clave edita los fotogramas clave seleccionados, en todas las pistas que toca la selección a la vez

## Inspector de objeto

Muestra los campos del objeto seleccionado. Todos los tipos tienen los campos comunes de un objeto vacío. Shape, Effect, Text y Prefab añaden los suyos debajo

`{{ui:field_common_active}}` desactiva tanto el dibujo *como* la colisión. Los hijos lo heredan. Un objeto oculto aquí no puede matar al jugador

> [!caution] Precaución
> `{{ui:editor_inspector_layer}}` se fija respecto al padre, no de forma absoluta. A su lado está la capa global, de solo lectura. Esa es la que usa el renderizado: tu capa más las capas de todos los antepasados

> [!tip] Consejo
> Editar un campo de un objeto que viene de un prefab guarda una **sobrescritura de instancia**. La casilla de al lado muestra la sobrescritura y la revierte

El botón del padre muestra de qué cuelga el objeto, `{{ui:editor_inspector-parent_btn}}` incluido. Abre la ventana `{{ui:editor_picker_select-parent}}`: todos los objetos del ámbito, con opciones fijas arriba:
- en el nivel - `{{ui:editor_inspector-parent_btn}}` y `{{ui:editor_search-option_camera}}`. `{{ui:editor_search-option_camera}}` es la cámara del nivel, y su hijo se mueve con ella
- dentro de una plantilla de prefab - una fila `{{ui:editor_search-option_prefab-root}}`. Significa a la vez "sin padre" y la raíz de la plantilla: ahí son lo mismo. La cámara y el jugador no pueden ser padres dentro de una plantilla

Un padre reservado se muestra con su ID: `Cámara (-1)`, `Jugador local (-2)`, `Raíz del prefab (-3)`. El asistente de IA solo puede usar la cámara (-1) y, dentro de una plantilla, la raíz (-3)

El botón de al lado selecciona el padre. En un objeto del nivel superior de una plantilla selecciona la raíz de la plantilla. No está disponible cuando hay varios objetos seleccionados ni cuando no hay nada que seleccionar: no hay padre, o el padre es la cámara o el jugador

Una pestaña del panel derecho que no tiene nada que mostrar se oculta. Si la pestaña abierta se queda vacía, el panel cambia a la primera pestaña que tenga algo. Si todas las pestañas están vacías, el panel dice `{{ui:editor_right-panel_placeholder}}`

Más: [[3_how-the-editor-thinks|Cómo funciona el editor]]

## Inspector de fotograma clave

Muestra los fotogramas clave seleccionados. **Se ven a la vez todas las pistas que toca la selección**, no solo la última en la que hiciste clic.
Una selección puede contener fotogramas clave de posición y de rotación, fotogramas clave de objetos distintos, y fotogramas clave de objetos, de audio y de eventos juntos

> [!tip] Consejo
> La opción `{{ui:enum_search-domain_ease}}` actúa sobre todas las pistas a la vez y ocupa **un solo paso de deshacer**. Una selección de posición y rotación cambia en una operación, no en dos

> [!info] Conviene saber
> El campo `{{ui:editor_frame-key-view_key-frame}}` se bloquea cuando hay varios fotogramas clave seleccionados. En una pista cada fotograma es único. Un solo número para todos los fotogramas clave los fundiría en uno y borraría el resto sin avisar. Para mover varios fotogramas clave a la vez, arrástralos en la línea de tiempo

Un valor en blanco significa que los fotogramas clave seleccionados **difieren** en él

Más: [[3_how-the-editor-thinks|Cómo funciona el editor]]

## Tramo

Fija cuándo existe el objeto. El rango es semiabierto: el fotograma inicial está dentro, el final no.
Un objeto que termina en 20 y un objeto que empieza en 20 nunca se dibujan los dos en ese fotograma

> [!info] Conviene saber
> **El tramo de un hijo debe estar dentro del de su padre. Eso se resuelve al leer y nunca se guarda.** Encoge el padre y los hijos se recortan, pero lo que está escrito aquí no cambia. Vuelve a estirarlo y todo regresa. Un objeto raíz más allá del final del nivel son datos válidos, simplemente no se reproduce

> [!info] Conviene saber
> **Las anclas** significan "este borde sigue al borde del padre", y deciden qué se reproduce. Un borde anclado se sitúa en el borde del padre, así que un hijo anclado se estira junto con un padre que crece. Su animación conserva los tiempos que fijó el autor

La longitud de una colocación de prefab viene de la plantilla de forma predeterminada, pero se puede escribir como cualquier otra. Un valor distinto guarda una sobrescritura de esta colocación. La casilla junto al tramo la muestra y devuelve la longitud de la plantilla

La raíz de una plantilla de prefab no tiene bloque de tramo. En su lugar hay una fila `{{ui:editor_prefab-mode-frame_length}}`: la longitud de toda la plantilla, el mismo valor que `{{ui:editor_prefab-mode-frame_length}}` en la pestaña `{{ui:field_common_prefab}}`. `{{ui:field_common_active}}` y `{{ui:editor_inspector_layer}}` de la raíz son de solo lectura, y la raíz no se puede eliminar ni recibir un padre

Más: [[4_frames-and-time|Fotogramas, tiempo y duración de un nivel]]

## Suavizado

Fija cómo llega el valor a este fotograma clave desde el anterior

> [!info] Conviene saber
> El suavizado pertenece al lado **entrante** de un fotograma clave. Fija el trecho desde el fotograma clave anterior hasta este, y así es exactamente como lo lee la reproducción. Por eso en el primer fotograma clave de una pista el suavizado no tiene efecto

> [!tip] Consejo
> Si hay varios fotogramas clave seleccionados, la opción se aplica a todos a la vez en **un solo paso de deshacer**. Incluso si los fotogramas clave están en pistas distintas y pertenecen a objetos distintos. Una opción en blanco significa que los fotogramas clave seleccionados difieren

Más: [[5_keyframes-and-easing]]

## Capa

Fija el orden de dibujo **respecto al padre**, no de forma absoluta. Una capa resultante más alta se dibuja delante. De dos formas en la misma capa resultante, la más nueva (el ID más alto) se dibuja detrás

> [!caution] Precaución
> El renderizado usa este número más las capas de todos los antepasados. La suma se muestra, de solo lectura, en el campo `{{ui:editor_inspector-global_layer}}` de abajo. Por eso la misma capa significa cosas distintas bajo padres distintos. Cambiar el padre cambia dónde se dibuja el objeto

> [!info] Conviene saber
> La capa también participa en la aleatoriedad. Un valor aleatorio está ligado a la capa resultante, así que mover un objeto en la jerarquía cambia los números que le salieron. Dos objetos con la misma capa resultante Y el mismo fotograma inicial obtienen los mismos números

Más: [[3_how-the-editor-thinks|Cómo funciona el editor]]

## Forma

Fija lo que el objeto **dibuja**

> [!info] Conviene saber
> Una forma es geometría real, no una imagen. Se encaja en su recuadro, y su lado largo mide exactamente 1. Por eso el recuadro del objeto es exactamente lo que se ve en pantalla

> [!info] Conviene saber
> El juego genera unas 500 formas a lo largo de cuatro ejes: figura, sector, grosor e inversión. Un nivel puede añadir las suyas. Un valor vacío es válido: un objeto sin imagen pero con hitbox es una pared invisible

Más: [[1_readability-and-fairness|Legibilidad y justicia]]

## Colisionador

Fija con qué **choca** el objeto. Es una elección aparte y no depende de lo que dibuja el objeto

> [!info] Conviene saber
> Lo uno no se deriva de lo otro a propósito. Un rayo de aviso inofensivo, un hitbox más simple que la imagen y una pared invisible son contenido normal, no trucos

> [!tip] Consejo
> Los dos campos eligen de las mismas dos colecciones. Una forma que creó el nivel sirve para cualquiera de los dos

En los modos de visualización de hitboxes, un objeto sin colisionador no dibuja nada, y tampoco un objeto inactivo. Así se distingue la decoración del peligro. Cómo se dibujan se fija en [[14_editor-settings]]

Más: [[1_readability-and-fairness|Legibilidad y justicia]]

## Tipo de shader

Fija por qué camino se renderiza el objeto

> [!caution] Precaución
> `{{ui:enum_shader-type_auto}}` decide una sola vez, cuando se carga el nivel. La regla es estricta: el aspecto del nivel no debe cambiar. Todo lo que no se puede demostrar opaco pasa a ser transparente. No se tiene en cuenta la geometría, solo el alfa

> [!tip] Consejo
> La etiqueta de al lado muestra en qué se resolvió de verdad `{{ui:enum_shader-type_auto}}`. Se lee directamente de los datos de renderizado, no se vuelve a calcular. Así la etiqueta no puede contradecir lo que hay en pantalla

Más: [[1_level-budget|El presupuesto del nivel]]

## Valores actuales

Muestra lo que los objetos seleccionados **son** en el fotograma actual, no lo que escribiste en ellos. Cada número se lee de la simulación en marcha. Por eso coincide con lo que se ve en la vista

El cuadrado al final de una fila es el estado de fotograma clave de ese campo:
- azul - hay un fotograma clave en este fotograma. Hacer clic en el cuadrado lo selecciona
- ámbar - el fotograma está entre dos fotogramas clave, el valor se interpola
- gris - la pista tiene fotogramas clave, pero el fotograma está fuera de ellos. El valor se mantiene
- hueco - la pista está vacía, el campo toma el valor predeterminado del motor

Las flechas llevan el cabezal al fotograma clave anterior o siguiente de esa pista

Una fila UV se lee como dos pares: primero el mosaico, luego el desplazamiento

Debajo de la línea van los valores compuestos: la capa sumada, la actividad heredada y la transformación con los padres tenidos en cuenta. Ningún fotograma clave los fija, así que no tienen indicador

> [!info] Conviene saber
> Una pista de fotogramas clave vacía son datos válidos, no datos que faltan. Significa que el objeto usa el valor predeterminado de ese campo

> [!info] Conviene saber
> En el modo prefab esta sección está oculta. Una plantilla no reproduce sus propios fotogramas, así que no hay nada que mostrar en un fotograma
