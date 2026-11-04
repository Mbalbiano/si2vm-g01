# Requerimientos · Frente 3 · Endosos y anulaciones

Convención: ver `skill/SKILL.md`. Fuentes: Caso (Aseguradora Pampa), Acta de la 2.ª reunión, SIGA (fuente complementaria).

## Requerimientos funcionales

| ID | Issue | Requerimiento | Nivel / Tipo | Fuente | Criterio de verificación |
|----|-------|---------------|--------------|--------|--------------------------|
| RF-01 | G01-2 | El sistema debe registrar cada endoso con la póliza, el tipo de modificación, la fecha y hora y el usuario que lo aplicó. | Sistema / Funcional | Caso §6 (endoso) y §2.1; Acta §3.1; SIGA, «Endosos registrados» (campos) | En cualquier endoso registrado se ven póliza, tipo, fecha y hora y usuario. |
| RF-02 | G01-3 | El sistema debe aumentar en uno la cantidad de endosos de una póliza cada vez que se aplica un endoso. [NEEDS CLARIFICATION: ¿el negocio necesita la cantidad de endosos de una póliza? Solo la muestra SIGA, en la columna «End.». Decide: Gerencia Técnica.] | Sistema / Funcional | SIGA, columna «End.»; hallazgo E1-4 | Pendiente. |
| RF-03 | G01-4 | El sistema debe permitir anular una póliza vigente. | Usuario / Funcional | Caso §6 (anulación) y §2.1; SIGA, botón «Anular» | Al anular una póliza vigente, su estado pasa a «Anulada». |
| RF-04 | G01-28 | El sistema no debe permitir anular una póliza que ya está anulada. | Negocio / Funcional | Caso §6 (deducido); SIGA, filas «Anulada» sin botón | En una póliza anulada no se ofrece ni se acepta la acción de anular. |
| RF-05 | G01-19 | El sistema debe registrar quién solicita cada endoso o anulación. [NEEDS CLARIFICATION: Caso §6 nombra al asegurado y la falta de pago como orígenes de la anulación, pero ninguna fuente dice si el solicitante es obligatorio ni si puede ser el productor. Decide: Gerencia Técnica.] | Negocio / Funcional | Caso §6, §1.1; Acta §3.4; hallazgo E0-1 | Pendiente. |
| RF-06 | G01-7 | El sistema debe exigir el detalle para guardar un endoso. [NEEDS CLARIFICATION: en SIGA el detalle es opcional (E0-2, E2-2) y ninguna fuente dice si debe ser obligatorio. Decide: Gerencia Técnica.] | Negocio / Funcional | Hallazgos E0-2 y E2-2 | Pendiente. |
| RF-07 | G01-8 | El sistema debe emitir una constancia de cada endoso o anulación. [NEEDS CLARIFICATION: el Caso §5 no lista ninguna constancia y SIGA no muestra ninguna (E1-5). Decide: Gerencia Técnica; H. Vidal confirma si existe fuera de SIGA.] | Usuario / Funcional | Caso §5; hallazgo E1-5 | Pendiente. |
| RF-08 | G01-9 | El sistema debe informar a Emisión de pólizas los datos de la póliza modificada por un endoso. [NEEDS CLARIFICATION: ninguna fuente describe un aviso entre endosos y emisión. Decide: A. Pampín.] | Sistema / Funcional | Acta §3.1; tabla 0.3 | Pendiente. |
| RF-09 | G01-10 | El sistema debe permitir aplicar a una póliza vigente un endoso de cambio de domicilio. | Usuario / Funcional | Caso §2.1 y §6; Acta §3.1 | Aplicado el endoso, queda registrado con el tipo «Cambio de domicilio» y la póliza sigue vigente. |
| RF-10 | G01-11 | El sistema debe permitir aplicar a una póliza vigente un endoso de cambio de forma de pago. | Usuario / Funcional | Caso §2.1 y §6; Acta §3.1 | Aplicado el endoso, queda registrado con el tipo «Cambio de forma de pago» y la póliza sigue vigente. |
| RF-11 | G01-12 | El sistema debe permitir aplicar a una póliza vigente un endoso de cambio de vehículo. [NEEDS CLARIFICATION: Caso §6 lo nombra como endoso; Caso §2.1 dice que SIGA no lo permite y se resuelve anulando y reemitiendo, pero el desplegable de SIGA lo ofrece (E3-1). Decide: Gerencia Técnica.] | Usuario / Funcional | Caso §2.1 y §6; hallazgo E3-1 | Pendiente. |
| RF-12 | G01-13 | El sistema debe permitir aplicar a una póliza vigente un endoso de cambio de cobertura. [NEEDS CLARIFICATION: mismo conflicto que RF-11. Decide: Gerencia Técnica.] | Usuario / Funcional | Caso §2.1 y §6; hallazgo E3-1 | Pendiente. |

## Fragmentos que NO son requerimientos funcionales

| Fragmento | Texto | Categoría | Justificación |
|-----------|-------|-----------|----------------|
| Devolución de la E1 | Débito, conciliación y cuotas impagas son de Cobranza (frente 8) | Dato de contexto | Delimita el alcance; no pide nada al frente 3. |
| SIGA, pie de pantalla | «La conciliación con el archivo del banco se ejecuta una vez por mes, en forma manual» | Dato de contexto | Describe un proceso de Cobranza (frente 8). |
| SIGA, pie de la ventana | Desarrollado en 2003, sin documentación técnica ni funcional | Dato de contexto | Describe el sistema actual; no pide una función. |
| Acta §4.5 | La Dirección pide un sistema rápido y usable sin capacitación | RNF | Sin métrica: no se puede responder sí o no. |

## Conflictos u observaciones detectadas

- Tipos de endoso: Caso §2.1 (SIGA solo permite domicilio y forma de pago) contra Caso §6 (el glosario nombra cuatro tipos) y contra el desplegable de SIGA (seis tipos, E3-1). Se resuelve en RF-11 y RF-12. [NEEDS CLARIFICATION: Decide: Gerencia Técnica.]
- «Vigente» en RF-03: [NEEDS CLARIFICATION: ¿«vigente» incluye una póliza con «Vigencia hasta» anterior a la fecha de hoy? Caso §6 define la anulación como baja antes del fin de la vigencia; SIGA ofrece «Anular» en AU-098771 (15/01/2026). Decide: Gerencia Técnica.]
- Acta §4.4: sin decidir qué pólizas se migran al sistema nuevo, no se sabe cuáles se podrán endosar o anular el 01/03/2027. Decide: A. Pampín y H. Vidal.
- Usuario que aplica el endoso: RF-01 pide registrarlo, pero ningún requerimiento dice cómo se identifica el operador. [NEEDS CLARIFICATION: ¿cómo se identifica al operador que aplica un endoso? Decide: H. Vidal.]
- Endosos sobre pólizas anuladas: SIGA los acepta (E3-8). [NEEDS CLARIFICATION: ¿el sistema nuevo debe permitir endosar una póliza anulada? Decide: Gerencia Técnica.]
- La anulación como endoso: SIGA la registra como un endoso más y suma uno a «End.» (E3-9). [NEEDS CLARIFICATION: ¿el sistema nuevo debe registrar la anulación como endoso? Decide: Gerencia Técnica.]
