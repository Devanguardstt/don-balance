# Conocimiento contable

> Fuente: guía de Don Balance para Control Total Advance Automatizado v7.6.22, §7. Las menciones «§N» apuntan a otras secciones de esa guía; ../SKILL.md indica en qué archivo está cada una.

## 7. Conocimiento contable para guiar al usuario

### 7.1 Partida doble y naturaleza de las cuentas
- Cada asiento tiene **debe = haber**. En el Libro Diario se ve en el color del N° de asiento.
- **Cuentas deudoras** (aumentan al Debe): activos (1), costos (5) y gastos (6, 7). También las cuentas de retiros (3-15-01).
- **Cuentas acreedoras** (aumentan al Haber): pasivos (2), patrimonio (3) e ingresos (4). También las correctoras de activo, como la depreciación acumulada 1-22-01.

### 7.2 Cuentas clave del plan sugerido
| Código | Cuenta | Uso |
|---|---|---|
| 1-11-01 / 1-11-02 | Caja / Bancos | Efectivo |
| 1-12-01 | Clientes | Facturas por cobrar |
| 1-13-01 | Otras cuentas por cobrar y anticipos | Anticipos al personal |
| 1-13-03 | Asignación familiar por recuperar | Remuneraciones |
| 1-14-01 | Inventarios | Existencias |
| 1-15-01 | IVA Crédito Fiscal | IVA de compras (función única) |
| 1-15-02 | Pagos Provisionales Mensuales | PPM pagados, crédito contra la renta |
| 1-15-04 | Remanente de Crédito Fiscal | Crédito de IVA que pasa al mes siguiente |
| 1-21-01 / 1-22-01 | Propiedades, planta y equipo / Depreciación acumulada | Activos fijos |
| 2-11-01 | Proveedores y cuentas comerciales por pagar | Facturas por pagar |
| 2-13-01 | Remuneraciones por pagar | Líquidos |
| 2-13-03 | Honorarios por pagar | Líquido de boletas |
| 2-14-01 | Cotizaciones previsionales por pagar | AFP, salud, AFC, SIS, mutual |
| 2-14-02 | Retenciones y otras obligaciones laborales | Impuesto único (48) |
| 2-14-03 | Retenciones de honorarios por pagar | Código 151 |
| 2-14-04 | Otros descuentos al personal por pagar | Caja de compensación, sindicato… |
| 2-15-01 | IVA Débito Fiscal | IVA de ventas (función única) |
| 2-15-02 | Impuesto a la renta por pagar | Impuesto anual |
| 2-15-03 | Otros impuestos por pagar | PPM por pagar del F29 |
| 2-15-04 | IVA por pagar | IVA determinado del F29 |
| 3-11-01 | Capital social y aportes | Patrimonio |
| 3-13-01 | Resultados acumulados | Años anteriores |
| 3-14-01 | Resultado del ejercicio | Función única |
| 3-15-01 | Dividendos, retiros y distribuciones | Retiros del dueño |
| 4-11-01 / 4-11-02 | Ventas de bienes / Ingresos por servicios | Ingresos del giro |
| 5-11-01 | Costo de ventas | |
| 6-11-01 / 6-11-02 | Sueldos / Leyes sociales | Remuneraciones |
| 6-12-01 | Arriendos, servicios básicos y mantenciones | |
| 6-13-01 | Servicios profesionales y asesorías | Honorarios |
| 6-14-01 | Gasto por depreciación | |
| 7-11-01 | Gastos financieros | Intereses, comisiones bancarias |
| 7-22-01 | Gasto por impuesto a la renta corriente | Impuesto del año |

El usuario puede tener otro plan: **lee siempre P. Cuentas antes de nombrar una cuenta.**

### 7.3 Asientos tipo
Cifras ilustrativas; IVA general del 19 %. **El formulario arma el asiento**: estos ejemplos sirven para explicar la vista previa y detectar errores.

**Venta con factura (33), pendiente de cobro.** Neto 1.000.000, IVA 190.000.

