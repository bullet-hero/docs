---
title: Recursos del nivel
date: 2026-10-12
tags: [level_author]
---

# Recursos del nivel

Las texturas, formas, temas, efectos y prefabs de un nivel viven en su carpeta y viajan con él. Cada recurso tiene su propia ficha con su origen, licencia y autores

## Biblioteca

Recursos guardados en **este dispositivo**. Los comparten todos los niveles que abres aquí

Importar copia el recurso *dentro del nivel*.
Un nivel es una carpeta de archivos, y lleva consigo todo lo que necesita. Eso es lo que lo mantiene portátil

Así que la biblioteca es una comodidad para ti. Quien juega tu nivel nunca depende de ella

La biblioteca muestra tres orígenes, cada uno como un chip: `{{ui:editor_library-source_library}}`, `{{ui:editor_library-source_local}}` y, en una compilación de Steam, `{{ui:editor_library-source_workshop}}`.
Elegir una entrada la importa con sus dependencias. Si el nivel ya tiene otra versión, el juego pregunta cuál conservar

Más - [[16_library-and-collections]], [[2_reuse]]

## Texturas

Imágenes que lleva este nivel.
**El juego en sí no trae ninguna textura.** Cada textura que usa un nivel se añadió aquí

Un nivel es solo una carpeta de archivos. Una textura vive en ella y viaja con el nivel: comprime la carpeta, envíala, descomprímela y juega

Las formas **no** son texturas, son geometría real. No necesitan nada de esta pestaña

Más - [[3_images-and-fonts]]

## Formas

Las formas propias del nivel. Se suman a las ~500 formas que genera el juego

Una forma es **geometría real**, no una imagen.
El rectángulo del objeto es el recuadro de la forma, y los dos tipos de forma se colocan en él de manera distinta:
- **una forma integrada conserva sus proporciones.** Su lado más largo ocupa el rectángulo, así que un `Triangle` de tamaño (2, 2) se dibuja con 2 de ancho y unos 1.73 de alto
- **una forma que define el nivel se estira al rectángulo** tal como se dibujó en su recuadro. Un contorno que da el asistente de IA se encaja en el recuadro, así que llena el rectángulo exactamente

> [!tip] Consejo
> **Una forma y una hitbox son el mismo tipo de dato.** Un objeto lleva dos referencias: una para lo que se dibuja y otra para lo que recibe el golpe. Ninguna se deriva de la otra. Así que un rayo de aviso inofensivo, una hitbox más simple que su dibujo y una pared invisible son contenido normal

Más - [[1_level-needs]]

### Nombres de las formas integradas

El nombre de una forma integrada se compone de partes, siempre en este orden. `Circle_S2_T8_I` es la mitad derecha de un círculo, como un anillo de 1/8 del radio de grosor, invertida

| Parte | Significado |
|---|---|
| forma | `Square`, `Circle`, `Triangle`, `RightTriangle` o un polígono regular: `Pentagon`, `Hexagon` y así sucesivamente |
| `S2`, `S4`, `S8` | un sector: una mitad, un cuarto, un octavo. Empieza recto hacia arriba y avanza en el sentido de las agujas del reloj, así que `S2` es la mitad derecha. Sin `S` - la forma entera |
| `_2` después de `S4` | el otro cuarto: el inferior derecho en lugar del superior derecho. Solo existe donde la forma da una figura distinta |
| `T2`, `T4`, `T8`, `T16`, `T32` | un anillo de 1/2, 1/4, 1/8, 1/16 o 1/32 del radio de grosor. Sin `T` - relleno |
| `I` | invertida: el recuadro (o su sector) menos la forma |

Una forma sin más partes, como `Circle`, es la forma entera rellena. No existen todas las combinaciones. La mitad de un cuadrado es solo un rectángulo, así que eso lo hace un tamaño más estrecho

## Temas

Un tema es una **paleta**. Los colores del nivel pueden apuntar a él en lugar de guardar valores literales

Cambiar el tema activo cambia de golpe el estilo de todo lo que apunta a él.
El tema activo se puede animar en la línea de tiempo de eventos. Así un nivel cambia todo su aspecto a mitad de canción

