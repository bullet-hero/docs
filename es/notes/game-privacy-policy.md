---
title: Política de privacidad del juego
date: 2026-10-17
tags: [legal]
---

# Política de privacidad del juego

El desarrollador de Bullet Hero no recoge, no recibe, no vende y no comparte ningún dato personal. El juego no tiene cuentas propias, ni publicidad, ni analítica, ni informes de fallos, ni seguimiento, ni identificador publicitario. Todo lo que el juego recuerda sobre ti se queda en tu propio dispositivo, salvo lo que permites que una tienda guarde para ti con tu propia cuenta en esa tienda

Estas cosas pueden salir de tu dispositivo, y ninguna de ellas va al desarrollador:

- un nivel que abres puede hacer referencia a un archivo alojado en un sitio web de terceros, y cargarlo conecta con ese sitio web ([[game-privacy-policy#Acceso a la red]])
- un nivel o un archivo de perfil que compartes a propósito con otra persona viaja adonde lo envíes ([[game-privacy-policy#Niveles que compartes]])
- en las builds de Steam, el juego se comunica con Steam Workshop a través del cliente de Steam ([[game-privacy-policy#Steam Workshop]])
- en las builds de Steam, el juego guarda una copia de tus datos guardados en Steam Cloud y comunica tus logros a Steam ([[game-privacy-policy#Steam Cloud y logros]])
- en las builds de Steam, el juego muestra tu actividad actual en Discord a través del cliente de Discord ([[game-privacy-policy#Discord Rich Presence]])
- en la build de Google Play, el juego comunica tus logros a Google Play Juegos y consulta a Google Play sobre actualizaciones y valoraciones ([[game-privacy-policy#Google Play]])
- en la build de RuStore, el juego consulta a la aplicación RuStore sobre actualizaciones y valoraciones ([[game-privacy-policy#RuStore]])
- en un equipo, un programa de IA que conectas al editor de niveles ve el nivel que tienes abierto ([[game-privacy-policy#Asistente de IA en el editor]])

| | |
|---|---|
| Fecha de entrada en vigor | 17 de octubre de 2026 |
| Versión de la política | 1.4 |
| Aplicación | Bullet Hero: `com.vertoker.BulletHero` en Android, `com.vertoker.Bullet-Hero` en iOS, y las builds de escritorio para Windows, Linux y macOS |
| Desarrollador | vertoker, desarrollador individual |
| Contacto | [kostyachurakov@gmail.com](mailto:kostyachurakov@gmail.com) |

Esta política cubre solo el juego. El sitio web tiene su propia política - [[privacy-policy]]. El servidor también tendrá su propia política, que se escribirá cuando el servidor exista

## A quién se aplica esta política

Esta política cubre todas las builds de Bullet Hero, en todas las plataformas y en todas las tiendas por las que se distribuye, y todas las versiones del juego que no tengan una política más reciente asociada

Cuando una tienda (Google Play, App Store, Steam, RuStore, VK Play o cualquier otra) recoge sus propios datos sobre tu compra, tu instalación o tu uso de la aplicación, esa recogida se rige por la política de privacidad de esa tienda y no por esta. El desarrollador recibe de esas tiendas solo lo que deciden mostrar a todos los desarrolladores: estadísticas agregadas y anónimas sobre instalaciones, fallos y logros que no se pueden vincular a un jugador concreto

## Qué se guarda en tu dispositivo

El juego escribe lo siguiente en su propio almacenamiento de aplicación y lo vuelve a leer en el siguiente inicio:

- **Configuración**: gráficos, audio, controles, asignación de teclas, interfaz y preferencias de idioma
- **Progreso y estadísticas**: intentos, mejores resultados, muertes, tiempo de juego y registros similares, tanto del dispositivo en conjunto como de cada nivel
- **Logros**: qué logros has desbloqueado y cuándo
- **Niveles**: los niveles que creas, importas o descargas, con su audio, sus imágenes y otros archivos multimedia, además de sus copias de seguridad automáticas y, si usas el asistente de IA, sus notas en la carpeta `ai` del nivel
- **Skins del avatar**: las skins que creas o importas, y cuál llevas puesta
- **Perfil de rendimiento del dispositivo**: si haces la prueba de estrés, sus tiempos junto con el modelo del dispositivo, el nombre del chip gráfico y el tamaño de la pantalla. Se usa solo para valorar lo pesado que es un nivel en este dispositivo y nunca sale del dispositivo: no lo lleva ni una transferencia de perfil ni Steam Cloud
- **Estado local**: la configuración del asistente de IA del editor, el estado de la última sincronización con Steam Cloud y, en Android, el momento en que el juego te pidió por última vez que lo valoraras
- **Registros de diagnóstico**: el propio archivo de registro del motor, escrito localmente para que un problema se pueda investigar en el dispositivo donde ocurrió

Nada de esto se envía al desarrollador, y nada se copia en ningún servicio gestionado por el desarrollador. Solo Steam Cloud, en las builds de Steam, guarda una copia con tu cuenta de Steam ([[game-privacy-policy#Steam Cloud y logros]]). Dónde se guarda depende de la plataforma:

- **Android e iOS**: el almacenamiento privado del juego. Otras aplicaciones no pueden leerlo, y se elimina junto con el juego al desinstalarlo
- **Windows, Linux y macOS**: la carpeta de datos de aplicación de tu perfil de usuario, la ubicación estándar del motor. Otros programas que se ejecutan con tu cuenta pueden leerla, como pueden leer cualquiera de tus archivos, y se queda ahí después de desinstalar el juego hasta que elimines esa carpeta. El desinstalador que viene con las builds gratuitas (`unins000`) elimina solo los archivos propios del juego y no toca esta carpeta

El juego también ofrece, en `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}`, controles explícitos para eliminar las estadísticas y las copias de seguridad guardadas sin desinstalarlo

El juego no pide acceso a tus contactos, fotos, cámara, micrófono, ubicación, calendario, registro de llamadas, lista de aplicaciones instaladas ni a ningún otro recurso sensible, y no pide ningún permiso en tiempo de ejecución

## Acceso a la red

Bullet Hero no tiene servidor. El desarrollador no gestiona ningún servicio al que se conecte el juego, y por tanto no recibe de él ningún dato

Un nivel es una carpeta de archivos, y su autor puede apuntar uno de esos archivos a una dirección de internet en lugar de incluirlo dentro de la carpeta. Cuando abres un nivel así, el juego descarga ese archivo del sitio web que eligió su autor. Ese sitio web ve entonces lo que ve cualquier sitio web cuando se le pide un archivo, sobre todo tu dirección IP y los detalles técnicos de la solicitud. El desarrollador ni controla ni observa esas solicitudes, y no se guarda ningún registro de ellas

Aparte de eso, el juego hace solicitudes de red solo a través de la tienda o de la aplicación con la que llegó, y solo en la build de esa tienda:

- las builds de Steam: Steam Workshop, Steam Cloud y los logros de Steam a través del cliente de Steam, y Discord Rich Presence a través del cliente de Discord
- la build de Google Play: los logros de Google Play Juegos, la comprobación de actualizaciones y la solicitud de valoración a través de Google Play en el teléfono
- la build de RuStore: la comprobación de actualizaciones y la solicitud de valoración a través de la aplicación RuStore en el teléfono

Ninguna otra build hace ninguna de estas solicitudes: el código de cada tienda se compila solo en la build de esa tienda. El asistente de IA del editor escucha solo en la dirección de bucle invertido (loopback) del propio equipo y no se puede alcanzar desde la red ([[game-privacy-policy#Asistente de IA en el editor]])

## Steam Workshop

Las builds de Steam usan Steam Workshop a través del cliente de Steam que se ejecuta en tu equipo. Las builds para cualquier otra tienda nunca inician Steam: el código que se comunica con él se compila solo en las builds de Steam

El juego pregunta a Steam a qué elementos del Workshop está suscrita tu cuenta, para poder mostrarlos como niveles y colecciones. El cliente de Steam los descarga. Cuando decides publicar un nivel o una colección, el juego se lo entrega al cliente de Steam junto con el título, la descripción, la imagen de vista previa, los descriptores de contenido y la visibilidad que hayas elegido, y Steam lo guarda en sus servidores con tu cuenta de Steam. Un elemento público puede verlo cualquiera en Steam hasta que lo retires allí

Todo esto pasa entre el cliente de Steam y los servidores de Valve y se rige por la política de privacidad de Steam y por el Acuerdo de Suscriptor de Steam. El desarrollador no recibe de ello nada más allá de lo que Steam muestra a todos los desarrolladores sobre un elemento del Workshop

## Steam Cloud y logros

En las builds de Steam el juego guarda una copia de tu configuración, tus estadísticas, tus logros, tus niveles, tu biblioteca y tus skins del avatar en Steam Cloud, con tu cuenta de Steam. Lee esa copia al iniciarse y escribe los cambios mientras juegas y al salir, a través del cliente de Steam. La configuración de gráficos y de controles, las copias de seguridad, los informes de errores, las grabaciones, el perfil de rendimiento del dispositivo y el estado local del editor nunca van ahí. Steam Cloud se puede desactivar para el juego en sus propiedades en Steam, y entonces el juego guarda todo solo en este equipo

Cada logro que desbloqueas también se comunica a Steam, que lo muestra en tu perfil de Steam según tu configuración de privacidad de Steam

Ambos se guardan en los servidores de Valve y se rigen por la política de privacidad de Steam y por el Acuerdo de Suscriptor de Steam. El desarrollador no recibe de ellos nada más allá de lo que Steam muestra a todos los desarrolladores, como el porcentaje de jugadores que desbloqueó cada logro

## Discord Rich Presence

Las builds de Steam pueden mostrar en tu perfil de Discord lo que haces en el juego: el menú, el editor de niveles, el sandbox o el nivel al que juegas, y durante cuánto tiempo. Un nivel se muestra con su nombre y sus autores solo cuando ya es público, es decir, un elemento de Steam Workshop o un nivel que viene con el juego. Cualquier otro nivel se muestra solo como nivel personalizado, y el nivel que estás editando nunca se nombra. Esto solo funciona mientras la aplicación de Discord se está ejecutando en el mismo equipo. Las builds para cualquier otra tienda no tienen integración con Discord: el código que se comunica con Discord se compila solo en las builds de Steam

El juego entrega esa actividad al cliente de Discord de tu dispositivo, nunca a un servidor propio. El cliente de Discord la publica después con tu cuenta de Discord, y tus amigos y servidores de Discord pueden verla. El juego no inicia sesión en Discord, no lee tus mensajes, servidores ni lista de amigos y no envía nada en tu nombre

Lo que ocurre con esa actividad del lado de Discord se rige por la [Política de privacidad de Discord](https://discord.com/privacy). El desarrollador no recibe nada de ello. Puedes ocultar tu actividad en cualquier momento en Discord: `User Settings` -> `Activity Privacy`

## Google Play

La build de Google Play usa tres servicios de Google Play en tu teléfono:

- **Google Play Juegos**: si iniciaste sesión en Google Play Juegos, cada logro que desbloqueas también se comunica ahí, con tu cuenta de Google, y se muestra en tu perfil de Play Juegos. El juego solo pregunta a Play Juegos si iniciaste sesión y qué logros ya están desbloqueados. No lee tu nombre, tus amigos ni nada más de tu cuenta. El inicio de sesión lo gestiona el propio Google Play Juegos, y sin él los logros se quedan solo en el juego
- **Actualizaciones**: cuando se abre el menú principal, el juego pregunta a Google Play si hay una versión más reciente, y Google Play la descarga en segundo plano
- **Valoración**: después de completar un nivel, a partir del tercero y como máximo una vez cada 60 días, el juego pide a Google Play que muestre su ventana de valoración. Si la ventana aparece, y lo que escribes en ella, depende de Google Play: el juego nunca ve tu valoración ni tu reseña

Lo que Google hace con estos datos se rige por la [Política de privacidad de Google](https://policies.google.com/privacy). El desarrollador no recibe de ello nada más allá de lo que Google Play muestra a todos los desarrolladores, como las reseñas publicadas y el porcentaje de jugadores que desbloqueó cada logro

## RuStore

La build de RuStore usa la aplicación RuStore de tu teléfono para dos cosas, y solo mientras esa aplicación está instalada:

- **Actualizaciones**: cuando se abre el menú principal, el juego pregunta a RuStore si hay una versión más reciente, y RuStore la descarga en segundo plano
- **Valoración**: después de completar un nivel, a partir del tercero y como máximo una vez cada 60 días, el juego pide a RuStore que muestre su ventana de valoración. Si la ventana aparece, y lo que escribes en ella, depende de RuStore: el juego nunca ve tu valoración ni tu reseña

Lo que RuStore hace con estos datos se rige por los propios documentos de RuStore. El desarrollador no recibe de ello nada más allá de lo que RuStore muestra a todos los desarrolladores

## Asistente de IA en el editor

En Windows, Linux y macOS el editor de niveles puede permitir que un programa asistente de IA edite el nivel abierto. Está desactivado hasta que activas `{{ui:settings_game-editor_mcp-enabled}}` en `{{ui:settings_common_title}}` → `{{ui:settings_game-editor_title}}` → `{{ui:settings_game-editor_mcp_title}}`. Mientras está activado, el juego escucha solo en la dirección de bucle invertido (loopback) del propio equipo, acepta un solo programa a la vez y solo lo deja entrar con un token aleatorio escrito en un archivo del almacenamiento del juego. Nada fuera de este equipo puede conectarse

El programa que conectas lo eliges tú y no forma parte del juego. Puede leer el nivel abierto, sus recursos y su música, e imágenes del campo de juego, y puede enviarlos a quien gestione su modelo de IA. Lo que ocurre con ellos ahí se rige por los propios términos y la propia política de privacidad de ese programa. El desarrollador no recibe nada de ello

## Niveles que compartes

Los niveles son portátiles por diseño: un nivel se puede exportar como un archivo comprimido normal y enviarse a otra persona por el medio que elijas. Ese archivo viaja directamente entre tú y el destinatario, o a través del servicio que uses para enviarlo. No pasa por el desarrollador, y el desarrollador no guarda ninguna copia

Lo mismo vale para los demás archivos que el juego puede escribir para que los traslades: un archivo de perfil creado con `{{ui:settings_profile-transfer_title}}`, que contiene tus niveles, estadísticas, configuración, biblioteca y skins del avatar, y una skin del avatar exportada por separado

Un nivel que creas puede contener tu propia música, imágenes y texto y, si los pones ahí, tu nombre o tu apodo. Todo lo que colocas dentro de un nivel lo ve cualquiera a quien le des ese nivel. Decidir qué incluir es cosa tuya. Si usas el asistente de IA, las notas que guarda en la carpeta `ai` del nivel van con las exportaciones del nivel y con las publicaciones en el Workshop salvo que se desmarque `{{ui:settings_level-settings_metadata-level-ai-share}}`, y una exportación protegida con contraseña nunca las lleva

Un nivel puede protegerse opcionalmente con una frase de contraseña. Esa frase se usa para cifrar el contenido del nivel en tu dispositivo y nunca se escribe en disco, nunca se registra y nunca se transmite. Si la pierdes, ni el desarrollador ni nadie más puede recuperar el contenido del nivel

## Menores

El juego no recoge datos personales de nadie, y eso incluye a los menores. No contiene publicidad, ni compras dentro de la aplicación, ni chat, ni ninguna otra función de comunicación, ni ningún mecanismo por el que un menor pueda revelar información personal al desarrollador o a otro jugador a través del propio juego

Como los niveles pueden compartirse como archivos y pueden contener texto, imágenes y audio arbitrarios elegidos por su autor, los padres y tutores siguen siendo responsables de los niveles que un menor obtiene de otras personas

## Componentes de terceros

El juego está hecho con el motor Unity. **Los servicios de recogida de datos propios de Unity (Unity Analytics, Unity Ads, Unity In-App Purchasing, Unity Cloud Diagnostics, el diagnóstico del motor, las estadísticas de hardware, los informes de fallos y los informes de rendimiento) están todos desactivados en este proyecto**, y los paquetes que los proporcionan no se incluyen en la build. No hay ningún SDK de publicidad, analítica, atribución ni informes de fallos de ningún tipo

La build de una tienda lleva la biblioteca propia de esa tienda, y ninguna otra build la lleva: Steamworks (a través de Facepunch.Steamworks) y el Discord Social SDK en las builds de Steam, Google Play Games Services y las bibliotecas de Google Play para reseñas y para actualizaciones dentro de la aplicación en la build de Google Play, el SDK de RuStore para reseñas y actualizaciones de la aplicación en la build de RuStore. Cada una de ellas se comunica solo con su propio servicio, como se describe más arriba

## Tus derechos

Normas como el RGPD, el RGPD del Reino Unido (UK GDPR), la CCPA/CPRA y la Ley Federal de Rusia n.º 152-FZ te otorgan derechos de acceso, rectificación, supresión y oposición al tratamiento de tus datos personales

Como el desarrollador no tiene ningún dato personal tuyo, no hay nada a lo que acceder, que rectificar, exportar o eliminar del lado del desarrollador, y no hace falta ninguna solicitud para ejercer esos derechos. Los datos descritos en [[game-privacy-policy#Qué se guarda en tu dispositivo]] están bajo tu control: puedes revisarlos en la carpeta de almacenamiento del juego en tu dispositivo, borrarlos desde el propio juego o eliminarlos por completo desinstalando la aplicación. Una copia que una tienda guarda con tu cuenta (Steam Cloud, los logros en Steam o en Google Play Juegos) la conserva esa tienda, y esos derechos sobre ella se ejercen ante esa tienda, según su propia política. Aun así, puedes escribir a la dirección de contacto de arriba con cualquier pregunta sobre esta política

## Conservación de datos

El desarrollador no conserva datos personales y por tanto no tiene ningún plazo de conservación que declarar. Los datos guardados en tu dispositivo se conservan mientras tú los mantengas ahí. Una copia que una tienda guarda con tu cuenta la conserva esa tienda según su propia política

## Cambios en esta política

Esta política cambiará si cambia el juego, muy probablemente cuando se añadan el servidor propio del juego, las cuentas de jugador o el multijugador, nada de lo cual existe hoy. Cuando cambie, se actualizarán la fecha de entrada en vigor y la versión de la política que figuran al principio de esta página, y el texto anterior seguirá disponible en el historial público de versiones de esta página. Seguir usando el juego después de un cambio significa que la política actualizada se aplica a ese uso

## Contacto

Las preguntas sobre esta política, o sobre la privacidad en Bullet Hero en general, van a la dirección de contacto que figura al principio de esta página
