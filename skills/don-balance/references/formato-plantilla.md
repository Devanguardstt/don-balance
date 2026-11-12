# Formato de la plantilla: cómo debe quedar cada dato

> Es el destino fijo de toda carga, venga el dato de donde venga. Verificado por lectura (cabeceras, tipos de celda, validaciones y fórmulas) en una copia de Control Total Advance Automatizado (FIN-06) v7.6.22 el 2026-11-12, más los archivos de demo del producto. Etiquetas: **Verificado** · **Documentado** (guía o Ficha) · **Inferido** · **Pendiente**.
>
> **Antes de cargar, leer siempre la cabecera y la fila de ejemplo de la hoja viva** con el conector: la copia del cliente puede traer otra versión.

## 1. Libro Diario (cabecera fila 4, datos desde la fila 5)

Una fila por línea de asiento. Todas las líneas de un asiento repiten el mismo N°.

| Col | Campo | Tipo real de la celda | Regla |
|---|---|---|---|
| F | N° Asiento | Número entero | Igual en todas las líneas del asiento. No repetir un N° ya usado: leer el máximo de F y seguir desde ahí |
| G | Fecha | **Fecha real** (formato dd/mm/aaaa) | Validación estricta: una fecha inexistente se rechaza o, al pegar, rompe el Libro de caja (E-04). Dentro del ejercicio de Config |
| H | Cuenta contable | **Texto** `código \| nombre` | Validación estricta contra `P. Cuentas!G6:G2073`. Ejemplo exacto: `1-12-01 \| Clientes`. Sin espacios de más |
| I | Monto Debe | Número (formato `$#,##0`) | Entero en pesos, sin texto. Vacío si la línea es de Haber |
| J | Monto Haber | Número | Vacío si la línea es de Debe |
| K | Glosa | Texto | Una por línea; incluir tipo y folio del documento |
| L | Libro Compra | Lista: `RCV Compras!P` | Solo con el documento ya en esa hoja |
| M | Libro Venta | Lista: `RCV Ventas!P` | Ídem |
| N | ID CxC | Lista: `CxC!AC` | Lo crean los formularios |
| O | ID CxP | Lista: `CxP!AC` | Ídem |
| P | Ref. Cartola | Lista: `Cartola Bancaria!O` | Solo en la línea de Efectivo (Caja o Bancos) |
| Q | Cliente | Lista: `Clientes!B` | El nombre debe existir **exacto** en el maestro |
| R | Proveedor | Lista: `Proveedores!B` | Ídem |
| S | Personal | Lista: `Personal!B` | Ídem |
| T | Sucursal | Lista: `Sucursales!B` | Ídem |
| U | Proyecto | Lista: `Proyectos!Z` | Ídem |
| V | Centro de Gasto | Lista: `Centro Gasto!Z` | Ídem |
| W | Centro de Negocio | Lista: `Centro Negocio!B` | Ídem |
| X | Observaciones | Texto | Libre |
| AH | `_Cuadre` | **Fórmula** | No escribir. Debe dar 0 en todas las líneas del asiento. Fórmula (Verificado): `=IF($F5="";"";ROUND(SUMIF(LD_NUM;$F5;LD_DEBE)-SUMIF(LD_NUM;$F5;LD_HABER);2))` |

- **Una línea de Banco o Caja no lleva dimensiones** (Q a W).
- Si el Debe y el Haber de un asiento necesitan dimensiones distintas, van en filas separadas con el mismo N° (lo dice la cabecera de la hoja).
- **No escribir** en AH en adelante ni en A:E (vínculo con la cartola; lo llena el sistema).
- El N° de asiento queda verde si el asiento cuadra y rojo si no.
- La hoja crece sola de a 1.000 filas al acercarse al final (`onEdit`).

## 2. Plan de cuentas (`P. Cuentas`)
- Cabecera en la fila 2. Col A código (`1-11-01`), B nombre, C tipo (Activo, Pasivo…), D naturaleza (Deudora o Acreedora), E descripción, G **`código | nombre`** (es la lista que usa el Libro Diario), H clasificación de flujo.
- Cada subgrupo tiene 15 casilleros; los vacíos solo muestran el código. **Una cuenta existe solo si tiene nombre.**
- Códigos de tres niveles, `N-NN-NN`. El primer dígito manda: 1 Activo, 2 Pasivo, 3 Patrimonio, 4 Ingresos, 5 Costos, 6 y 7 Gastos.
- Se modifica **solo** por «• Configuración › Editor del Plan de Cuentas».

