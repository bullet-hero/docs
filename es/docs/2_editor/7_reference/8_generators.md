---
title: Generadores
date: 2026-10-12
tags: [level_author]
---

# Generadores

Un generador crea contenido y lo aplica al nivel en una sola operación que se deshace en un solo paso. Todos los generadores se ejecutan desde la ventana "Generadores" de la barra de herramientas

## Generadores

El formulario de un generador se construye a partir de sus propios campos. No hay una interfaz aparte para cada generador

> [!caution] Precaución
> Todo lo que reescribe o elimina contenido existente pide confirmación antes

> [!info] Conviene saber
> Hay dos familias. Los **generadores** (*gen_*) crean contenido: olas de balas, patrones radiales y una caché de fuentes. Los **modificadores** (*mod_*) cambian lo que ya existe: encajar tramos, cuantizar fotogramas clave. Los modificadores se describen aparte - [[9_modifiers]]

Más - [[2_reuse]]

## La ventana de generadores

Los generadores de contenido y los modificadores se ejecutan desde la ventana `{{ui:editor_generators_text}}` de la barra de herramientas. Su bloque `{{ui:editor_generators_base-parameters}}` lo comparten todos los generadores: `{{ui:editor_generators-start_frame}}`, `{{ui:editor_generators-end_frame}}`, `{{ui:editor_inspector_layer}}` y `{{ui:editor_generators_seed}}`. Pertenecen a la ventana, no a un generador concreto

Cómo se comporta el bloque:
- La ventana se abre con un segundo a partir del cabezal y la semilla en 0. `{{ui:editor_generators-seed_random}}` genera una semilla nueva
- Los fotogramas se quedan dentro de la línea de tiempo en la que trabajas, del fotograma 1 a su último fotograma. En el modo prefab es la longitud de la plantilla
- Editar `{{ui:editor_generators-start_frame}}` empuja `{{ui:editor_generators-end_frame}}` con él. Editar `{{ui:editor_generators-end_frame}}` se detiene en `{{ui:editor_generators-start_frame}}`. Nunca se cruzan
- `{{ui:editor_inspector_layer}}` se queda dentro del rango permitido de capas
- Cada campo de fotograma tiene una chincheta que lo sujeta al borde de la línea de tiempo. `{{ui:editor_generators-whole_level}}` fija las dos, y la ventana va del fotograma 1 al último fotograma. Los campos siguen siendo editables, y escribir en un campo quita la chincheta de ese borde

`{{ui:editor_generators_group}}` y `{{ui:editor_generators-split_layers}}` están activados de forma predeterminada. El grupo lleva el nombre del generador. Los dos afectan solo a los generadores de contenido: un modificador no crea nada, así que no hay nada que agrupar

El contenido generado nunca va debajo del objeto seleccionado. Cae en el nivel superior del ámbito o en su propio grupo

Antes de pulsar `{{ui:editor_generators_run}}`, la ventana muestra lo que añadirá la ejecución. El botón no está disponible, y en lugar de la estimación se escribe el motivo, si:
- el generador necesita el nivel entero y estás en el modo prefab. Son Destello de pulso, Caché de fuentes, Previsión de capacidad y Cambiar frecuencia de fotogramas
- el generador necesita una selección y no hay nada seleccionado
- después de la ejecución el nivel tendría más de 262 144 objetos
- un generador de contenido no añadiría nada. Un modificador no se rechaza por esto

Un generador que necesita datos externos (una pista de audio, pulsos, una imagen) no crea nada sin ellos, y la estimación lo dice

`{{ui:editor_generators_run}}` cierra la ventana. El contenido generado queda seleccionado, en el mismo paso de deshacer

La ventana recuerda en qué generador estabas y qué parámetros introdujiste cuando se cierra y se vuelve a abrir. `{{ui:editor_generators_reset}}` devuelve los valores predeterminados

## Niveles

El asistente de IA no puede ejecutar estos tres. En su lugar empieza un nivel nuevo con su propio `level_create`

### Nivel vacío

Vacía el nivel por completo. Todo lo creado se elimina.
Sirve para empezar de cero, no para editar

`Pin Screen Aspect` (activado de forma predeterminada) coloca un fotograma clave con un 16:9 fijo en la pista `{{ui:editor_events-timeline_track_screen-limit}}`, en el primer fotograma

Más - [[2_first-level]]

### Nivel desde archivo de audio

Empieza un nivel a partir de una pista.
Conecta el audio, encaja la longitud del nivel con la pista y te deja al inicio de una línea de tiempo vacía

`Pin Screen Aspect` (activado de forma predeterminada) coloca un fotograma clave con un 16:9 fijo en la pista `{{ui:editor_events-timeline_track_screen-limit}}`, en el primer fotograma

