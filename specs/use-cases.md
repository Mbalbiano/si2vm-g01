# specs/use-cases.md

*Nota: Solo cambia UC-01 Aplicar endoso; UC-02, UC-03 y UC-04 no cambian. El archivo completo se entregó como use-cases.md.*

---

## UC-01: Aplicar endoso

### Flujo principal (nuevo)
1. El operador abre «Endosos y modificaciones».
2. Se ejecuta UC-03 Seleccionar póliza (include).
3. El operador elige el tipo de modificación.
4. El operador aplica el endoso.
5. *(nuevo)* Si el tipo es cambio de vehículo, el sistema aplica al vehículo nuevo los controles de una emisión (RF-14). `[NEEDS CLARIFICATION: quién ejecuta los controles. Decide: A. Pampín.]`
6. *(nuevo)* Si el tipo es cambio de vehículo o de cobertura, el sistema recalcula el premio con la tarifa vigente y aplica la diferencia (RF-13). `[NEEDS CLARIFICATION: base de la proporción. Decide: M. Duarte.]`
7. El sistema registra el endoso con fecha y hora, tipo, detalle y usuario (era el paso 5).
8. El sistema muestra el endoso en «Endosos registrados» (era el 6).
9. El sistema informa a Emisión de pólizas los datos de la póliza modificada (era el 7). `[NEEDS CLARIFICATION: flujo supuesto (RF-08). Decide: A. Pampín.]`

### Flujos alternativos nuevos
* **5a.** El vehículo nuevo no pasa la antigüedad máxima o el umbral de suscripción: el sistema rechaza el endoso, no lo registra y la póliza conserva su vehículo (RF-14). `[NEEDS CLARIFICATION: ¿rechazo directo o derivación a suscripción? Decide: R. Ferreyra.]`
* **6a.** La diferencia de premio es a favor del cliente: `[NEEDS CLARIFICATION: ¿se devuelve o se descuenta de las cuotas siguientes? Decide: M. Duarte (Acta 3.ª §4.2, 20/11/2026).]` (RF-15)

### Actor secundario
* Emisión de pólizas pasa de «paso 7» a «paso 9».

### Postcondición (nueva)
* El endoso queda registrado, el estado de la póliza no cambia y conserva su número y su vigencia.

---

## Página v2: Resultados de los criterios

La página v2 se regeneró desde la especificación actualizada y pasa los 9 criterios ejecutados (los 6 de la E3 y los 3 nuevos). Se corrieron en un navegador automatizado; las capturas con la hora del sistema para el Anexo A las saca el grupo. El archivo es `index.html` (entregado aparte). Las pólizas AU-240115 a AU-240117 son de ejemplo.

| Criterio | Póliza | Resultado en la página v2 | Pasó |
|---|---|---|---|
| **RF-01** | AU-222410 | Fila con póliza, «Cambio de domicilio», fecha y hora y HECTOR.V | Sí |
| **RF-03** | AU-228696 | Pasa a «Anulada» | Sí |
| **RF-04 · A** | AU-119887 | Sin botón «Anular» | Sí |
| **RF-04 · B** | AU-203523 | Segundo intento: «Rechazado por RF-04» | Sí |
| **RF-09** | AU-201674 | Endoso aceptado; sigue «Al dia» | Sí |
| **RF-10** | AU-203611 | Registrado como «Cambio de forma de pago»; sigue «Al dia» | Sí |
| **RF-11 (con $45.000.000)** | AU-240115 | Aceptado, registrado como «Cambio de vehículo», mismo número y vigencia (30/09/2027) | Sí |
| **RF-12** | AU-240117 | Aceptado, registrado como «Cambio de cobertura», mismo número y vigencia | Sí |
| **RF-14 · A (con $50.000.000)** | AU-240116 | Rechazado; no se registra (5 filas antes y después) | Sí |

---

## Observaciones de implementación y agente

* **Qué cambió de v1 a v2:** El desplegable pasa de 2 a 4 tipos; aparece el campo «Valor del vehículo nuevo» solo con «Cambio de vehículo»; el endoso aceptado informa que la póliza conserva número y vigencia; el panel de pendientes suma RF-13, RF-14 (antigüedad), RF-15 y conductor habitual/suma asegurada, y quita RF-11 y RF-12.
* **Lo que la página no pudo hacer, y por qué:** No calcula el premio (RF-13) ni la diferencia: la especificación no dice de dónde salen la tarifa ni los datos de riesgo. No controla la antigüedad: falta su valor. Solo pide el valor del vehículo nuevo: ningún requerimiento dice qué otros datos se cargan.
* **Aclaración sobre el agente:** La v2 la generó Claude (Sonnet 5.5) en esta sesión con el mismo prompt de la 3.3 más la línea del cambio. La v1 se hizo en claude.ai: si quieren registrar exactamente el mismo entorno, pueden repetir el prompt allí.
