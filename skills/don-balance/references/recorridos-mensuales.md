# Recorridos: primer mes, plan, maestros, importaciones y asientos

> Fuente: guía de Don Balance para Control Total Advance Automatizado v7.6.22, §6.0–§6.6. Las menciones «§N» apuntan a otras secciones de esa guía; ../SKILL.md indica en qué archivo está cada una.

## 6. Recorridos paso a paso

### 6.0 Ruta del primer mes
**Una sola vez:**
1. Config (§5.3).
2. Plan de cuentas (§6.1).
3. Maestros (§6.2).
4. Configuración inicial del F29 (§6.7).
5. Saldos iniciales si la empresa ya tenía historia: un **Asiento libre** al primer día del ejercicio, solo con cuentas de activo, pasivo y patrimonio. Si viene de un año cerrado en este sistema, usa la apertura (§6.11).

**Cada mes:**
1. Importar el RCV de compras y ventas, y la cartola si la usa.
2. Contabilizar ventas y compras (§6.4).
3. Registrar cobros y pagos (§6.4).
4. Registrar lo que no tiene factura (§6.5).
5. Remuneraciones, honorarios y depreciación (§6.8 a §6.10).
6. F29 (§6.7).
7. Revisar los reportes (§8).

**El mes está completo cuando:**
- En *Asientos › Desde el RCV*, con el filtro «Todos con su estado», no quedan documentos del mes por contabilizar.
- En el Libro Diario **ningún N° de asiento está en rojo**.
- El F29 del período dice **Contabilizado · Pagado** (o pendiente de pago, si aún no se paga).
- *Asientos › Revisar operaciones pendientes* responde que no hay operaciones pendientes.

### 6.1 Plan de cuentas · *• Configuración › Editor del Plan de Cuentas*
El editor trabaja en memoria: **nada se escribe hasta «✅ Aplicar y guardar cambios»**.
1. Espera a que cargue el árbol.
2. **📋 Cargar estructura sugerida** deja 41 subgrupos y 79 cuentas.
   - Con plan vacío se carga directo.
   - Si ya hay cuentas, elige **Combinar** (recomendado: conserva el plan y agrega lo que falta) o **Reemplazar** (vuelve a una base limpia; las cuentas con movimientos se conservan).
3. **Etapa 1, estructura:** renombrar, agregar o quitar cuentas. «💾 Guardar borrador» permite seguir otro día.
4. **Etapa 2, funciones y clasificación:** deben existir una sola vez **IVA Débito, IVA Crédito y Resultado del Ejercicio**. Revisa además la clasificación de flujo de las cuentas nuevas.
5. **Etapa 3, revisión:** muestra «Qué se va a aplicar» (altas, bajas, funciones contables asignadas) y las etiquetas «Sin bloqueos» y «Sin advertencias». Si no hay conflictos, «✅ Aplicar y guardar cambios» (pide OK al usuario). Escribe P. Cuentas, reconstruye los reportes e instala las 43 asignaciones de los módulos.
6. **Cómo comprobarlo:**
   - El cuadro final dice «Plan aplicado».
   - P. Cuentas muestra las cuentas.
   - *• Reportes › Ver estado de actualización* no informa nada pendiente.
7. **Si dice «instalación incompleta», «reportes pendientes» o «asociaciones por revisar»:** el Plan sí quedó escrito. Pulsa «Reintentar la instalación» o vuelve a abrir el editor. **No apliques otro plan para forzarlo.**

**Niveles:**
- **Clase:** la decide el primer dígito (1 Activos, 2 Pasivos, 3 Patrimonio, 4 Ingresos, 5 Costos, 6 Gastos operacionales, 7 Gastos no operacionales).
- **Grupo:** 1-1.
- **Subgrupo:** 1-11.
- **Cuenta imputable:** 1-11-02. Es la única que va en un asiento.

### 6.2 Maestros
- **Clientes y Proveedores:** RUT y nombre. El RUT identifica al tercero aunque el nombre del SII cambie.
- **Personal:** código, nombre completo y RUT de cada trabajador; la sucursal va como código (SUC-01).
- **Sucursales, Proyectos y Centros:** solo si se quieren informes por ellos.
  - Un centro de gasto aparece en las listas solo con Estado «Activo».
  - Un proyecto deja de aparecer con Estado Inactivo, Cerrado, Terminado, Finalizado, Suspendido o Anulado.
  - Para dar de baja, cambia el Estado; **no borres la fila**.
- La asignación (tercero, sucursal, proyecto, centro) se elige **una vez por operación** en el formulario. El sistema la escribe en las columnas Q:W.

### 6.3 Importar · *• Importaciones*
**Importar no contabiliza**: no escribe asientos ni marca nada como cobrado o pagado.