Más - [[2_preparing-the-track]]

### Importar archivo comprimido de nivel

Construye un nivel a partir de un archivo comprimido creado por este juego.
Formatos: `.tar.gz` y `.zip`. Los dos pueden estar protegidos con contraseña

El tipo de archivo se detecta por el contenido, no por el nombre. Un archivo comprimido con otro nombre se abre igual.
El juego reconoce `7z`, pero todavía no lo lee y lo rechaza

> [!tip] Consejo
> Un archivo comprimido de una build antigua se abre sin preparación. El propio juego lo convierte al formato actual al importarlo

> [!warning] Advertencia
> De forma predeterminada un nivel importado recibe un ID nuevo. Así no sobrescribe un nivel que ya está en este dispositivo. Desmarca esta casilla solo para restaurar un nivel que antes estaba en este dispositivo

## Balas

Más sobre todos los generadores de balas - [[1_readability-and-fairness]]

> [!caution] Precaución
> El `Collider` de un generador de balas está vacío de forma predeterminada. Sus balas dibujan un cuadrado y no pueden dañar al jugador hasta que eliges un colisionador, por ejemplo la misma forma que en `Shape`. Los demás generadores que colocan formas, los de geometría y Forma de onda, tienen el mismo campo con el mismo valor predeterminado

### Ola de balas

Una fila de balas que se mueven juntas.
El patrón básico, y por el que conviene empezar. Sus parámetros se repiten en los demás generadores de balas

### Espiral de balas

Las balas salen a lo largo de un rayo que gira. El resultado es el clásico muro en espiral

### Lluvia de balas

Las balas caen sobre una zona durante un tiempo fijado.
La densidad y la dispersión se pueden ajustar.
Dónde cae cada bala sale de la `{{ui:editor_generators_seed}}` de la ventana, no de la semilla del nivel. La misma semilla repite una ejecución exactamente, y una semilla distinta da otra distribución. El asistente de IA pasa su propia semilla, `0` salvo que indique otra, así que dos ejecuciones que deban ser distintas necesitan dos semillas

### Balas teledirigidas

Las balas se curvan hacia donde se espera que esté el jugador.
La trayectoria se calcula de antemano, no durante la partida. Por eso el resultado es el mismo en cualquier dispositivo

### Barrido láser

Un rayo atraviesa el campo.
El aviso y la fase que hace daño son objetos distintos. Así el aviso se puede mostrar y no mata.
El rayo de aviso nunca colisiona. El rayo que dispara solo hace daño con un `Collider` elegido

## Geometría

Más sobre todos los generadores de geometría - [[2_reuse]]

### Polígono

Coloca formas en los vértices o en las aristas de un polígono regular

### Radial

Coloca copias alrededor de un círculo. La base de la mayoría de los patrones simétricos

### Espiral

Coloca copias a lo largo de una espiral. El radio y el ángulo crecen a la vez

### Cuadrícula

Llena un rectángulo con copias de una forma a distancias iguales

### Fractal

Repite una forma dentro de sí misma, cada vez más pequeña.
La cantidad de objetos crece de forma exponencial con la profundidad. Sube la profundidad paso a paso

## Audio y efectos

### Forma de onda

Construye objetos a partir de la forma de una pista de audio. El nivel sigue a la vista lo que se oye

Más - [[2_reuse]]

### Destello de pulso

Pone un destello en cada pulso.
Los pulsos salen del mapa de pulsos del nivel. Si no hay mapa, de los marcadores.
Así parpadea exactamente lo que ves en la cuadrícula

Más - [[2_rhythm-and-structure]]

## Recursos y utilidades

### Objetos desde textura

Convierte una imagen en objetos, uno por celda.
La imagen pasa a ser contenido del nivel y se anima como todo lo demás

Más - [[3_images-and-fonts]]

### Caché de fuentes

Reúne todos los caracteres que usa el texto del nivel y los prepara de antemano.
Así ningún carácter se prepara en el momento en que se muestra por primera vez

> [!tip] Recomendación
> Ejecútalo cuando el texto esté terminado. Un carácter añadido más tarde sin volver a prepararlo provoca un tirón la primera vez que se muestra

Más - [[3_images-and-fonts]]

### Previsión de capacidad

Guarda los límites recomendados del nivel: cuántos objetos y efectos necesita a la vez

> [!info] Conviene saber
> No afecta a lo que se muestra. El juego reserva búferes para estos límites de antemano. Si no, los búferes crecerían en mitad del nivel, y eso provocaría un tirón

Más - [[1_level-budget]]
