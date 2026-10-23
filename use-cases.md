# Casos de uso

## UC-01: Aplicar endoso

**Actor:** Operador de Pampa, usuario de SIGA (principal). Emisión de pólizas (secundario, paso 7).

**Precondición:** La póliza existe y está vigente.

**Flujo principal:**
1. El operador abre «Endosos y modificaciones».
2. Se ejecuta UC-03 Seleccionar póliza (include).
3. El operador elige el tipo de modificación.
4. El operador pulsa «Aplicar».
5. El sistema registra el endoso con fecha y hora, tipo, detalle y usuario, y suma uno a «End.» de la póliza.
6. El sistema muestra el endoso en «Endosos registrados».
7. El sistema informa a Emisión de pólizas los datos de la póliza modificada. [NEEDS CLARIFICATION: flujo supuesto (RF-08). Decide: docente.]

**Flujo(s) alternativo(s):**
- 3a. El operador quiere dejar un detalle: se ejecuta UC-04 Registrar detalle del endoso (extend) antes del paso 4.
- 2a. La póliza está anulada: [NEEDS CLARIFICATION: SIGA no permite verificar si se puede endosar una póliza anulada. Decide: docente.]

**Postcondición:** El endoso queda registrado, «End.» sube en uno y el estado de la póliza no cambia.

**Relaciones con otros casos de uso:**

| Relación | Caso de uso relacionado | Tipo (include/extend) | Justificación |
|----------|--------------------------|------------------------|----------------|
| UC-01 → UC-03 | Seleccionar póliza | include | Siempre se ejecuta: sin póliza elegida en «Endosos y modificaciones» no hay endoso. |
| UC-04 → UC-01 | Registrar detalle del endoso | extend | Solo ocurre si el operador escribe un detalle; el campo es opcional (E0-2) y el endoso se completa sin él. |

## Fragmentos considerados para este caso de uso

| Fragmento | Qué aporta al caso de uso |
|-----------|------------------------------|
| SIGA, «Endosos y modificaciones» | Selección de póliza, tipo, detalle y botón «Aplicar»; tabla «Endosos registrados». |
| SIGA, «Cobranza y estado de cuenta» | Columna «End.» (RF-02). |
| Tabla 0.3 y devoluciones | El paso 7 con Emisión de pólizas, marcado como supuesto. |

---

## UC-02: Anular póliza

**Actor:** Operador de Pampa, usuario de SIGA (principal). Cobranza (secundario, paso 5).

**Precondición:** La póliza existe y está vigente. El operador recibió un pedido de anulación.

**Flujo principal:**
1. El operador abre «Cobranza y estado de cuenta».
2. Se ejecuta UC-03 Seleccionar póliza (include).
3. El operador pulsa «Anular» en la fila de la póliza.
4. El sistema pasa la póliza a «Anulada» y quita el botón «Anular» de la fila.
5. El sistema confirma la anulación a Cobranza. [NEEDS CLARIFICATION: flujo supuesto. Decide: docente.]

**Flujo(s) alternativo(s):**
- 1a. El pedido llega de Cobranza por impago: se sigue desde el paso 2. [NEEDS CLARIFICATION: la regla de cuándo se anula por impago es de Cobranza (frente 8); el flujo es un supuesto.]
- 3a. La póliza ya está anulada: el sistema no ofrece el botón «Anular» (RF-04).

**Postcondición:** La póliza queda «Anulada» y no se puede volver a anular. [NEEDS CLARIFICATION: si la anulación cuenta como endoso (hallazgo E1-2). Decide: Sistemas.]

**Relaciones con otros casos de uso:**

| Relación | Caso de uso relacionado | Tipo (include/extend) | Justificación |
|----------|--------------------------|------------------------|----------------|
| UC-02 → UC-03 | Seleccionar póliza | include | Siempre se ejecuta: el botón «Anular» está en la fila de una póliza, así que la póliza se elige antes. |

## Fragmentos considerados para este caso de uso

| Fragmento | Qué aporta al caso de uso |
|-----------|------------------------------|
| SIGA, «Cobranza y estado de cuenta» | Botón «Anular», estado «Anulada» y fila sin botón. |
| Tabla 0.3 y devoluciones | Los pasos con Cobranza, marcados como supuestos. |

---

## UC-03: Seleccionar póliza

**Actor:** Operador de Pampa, usuario de SIGA.

**Precondición:** El operador está en «Endosos y modificaciones» o en «Cobranza y estado de cuenta».

**Flujo principal:**
1. El operador elige la póliza en la lista de la pantalla.
2. El sistema muestra los datos de la póliza (tomador, dominio, estado).

**Flujo(s) alternativo(s):**
- 1a. La póliza no está en la lista: el operador no puede continuar. [NEEDS CLARIFICATION: SIGA no muestra una búsqueda ni qué pasa si falta la póliza.]

**Postcondición:** La póliza queda seleccionada para el caso de uso que lo incluye.

**Relaciones con otros casos de uso:** incluido por UC-01 y UC-02 (ver arriba).

## Fragmentos considerados para este caso de uso

| Fragmento | Qué aporta al caso de uso |
|-----------|------------------------------|
| SIGA, «Endosos y modificaciones» y «Cobranza y estado de cuenta» | La póliza se elige de una lista antes de actuar sobre ella. |

---

## UC-04: Registrar detalle del endoso

**Actor:** Operador de Pampa, usuario de SIGA.

**Precondición:** El operador está aplicando un endoso (UC-01) y eligió el tipo de modificación.

**Flujo principal:**
1. El operador escribe el detalle en el campo «Detalle».
2. El sistema lo guarda junto con el endoso al aplicarlo.

**Flujo(s) alternativo(s):**
- 1a. El operador deja el campo vacío: el endoso se guarda sin detalle (así funciona hoy, E0-2). [NEEDS CLARIFICATION: RF-06, si el detalle pasa a ser obligatorio. Decide: docente.]

**Postcondición:** El endoso queda registrado con su detalle.

**Relaciones con otros casos de uso:**

| Relación | Caso de uso relacionado | Tipo (include/extend) | Justificación |
|----------|--------------------------|------------------------|----------------|
| UC-04 → UC-01 | Aplicar endoso | extend | Solo ocurre si el operador escribe un detalle; si pasa a ser obligatorio (RF-06), sería include. |

## Fragmentos considerados para este caso de uso

| Fragmento | Qué aporta al caso de uso |
|-----------|------------------------------|
| SIGA, «Endosos y modificaciones», columna «Detalle» | El campo es opcional y tres de cinco endosos de AU-098771 lo tienen vacío (E2-2). |