- **RCV:**
  1. El usuario descarga del SII el CSV del Registro de Compras o de Ventas del mes y no lo edita (separador «;»).
  2. Usa *Cargar RCV Ventas (CSV)* o *Cargar RCV Compras (CSV)*, el que corresponda.
  3. Elige o arrastra el archivo.
  4. Revisa el «Período del registro» propuesto. En compras, un documento recibido después de su mes queda en el período en que se registró.
  5. *📥 Cargar Documentos*.
  6. El cuadro informa cuántos había, cuántos se agregaron y cuántos ya existían.
  - Reimportar no duplica.
  - Un documento **pegado a mano dos veces** sí se cuenta dos veces en el IVA.
- **Cartola:** solo **Mercado Pago en .xlsx** (Movimientos › Descargar › Excel), sin editar. Otros bancos no se reconocen todavía: el cuadro lo dice y no importa nada. Vanguard adapta la cartola de otros bancos como servicio aparte.
- **LRE** (remuneraciones): ver §6.8.

### 6.4 Ventas, compras, cobros y pagos · *• Asientos › Desde el RCV…*
Tres pestañas: **Ventas · Compras · Cobros y pagos**.

**Ventas o compras:**
1. **1 · Seleccionar:** marca los documentos o pulsa «Seleccionar los disponibles filtrados». Un documento bloqueado dice por qué; por ejemplo, a una nota de crédito le falta la factura que corrige.
2. **2 · Configurar:** en cada fila, Condición, cuenta y asignación. «Aplicar en bloque» copia una elección a varias filas y muestra a cuáles. La Condición puede ser:
   - **Según el RCV.**
   - **Pendiente**: crea la ficha en CxC o CxP con su plazo.
   - **Cobrada/Pagada**: pide cuenta y fecha del cobro o pago.
3. **3 · Vista previa:** revisa cada asiento (cuentas, debe, haber, glosa). Puedes excluir documentos.
4. **«Generar n…» (dorado):** pide OK al usuario con el resumen.
5. **4 · Resultado:** número de asiento por documento, o el motivo si alguno no se contabilizó.

**Cobros y pagos:**
1. Elige *Cobros de ventas (CxC)* o *Pagos de compras (CxP)*. Solo aparecen documentos contabilizados como pendientes, con su saldo.
2. En Configurar, cuenta de banco o caja y fecha.
   - **Abono parcial:** escribe el importe (no más que el saldo); vacío registra el saldo completo.
   - Varios documentos pagados con un movimiento van en el mismo grupo.
3. «Sugerir desde la Cartola…» propone el movimiento del banco de cada documento.
4. Vista previa y **«Registrar n…»** (dorado, con OK).

**Más reglas:**
- **Notas de crédito:** necesitan la factura que corrigen. Si el RCV no la trae, se elige en Configurar entre las del mismo RUT. Si la factura no está contabilizada, se seleccionan las dos en el mismo lote.
- **Preferencias por RUT:** en Configurar se puede guardar la cuenta y asignación habituales de un tercero. La próxima vez se completan solas; lo elegido en el documento manda.
- **Eliminar:** filtra los contabilizados, márcalos, «Eliminar asientos de…». Revisa la vista previa (incluye cobros y pagos dependientes) y pide OK.

### 6.5 Registro manual · *• Asientos › Registrar a mano*
Es para operaciones **sin documento del RCV**. Pestañas:

| Pestaña | Para qué | Ejemplo |
|---|---|---|
| Ingreso | Dinero que entra sin documento del RCV | Arriendo de una bodega, intereses, aporte |
| Egreso | Dinero que sale sin documento del RCV | Comisión bancaria, gasto sin factura |
| Cobrar o pagar | Cobrar o pagar un pendiente creado aquí | Pagar el arriendo que quedó por pagar |
| Traspaso | Entre cuentas propias de banco o caja | Del banco a la caja |
| Asiento libre | Cualquier asiento con sus cuentas y montos | Ajustes, saldos iniciales, abonos con varias cuentas |
| Registradas | Buscar, ver, cobrar un pendiente o eliminar lo registrado aquí | — |

**Pasos:**
1. Fecha, descripción (va en la glosa), si se pagó ahora o queda pendiente, la cuenta de banco o caja y la cuenta que explica la operación.
2. Asignación de la operación. «+ Repartir entre varias cuentas» agrega líneas.
3. «Revisar solo este →»: la vista previa, que no escribe nada.
4. **«Contabilizar $…»** (dorado, con OK).

**Bandeja:** «Agregar a la bandeja» (Ctrl+Intro) junta varios asientos. «Revisar los n elegidos →» y «Contabilizar n asientos · $…» (dorado). **La bandeja se pierde si se cierra la ventana sin contabilizar.**

Las facturas del RCV no se registran aquí: van por *Desde el RCV*. Este formulario no calcula IVA.

### 6.6 Pendientes de un ingreso o egreso
Un ingreso o egreso con «Queda por cobrar / por pagar» queda en una cuenta propia, no en Clientes ni Proveedores. Se cobra o paga en la pestaña *Cobrar o pagar*.

Un abono que usa otra cuenta además del banco se registra en *Asiento libre*, eligiendo el documento en la línea de Clientes o Proveedores.
