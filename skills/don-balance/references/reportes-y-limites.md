# Reportes, revisión mensual y límites del sistema

> Fuente: guía de Don Balance para Control Total Advance Automatizado v7.6.22, §10, §11. Las menciones «§N» apuntan a otras secciones de esa guía; ../SKILL.md indica en qué archivo está cada una.

## 10. Reportes y revisión mensual

| Acceso | Qué muestra | Fechas |
|---|---|---|
| ▸ Estado de Resultados (PDF) | Ingresos, costos, gastos y resultado | Inicio del ejercicio al cierre del mes de corte |
| ▸ Estado de Situación Financiera (PDF) | Activos, pasivos y patrimonio | Saldos al corte |
| ▸ Balance de 8 Columnas (PDF)… | Sumas, saldos, inventario y resultados | Al corte, o un período desde/hasta |
| ▸ Libro de caja… | Movimientos de caja y bancos, en vista contable o tributaria, con CSV y PDF | Desde/hasta |
| ▸ Informe Financiero mensual (PDF) | Balance, resultados, flujo y ratios por mes | Meses hasta el corte |
| ▸ Determinación de la renta (PDF) | Lo guardado en Renta y cierre. **No es el F22** | Año comercial |

- Los PDF y CSV se guardan en la **carpeta principal del Drive** del usuario. El cuadro ofrece «Abrir PDF» y «Descargar».
- La hoja **Ratios Financieros** tiene 20 indicadores:
  - Liquidez: razón corriente, prueba ácida, capital de trabajo.
  - Endeudamiento: razón de deuda, apalancamiento.
  - Márgenes: bruto, operacional, antes de impuestos, neto, EBITDA.
  - Rentabilidad: ROE, ROA, ROIC.
  - Gestión: días de cobro y de pago, rotación de inventarios, de activos y de activos fijos.
  - Cobertura de intereses y eficiencia operativa.

  El ROIC queda «Sin datos» si C36 está vacía.
- **Filtros por dimensión:** en Estado Resultados y Flujo de Caja, las celdas **O1** (dimensión) y **O2** (valor). Déjalos en «Todos» antes de exportar.

**Antes de exportar o dar el mes por cerrado:**
- No hay asientos en rojo.
- El Balance General tiene las sumas iguales.
- Config tiene la razón social, el RUT y la fecha de actualización al día.
- Los filtros O1 y O2 están en «Todos».
- IVA Mensual coincide con las cuentas de IVA del Mayor.

## 11. Lo que el sistema NO hace (no lo prometas)
- No se conecta al SII, al banco, a la DT ni a Previred: **todo entra por archivo**.
- No presenta ni paga el F29, el F22 ni las declaraciones juradas.
- No emite facturas ni boletas.
- No calcula liquidaciones de sueldo: contabiliza las ya calculadas.
- Hoy solo importa cartolas de **Mercado Pago**.
- No determina la renta presunta.
- Nada se contabiliza solo: cada lote lo confirma el usuario.
- No envía correos ni tiene tareas programadas.
