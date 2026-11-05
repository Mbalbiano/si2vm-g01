# specs/requirements.md actualizado

## Tabla de Requerimientos Funcionales

| ID | Issue | Requerimiento | Nivel / Tipo | Fuente | Criterio de verificación |
|---|---|---|---|---|---|
| **RF-01** | G01-16 | El sistema debe registrar cada endoso con la póliza, el tipo de modificación, la fecha y hora y el usuario que lo aplicó. | Sistema / Funcional | Caso §6 (endoso) y §2.1; Acta §3.1; SIGA, «Endosos registrados» (campos) | En cualquier endoso registrado se ven póliza, tipo, fecha y hora y usuario. |
| **RF-02** | G01-18 | El sistema debe aumentar en uno la cantidad de endosos de una póliza cada vez que se aplica un endoso. [NEEDS CLARIFICATION: ¿el negocio necesita la cantidad de endosos de una póliza? Solo la muestra SIGA, en la columna «End.». Decide: Gerencia Técnica.] | Sistema / Funcional | SIGA, columna «End.»; hallazgo E1-4 | Pendiente. |
| **RF-03** | G01-17 | El sistema debe permitir anular una póliza vigente. | Usuario / Funcional | Caso §6 (anulación) y §2.1; SIGA, botón «Anular» | Al anular una póliza vigente, su estado pasa a «Anulada». |
| **RF-04** | G01-28 | El sistema no debe permitir anular una póliza que ya está anulada. | Negocio / Funcional | Caso §6 (deducido); SIGA, filas «Anulada» sin botón | En una póliza anulada no se ofrece ni se acepta la acción de anular. |
| **RF-05** | G01-19 | El sistema debe registrar quién solicita cada endoso o anulación. [NEEDS CLARIFICATION: Caso §6 nombra al asegurado y la falta de pago como orígenes de la anulación, pero ninguna fuente dice si el solicitante es obligatorio ni si puede ser el productor. Decide: Gerencia Técnica.] | Negocio / Funcional | Caso §6, §1.1; Acta §3.4; hallazgo E0-1 | Pendiente. |
| **RF-06** | G01-20 | El sistema debe exigir el detalle para guardar un endoso. [NEEDS CLARIFICATION: en SIGA el detalle es opcional (E0-2, E2-2) y ninguna fuente dice si debe ser obligatorio. Decide: Gerencia Técnica.] | Negocio / Funcional | Hallazgos E0-2 y E2-2 | Pendiente. |
| **RF-07** | G01-29 | El sistema debe emitir una constancia de cada endoso o anulación. [NEEDS CLARIFICATION: el Caso §5 no lista ninguna constancia y SIGA no muestra ninguna (E1-5). Decide: Gerencia Técnica; H. Vidal confirma si existe fuera de SIGA.] | Usuario / Funcional | Caso §5; hallazgo E1-5 | Pendiente. |
| **RF-08** | G01-22 | El sistema debe informar a Emisión de pólizas los datos de la póliza modificada por un endoso. [NEEDS CLARIFICATION: ninguna fuente describe un aviso entre endosos y emisión. Decide: A. Pampín.] | Sistema / Funcional | Acta §3.1; tabla 0.3 | Pendiente. |
| **RF-09** | G01-23 | El sistema debe permitir aplicar a una póliza vigente un endoso de cambio de domicilio. | Usuario / Funcional | Caso §2.1 y §6; Acta §3.1 | Aplicado el endoso, queda registrado con el tipo «Cambio de domicilio» y la póliza sigue vigente. |
| **RF-10** | G01-25 | El sistema debe permitir aplicar a una póliza vigente un endoso de cambio de forma de pago. | Usuario / Funcional | Caso §2.1 y §6; Acta §3.1 | Aplicado el endoso, queda registrado con el tipo «Cambio de forma de pago» y la póliza sigue vigente. |
| **RF-11 (v2)** | G01-26 | El sistema debe permitir aplicar a una póliza vigente un endoso de cambio de vehículo, sin cambiar el número ni la vigencia de la póliza. | Usuario / Funcional | Caso §2.1 y §6; Acta 3.ª §3.3; hallazgo E3-1 | Aplicado el endoso, queda registrado con el tipo «Cambio de vehículo» y la póliza sigue vigente con el mismo número y la misma vigencia. |
| **RF-12 (v2)** | G01-27 | El sistema debe permitir aplicar a una póliza vigente un endoso de cambio de cobertura, sin cambiar el número ni la vigencia de la póliza. | Usuario / Funcional | Caso §2.1 y §6; Acta 3.ª §3.3; hallazgo E3-1 | Aplicado el endoso, queda registrado con el tipo «Cambio de cobertura» y la póliza sigue vigente con el mismo número y la misma vigencia. |
| **RF-13 (nuevo)** | G01-33 | El sistema debe recalcular el premio con la tarifa vigente al aplicar un endoso de cambio de vehículo o de cobertura y aplicar la diferencia en proporción a los días que faltan para el fin de la vigencia. [NEEDS CLARIFICATION: el acta no dice sobre qué base se calcula la proporción (premio mensual o vigencia completa) ni de dónde salen los datos de riesgo para recalcular. La tarifa es del frente 1 (Anexo técnico 3). Decide: M. Duarte.] | Negocio / Funcional | Acta 3.ª §3.3; Anexo técnico 3 (tarifario v3) | Pendiente. |
| **RF-14 (nuevo)** | G01-34 | El sistema debe aplicar al vehículo nuevo de un endoso de cambio de vehículo los mismos controles que en una emisión (antigüedad máxima y umbral de suscripción) y rechazar el endoso si no los pasa. [NEEDS CLARIFICATION: en la emisión, superar el umbral lleva la solicitud a suscripción; acá el acta dice que el endoso se rechaza. ¿Rechazo directo o derivación a suscripción? Decide: R. Ferreyra.] | Negocio / Funcional | Acta 3.ª §3.3 y §3.2; Acta 2.ª §3.3 | Con un vehículo nuevo de valor $50.000.000, el endoso se rechaza, no se registra y la póliza conserva su vehículo; con $45.000.000 se acepta. Con un vehículo de 21 años (tope de 20, Acta 2.ª §3.3) se rechaza, y con 20 años se acepta. |
| **RF-15 (nuevo)** | G01-35 | El sistema debe aplicar al cliente la diferencia de premio a su favor de un endoso. [NEEDS CLARIFICATION: Acta 3.ª §4.2: ¿se devuelve o se descuenta de las cuotas siguientes? Decide: M. Duarte (20/11/2026).] | Negocio / Funcional | Acta 3.ª §3.3 (observación) y §4.2 | Pendiente. |

