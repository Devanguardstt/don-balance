# Renta, cierre y apertura

> Fuente: guía de Don Balance para Control Total Advance Automatizado v7.6.22, §6.11. Las menciones «§N» apuntan a otras secciones de esa guía; ../SKILL.md indica en qué archivo está cada una.

### 6.11 Renta y cierre · *• Asientos › Procesos anuales › Renta y cierre del ejercicio…*
Pasos: **Resumen → Régimen y revisión → Base tributaria → PPM y créditos → Determinación → Impuesto y cierre → Declaraciones**.

1. **Resumen:** qué falta. «Usar las de AAAA» copia las clasificaciones del año anterior para revisarlas.
2. **Régimen y revisión:** confirma el régimen y resuelve observaciones: cuentas sin clasificar, movimientos que no forman la base, tasa vacía o distinta.
3. **Base tributaria:** clasifica las cuentas y orígenes que el sistema no pudo deducir. «Detalle por cuenta (CSV)» sirve para revisar con calma.
4. **PPM y créditos:** los PPM pagados salen del F29 y del libro. Se agregan créditos si corresponden.
5. **Determinación:** renta líquida imponible e impuesto. «Guardar antecedentes» **no contabiliza**.
6. **Impuesto y cierre:**
   - **«Registrar el impuesto en el Libro Diario»** (dorado, con OK) crea el asiento al 31-12.
   - Luego «Cerrar el ejercicio AAAA» escribe Config C49 y bloquea esas fechas en todos los módulos. Se puede reabrir con un motivo.
   - Con el año cerrado, «Preparar la hoja "Apertura AAAA"» arma los saldos iniciales del año siguiente.
7. **Declaraciones:** Balance de 8 columnas (PDF), la planilla de apoyo de la DJ 1887 (CSV) y el registro de la fecha y el folio de lo presentado.

**Apertura del año siguiente:**
1. La hoja «Apertura AAAA» se copia al libro del año nuevo.
2. En el libro nuevo, *Renta y cierre › Vista previa de la apertura* comprueba la empresa y las cuentas.
3. «Registrar la apertura en el Libro Diario».
4. Los documentos pendientes quedan en CxC y CxP.

| Acción | Qué escribe |
|---|---|
| PDF de la determinación | Solo un archivo en Drive |
| Guardar antecedentes | Respuestas en una hoja técnica. No contabiliza |
| Registrar el impuesto | Un asiento al 31-12. Con el año abierto se puede eliminar y volver a registrar |
| Cerrar el ejercicio | La fecha de cierre (C49). No contabiliza |
| Registrar la apertura | El asiento de apertura en el libro del año siguiente |

El **pago del impuesto anual** se registra en el año en que se paga, con un **Egreso** desde la cuenta de impuesto por pagar.