Los temas se pueden guardar en la biblioteca del dispositivo y reutilizar en otros niveles

Más - [[6_themes]], [[5_color-and-postprocessing]]

## Efectos

Efectos de partículas de `VFX Graph` que el nivel puede colocar

Los efectos son un **enriquecimiento opcional**. Un nivel que nunca usa ninguno se juega exactamente como se diseñó

Un efecto usa la misma aleatoriedad con semilla que todo lo demás en el nivel. Por eso se reproduce de forma idéntica en cualquier dispositivo.
Los efectos se pueden guardar en la biblioteca del dispositivo y reutilizar en otros niveles

**El juego no trae efectos predefinidos.** Cada efecto que usa un nivel se creó en él o se tomó de la biblioteca

Más - [[1_level-budget]]

## Prefabs

Grupos reutilizables de objetos.
Un prefab guarda sus propios objetos de plantilla. Colocar un prefab escribe en el nivel copias reales de ellos

Editar la plantilla más tarde se traslada a cada colocación.
Aun así, una colocación puede diferir de la plantilla mediante sobrescrituras por instancia

> [!warning] Advertencia
> Los prefabs **no tienen presets definidos por el juego**, y los efectos tampoco. El juego trae presets solo para temas, fuentes, sonidos de la interfaz y las formas integradas. La biblioteca es la única manera de compartir un prefab entre niveles: la biblioteca de tu dispositivo o una colección. Más - [[16_library-and-collections]]

Más - [[2_reuse]]

## Metadatos del recurso

Título, descripción, orígenes, licencia y autores de un recurso

Así se conserva la atribución.
Una textura, una fuente o un archivo de audio tomados de algún sitio llevan, dentro del nivel, de dónde vienen y en qué condiciones. Ese registro va allá donde vaya el nivel

> [!tip] Recomendación
> Rellénalo al añadir el recurso. Es el único momento en que todavía recuerdas de dónde salió

Más - [[4_resource-record]]

## Editor de temas

Las ranuras de un tema y los colores que contienen

> [!caution] Precaución
> El contenido del nivel apunta a una ranura por su posición. Por eso **renumerar las ranuras cambia el estilo de todo lo que las referencia**

> [!tip] Consejo
> Guarda un tema terminado en la biblioteca del dispositivo. Así podrás usarlo en otros niveles

Más - [[6_themes]], [[5_color-and-postprocessing]]

## Referencia a un color del tema

Hace que este color apunte a una **ranura del tema del nivel** en lugar de a un valor literal

Cuando cambia el tema, todo lo que referencia una ranura cambia de estilo de golpe.
Los temas se pueden animar en la línea de tiempo de eventos. Así un nivel cambia toda su paleta a mitad de canción sin tocar un solo objeto

> [!tip] Consejo
> Las muestras enseñan la paleta en el fotograma del fotograma clave que editas, nunca en el cabezal. La ventana nombra los temas a cada lado de ese fotograma. Para elegir según un aspecto posterior, edita un fotograma clave situado más adelante

Más - [[6_themes]], [[5_color-and-postprocessing]]

## Editor de formas

Construye una forma a partir de puntos y las aristas entre ellos

Editas puntos y aristas. **Los triángulos se calculan automáticamente y nunca se editan.**
Así, una esquina que comparten tres triángulos es un solo punto que arrastrar, no tres que se separan

> [!warning] Advertencia
> Las aristas existen solo en el editor, el formato guarda triángulos. Por eso una arista que no cierra ningún contorno se descarta al guardar. El editor lo informa en lugar de descartarla en silencio

Más - [[3_images-and-fonts]]

## Licencias

Las condiciones bajo las que se distribuyen este nivel y sus recursos

Un nivel lleva todos los archivos que necesita: imágenes, fuentes, audio. Cada archivo puede venir con sus propias condiciones.
**Esas condiciones se registran por recurso**, no solo para el nivel en conjunto. Así, un nivel hecho de piezas ajenas puede decir exactamente qué se tomó y en qué condiciones

> [!tip] Recomendación
> Léelas antes de reutilizar cualquier cosa del nivel de otra persona

Más - [[1_licensing-basics]]
