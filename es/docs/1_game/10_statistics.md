---
title: Estadísticas
date: 2026-10-02
tags: [advanced_player]
---

# Estadísticas

El juego cuenta intentos, muertes, impactos y tiempo de cada nivel y de todo el dispositivo. Todo se guarda localmente en la carpeta stats. Se guarda un récord aparte para cada conjunto de condiciones de partida

## Dos archivos

| Archivo | Qué contiene |
|---|---|
| `stats/statistics.json` | todo sobre ti: en todos los niveles y pantallas |
| `stats/<LevelId>.json` | todo lo que hiciste con un nivel |

Los archivos son JSON, las horas están en UTC. No se envía nada a ningún sitio

La carpeta `stats` está junto a `levels` en la carpeta del juego, [[1_installation]]. Nunca está dentro de un nivel.
Así un nivel enviado a otra persona no llega ya completado. Y tu progreso sobrevive a eliminar el nivel y volver a importarlo

## La pestaña "Perfil"

`{{ui:settings_common_title}}` → `{{ui:settings_profile_tab}}` muestra el archivo común del dispositivo:

| Sección | Filas |
|---|---|
| `{{ui:settings_profile_section-account}}` | `{{ui:settings_profile_first-played}}`, `{{ui:settings_profile_last-played}}`, `{{ui:settings_profile_launches}}`, `{{ui:settings_profile_app-time}}` |
| `{{ui:field_common_time}}` | `{{ui:settings_profile_menu-time}}`, `{{ui:settings_profile_game-time}}`, `{{ui:settings_profile_editor-time}}`, `{{ui:settings_profile_loading-time}}` |
| `{{ui:settings_profile_section-totals}}` | `{{ui:settings_profile_attempts}}`, `{{ui:settings_profile_clears}}`, `{{ui:settings_profile_deaths}}`, `{{ui:settings_profile_hits}}`, `{{ui:settings_profile_levels-played}}`, `{{ui:settings_profile_levels-cleared}}`, `{{ui:settings_profile_frames}}` |
| `{{ui:settings_profile_section-streaks}}` | `{{ui:settings_profile_streak-current}}`, `{{ui:settings_profile_streak-longest}}` |
| `{{ui:settings_profile_section-avatar}}` | `{{ui:settings_profile_dashes}}`, `{{ui:settings_profile_distance}}` |
| `{{ui:settings_profile_section-tutorial}}` | `{{ui:settings_profile_tutorial-completions}}`, `{{ui:settings_profile_tutorial-first}}`, `{{ui:settings_profile_tutorial-last}}` - se cuenta como completado solo cuando terminas todos los pasos del [[13_sandbox|tutorial del sandbox]] |
| `{{ui:settings_profile_section-editor}}` | `{{ui:settings_profile_levels-created}}`, `{{ui:settings_profile_levels-deleted}}`, `{{ui:settings_profile_objects}}`, `{{ui:settings_profile_operations}}`, `{{ui:settings_profile_generators}}`, `{{ui:settings_profile_resources}}` |
| `{{ui:settings_profile_section-devices}}` | `{{ui:settings_profile_device-keyboard}}`, `{{ui:settings_profile_device-touch}}`, `{{ui:settings_profile_device-gamepad}}`, `{{ui:settings_profile_device-gyro}}` |

El tiempo se cuenta en segundos reales, no en tiempo del nivel. La cámara lenta de un checkpoint y una partida a media velocidad cuentan lo que duraron de verdad

Las filas de dispositivos muestran qué dispositivo guió al avatar durante el juego. Un dispositivo que solo está conectado no cuenta

## Por nivel

El archivo de un nivel guarda:

- cuándo lo jugaste por primera y por última vez
- el tiempo real pasado en el nivel y el número de sesiones
- los intentos (cada reinicio es uno nuevo), los completados, las muertes, los impactos, los dashes
- las vueltas a un checkpoint y las partidas abandonadas
- el punto más lejano alcanzado y la primera vez que lo completaste
- dónde mueres en el nivel: por fracción de la duración y por checkpoint

## Récords

Se guarda un récord por cada conjunto de condiciones de partida: vidas, velocidad, checkpoints activados o desactivados, colisiones activadas o desactivadas, y el bot.
La velocidad cuenta hasta las centésimas, exactamente como en pantalla

Zen (0 vidas) sigue contando los impactos: cada colisión entra en sus números, solo se libran las vidas y el final de la partida

Una partida supera el récord con las mismas condiciones si, en este orden:

1. llegó más lejos
2. recibió menos impactos
3. terminó con más vidas
4. usó menos dashes

Un récord también guarda la semilla de la partida y la versión del nivel en ese momento.
La versión no forma parte de las condiciones. Por eso un récord conseguido antes de que se rehiciera el nivel sigue visible, con la versión al lado

**Una partida desde el editor cuenta, pero no establece récords.** Se suma a los intentos, las muertes y los impactos. No da récord, ni mejor progreso, ni primera vez completado, porque el nivel solo existía en memoria

## Escritura, eliminación, congelación

El juego escribe las estadísticas cada 30 segundos. Y al instante al final de una partida, al cambiar de pantalla y al salir.
Un cierre inesperado cuesta como mucho 30 segundos de datos

- **Eliminar:** `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_other_cache-title}}`. Ahí están `{{ui:settings_other_cache-orphan-statistics}}` y `{{ui:settings_other_cache-all-statistics}}`
- **Eliminar con el nivel:** al eliminar un nivel se ofrece `{{ui:root_level-delete_statistics}}`
- **Congelar:** el modo anónimo detiene toda escritura hasta que se cierra el juego, [[4_settings]]
- **Llevar a otro dispositivo:** exporta el perfil e impórtalo allí. Una fusión conserva el valor mayor de cada contador, [[14_profile-transfer]]

> [!warning] Advertencia
> Una carpeta de nivel copiada a mano conserva el id del nivel. El original y la copia comparten un mismo archivo de estadísticas
