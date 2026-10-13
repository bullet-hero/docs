---
title: Imágenes con formas
date: 2026-10-13
tags: [level_author]
---

# Imágenes con formas

Monta una imagen primero con formas integradas y dibuja las tuyas solo donde ninguna encaje. Pon luces y sombras sobre una forma base, convierte cada elemento repetido en un prefab y compara el resultado con la imagen original colocada sobre el nivel

## Primero las formas integradas

Una forma integrada es geometría real con bordes limpios, y reutilizarla no cuesta nada.
Un círculo y un cuadrado se estiran a cualquier tamaño: un cuadrado estirado y girado es cualquier barra, línea o palo, un círculo estirado es una elipse

Dibuja tu propia forma en el editor de formas solo donde no encaje ninguna integrada: un abrigo, una mano, una vela.
Dale solo sus esquinas reales, con aristas rectas entre ellas. Una docena de esquinas se lee mejor que cien trazadas siguiendo cada píxel

> [!tip] Recomendación
> El detalle es el precio de los bordes limpios. Un contorno irregular o una costura visible estropean una imagen más que una muesca perdida

## Una base, detalles encima

La luz y la sombra son formas separadas colocadas encima de una forma base, recortadas por su borde.
Dos formas que solo se tocan arista con arista dejan entre ellas una fina costura de fondo, y se nota

Una parte que otra tapa continúa por debajo de ella. Un cuello entra un poco bajo el abrigo y la cabeza, una pierna bajo el dobladillo.
Así las partes siguen encajando cuando una de ellas se mueve

## Las repeticiones son prefabs

Todo lo que aparece más de una vez es un prefab: un ojo, una ventana, un pétalo.
Monta uno, conviértelo en prefab, coloca el resto y cambia en cada copia solo lo que difiere: su posición, tamaño, colores. Cada uno de esos cambios es una sobrescritura de esa copia

Así una sola edición de la plantilla llega a todas las copias, y el nivel sigue siendo pequeño

## Capas

Da a cada objeto su propia capa. Dos objetos en la misma capa al mismo tiempo se dibujan en un orden que no elegiste.
Mantén la base debajo de sus detalles y los detalles debajo de lo que vaya encima de ellos

## Comparar con el original

Importa la imagen original como textura y ponla en un rectángulo de exactamente su tamaño, encima de todo.
Para comparar, activa el rectángulo. Desactívalo durante el resto del trabajo en lugar de hacerlo transparente: un objeto desactivado no dibuja nada en absoluto

Revisa la imagen en conjunto y luego con zoom, parte por parte: los bordes, las uniones entre partes, las sombras

A continuación: [[2_reuse]], [[4_composition-and-camera]]