---

## Fragmentos que NO son Requerimientos Funcionales

*(Sin cambios)*
* **Devolución de la E1:** Cobranza es del frente 8.
* **Pie de pantalla de SIGA sobre la conciliación y pie de ventana (desarrollado en 2003):** Datos de contexto.
* **Acta §4.5 (sistema rápido y usable):** RNF sin métrica.

---

## Conflictos u Observaciones Detectadas

* **Tipos de endoso:** Caso §2.1 contra Caso §6 y el desplegable de SIGA (seis tipos, E3-1). Resuelto en parte por Acta 3.ª §3.3: vehículo y cobertura son endosos (RF-11 y RF-12, versión 2, issue G01-15). Sigue abierto el conductor habitual y la suma asegurada. `[NEEDS CLARIFICATION: ¿son endosos del sistema nuevo? Decide: Gerencia Técnica.]`
* **Cobertura y controles:** `[NEEDS CLARIFICATION: ¿un cambio de cobertura debe pasar los controles de la tarifa (por ejemplo, Todo Riesgo en un vehículo de 21 años o más, Anexo técnico 3 §4)? Decide: R. Ferreyra.]`
* **Quién ejecuta los controles del vehículo nuevo:** `[NEEDS CLARIFICATION: ¿los hace el frente 3 o los pide a Emisión de pólizas (flujo nuevo con una entidad externa)? Decide: A. Pampín.]`
* **Datos del vehículo nuevo:** `[NEEDS CLARIFICATION: ¿qué datos del vehículo nuevo se cargan (patente, modelo, año, valor)? Decide: Gerencia Técnica.]`
* **Anular y reemitir:** Acta 3.ª §3.3 lo deja solo para el cambio de tomador, que no es un tipo de endoso de este frente. No cambia ningún requerimiento.
* **«Vigente» en RF-03:** `[NEEDS CLARIFICATION: ¿«vigente» incluye una póliza con «Vigencia hasta» anterior a la fecha de hoy? Decide: Gerencia Técnica.]`
* **Acta §4.4:** Sin decidir qué pólizas se migran, no se sabe cuáles se podrán endosar o anular el 01/03/2027. `[Decide: A. Pampín y H. Vidal.]`
* **Usuario que aplica el endoso:** `[NEEDS CLARIFICATION: ¿cómo se identifica al operador? Decide: H. Vidal.]`
* **Endosos sobre pólizas anuladas (E3-8):** `[NEEDS CLARIFICATION: ¿el sistema nuevo debe permitirlos? Decide: Gerencia Técnica.]`
* **La anulación como endoso (E3-9):** `[NEEDS CLARIFICATION: ¿el sistema nuevo debe registrarla como endoso? Decide: Gerencia Técnica.]`
