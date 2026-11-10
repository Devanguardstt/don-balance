# Procesos mensuales: F29, remuneraciones, honorarios y activos fijos

> Fuente: guía de Don Balance para Control Total Advance Automatizado v7.6.22, §6.7–§6.10. Las menciones «§N» apuntan a otras secciones de esa guía; ../SKILL.md indica en qué archivo está cada una.

### 6.7 F29 · *• Asientos › Procesos mensuales › Impuestos mensuales (F29)…*
Tres pasos separados por mes. **El módulo no presenta ni paga.**

**Configuración inicial (la primera vez):**
- Cuentas de IVA y PPM: con el plan sugerido son 1-15-04 remanente, 2-15-04 IVA por pagar y 2-15-03 PPM por pagar.
- Primer mes que se llevará aquí.
- Retenciones, si el F29 trae código 48 o 151.

**Cada mes:**
1. **Registrar lo declarado:**
   - Tipo, folio, fecha de presentación y los códigos tal como se presentaron: 538 débito, 504 remanente anterior, 537 total créditos, 62 PPM, 48, 151…
   - «Precargar la propuesta» trae la estimación de la hoja IVA Mensual para comparar. Si un código difiere, se pide el motivo.
   - *Guardar lo declarado* (con borde) no contabiliza.
2. **Contabilizar:** «Revisar los asientos que genera →» muestra la liquidación de IVA, el PPM y el reajuste del remanente. Luego **«Registrar estos asientos»** (dorado, con OK). Queda «Contabilizado · Pendiente de pago».
3. **Registrar el pago:** fecha, banco e importe (más recargos si fue fuera de plazo).
   - Un pago menor deja el período «Pagado en parte».
   - Si el pago ya está como asiento manual, usa **«Adoptar como pago de este F29»** para no duplicarlo.

**Estados de un período:** Sin registrar · Borrador · faltan datos · Listo para contabilizar · Contabilizado · Pendiente de pago · Pagado en parte · Pagado.

### 6.8 Remuneraciones · *• Asientos › Procesos mensuales › Remuneraciones…*
**El sistema no calcula sueldos**: contabiliza remuneraciones ya calculadas. Hay tres fechas distintas:
- El **mes de la remuneración**.
- La **fecha de contabilización**, por ejemplo el 31/03.
- La **fecha de pago**, por ejemplo el 05/04 para los líquidos y el 13/04 para las cotizaciones.

**Camino A, a mano:**
1. «Preparar un mes…»: mes, proceso y trabajadores.
2. «Agregar filas a la hoja».
3. En la hoja Remuneraciones, escribe los importes por concepto (SUELDO, GRATIF, AFP, SALUD, IMPUNICO…). No crees filas a mano.
4. Vuelve al formulario: «Actualizar», el mes, *1 · Revisar y contabilizar*, «Contabilizar remuneraciones» (dorado).

**Camino B, LRE:**
1. *• Importaciones › Importar Libro de Remuneraciones de RRHH (LRE)…*: el mismo CSV que se carga en Mi DT (o CT-REM), sin convertir.
2. El formulario propone el mes por el nombre del archivo (`<RUT>_<AAAAMM>.csv`) y reconoce la empresa.
3. Los códigos del LRE sin concepto piden una correspondencia, que queda recordada.
4. Un trabajador nuevo se da de alta por su RUT.
5. «Importar» escribe los importes en la hoja, **sin contabilizar**. Luego sigue como en el camino A.

**Pagos:**
- *2 · Pagar líquidos*.
- *3 · Pagar obligaciones* (cotizaciones). El **impuesto único (48) se paga con el F29**.
- Si un pago ya existe como asiento manual: *Pagos externos › Adoptar como pago de este mes*.

**Conceptos por omisión:**

| Concepto | Naturaleza | Cuenta |
|---|---|---|
| SUELDO, GRATIF, HEXTRA, BONOS, NOIMP | Haberes | 6-11-01 |
| ASIGFAM (asignación familiar) | Recuperable | 1-13-03 |
| AFP, SALUD, AFC_T | Cotización del trabajador | 2-14-01 |
| AFC_E, SIS, MUTUAL | Aportes del empleador | Gasto 6-11-02 contra 2-14-01 |
| IMPUNICO | Impuesto único | 2-14-02 |
| ANTICIPO | Anticipo | 1-13-01 |
| DESC_AUT (otros descuentos autorizados) | Descuento | 2-14-04 |

Si la hoja cambia después de contabilizar, el estado dice «la hoja cambió: falta la diferencia».

### 6.9 Boletas de honorarios recibidas · *Procesos mensuales › Boletas de honorarios recibidas…*
1. **Configuración** (la primera vez): gasto 6-13-01, honorarios por pagar 2-13-03 y retención 151 en 2-14-03. Es la misma cuenta del 151 que usa el F29.
2. Elige o arrastra el **informe mensual de boletas recibidas del SII** (.xls, .htm o .html). La vista muestra el período, los totales y cada boleta.
3. «Importar n boleta(s)»: todavía no hay asientos. No se repiten las ya importadas.
4. Marca las boletas y «Contabilizar las elegidas». Revisa la vista previa (gasto bruto al Debe; retención y líquido por pagar al Haber) y confirma con OK.
5. **Pago:** abre la boleta, fecha, cuenta e importe, «Registrar el pago». Si el pago ya está en el Diario, usa «Ya está en el Libro Diario: asociarlo…».
6. **Confirma la retención por mes**: se declara en el F29 del **mes en que se pagó** la boleta.

Un pago anterior a la boleta se marca como «Es un anticipo de esta boleta». Un pago menor deja la boleta pagada en parte.

### 6.10 Activos fijos · *Procesos mensuales › Activos fijos y depreciación…*
**La compra del activo se registra una sola vez**, desde el RCV o un asiento. Aquí solo se crea la ficha.

| Forma | Cuándo usarla |
|---|---|
| **Desde el Diario** | La compra ya está contabilizada. Se elige la línea en «Líneas del Diario sin ficha» y se completan descripción, categoría, mes disponible para uso, vida útil en meses y valor residual |
| **Existente al corte** | Activo anterior a llevar la contabilidad aquí. Se completan costo, depreciación acumulada al corte, mes de corte, vida restante, fecha de adquisición y vida útil total. **No se usa para compras de este año** |

**Depreciar:** *Depreciar › Por contabilizar*, «Depreciar hasta» el último mes, Vista previa y «Contabilizar n meses» (dorado). Asiento: gasto 6-14-01 contra depreciación acumulada 1-22-01.

**Bajas y ventas:** revierten la acumulada y llevan el valor libro a resultados. También hay:
- **Cambio de estimación:** ajusta la vida restante.
- **Corregir: no era activo:** retira algo que nunca debió capitalizarse.
- **A gasto:** lleva a gasto la parte de una compra que no es activo.
