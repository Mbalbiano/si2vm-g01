# Casos de uso · Frente 3 · Endosos y anulaciones

## UC-01: Aplicar endoso

**Actor:** Operador de Pampa, usuario de SIGA (principal). Emisión de pólizas (secundario, paso 7).

**Precondición:** La póliza existe y está vigente.

**Flujo principal:**
1. El operador abre «Endosos y modificaciones».
2. Se ejecuta UC-03 Seleccionar póliza (include).
3. El operador elige el tipo de modificación.
4. El operador aplica el endoso.
5. El sistema registra el endoso con fecha y hora, tipo, detalle y usuario.
6. El sistema muestra el endoso en «Endosos registrados».
7. El sistema informa a Emisión de pólizas los datos de la póliza modificada. [NEEDS CLARIFICATION: flujo supuesto (RF-08). Decide: A. Pampín.]

**Flujo(s) alternativo(s):**
- 3a. El operador quiere dejar un detalle: se ejecuta UC-04 Registrar detalle del endoso (extend) antes del paso 4.
- 2a. La póliza está anulada: [NEEDS CLARIFICATION: SIGA acepta endosos sobre una póliza anulada (E3-8). ¿El sistema nuevo debe permitirlo? Decide: Gerencia Técnica.]

**Postcondición:** El endoso queda registrado y el estado de la póliza no cambia.

## UC-02: Anular póliza

**Actor:** Operador de Pampa, usuario de SIGA (principal). Cobranza (secundario, paso 5).

**Precondición:** La póliza existe y está vigente. El operador recibió un pedido de anulación.

**Flujo principal:**
1. El operador abre «Cobranza y estado de cuenta».
2. Se ejecuta UC-03 Seleccionar póliza (include).
3. El operador anula la póliza de la fila.
4. El sistema pasa la póliza a «Anulada» y deja de ofrecer la acción de anular.
5. El sistema confirma la anulación a Cobranza. [NEEDS CLARIFICATION: flujo supuesto. Decide: A. Pampín.]

**Flujo(s) alternativo(s):**
- 1a. El pedido llega de Cobranza por impago: se sigue desde el paso 2. [NEEDS CLARIFICATION: la regla de cuándo se anula por impago es de Cobranza (frente 8); el flujo es un supuesto.]
- 3a. La póliza ya está anulada: el sistema no ofrece la acción de anular (RF-04).

**Postcondición:** La póliza queda «Anulada» y no se puede volver a anular. [NEEDS CLARIFICATION: en SIGA la anulación se registra como endoso y suma uno a «End.» (E3-9). ¿Debe seguir así? Decide: Gerencia Técnica.]

## UC-03: Seleccionar póliza

**Actor:** Operador de Pampa, usuario de SIGA.

**Precondición:** El operador está en «Endosos y modificaciones» o en «Cobranza y estado de cuenta».

**Flujo principal:**
1. El operador elige la póliza en la lista de la pantalla.
2. El sistema muestra los datos de la póliza (tomador, dominio, estado).

**Flujo(s) alternativo(s):**
- 1a. La póliza no está en la lista: el operador no puede continuar. [NEEDS CLARIFICATION: SIGA no muestra una búsqueda ni qué pasa si falta la póliza.]

**Postcondición:** La póliza queda seleccionada para el caso de uso que lo incluye.

## UC-04: Registrar detalle del endoso

**Actor:** Operador de Pampa, usuario de SIGA.

**Precondición:** El operador está aplicando un endoso (UC-01) y eligió el tipo de modificación.

**Flujo principal:**
1. El operador escribe el detalle en el campo «Detalle».
2. El sistema lo guarda junto con el endoso al aplicarlo.

**Flujo(s) alternativo(s):**
- 1a. El operador deja el campo vacío: el endoso se guarda sin detalle (así funciona hoy, E0-2). [NEEDS CLARIFICATION: RF-06, si el detalle pasa a ser obligatorio. Decide: Gerencia Técnica.]

**Postcondición:** El endoso queda registrado con su detalle.

## Relaciones con otros casos de uso

| Relación | Caso de uso relacionado | Tipo (include/extend) | Justificación |
|----------|--------------------------|------------------------|----------------|
| UC-01 → UC-03 | Seleccionar póliza | include | Siempre se ejecuta: sin póliza elegida no hay endoso. No tiene sentido por separado en este contexto. |
| UC-02 → UC-03 | Seleccionar póliza | include | Siempre se ejecuta: la acción de anular está en la fila de una póliza, así que la póliza se elige antes. |
| UC-04 → UC-01 | Registrar detalle del endoso | extend | Solo ocurre si el operador escribe un detalle; el campo es opcional (E0-2) y el endoso se completa sin él. Si pasa a ser obligatorio (RF-06), sería include. |

## Fragmentos considerados para estos casos de uso

| Fragmento | Qué aporta al caso de uso |
|-----------|------------------------------|
| Caso §2.1 y §6 | Los tipos de endoso (UC-01) y la definición de anulación (UC-02). |
| Acta §3.1 y §3.4 | Los endosos dentro del alcance y los posibles solicitantes. |
| SIGA, «Endosos y modificaciones» | Los pasos de UC-01: selección de póliza, tipo, detalle, aplicar; la tabla «Endosos registrados»; el detalle opcional (UC-04). |
| SIGA, «Cobranza y estado de cuenta» | Los pasos de UC-02: anular, estado «Anulada», fila sin la acción. |
| Tabla 0.3 y devoluciones | Los pasos con Emisión de pólizas y con Cobranza, marcados como supuestos. |
