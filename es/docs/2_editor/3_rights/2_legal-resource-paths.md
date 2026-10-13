---
title: Dos formas de que un recurso sea válido
date: 2026-09-25
tags: [level_author]
---

# Dos formas de que un recurso sea válido

Un recurso es válido si tiene una licencia adecuada o el permiso del titular de los derechos. No hay una tercera vía

Un recurso externo es todo lo que el nivel trae consigo: música, imágenes, fuentes, textos, cualquier archivo.
Cada recurso tiene que encajar en **una de dos** opciones

## Opción A: una licencia abierta

El recurso ya se distribuye en condiciones no más estrictas que `CC BY-NC`.
Conserva sus propias condiciones. No se convierte en `CC BY-NC`

El perfil estándar acepta:
- [CC0](https://creativecommons.org/publicdomain/zero/1.0/) - dominio público
- [CC BY](https://creativecommons.org/licenses/by/4.0/), versiones 4.0 y 3.0
- [CC BY-NC](https://creativecommons.org/licenses/by-nc/4.0/), versiones 4.0 y 3.0
- [MIT](https://choosealicense.com/licenses/mit/) y [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0) - para texto y código
- [SIL OFL 1.1](https://openfontlicense.org/open-font-license-official-text/) - para fuentes, hay que indicarla en los metadatos
- [Unlicense](https://choosealicense.com/licenses/unlicense/)

> [!tip] Recomendación
> Si la elección es tuya, quédate con `CC0`. Es la única licencia que no le pide nada al nivel

## Lo que el perfil rechaza

- **Propietaria**, también conocida como "todos los derechos reservados"
- [CC BY-SA](https://creativecommons.org/licenses/by-sa/4.0/) - el nivel tendría que publicarse bajo CC BY-NC-SA, y los niveles no se distribuyen bajo ella
- [CC BY-ND](https://creativecommons.org/licenses/by-nd/4.0/) - prohíbe las modificaciones, algo que el juego no admite
- [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/) y [CC BY-NC-ND](https://creativecommons.org/licenses/by-nc-nd/4.0/) - por las mismas dos razones

La familia GPL no está en la lista, aunque es más libre que CC BY-NC.
El código GPL no puede distribuirse por la App Store sin entrar en conflicto con las condiciones de Apple. Así que todo lo que llega a una compilación para iOS tiene que quedarse en forma de MIT o Apache

## El perfil depende del servicio

Qué licencias se aceptan lo decide el servicio, no la licencia.
La lista de arriba es el perfil estándar. Una compilación para tiendas acepta menos, y un servidor de la comunidad puede aceptar otras

## Opción B: el permiso del titular de los derechos

Un "claro, úsalo" en privado no basta.
Un nivel bajo `CC BY-NC` se distribuye públicamente, y el permiso tiene que cubrir justo eso, no tu uso personal

Un permiso válido concede los tres puntos:
1. El derecho a usar el recurso dentro de un nivel de Bullet Hero
2. El derecho a que terceros distribuyan el nivel, recurso incluido, de forma libre y no comercial a través de los servicios del juego, con atribución
3. Uso explícitamente solo no comercial

Cómo pedirlo - [[6_asking-permission]]

> [!caution] Precaución
> Un permiso no convierte un rechazo en un aprobado. Si la licencia del recurso es una de las rechazadas, el permiso lo envía a una revisión humana, pero no lo vuelve "permitido"

## Alcance y plazo de un permiso

Un permiso sin alcance o sin prueba cuenta como incompleto.
Un permiso caducado no cuenta en absoluto

**El alcance se registra**, y es importante:
- un permiso para un nivel concreto deja de valer cuando el recurso se copia a otro nivel
- un permiso para cualquier nivel sobrevive a cualquier reutilización

A continuación: [[6_asking-permission]], [[4_resource-record]]
