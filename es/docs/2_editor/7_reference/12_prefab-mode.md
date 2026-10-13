---
title: Modo prefab
date: 2026-10-02
tags: [level_author]
---

# Modo prefab

En el modo prefab editas la plantilla, y al guardar la edición llega a todas sus colocaciones. Se entra con el botón "Editar prefab" del inspector de una colocación y se vuelve al nivel con Ctrl+Shift+E

## Modo prefab

> [!caution] Precaución
> Estás editando la plantilla, no una de sus colocaciones. Al guardar, el cambio llega a todas las colocaciones que referencian esta plantilla

Cómo funciona una colocación:
- En cuanto apuntas una colocación a una plantilla, la colocación recibe copias reales de sus objetos con ids permanentes. En el editor, un hijo de un prefab es un objeto totalmente normal
- El archivo del nivel guarda solo la colocación: la plantilla, los ids de las copias y las sobrescrituras. Las copias se reconstruyen a partir de la plantilla cada vez que se carga el nivel
- Una colocación puede diferir de la plantilla mediante **sobrescrituras por instancia**. Se registran cuando editas un objeto así *fuera* del modo prefab
- Las ediciones hechas en el modo prefab no registran sobrescrituras. Cambian la propia plantilla

> [!tip] Consejo
> Las plantillas se abren unas encima de otras. Una colocación dentro de una plantilla abre su propia plantilla, y `{{ui:editor_prefab-timeline_close}}` te devuelve atrás. La misma plantilla no se puede abrir dos veces a la vez. El límite de anidamiento es de 8 niveles

Más - [[2_reuse]]

## Entrar y salir

Hay dos maneras de entrar:
- `{{ui:editor_inspector-prefab_edit}}` en el inspector de una colocación
- `{{ui:editor_level-prefab-item_edit}}` en la fila de una plantilla en la configuración del nivel, pestaña `Prefabs`. No necesita ninguna colocación, así que también abre una plantilla que no está colocada en ningún sitio, o que solo está colocada dentro de otra plantilla

`{{ui:editor_context-menu_open-prefab}}` en un menú contextual y en la paleta de comandos hace lo mismo con una colocación seleccionada, o con un objeto que trajo una colocación. El objeto correspondiente dentro de la plantilla queda seleccionado al instante

Hay dos maneras de salir:
- `{{ui:editor_prefab-timeline_close}}` en la línea de tiempo del prefab sube un nivel, a la plantilla que abrió esta
- el estado en la barra de herramientas principal (`Editando '...'`) y `Ctrl+Shift+E` salen de todas las plantillas abiertas a la vez y vuelven al nivel

La selección se borra cada vez que entras o sales. Volver un nivel atrás restaura lo que estaba seleccionado en esa plantilla

Dentro de una plantilla, la selección funciona como en el nivel: clic, clic con `Ctrl`, un recuadro, eliminar, copiar y contraer. Un clic en la vista no selecciona nada allí: la vista sigue mostrando el nivel, y una plantilla no tiene vista previa en directo en ella

## Dentro de una plantilla

Todos los objetos de una plantilla cuelgan de su **raíz**. La raíz:
- abarca toda la plantilla. Su duración es `{{ui:editor_prefab-mode-frame_length}}`, el mismo número en el inspector de la raíz y en la pestaña `Prefab`
- no se puede eliminar ni tener padre
- tiene `{{ui:field_common_active}}` y `{{ui:editor_inspector_layer}}` de solo lectura. Esos pertenecen a cada colocación

Un objeto nuevo va bajo el objeto seleccionado cuando hay exactamente uno seleccionado, la raíz incluida. Si no, va al nivel superior de la plantilla, bajo la raíz.
Abarca a su padre, anclado por los dos extremos. En el nivel superior, eso es toda la plantilla

Los generadores que necesitan el nivel entero no están disponibles aquí. Crear un prefab a partir de una selección y aplanar una colocación también se rechazan dentro de una plantilla

## Crear un prefab a partir de una selección

Convierte los objetos seleccionados en una plantilla nueva y pone una colocación de ella donde estaban. Después, el nivel se ve y se juega igual

Dónde encontrarlo:
- `{{ui:editor_context-menu_pack-prefab}}` en el menú de una fila de la jerarquía
- el menú contextual de la vista
- `{{ui:cmd_editor_pack-prefab}}` en la paleta de comandos, `Ctrl+G`
- `{{ui:settings_level-settings_resources-prefabs-pack}}` en la configuración del nivel, pestaña `Prefabs`

No pide confirmación y es un solo paso de deshacer. La colocación nueva queda seleccionada.
Un solo objeto da su nombre a la plantilla. Varios objetos dan una plantilla llamada `Prefab`. Cámbiale el nombre en la configuración del nivel, pestaña `Prefabs`

Qué se rechaza:
- una colocación, o un objeto que trajo una colocación. Para esos, los menús ofrecen `{{ui:editor_context-menu_open-prefab}}`
- una selección que quedaría anidada a más de 15 niveles. No se escribe nada, y el mensaje lo dice

## Aplanar una colocación

Desvincula una colocación de su plantilla: sus objetos pasan a ser objetos normales del nivel y se quedan exactamente donde están

Dónde encontrarlo: `{{ui:editor_inspector-prefab_flatten}}` en el inspector de la colocación, en el menú de una fila de la jerarquía y en la paleta de comandos

Siempre pregunta antes. Después, el nivel se ve igual, así que un aplanado hecho por error se descubriría mucho más tarde, cuando una edición de la plantilla dejara de llegarle. Varias colocaciones seleccionadas dan una sola confirmación y un solo paso de deshacer

Un objeto que trajo una colocación no se puede aplanar por separado. Aplana la colocación a la que pertenece

## Aplanar también los prefabs anidados

Decide qué pasa con los prefabs que hay dentro del que aplanas

**Desactivado** - solo la colocación que señalaste deja de seguir a su plantilla.
Un prefab colocado dentro de ella sigue siendo una colocación y conserva su vínculo. Editar esa plantilla interior sigue llegando al nivel.
Es el valor predeterminado: es lo que suele pedir "desempaquetar este prefab". El interruptor está desactivado cada vez que se abre la confirmación

**Activado** - todo lo anidado se aplana también.
Tras una sola pulsación, nada del nivel queda vinculado a esas plantillas interiores, a ninguna profundidad

En ambos casos, las propias plantillas se quedan en el nivel. Todo el aplanado es un solo paso de deshacer