## 3. Maestros (rótulos en la fila 3, datos desde la fila 4)
| Hoja | Columnas |
|---|---|
| Clientes | A RUT · B Nombre / Razón Social · C Contacto · D Correo · E Teléfono · F Dirección · G Notas |
| Proveedores | A RUT · B Nombre / Razón Social · C Contacto · D Correo · E Teléfono · F Dirección · G Datos Bancarios · H Notas |
| Personal | A Código (`PER-01`) · B Nombre Completo · C RUT · D Tipo (`Sueldo` u `Honorario`) · E Cargo / Rol · F Sucursal (`SUC-01`) · G Datos Bancarios · H Notas |
| Sucursales, Proyectos, Centro Gasto, Centro Negocio | Nombre en la columna B; el código es propio de cada hoja (leer la cabecera) |

- RUT con puntos y guion: `76.318.442-0`. El nombre es la **llave**: debe escribirse igual en el maestro y en el Libro Diario.
- Escritura a mano permitida (Documentado). El sistema también da de alta clientes y proveedores al contabilizar desde el RCV.

## 4. RCV Ventas y RCV Compras (cabecera fila 3, datos desde la fila 4)

| Col | RCV Ventas | RCV Compras | Tipo |
|---|---|---|---|
| A | Período SII | Período SII | Texto `AAAA-MM` (`2026-10`) |
| B | Tipo Documento | Tipo Documento | Texto con el nombre (`Factura Electrónica`; también `Nota de Crédito…`, boletas). Copiar el texto que usa la hoja |
| C | Folio | Folio | Número |
| D | RUT Cliente | RUT Proveedor | Texto `76.318.442-0` |
| E | Cliente / Razón Social | Proveedor / Razón Social | Texto |
| F | Fecha Doc | Fecha Doc | Fecha real |
| G | Monto Exento | Monto Exento | Número |
| H | Monto Neto | Monto Neto | Número |
| I | IVA Débito | IVA Recuperable | Número |
| J | Monto Total | Monto Total | Número |
| K | Estado Cobro | Estado Pago | Texto: `Pendiente` al cargar |
| L | Documento corregido | Documento corregido | Lista; solo en notas de crédito |
| M | Decisión de la NC | — | Lista `Rebaja` o `Sin rebaja`; solo notas de crédito |
| N, O | Resultado de la NC · `_Período` | ídem | **Fórmulas**: no escribir |
| P (oculta) | Ref. RCV Venta | Ref. RCV Compra | **Texto llave** (ver abajo) |

**Llave de la columna P** (Verificado en los ejemplos): `VENT-<tipo>-<RUT sin puntos ni guion>-<folio>-<AAAA-MM-DD> | <razón social> | $<total con puntos>`. Ejemplo: `VENT-33-763184420-1001-2026-10-02 | Constructora Maipo Demo Ltda | $1.487.500`. En compras el prefijo es `COMP-`. Cómo trata el sistema el dígito verificador K: **Pendiente**.

**Importación por menú (Documentado):** «• Importaciones › Cargar RCV Compras o Ventas (CSV)» acepta el CSV que baja el SII: separador `;`, primera fila con los rótulos, fechas dd/mm/aaaa, montos enteros sin puntos. Columnas de ventas: `Nro; Tipo Doc; Tipo Venta; Rut cliente; Razón Social; Folio; Fecha Docto; Fecha Recepción; Fecha Acuse Recibo; Fecha Reclamo; Monto Exento; Monto Neto; Monto IVA; Monto total; …`. Columnas de compras: `Nro; Tipo Doc; Tipo Compra; RUT Proveedor; Razón Social; Folio; Fecha Docto; Fecha Recepción; Fecha Acuse; Monto Exento; Monto Neto; Monto IVA Recuperable; Monto Iva No Recuperable; Código IVA No Rec.; Monto Total; Monto Neto Activo Fijo; IVA Activo Fijo; …`. Reimportar no duplica.

## 5. Otros archivos que acepta «• Importaciones»
| Archivo | Formato |
|---|---|
| Cartola | **Solo Excel de Mercado Pago**. Hoja `Cartola Bancaria`: A Banco, B Fecha, C Descripción, D Referencia, E Monto (negativo si sale), F a I fórmulas, N `_ID` oculto (la referencia en números) |
| Boletas de honorarios recibidas | Informe del SII (.xls, .htm). Columnas: `N° Boleta; Fecha; Estado; RUT emisor; Nombre emisor; Sociedad profesional; Honorario bruto; Retención; Líquido a pagar; Servicio` |
| LRE (remuneraciones) | `.csv` o `.txt` de la DT |

