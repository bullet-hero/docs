---
title: Glosario
date: 2026-10-15
tags: [level_author]
---

# Glosario

La lista principal de términos del proyecto. La interfaz del juego, esta documentación y cualquier otro texto sobre Bullet Hero usan estas palabras, y un término nuevo se añade aquí primero

## Contenido del nivel

| Término | Significado |
|---|---|
| **Nivel** | Todo lo que forma una partida: objetos, audio, eventos y sus propios recursos |
| **Objeto** | Un elemento creado por el autor en la línea de tiempo, con su propio tiempo de vida, transformación y padre |
| **Objeto vacío** | Un objeto que no dibuja nada: una transformación, un tiempo de vida e hijos. Cada uno de los demás tipos añade lo suyo encima |
| **Forma** | Geometría real que dibuja un objeto, no una imagen. El juego genera unas 500 por sí mismo |
| **Colisionador** | Con lo que choca un objeto. Puede no coincidir con lo que el objeto dibuja |
| **Prefab** | Una plantilla reutilizable de objetos que se coloca en un nivel tantas veces como haga falta |
| **Modo prefab** | Editar el contenido propio de una plantilla en lugar del nivel que la rodea |
| **Efecto** | Un emisor: cada fotograma crea sus propios objetos a partir de unos pocos parámetros |
| **Objeto de fotograma** | Un objeto creado por un efecto. Lo gestiona el motor: no se puede seleccionar ni editar |
| **Tema** | Una paleta a la que el nivel se refiere por índice: recolorear es un cambio, no cien |

## Tiempo y animación

| Término | Significado |
|---|---|
| **Fotograma** | La unidad de tiempo del nivel. Un fotograma es una celda, y el tiempo es el límite entre dos celdas |
| **Fotograma clave** | Un valor fijado por el autor en un fotograma. Entre dos fotogramas clave el valor se interpola |
| **Pista** | Una fila de fotogramas clave de una propiedad animable: posición, rotación, volumen |
| **Línea de tiempo** | El eje de fotogramas sobre el que se crea el nivel: una pestaña por cada tipo de contenido |
| **Tramo** | Cuándo existe un objeto: un fotograma inicial y una duración, pero no un fotograma final |
| **Cabezal** | El fotograma que se muestra ahora mismo |
| **Suavizado** | Cómo pasa un valor del fotograma clave anterior a este |
| **Marcador** | Un punto con nombre en la regla del nivel, para volver al sitio exacto |
| **Checkpoint** | Adonde una muerte devuelve al jugador |

## Colocación y dibujo

| Término | Significado |
|---|---|
| **Ancla** | Un borde que sigue al borde del padre: si encoges el padre, el hijo se mueve con él |
| **Capa** | El orden de dibujo, y es relativo: la capa del hijo se suma a la capa del padre |
| **Pivote** | El punto sobre el que un objeto gira y escala, dentro de su propio recuadro |
| **Gizmo** | Las asas de arrastre dibujadas sobre el objeto seleccionado en la vista |
| **Ajuste** | Atraer un arrastre hacia algo: hacia el contenido con el imán, hacia la música con el interruptor de pulso |

## Música

| Término | Significado |
|---|---|
| **Pulso** | La rejilla propia de la música: la fija el autor y nada la lee durante el juego |
| **Segmento de pulso** | Una parte de tempo constante con su propio tempo, fase y longitud de compás |
| **BPM** | Pulsos por minuto - lo rápido que avanza un segmento de pulso |
| **Toque** | Una pulsación mientras marcas el tempo. Con suficientes toques queda descrito un segmento de pulso |

## Automatización y datos

| Término | Significado |
|---|---|
| **Generador** | Automatización de la creación: produce contenido del nivel a partir de unos pocos parámetros |
| **Modificador** | Un generador que edita o elimina lo que ya existe en lugar de añadir |
| **Semilla** | El número del que sale cada valor aleatorio del nivel: una partida se repite exactamente igual |
| **Datos sin procesar** | Todo el modelo guardado como un árbol editable. Aquí no se comprueba nada, y es a propósito |
| **Asistente de IA** | Un cliente de IA conectado al editor por MCP. Edita el nivel abierto mientras tú miras, un paso de deshacer por lote |

## Recursos y compartir

| Término | Significado |
|---|---|
| **Biblioteca** | Recursos en el dispositivo para reutilizar entre niveles: tu biblioteca, tus colecciones y aquellas a las que te has suscrito |
| **Colección** | Una carpeta de recursos reutilizables de hasta siete tipos. Importar copia desde ella, así que el nivel no depende de ella |
| **Dificultad** | Lo difícil que es un nivel: un número que fija el autor y que un moderador puede sobrescribir. El jugador lo ve como un grado, de `{{ui:enum_difficulty-tier_auto}}` a `{{ui:enum_difficulty-tier_singularity}}` |
