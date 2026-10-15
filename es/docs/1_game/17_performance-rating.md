---
title: Valoración de rendimiento
date: 2026-10-15
tags: [player, level_author]
---

# Valoración de rendimiento

Antes de jugar, el juego muestra cuánto le cuesta a tu dispositivo ejecutar un nivel. Verde significa que va fluido, amarillo que va justo y rojo que es demasiado pesado y la tasa de fotogramas bajará

La puntuación es un número en el que `{{v:performance.score-limit}}` es exactamente el tiempo que puede tardar un fotograma a tu tasa de fotogramas objetivo. La franja sale de la puntuación:

| Franja | Puntuación |
|---|---|
| `{{ui:level_performance_holds}}` | por debajo de `{{v:performance.score-warning}}` |
| `{{ui:level_performance_tight}}` | de `{{v:performance.score-warning}}` a `{{v:performance.score-limit}}` |
| `{{ui:level_performance_does-not-hold}}` | por encima de `{{v:performance.score-limit}}` |
| `{{ui:level_performance_unknown}}` | el nivel o el dispositivo no se han medido |

La puntuación es una previsión del momento más pesado del nivel, no de su media. Un nivel ligero durante tres minutos que se congela un segundo recibe la puntuación de ese segundo

## Dónde la ves

- el explorador de niveles: un punto de color en cada tarjeta y el grupo `{{ui:root_level-filters_performance}}` en los filtros
- la página del nivel en el menú: la franja y la puntuación
- el editor de niveles, en los metadatos del nivel: la puntuación en tu dispositivo y en los dispositivos de referencia, además de los momentos más pesados del nivel como marcas de tiempo

## Las dos mitades de la puntuación

**La mitad del nivel** se mide al guardar el nivel en el editor y se guarda en sus metadatos. Describe lo que pide el nivel: cuántos objetos están vivos, cuánta pantalla cubren, cuántos efectos y pasadas de posprocesado se ejecutan. Un nivel guardado antes de esta función no tiene ese registro y aparece como `{{ui:level_performance_unknown}}` hasta que se guarde de nuevo. El editor lo mide al abrir el nivel y guarda el resultado hasta que cierras el juego, sin escribirlo en el archivo

**La mitad del dispositivo** dice lo rápido que tu dispositivo hace cada una de esas cosas. Hasta que midas tu dispositivo, el juego usa un dispositivo de referencia de tu plataforma. Tus ajustes también cuentan: la escala de renderizado, el antialiasing, los efectos y el posprocesado cambian la puntuación sin una nueva medición

## Medir tu dispositivo

1. Desde el menú principal, abre `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}`
2. Pulsa `{{ui:settings_graphics-performance_measure}}`
3. Espera unos minutos. La pantalla de ajustes se oculta y el juego reproduce niveles de prueba. No cambies a otra aplicación

Al terminar, la sección dice qué limita tu dispositivo (el procesador o el chip gráfico) y qué preajuste de `{{ui:settings_quick-setup_performance}}` sugiere

Si la medición fue inestable (el dispositivo se calentó demasiado, otra aplicación estaba ocupada), el juego la ignora y mantiene el dispositivo de referencia. Cierra otras aplicaciones y vuelve a medir

## Pasar a otro dispositivo

La medición pertenece al dispositivo en el que se hizo. La transferencia de perfil ([[14_profile-transfer]]) y los guardados en la nube no la llevan, así que un dispositivo nuevo empieza con su dispositivo de referencia hasta que lo vuelvas a medir
