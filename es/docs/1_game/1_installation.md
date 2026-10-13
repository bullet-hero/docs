---
title: Instalación
date: 2026-10-14
tags: [player]
---

# Instalación

El juego guarda los niveles, la configuración y las estadísticas en una sola carpeta de datos. Actualizar es seguro: una versión nueva lee todos los datos antiguos. En Android, desinstalar el juego también borra los niveles

Descarga aquí - [[download]]

## Dónde están tus archivos

| Sistema | Carpeta |
|---|---|
| Windows | `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` |
| Android | `/storage/emulated/0/Android/data/com.vertoker.BulletHero/files` |

La forma más rápida de abrirla es desde el juego: `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general-open_folder}}`

Qué hay dentro:

| Carpeta | Qué contiene |
|---|---|
| `levels` | tus niveles, cada uno en su propia carpeta |
| `backups` | los autoguardados del editor |
| `stats` | las estadísticas |
| `settings.json` | la configuración |
| `reports` | los informes de errores |

## Desinstalación

En Windows, Linux y Mac la versión gratuita trae un desinstalador junto al juego: `unins000.exe` en Windows, `unins000` en Linux y `unins000` junto a `Bullet Hero.app` en Mac. Ejecútalo y quita el juego por sí mismo, sin hacer ni una sola pregunta. Tus niveles, tu configuración y tus estadísticas se quedan en la carpeta de datos

Solo quita los archivos propios del juego. Lo que hayas puesto tú en la carpeta del juego se queda, y la carpeta solo desaparece cuando está vacía. Si el juego está abierto, el desinstalador primero lo cierra, igual que su botón de cerrar, y con él el servidor MCP de la IA. Un nivel con cambios sin guardar los pierde, así que guárdalo antes de desinstalar

Si instalaste el juego con el instalador de Windows, se quita como cualquier otro programa, en la Configuración de Windows, en Aplicaciones

Una versión de tienda la quita su tienda

## Actualización

Una versión nueva del juego lee todos los datos antiguos sin problemas, sea cual sea la actualización y cambie lo que cambie

Una versión antigua no abre niveles de una más nueva. Si el juego te pide actualizar, actualiza

En las versiones de Google Play y RuStore, el menú principal ofrece una actualización nueva y esta se descarga en segundo plano. Cuando está lista, el menú principal muestra `{{ui:menu_update-ready_text}}` - pulsa `{{ui:menu_update-ready_install-btn}}`. Después de superar un nivel, puede pedirte que valores el juego

> [!caution] Precaución
> En Android, desinstalar el juego también borra todos tus niveles. Exporta el perfil antes de desinstalar - [[14_profile-transfer]]