| Cuenta | Debe | Haber |
|---|---|---|
| 1-12-01 Clientes | 1.190.000 | |
| 4-11-01 Ventas de Bienes | | 1.000.000 |
| 2-15-01 IVA Débito Fiscal | | 190.000 |

**Cobro de esa factura.** Bancos 1.190.000 al Debe, contra Clientes al Haber. Un abono parcial cobra menos y deja saldo en CxC.

**Compra con factura, pendiente de pago.** Neto 500.000, IVA 95.000.

| Cuenta | Debe | Haber |
|---|---|---|
| 6-12-01 (u otra cuenta de gasto, inventario o activo) | 500.000 | |
| 1-15-01 IVA Crédito Fiscal | 95.000 | |
| 2-11-01 Proveedores | | 595.000 |

**Nota de crédito de venta (61).** Es el reverso parcial o total de la factura que corrige. El sistema le da la misma cuenta de ingreso de esa factura:
- Ventas e IVA Débito al Debe.
- Clientes al Haber.

**Boleta de honorarios recibida.** Bruto 1.000.000, retención 2026 de 15,25 %.

| Cuenta | Debe | Haber |
|---|---|---|
| 6-13-01 Servicios Profesionales | 1.000.000 | |
| 2-14-03 Retenciones de honorarios por pagar (151) | | 152.500 |
| 2-13-03 Honorarios por pagar | | 847.500 |

El pago va de Honorarios por pagar (Debe) a Bancos (Haber). La retención se paga con el F29 del mes del pago.

**Remuneraciones del mes** (esquema):
- Al Debe: los haberes en 6-11-01 y los aportes del empleador en 6-11-02.
- Al Haber: las cotizaciones en 2-14-01, el impuesto único en 2-14-02, los otros descuentos en 2-14-04 y el **líquido** en 2-13-01.
- Los anticipos ya pagados rebajan el líquido contra 1-13-01.

**Liquidación del F29.** Ejemplo con débito 380.000, créditos 520.000 y PPM 30.000:

| Cuenta | Debe | Haber |
|---|---|---|
| 2-15-01 IVA Débito | 380.000 | |
| 1-15-04 Remanente de crédito fiscal | 140.000 | |
| 1-15-01 IVA Crédito | | 520.000 |
| 1-15-02 PPM | 30.000 | |
| 2-15-03 PPM por pagar | | 30.000 |

- Ese mes se paga solo el PPM.
- El mes siguiente, el remanente reajustado vuelve como código 504 y el reajuste se registra primero.
- Si el débito supera los créditos, la diferencia va a 2-15-04 IVA por pagar.

**Depreciación mensual.** 6-14-01 Gasto por depreciación al Debe, contra 1-22-01 Depreciación acumulada al Haber.
- Cuota lineal = (costo − valor residual) / vida útil en meses.
- Ejemplo: notebook de 1.800.000 a 36 meses, residual 0, deprecia 50.000 al mes.

**Traspaso banco a caja.** 1-11-01 Caja al Debe, contra 1-11-02 Bancos al Haber.

**Saldos iniciales** (Asiento libre al primer día del ejercicio). Cada activo al Debe y cada pasivo y el patrimonio al Haber, con debe = haber. Se usan solo cuentas 1, 2 y 3.

**Impuesto a la renta del año.** El módulo de Renta propone el asiento al 31-12. En general va 7-22-01 Gasto por impuesto contra 2-15-02 Impuesto a la renta por pagar, y considera los PPM (1-15-02) como crédito. Muestra siempre la vista previa del sistema; no armes este asiento a mano.

### 7.4 Cómo revisar un asiento en la vista previa
- ¿Debe = haber?
- ¿La cuenta es imputable (tres niveles, como 6-12-01) y existe en P. Cuentas?
- ¿El IVA va en IVA Débito (ventas) o IVA Crédito (compras), y no en el gasto?
- ¿La fecha está dentro del ejercicio y no en un año cerrado?
- ¿La glosa permite reconocer la operación?
- ¿La asignación (cliente, proyecto…) está en la línea correcta y no en Banco o Caja?
