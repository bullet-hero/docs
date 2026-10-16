---
title: Valoración de rendimiento
date: 2026-10-17
tags: [player, level_author]
---

# Valoración de rendimiento

Antes de jugar, el juego muestra cuánto le cuesta a tu dispositivo ejecutar un nivel, con un indicador de cinco barras: cuantas más barras se encienden, más ligero es el nivel. Las barras verdes significan que va fluido, las amarillas que va justo y las rojas que la tasa de fotogramas bajará

La puntuación es un número en el que `{{v:performance.score-limit}}` es exactamente el tiempo que puede tardar un fotograma a tu tasa de fotogramas objetivo. La franja sale de la puntuación:

| Barras | Franja | Puntuación |
|---|---|---|
| 5 | `{{ui:level_performance_holds}}` | por debajo de `{{v:performance.score-warning}}` |
| 4 | `{{ui:level_performance_tight}}` | de `{{v:performance.score-warning}}` a `{{v:performance.score-limit}}` |
| 3 | `{{ui:level_performance_drops}}` | por encima de `{{v:performance.score-limit}}`, hasta `{{v:performance.score-heavy}}` |
| 2 | `{{ui:level_performance_severe-drops}}` | por encima de `{{v:performance.score-heavy}}`, hasta `{{v:performance.score-severe}}` |
| 1 | `{{ui:level_performance_does-not-hold}}` | por encima de `{{v:performance.score-severe}}` |
| ninguna | `{{ui:level_performance_unknown}}` | el nivel o el dispositivo no se han medido |

La puntuación es una previsión del momento más pesado del nivel, no de su media. Un nivel ligero durante tres minutos que se congela un segundo recibe la puntuación de ese segundo

## Dónde la ves

- el explorador de niveles: el indicador en cada tarjeta y el grupo `{{ui:root_level-filters_performance}}` en los filtros
- la página del nivel en el menú: el indicador, la franja y la puntuación
- el editor de niveles, en los metadatos del nivel: la puntuación en tu dispositivo y en los dispositivos de referencia, además de los momentos más pesados del nivel como marcas de tiempo

## Las dos mitades de la puntuación

**La mitad del nivel** se mide en el editor en los segundos posteriores a cada guardado, mientras sigues trabajando, y se guarda en sus metadatos. Si sales del editor antes de que termine, el archivo conserva la medición anterior. Describe lo que pide el nivel: cuántos objetos están vivos, cuánta pantalla cubren, cuántos efectos y pasadas de posprocesado se ejecutan. Un nivel guardado antes de esta función no tiene ese registro y aparece como `{{ui:level_performance_unknown}}` hasta que se guarde de nuevo. El editor lo mide al abrir el nivel y guarda el resultado hasta que sales del editor, sin escribirlo en el archivo

**La mitad del dispositivo** dice lo rápido que tu dispositivo hace cada una de esas cosas. Hasta que midas tu dispositivo, el juego usa un dispositivo de referencia de tu plataforma. Tus ajustes también cuentan: la escala de renderizado, el antialiasing, los efectos y el posprocesado cambian la puntuación sin una nueva medición

## Medir tu dispositivo

1. Desde el menú principal, abre `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}`
2. Pulsa `{{ui:settings_graphics-performance_measure}}`. Una ventana indica lo que ayuda a la medición: cerrar otras aplicaciones y juegos, conectar el teléfono o el portátil al cargador, no tocar el dispositivo
3. Pulsa `{{ui:settings_graphics-performance_start}}` y espera hasta {{v:performance.benchmark-max-seconds}} segundos. La pantalla de ajustes se oculta y el juego reproduce niveles de prueba y muestra en las esquinas superiores lo que mide. No cambies a otra aplicación

`{{ui:settings_graphics-performance_stop}}` detiene la medición antes de tiempo. Una medición detenida o que se queda sin tiempo no guarda nada, y el resultado anterior se mantiene

Al terminar, la ventana muestra el resultado: el indicador del nivel de demostración en tu dispositivo, qué limita tu dispositivo (el procesador o el chip gráfico), qué preajuste de `{{ui:settings_quick-setup_performance}}` sugiere y cuántos de tus niveles caen en cada franja. `{{ui:settings_graphics-performance_again}}` mide una vez más

Si la medición fue irregular (el dispositivo se calentó demasiado, otra aplicación estaba ocupada), el juego la usa igualmente, porque se acerca más a tu dispositivo que cualquier referencia, y la ventana lo avisa. Cierra otras aplicaciones y vuelve a medir para obtener una puntuación más exacta

## Pasar a otro dispositivo

La medición pertenece al dispositivo en el que se hizo. La transferencia de perfil ([[14_profile-transfer]]) y los guardados en la nube no la llevan, así que un dispositivo nuevo empieza con su dispositivo de referencia hasta que lo vuelvas a medir
