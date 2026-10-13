---
title: Efectos
date: 2026-10-01
tags: [level_author]
---

# Efectos

Un efecto son partículas de VFX Graph cuyos parámetros se dividen en módulos: cuántas partículas hay, desde dónde salen, cómo se mueven, de qué color y tamaño son. Se editan en el inspector o en el editor de efectos

## Inspector de efecto

Muestra los parámetros de un efecto `VFX Graph` por grupos: configuración, núcleo, fuerzas, forma, ángulo, escala y color. Todos los grupos se ven a la vez

> [!info] Conviene saber
> Los efectos **toman su semilla igual que todo lo demás**: de los números que editas, no del estado de un generador. Por eso el nivel se reproduce igual en cualquier dispositivo

> [!tip] Consejo
> Los colores pueden referirse al tema del nivel en lugar de a un valor fijo. Los tipos de degradado abren el editor de degradados compartido

Más: [[1_level-budget|El presupuesto del nivel]]

## Principal - cuántas partículas y durante cuánto tiempo

Fija cuántas partículas existen, cuánto viven y con qué se dibujan. Es todo lo que vale antes de la primera fuerza. La otra mitad es [[6_effects#Fuerzas - qué mueve una partícula|Fuerzas]]

`Cantidad de partículas` es el principal mando del coste. Es exactamente el número que cuenta la ayuda de capacidad del nivel

Un emisor cuesta aproximadamente su cantidad por su tiempo de vida. Duplicar `Límites del tiempo de vida` cuesta lo mismo que duplicar la cantidad

`Forma` es la silueta de cada partícula, del mismo conjunto que usan los objetos normales. `Textura` es la imagen encima de ella. Los dos campos pueden estar vacíos. Una partícula sin textura es el caso normal y barato

> [!warning] Advertencia
> La cantidad tiene un tope de 1024. Es la capacidad del propio grafo. Un grafo de VFX procesa toda su CAPACIDAD en cada fotograma, no solo las partículas vivas. Así que un sistema cuesta lo que pidió, aunque necesite menos

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todos los campos a su valor predeterminado en un solo paso de deshacer

Más: [[1_level-budget|Lo que un nivel se puede permitir]]

## Configuración - cuándo se calla el emisor

Fija cuándo deja de generar partículas el emisor. Si está desactivado, genera mientras vive el objeto. Es el caso normal: la ráfaga termina junto con el objeto

`Fotograma de parada` cuenta desde el inicio del tramo propio del OBJETO, no desde la línea de tiempo del nivel. Así que un efecto al final de un nivel puede callarse trescientos de sus propios fotogramas después

Las partículas que ya están vivas terminan su vida. La emisión se corta, y la imagen se desvanece con suavidad

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve los dos campos a su valor predeterminado en un solo paso de deshacer

Más: [[1_level-budget|Lo que un nivel se puede permitir]]

## Ángulo - rotación de la partícula

Fija cómo gira una partícula a lo largo de su vida. Hay cinco variantes:
- `Valor` - un ángulo fijo
- las dos variantes `Curvas` leen una curva
- las dos variantes `Aleatorio` sortean un valor entre A y B para cada partícula

Qué filas existen depende de la elección. Las dos variantes con curva se diferencian en POR QUÉ se lee la curva:
- `Curvas durante la vida` - por el tiempo de vida de la partícula
- `Curvas por velocidad` - por la velocidad de la partícula, a través de la ventana de velocidades de abajo

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todo el grupo a sus valores predeterminados, `Tipo` incluido. Se pierde la curva o el par aleatorio que configuraste

Más: [[1_readability-and-fairness|Legibilidad]]

## Color - color de la partícula

Fija cómo se colorea una partícula a lo largo de su vida. Seis variantes: las mismas cinco que [[6_effects#Ángulo - rotación de la partícula|Ángulo]] y [[6_effects#Escala - tamaño de la partícula|Escala]], solo que con degradados en lugar de curvas, más un `Degradado aleatorio`:
- `Degradado durante la vida` lee el degradado por el tiempo de vida de la partícula
- `Degradado por velocidad` lo lee por la velocidad de la partícula
- `Degradado aleatorio` toma un color del degradado por partícula en lugar de recorrerlo
- las dos variantes `Aleatorio` de abajo sortean un color entre dos colores

> [!tip] Consejo
> Un color aquí puede ser una referencia al tema, como en cualquier otro sitio del nivel. Así el efecto sigue a un nivel que cambia su paleta por el camino

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todo el grupo a sus valores predeterminados, `Tipo` incluido. Se pierde el degradado o el par de colores que configuraste

Más: [[5_color-and-postprocessing|Color y temas]]

## Escala - tamaño de la partícula

Fija el tamaño de una partícula a lo largo de su vida. Las mismas cinco variantes que [[6_effects#Ángulo - rotación de la partícula|Ángulo]]: un tamaño fijo, una curva o un rango por partícula

Aquí hay dos curvas, porque el tamaño tiene dos ejes. `Curve X` y `Curve Y` se leen por separado. Una partícula puede estirarse y encogerse a la vez

> [!warning] Advertencia
> La fila bajo las curvas se REUTILIZA. Con `Valor` y las dos variantes `Aleatorio` es el tamaño en sí. Con `Curvas por velocidad` es la ventana de velocidades. La etiqueta de al lado y su ayuda dicen qué es la fila en cada momento

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todo el grupo a sus valores predeterminados, `Tipo` incluido. Se pierden las dos curvas y el par aleatorio

Más: [[1_readability-and-fairness|Legibilidad]]

## Forma - desde dónde salen las partículas

Fija el volumen de aparición: un punto, un anillo, un rectángulo, un segmento, un cono o un toro. Solo decide dónde EMPIEZA una partícula. Lo que le pasa después es cosa de [[6_effects#Fuerzas - qué mueve una partícula|Fuerzas]]

Cambiar `Tipo` cambia el conjunto de campos de abajo. Las filas se reutilizan: la primera es el radio de un círculo, el radio superior de un cono o el radio menor de un toro, según lo que esté seleccionado

`Arco` es cuánto del borde se usa, en radianes, en sentido antihorario desde el eje +X. Menos de una vuelta completa da un abanico

> [!tip] Consejo
> `Apertura` convierte un anillo estático en uno que se mueve. Decide en qué punto del borde cae la siguiente partícula: al azar, dando vueltas en un sentido, de ida y vuelta o siguiendo un seno. `Bucle` es el clásico emisor giratorio

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve todo el grupo a sus valores predeterminados, `Tipo` incluido. Se pierde la forma que configuraste, con sus radios y su apertura

Más: [[4_composition-and-camera|Composición]]

## Fuerzas - qué mueve una partícula

Fija todo lo que mueve una partícula después de aparecer. [[6_effects#Forma - desde dónde salen las partículas|Forma]] decide dónde empieza, y este grupo decide hacia dónde vuela

Los campos son de dos tipos. Confundirlos es el error habitual:
- los pares de campos iniciales (`inicial` en el nombre) se sortean UNA vez cuando nace una partícula, entre su mínimo y su máximo. Separa los valores de un par y una ráfaga uniforme se convierte en un abanico
- todo lo demás actúa de forma CONTINUA durante toda la vida de la partícula

Campos del segundo tipo:
- `Velocidad lineal` es viento, no un empujón
- `Fuerza lineal` es una aceleración, así que se acumula
- `Velocidad orbital` hace girar las partículas alrededor del centro, no sobre sí mismas

> [!tip] Consejo
> `Velocidad de movimiento` multiplica todo el resultado. Así un efecto terminado se puede ralentizar o acelerar sin tocar los demás campos

> [!info] Conviene saber
> El **restablecimiento** junto a este botón devuelve los once campos a su valor predeterminado en un solo paso de deshacer

Más: [[4_composition-and-camera|Composición]]

## Editor de efectos

Construye un efecto de partículas y lo muestra en el lienzo

> [!info] Conviene saber
> Los grupos de parámetros son los mismos que en el inspector de efecto. Aquí se editan como **borrador**: nada llega al nivel hasta que guardas

> [!tip] Consejo
> Guarda el efecto en la biblioteca compartida del dispositivo para usarlo en otros niveles

Más: [[1_level-budget|El presupuesto del nivel]]
