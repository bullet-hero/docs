---
title: "Tu primer nivel: la ruta"
date: 2026-10-02
tags: [level_author]
---

# Tu primer nivel: la ruta

Seis pasos hasta la primera prueba: crear un nivel, añadir la canción, marcar el ritmo, colocar objetos, hacer una prueba, guardar

## Seis pasos

Aquí solo está el orden de trabajo. Qué hace cada campo lo explica la ayuda que hay junto a su panel

**1. Crea el nivel.** `{{ui:settings_editor-settings_editor-settings}}` → `{{ui:settings_editor-settings_create-level}}`. Elige un preset, pon un nombre y una duración. La duración se puede cambiar después

**2. Añade la canción.** Copia el archivo de audio a la carpeta del nivel y conéctalo. `ogg` es lo que mejor funciona, y `flac` no se carga. Más - [[2_preparing-the-track]]

**3. Marca el ritmo.** La pestaña `{{ui:editor_inspector-beat_tab}}`: BPM, desfase, pulsos por compás. La cuadrícula no es para el juego, es para ti: el contenido se ajusta a ella

¿No sabes el tempo? Márcalo con toques al ritmo de la canción en la ventana `{{ui:editor_beat-window_title}}` (`Shift+T`). Marcar con toques no tiene tecla predeterminada

**4. Coloca los primeros objetos.** Crea un objeto, dale una forma y pon dos fotogramas clave en su posición. El juego lleva el valor de un fotograma clave a otro por sí solo

**5. Compruébalo.** Haz una prueba directamente desde el editor. Lo más probable es que todo se mueva o demasiado rápido o demasiado lento. Es normal: la velocidad solo se afina de oído

**6. Guarda.** `Ctrl+S`

El guardado automático está activado de forma predeterminada. {{v:editor.autosave-delay}} segundos después de un cambio sin guardar, guarda el nivel y pone una copia en `backups/<level id>/`. Más - [[4_not-losing-work#Guardado automático]]

## Que el primer nivel sea pequeño

> [!tip] Recomendación
> Elige una canción corta, de 1-2 minutos. Un nivel de 4 minutos es cuatro veces más trabajo y diez veces más motivos para dejarlo sin terminar

Empieza por el patrón más simple que funcione, no por el más difícil que se te haya ocurrido.
Juega el nivel entero tú antes de enseñárselo a nadie

Deja los generadores, los prefabs y los modificadores para más adelante. Ahorran tiempo en un nivel grande y estorban en el primero

## La canción y los derechos

Una canción para ti no necesita el permiso de nadie. Los derechos solo se comprueban al publicar.
Más - [[1_licensing-basics]]

Las reglas completas para publicar en el servidor oficial - [[ugc-licensing-policy]]

## Siguientes pasos

Cómo funciona el editor - [[3_how-the-editor-thinks]]

Después de la primera prueba - el diseño de niveles: [[2_editor/4_craft/index]]

Cuando el nivel crezca más allá de un boceto - [[1_order-of-work]]
