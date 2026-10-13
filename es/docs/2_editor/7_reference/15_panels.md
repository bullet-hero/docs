---
title: Paneles
date: 2026-10-02
tags: [level_author]
---

# Paneles

La jerarquía, los inspectores y las líneas de tiempo están acoplados alrededor de la vista. Un clic en el tirador del borde de un panel lo abre o lo cierra, un arrastre cambia su ancho

## Tres paneles

La vista está en el centro, y a su alrededor hay tres paneles acoplados:
- el panel izquierdo contiene la jerarquía
- el panel derecho contiene los inspectores
- el panel inferior contiene las líneas de tiempo

Una pestaña del panel derecho que no tiene nada que mostrar se oculta. Más - [[5_object-properties]]

## Tirador del panel

Cada panel tiene un tirador en su borde:
- un clic abre o cierra el panel
- un arrastre cambia su tamaño. Un solo movimiento puede sacar un panel cerrado hasta cualquier ancho

La flecha del tirador muestra el estado del panel. En un panel cerrado apunta hacia un lado, en un panel abierto está girada media vuelta, sea cual sea el ancho. Una flecha girada solo en parte significa que hay un arrastre en curso

Un clic abre el panel con una animación, y los atajos también: `Ctrl+Left`, `Ctrl+Right` y `Ctrl+Down`. Más - [[3_speed-and-shortcuts]]

## Ancho

Un panel está cerrado o en algún punto entre su ancho mínimo y su ancho máximo. El ancho mínimo es también el normal: es el espacio que necesita el contenido del panel

| Panel | Mínimo | Máximo |
|---|---|---|
| izquierdo | 25% de la pantalla | 25% de la pantalla |
| derecho | 40% de la pantalla | 50% de la pantalla |
| inferior | 35% del alto de la pantalla | 70% del alto de la pantalla |

El panel izquierdo solo se abre y se cierra. El resto del editor se distribuye según su ancho

Si sueltas un arrastre por debajo del ancho mínimo, el panel va a lo que esté más cerca: la posición cerrada o el ancho mínimo. Justo a mitad de camino, se abre. Así, un solo movimiento sigue cerrando un panel

Un clic abre el panel con el ancho que tenía la última vez que lo dejaste abierto

> [!info] Conviene saber
> Un ancho arrastrado no se guarda. Vive solo en la sesión actual, así que un panel ensanchado no seguirá ancho la próxima vez

## Minimizar y abrir solo

`{{ui:cmd_editor_toggle-minimize-panels}}` cierra todos los paneles abiertos y deja sola la vista. Ejecutarlo de nuevo abre los paneles que estaban abiertos. Si no había ninguno abierto, se abren los tres

`{{ui:settings_game-editor_interface-auto-open-panel}}` (configuración, pestaña `{{ui:settings_game-editor_title}}`, `{{ui:settings_interface_label}}`) abre el panel derecho por sí solo cuando seleccionas algo. Desactivado por defecto