## 6. CxC y CxP
Rótulos en la fila 6, una nota en la fila 7 y datos desde la fila 8: `ID CxC · Documento asociado · Condición de pago · Cliente · RUT · Folio · Fecha de emisión · Fecha de vencimiento · Monto total · Cobrado · Saldo pendiente · Estado · Notas`. Los crean los asientos automáticos desde el RCV; el usuario solo completa la condición (`Contado`, `30 días`, `60 días` o `90 días`) y las notas. Los importes y saldos salen del Libro Diario.

## 7. Cómo se carga (por tipo de dato)

| Dato del cliente | Hoja destino | Después |
|---|---|---|
| Facturas y notas de venta o compra (de cualquier sistema) | **RCV Ventas / RCV Compras**, en el formato del §4 | «• Asientos › Desde el RCV» arma los asientos con el plan, los vínculos y las CxC y CxP |
| Clientes, proveedores, personal | **Maestros**, §3 | Disponibles en las listas del Libro Diario |
| Movimientos del banco | **Cartola** (solo Mercado Pago por menú) | «Desde el RCV › cobros y pagos» o «Registrar a mano» |
| Asientos que no vienen de un documento (apertura, ajustes, traspasos) | **Registrar a mano › Asiento libre** (bandeja) | Verificar N° en verde |
| Asientos ya hechos en otro sistema, o dictados en el chat | **Libro Diario**, §1, fila por fila (modalidad 3, **pendiente de validación**) | Protocolo completo en `carga-directa-mcp.md` |

- El RCV oficial se baja del SII. Si el cliente solo tiene las facturas en su otro sistema, cargarlas en las hojas RCV con el formato del §4 es posible, pero el respaldo tributario deja de ser el del SII: **decirlo al usuario y esperar su decisión**.

## 8. Reglas al escribir con el conector (modalidad 3: `carga-directa-mcp.md`)
1. **Leer antes:** cabecera, última fila usada y una fila de ejemplo de la hoja destino.
2. **Tipos:** números como números (sin `$` ni puntos como texto), fechas como fechas reales, cuentas y nombres como texto idéntico al de la lista.
3. **Nunca** sobre fórmulas (AH, N, O del RCV, F a I de la cartola) ni sobre hojas con candado.
4. **Verificar al terminar:** releer lo escrito, comprobar que cada celda con lista quedó sin el aviso de dato inválido, que `_Cuadre` (AH) es 0 en cada línea y, si hay Chrome, que el N° de asiento está verde (el conector no lee el color).
5. En lotes de pocas filas; un error se corrige antes de seguir.
6. Dejar registro en la bitácora del cliente (`memoria-cliente.md`).

## 9. Registrar un asiento a mano en el Libro Diario (modalidad 1)
Guía para el usuario que escribe él mismo en la hoja. Es lo que la guía llama «a mano solo con cuidado».
1. **Elige el N° de asiento:** el siguiente al máximo de la columna F. No repitas uno usado por otro asiento.
2. **Una fila por línea**, con el mismo N° en todas. Fecha (G) como fecha real dd/mm/aaaa; cuenta (H) elegida de la lista desplegable (`1-12-01 | Clientes`); monto en Debe (I) o en Haber (J), nunca en ambos; glosa (K).
3. **Dimensiones** (Q a W) solo si corresponden y elegidas de su lista; nunca en líneas de Banco o Caja. Si Debe y Haber necesitan dimensiones distintas, filas separadas con el mismo N°.
4. **No escribas** en A a E, ni de AH en adelante, ni en las columnas de vínculos (L a P) salvo que el documento exista en su lista.
5. **Comprueba:** `_Cuadre` (AH) en 0,00 en todas las líneas y el N° de asiento en verde (rojo = no cuadra).
6. **Limitaciones frente a un formulario:** el asiento escrito a mano no tiene identidad en `_Registro Asientos` ni registro en `_Operaciones`; no crea CxC, CxP ni vínculos con el RCV; no se elimina desde «Registradas»; las validaciones son las de la hoja. Para facturas usa «Desde el RCV». Para asientos sin documento, «Registrar a mano › Asiento libre» es más seguro.
7. Don Balance puede acompañar al usuario en esto y verificar el resultado leyendo la hoja.
