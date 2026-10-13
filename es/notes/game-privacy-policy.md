---
title: Política de privacidad del juego
date: 2026-10-03
tags: [legal]
---

# Política de privacidad del juego

Bullet Hero no recoge, no transmite, no guarda en ningún servidor, no vende y no comparte ningún dato personal. No hay cuentas, ni inicio de sesión, ni publicidad, ni analítica, ni informes de fallos, ni seguimiento, ni identificador publicitario. Todo lo que el juego recuerda sobre ti se queda en tu propio dispositivo

Cuatro cosas pueden salir de tu dispositivo, y ninguna de ellas va al desarrollador:

- un nivel que abres puede hacer referencia a un archivo alojado en un sitio web de terceros, y cargarlo conecta con ese sitio web ([[game-privacy-policy#Acceso a la red]])
- un nivel que compartes a propósito con otra persona viaja adonde lo envíes ([[game-privacy-policy#Niveles que compartes]])
- en las builds de Steam, el juego se comunica con Steam Workshop a través del cliente de Steam ([[game-privacy-policy#Steam Workshop]])
- en las builds de Steam, el juego muestra tu actividad actual en Discord a través del cliente de Discord ([[game-privacy-policy#Discord Rich Presence]])

| | |
|---|---|
| Fecha de entrada en vigor | 3 de octubre de 2026 |
| Versión de la política | 1.3 |
| Aplicación | Bullet Hero: `com.vertoker.BulletHero` en Android, `com.vertoker.Bullet-Hero` en iOS, y las builds de escritorio para Windows, Linux y macOS |
| Desarrollador | vertoker, desarrollador individual |
| Contacto | [kostyachurakov@gmail.com](mailto:kostyachurakov@gmail.com) |

Esta política cubre solo el juego. El sitio web tiene su propia política - [[privacy-policy]]. El servidor también tendrá su propia política, que se escribirá cuando el servidor exista

## A quién se aplica esta política

Esta política cubre todas las builds de Bullet Hero, en todas las plataformas y en todas las tiendas por las que se distribuye, y todas las versiones del juego que no tengan una política más reciente asociada

Cuando una tienda (Google Play, App Store, Steam, RuStore, VK Play o cualquier otra) recoge sus propios datos sobre tu compra, tu instalación o tu uso de la aplicación, esa recogida se rige por la política de privacidad de esa tienda y no por esta. El desarrollador recibe de esas tiendas solo lo que deciden mostrar a todos los desarrolladores: estadísticas agregadas y anónimas sobre instalaciones y fallos que no se pueden vincular a un jugador concreto

## Qué se guarda en tu dispositivo

El juego escribe lo siguiente en su propio almacenamiento de aplicación y lo vuelve a leer en el siguiente inicio:

- **Configuración**: gráficos, audio, controles, asignación de teclas, interfaz y preferencias de idioma
- **Progreso y estadísticas**: intentos, mejores resultados, muertes, tiempo de juego y registros similares, tanto del dispositivo en conjunto como de cada nivel
- **Niveles**: los niveles que creas, importas o descargas, con su audio, sus imágenes y otros archivos multimedia, además de sus copias de seguridad automáticas
- **Registros de diagnóstico**: el propio archivo de registro del motor, escrito localmente para que un problema se pueda investigar en el dispositivo donde ocurrió

Nada de esto se transmite a ninguna parte, y nada se copia en ningún servicio gestionado por el desarrollador. Dónde se guarda depende de la plataforma:

- **Android e iOS**: el almacenamiento privado del juego. Otras aplicaciones no pueden leerlo, y se elimina junto con el juego al desinstalarlo
- **Windows, Linux y macOS**: la carpeta de datos de aplicación de tu perfil de usuario, la ubicación estándar del motor. Otros programas que se ejecutan con tu cuenta pueden leerla, como pueden leer cualquiera de tus archivos, y se queda ahí después de desinstalar el juego hasta que elimines esa carpeta

El juego también ofrece, en `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}`, controles explícitos para eliminar las estadísticas y las copias de seguridad guardadas sin desinstalarlo

El juego no pide acceso a tus contactos, fotos, cámara, micrófono, ubicación, calendario, registro de llamadas, lista de aplicaciones instaladas ni a ningún otro recurso sensible, y no pide ningún permiso en tiempo de ejecución

## Acceso a la red

Bullet Hero no tiene servidor. El desarrollador no gestiona ningún servicio al que se conecte el juego, y por tanto no recibe de él ningún dato

Un nivel es una carpeta de archivos, y su autor puede apuntar uno de esos archivos a una dirección de internet en lugar de incluirlo dentro de la carpeta. Cuando abres un nivel así, el juego descarga ese archivo del sitio web que eligió su autor. Ese sitio web ve entonces lo que ve cualquier sitio web cuando se le pide un archivo, sobre todo tu dirección IP y los detalles técnicos de la solicitud. El desarrollador ni controla ni observa esas solicitudes, y no se guarda ningún registro de ellas

Aparte de eso, de Steam Workshop en las builds de Steam ([[game-privacy-policy#Steam Workshop]]) y de Discord Rich Presence en las builds de Steam ([[game-privacy-policy#Discord Rich Presence]]), el juego no hace ninguna solicitud de red por su cuenta

## Steam Workshop

Las builds de Steam usan Steam Workshop a través del cliente de Steam que se ejecuta en tu equipo. Las builds para cualquier otra tienda nunca inician Steam: el código que se comunica con él se compila solo en las builds de Steam

El juego pregunta a Steam a qué elementos del Workshop está suscrita tu cuenta, para poder mostrarlos como niveles y colecciones. El cliente de Steam los descarga. Cuando decides publicar un nivel o una colección, el juego se lo entrega al cliente de Steam junto con el título, la descripción, la imagen de vista previa, los descriptores de contenido y la visibilidad que hayas elegido, y Steam lo guarda en sus servidores con tu cuenta de Steam. Un elemento público puede verlo cualquiera en Steam hasta que lo retires allí

Todo esto pasa entre el cliente de Steam y los servidores de Valve y se rige por la política de privacidad de Steam y por el Acuerdo de Suscriptor de Steam. El desarrollador no recibe de ello nada más allá de lo que Steam muestra a todos los desarrolladores sobre un elemento del Workshop

## Discord Rich Presence

Las builds de Steam pueden mostrar en tu perfil de Discord lo que haces en el juego: el menú, el editor de niveles, el sandbox o el nivel al que juegas, y durante cuánto tiempo. Un nivel se muestra con su nombre y sus autores solo cuando ya es público, es decir, un elemento de Steam Workshop o un nivel que viene con el juego. Cualquier otro nivel se muestra solo como nivel personalizado, y el nivel que estás editando nunca se nombra. Esto solo funciona mientras la aplicación de Discord se está ejecutando en el mismo equipo. Las builds para cualquier otra tienda no tienen integración con Discord: el código que se comunica con Discord se compila solo en las builds de Steam

El juego entrega esa actividad al cliente de Discord de tu dispositivo, nunca a un servidor propio. El cliente de Discord la publica después con tu cuenta de Discord, y tus amigos y servidores de Discord pueden verla. El juego no inicia sesión en Discord, no lee tus mensajes, servidores ni lista de amigos y no envía nada en tu nombre

Lo que ocurre con esa actividad del lado de Discord se rige por la [Política de privacidad de Discord](https://discord.com/privacy). El desarrollador no recibe nada de ello. Puedes ocultar tu actividad en cualquier momento en Discord: `User Settings` -> `Activity Privacy`

## Niveles que compartes

Los niveles son portátiles por diseño: un nivel se puede exportar como un archivo comprimido normal y enviarse a otra persona por el medio que elijas. Ese archivo viaja directamente entre tú y el destinatario, o a través del servicio que uses para enviarlo. No pasa por el desarrollador, y el desarrollador no guarda ninguna copia

Un nivel que creas puede contener tu propia música, imágenes y texto y, si los pones ahí, tu nombre o tu apodo. Todo lo que colocas dentro de un nivel lo ve cualquiera a quien le des ese nivel. Decidir qué incluir es cosa tuya

Un nivel puede protegerse opcionalmente con una frase de contraseña. Esa frase se usa para cifrar el contenido del nivel en tu dispositivo y nunca se escribe en disco, nunca se registra y nunca se transmite. Si la pierdes, ni el desarrollador ni nadie más puede recuperar el contenido del nivel

## Menores

El juego no recoge datos personales de nadie, y eso incluye a los menores. No contiene publicidad, ni compras dentro de la aplicación, ni chat, ni ninguna otra función de comunicación, ni ningún mecanismo por el que un menor pueda revelar información personal al desarrollador o a otro jugador a través del propio juego

Como los niveles pueden compartirse como archivos y pueden contener texto, imágenes y audio arbitrarios elegidos por su autor, los padres y tutores siguen siendo responsables de los niveles que un menor obtiene de otras personas

## Componentes de terceros

El juego está hecho con el motor Unity. **Los servicios de recogida de datos propios de Unity (Unity Analytics, Unity Ads, Unity In-App Purchasing, Unity Cloud Diagnostics, el diagnóstico del motor, las estadísticas de hardware, los informes de fallos y los informes de rendimiento) están todos desactivados en este proyecto**, y los paquetes que los proporcionan no se incluyen en la build. No hay ningún SDK de publicidad, analítica, atribución ni informes de fallos de ningún tipo

## Tus derechos

Normas como el RGPD, el RGPD del Reino Unido (UK GDPR), la CCPA/CPRA y la Ley Federal de Rusia n.º 152-FZ te otorgan derechos de acceso, rectificación, supresión y oposición al tratamiento de tus datos personales

Como el desarrollador no tiene ningún dato personal tuyo, no hay nada a lo que acceder, que rectificar, exportar o eliminar del lado del desarrollador, y no hace falta ninguna solicitud para ejercer esos derechos. Los datos descritos en [[game-privacy-policy#Qué se guarda en tu dispositivo]] están bajo tu control: puedes revisarlos en la carpeta de almacenamiento del juego en tu dispositivo, borrarlos desde el propio juego o eliminarlos por completo desinstalando la aplicación. Aun así, puedes escribir a la dirección de contacto de arriba con cualquier pregunta sobre esta política

## Conservación de datos

El desarrollador no conserva datos personales y por tanto no tiene ningún plazo de conservación que declarar. Los datos guardados en tu dispositivo se conservan mientras tú los mantengas ahí

## Cambios en esta política

Esta política cambiará si cambia el juego, muy probablemente cuando se añadan el servidor propio del juego, las cuentas de jugador o el multijugador, nada de lo cual existe hoy. Cuando cambie, se actualizarán la fecha de entrada en vigor y la versión de la política que figuran al principio de esta página, y el texto anterior seguirá disponible en el historial público de versiones de esta página. Seguir usando el juego después de un cambio significa que la política actualizada se aplica a ese uso

## Contacto

Las preguntas sobre esta política, o sobre la privacidad en Bullet Hero en general, van a la dirección de contacto que figura al principio de esta página
