## Alcance por defecto — no agregar sin pedirlo

Salvo que se pida explícitamente, generar la solución MÁS SIMPLE posible:
- Sin arquitectura en capas (sin Repository, sin Service, sin capas de
  dominio separadas) — un CRUD simple va en un único archivo o en muy
  pocos, no en 5+ módulos.
- Sin patrones de diseño (Repository, Strategy, Factory, etc.) a menos
  que se pidan por nombre.
- Sin suite de tests automatizada a menos que se pida.
- Sin README ni documentación extra a menos que se pida.
- HTML/CSS/JS vanilla, sin frameworks, salvo que se indique lo contrario.

Si el agente considera que la tarea genuinamente necesita más estructura
de la pedida, debe DECIRLO Y PREGUNTAR antes de implementarlo, nunca
decidirlo unilateralmente y proceder.

## Confirmación obligatoria antes de crear o modificar código

Antes de crear o modificar cualquier archivo, presentar primero un plan
breve: qué archivos se van a crear/modificar y el enfoque general (2-4
líneas). Esperar confirmación explícita del usuario ("dale", "sí",
"procedé") antes de escribir una sola línea de código. No asumir
aprobación por el solo hecho de que el pedido sonara claro.

# Skill: relevamiento de requerimientos a partir de fragmentos de entrevista

Todo RF necesita fragmento de origen real

Aplica a cualquier caso de relevamiento con fragmentos textuales de
distintos interlocutores (no específico de un caso particular — sirve
para cualquier ejercicio de este tipo).

## Convención de requerimiento bien formado

Un requerimiento (`RF-XX`) debe ser:
- **Atómico**: una sola idea verificable por renglón. Si un fragmento
  mezcla dos ideas ("que sea rápido y además registre las
  devoluciones"), se separan en dos requerimientos o se descarta la
  parte no verificable.
- **Verificable**: tiene que poder responderse sí/no si se cumplió.
  "Que sea práctico" no es verificable; "el registro de préstamo no
  debe superar los 2 pasos" sí lo sería.
- **Sin tecnología de implementación mezclada**: un RF describe qué
  debe hacer el sistema, no en qué herramienta está hecho.
- **Sin ambigüedad de valores**: si dos fragmentos asignan valores
  distintos a la misma condición sin aclarar cuál prevalece, no se
  redacta el RF como si estuviera resuelto (ver sección de conflictos).

## Qué fragmentos NO son requerimientos funcionales — clasificar así, no descartar en silencio

Al procesar cada fragmento, clasificarlo explícitamente en una de estas
categorías si no califica como RF. Nunca simplemente omitirlo:

- **Objetivo/meta de negocio (KPI)**: describe un resultado deseado a
  nivel organizacional, no una función del sistema. El sistema puede
  contribuir a la meta, pero la meta en sí no es un RF.
  (Señal: números de mejora porcentual, plazos de negocio, "el
  objetivo es...".)
- **Restricción técnica o de implementación**: impone una tecnología,
  plataforma o herramienta específica. Se documenta aparte (como
  restricción o RNF), nunca como RF — mezclar esto en `requirements.md`
  es un error común que hay que evitar activamente.
  (Señal: nombra un producto de software, un lenguaje, "ya está
  instalado", "lo hacemos en...".)
- **Requisito no funcional (RNF)**: describe una cualidad del sistema
  (velocidad, usabilidad) sin especificar una función concreta y
  verificable.
  (Señal: "rápido", "práctico", "fácil de usar", sin métrica.)
- **Dato de contexto/negocio, no de requerimiento**: describe cómo
  funciona hoy el proceso manual, sin pedir nada del sistema nuevo.

Cada fragmento descartado como RF va igual en `requirements.md`, en la
sección de fragmentos no-RF, con su categoría y una justificación de
una línea. Un fragmento sin justificación de por qué se descartó no
está completo.

## Detección de conflictos entre fragmentos — cuándo detener y marcar

Si dos fragmentos (de la misma persona o de personas distintas) asignan
**valores distintos a la misma condición de negocio**, sin que ningún
fragmento aclare cuál prevalece o en qué caso aplica cada uno:

- **No elegir un valor arbitrariamente.** No hay una interpretación
  "más razonable" cuando el material mismo está en conflicto — elegir
  una silenciosamente es inventar información que el relevamiento no
  dio.
- Marcar el requerimiento, la fila de tabla de decisión, o el caso de
  uso afectado con `[NEEDS CLARIFICATION: <descripción breve del
  conflicto, citando los fragmentos>]`.
- Este conflicto va también en la sección de observaciones del archivo
  correspondiente (ver decision-table.md), listado explícitamente como
  conflicto pendiente de resolución con el cliente/usuario.
- Señal típica de este caso: una política general declarada por un
  interlocutor, contradicha por una excepción mencionada como práctica
  informal por otro interlocutor ("en la práctica", "en realidad",
  "igual le estiramos").

## Convención de caso de uso

- Actor, precondición, flujo principal (numerado), flujo(s)
  alternativo(s), postcondición.
- Relación **include**: se usa cuando un caso de uso siempre necesita
  ejecutar otro como parte de su flujo, sin excepción — el incluido es
  obligatorio y no tiene sentido por separado en ese contexto.
- Relación **extend**: se usa cuando un caso de uso opcionalmente
  extiende a otro bajo una condición específica — el flujo base es
  completo sin la extensión.
- Toda relación declarada debe justificarse en una línea (por qué es
  include y no extend, o viceversa) — declararla sin justificar no
  cuenta como completo.

## Convención de tabla de decisión

- Una columna por regla, una fila por condición, una fila (o sección)
  por acción resultante.
- Usar guion (`-`) en las celdas de condiciones que no afectan esa
  regla en particular (no forzar un valor irrelevante).
- Debe existir una **regla por defecto** explícita, para combinaciones
  no cubiertas por las reglas nombradas — nunca dejar un caso posible
  sin regla asignada, ni implícito.
- Sección final obligatoria de **observaciones**: conflictos detectados
  (ver arriba), huecos del material relevado (una condición que se
  necesita pero ningún fragmento la aclaró), y decisiones de negocio
  pendientes de confirmar. Esta sección no es opcional — una tabla sin
  observaciones cuando el material tiene conflictos reales está
  incompleta, no "más prolija".
