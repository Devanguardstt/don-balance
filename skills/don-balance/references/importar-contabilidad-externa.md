# Cargar datos del cliente en la plantilla (venga de donde venga)

> Cada cliente trae archivos distintos (Defontana, Nubox, Visual, Excel propio, PDF…) y trabaja a su manera. **No se aprende el formato de cada sistema: se entiende a fondo el formato de la plantilla** (`formato-plantilla.md`) y se traduce lo que traiga el cliente a ese formato. Etiquetas: **Verificado** (lectura de una copia real de FIN-06 v7.6.22, 2026-11-12) · **Documentado** · **Inferido** · **Propuesto** · **Pendiente**.

## 1. Idea de fondo
1. El destino es siempre el de `formato-plantilla.md`: hoja, columna, tipo de celda y lista permitida.
2. El origen se lee **tal como venga**: se abre el archivo, se dice qué se ve y se hace una tabla «columna del cliente → campo de la plantilla», que el usuario confirma.
3. Esa tabla se guarda en la carpeta del cliente (`formatos/`), así la próxima vez no se pregunta.
4. Nada se escribe sin vista previa y sin un «sí» (reglas 1 y 2).

## 2. Qué camino usar (Control Total Advance Automatizado, FIN-06)

| Dato | Camino |
|---|---|
| Facturas de venta y compra | Hojas **RCV Ventas / Compras** en el formato del §4 de `formato-plantilla.md`, y luego «• Asientos › Desde el RCV». El sistema arma los asientos con el plan y crea las CxC y CxP. Es el camino nativo |
| Clientes, proveedores, personal | Hojas maestras (§3) |
| Saldos iniciales y ajustes sin documento | «Registrar a mano › Asiento libre» con bandeja (Chrome) |
| Asientos ya hechos en otro sistema, o dictados en el chat | **Modalidad 3, carga directa con el conector** (`carga-directa-mcp.md`). Diseñada, **pendiente de validación**; con el «sí» del usuario y un aviso de que no está validada |
| Cartola de banco | Solo Excel de Mercado Pago por menú; otro banco lo adapta Vanguard como servicio aparte |
| Control Total Starter (FIN-03) | Conector, columnas A:G (`mcp-vs-chrome.md`) |

**No existe un importador nativo de asientos de otro sistema** (Documentado: «• Importaciones» solo trae RCV, cartola, honorarios y LRE). Una carga asistida por Don Balance con el conector **no es** ese importador: es la modalidad 3 de `SKILL.md`. Propuesto: pedir a Vanguard una opción nativa «Importar asientos (CSV)» para cargas grandes.

## 3. Procedimiento

### Paso 1 · Mirar el archivo antes de tocarlo
1. Pedir la ruta (Excel, CSV, TXT o PDF). Copiarlo a `importaciones/AAAA-MM-DD_<origen>/original.*` si el cliente tiene la carpeta (`memoria-cliente.md`).
2. Leer las primeras 15 filas y contar: qué parece ser (diario, libro de ventas, balance…), cuántas filas, rango de fechas, columnas.
3. Si existe `formatos/<origen>.md` del cliente, usarlo. Si no, proponer la tabla de columnas y **pedir confirmación** («¿la columna Cargo es el Debe?»). No se supone nada sobre sistemas que no se hayan visto.
4. Guardar la tabla confirmada en `formatos/<origen>.md`.

### Paso 2 · Traducir al formato de la plantilla
El destino y los tipos están en `formato-plantilla.md`. Reglas de limpieza:
- **Números:** detectar si el formato es 1.234,56 o 1,234.56; quitar `$` y espacios; entero en pesos. Un paréntesis o signo menos en el Debe se revisa, no se invierte solo. Un monto con signo en una sola columna se separa en Debe y Haber.
- **Fechas:** a fecha real dd/mm/aaaa, dentro del ejercicio de Config (C28 y C29).
- **Una fila por línea de asiento**, con el mismo N° en todas. Si el origen pone el comprobante en un encabezado aparte, repetirlo en cada línea.
- **Sin totales, subtotales ni filas de resumen.**
- **N° de asiento:** nuevo, continuando el máximo de la columna F. El número original va en la glosa u Observaciones («Comprobante 4521») para poder cruzar.
- **RUT** con puntos y guion; **nombres** idénticos a los del maestro.
- Dejar la salida en `normalizado.tsv` con las columnas del destino, más `estado` y `observación`.

### Paso 3 · Asignar las cuentas del plan (mapeo)

1. **Leer el plan vivo** del cliente: `P. Cuentas` columnas A, B, C y D (código, nombre, tipo, naturaleza) o G («código | nombre»). **El plan es de cada cliente**: nunca nombrar una cuenta de memoria.
2. Para cada cuenta del origen, buscar en este orden y anotar la confianza:
   1. Código igual y nombre parecido → **Alta**
   2. Equivalencia ya guardada en `mapeo-cuentas.md` → **Alta**
   3. Nombre igual o casi igual → **Alta**
   4. Mismo concepto con otro nombre → **Media** (pedir confirmación)
   5. Duda → **Baja**: se pregunta, no se adivina
3. **Equivalencias típicas con el plan sugerido** (**Propuesto**, confirmar siempre):

   | En otros sistemas suele llamarse | Cuenta del plan sugerido |
   |---|---|
   | Deudores por ventas, Clientes nacionales | 1-12-01 \| Clientes |
   | Banco (Cta. Cte.), Banco Estado, Banco de Chile | 1-11-02 \| Bancos |
   | Caja, Fondo fijo | 1-11-01 \| Caja |
   | IVA Crédito, IVA CF | 1-15-01 \| IVA Crédito Fiscal |
   | IVA Débito, IVA DF | 2-15-01 \| IVA Débito Fiscal |
   | Proveedores nacionales, Acreedores | 2-11-01 \| Proveedores y cuentas comerciales por pagar |
   | Remuneraciones por pagar | 2-13-01 \| Remuneraciones por pagar |
   | Capital | 3-11-01 \| Capital Social y Aportes |
   | Ventas, Ingresos por ventas | 4-11-01 \| Ventas de Bienes |
   | Honorarios recibidos | 6-13-01 \| Servicios profesionales y asesorías |
   | Costo de ventas | 5-11-01 \| Costo de ventas |

   Esta tabla es una guía: el nombre exacto sale de P. Cuentas.
4. **Cuenta que no existe en el plan:** no se fuerza a otra cuenta. Se propone crearla por «• Configuración › Editor del Plan de Cuentas» (regla 3), con OK del usuario, y se vuelve a este paso.
5. Mostrar la tabla de mapeo al usuario y esperar su confirmación. Guardar lo confirmado en `mapeo-cuentas.md`.
6. En el Libro Diario la cuenta va **escrita exactamente como en la lista desplegable**: `1-12-01 | Clientes` (**Verificado**).

### Paso 4 · Cruce: qué ya está y qué falta

Antes de cargar nada, comparar lo normalizado con lo que ya hay en el Libro Diario (leído con el conector):

1. **Controles del origen:** cada asiento cuadra (Debe = Haber); total Debe = total Haber del archivo; las sumas por cuenta coinciden con el balance del otro sistema, si el cliente lo entregó.
2. **Contra el Libro Diario de la planilla**, por documento (tipo, folio, RUT, monto) o por fecha y monto:

   | Resultado | Qué hacer |
   |---|---|
   | Ya está igual | No se carga |
   | Ya está con otra cuenta o monto | Se informa la diferencia; la decisión es del usuario |
   | No está | Candidato a cargar |
   | Está en la planilla y no en el origen | Se informa |

3. **Cuentas con otro nombre** (ejemplo: «Deudores por venta» frente a «Clientes»): se resuelven con el mapeo del paso 3, no se cuentan como diferencia.
4. Escribir `cruce.md` con totales por resultado y las líneas dudosas.
5. Un asiento del RCV (venta o compra con factura) que ya fue contabilizado por «Desde el RCV» no se vuelve a cargar desde el otro sistema, aunque el cliente lo pida: duplicaría ventas e IVA.

### Paso 5 · Terceros y dimensiones
- Cliente y proveedor (columnas Q y R) deben coincidir con los maestros **Clientes** y **Proveedores**. Un RUT nuevo se propone para agregar al maestro (escritura a mano permitida en los maestros).
- Las dimensiones **nunca van en líneas de Banco o Caja** (`mapa-sistema.md`).
- Los vínculos con CxC, CxP y RCV (columnas L a O) los crean los formularios del RCV; un asiento de otro sistema no los trae. **Inferido:** las cuentas por cobrar y pagar cargadas así no quedan ligadas a la gestión de CxC y CxP.

### Paso 6 · Cargar
1. Resumen al usuario: cantidad de asientos, rango de fechas, cuentas principales, total, y qué se deja fuera. **Esperar un «sí»**.
2. Elegir el camino del §2. FIN-06 con formulario (modalidad 2): Chrome, en lotes pequeños (**la bandeja se pierde si se cierra la ventana sin contabilizar**, `recorridos-mensuales.md` §6.5). FIN-06 con el conector (modalidad 3): fases C a F de `carga-directa-mcp.md`. Starter: conector (`mcp-vs-chrome.md`).
3. Verificar al terminar: en la modalidad 3, la fase F de `carga-directa-mcp.md`; en las demás, las reglas del §8 de `formato-plantilla.md` y los totales de `normalizado.tsv`.
4. Informar con los N° de asiento creados.

### Paso 7 · Aprender
Actualizar `mapeo-cuentas.md`, `formatos/<sistema>.md`, `terceros.md` y `bitacora.md` (`memoria-cliente.md`).

## 4. Carga directa al Libro Diario de FIN-06
El protocolo completo (lectura de la plantilla, prevalidación, autorización, escritura, verificación, recuperación, diferencia de trazabilidad y pruebas pendientes) está en `carga-directa-mcp.md`. Este archivo cubre solo la interpretación, el mapeo de cuentas y el cruce que lo preceden.

## 5. Límites que se dicen al cliente
- No se carga nada que no cuadre ni nada que tenga una cuenta sin confirmar.
- Mover meses cerrados o afectar un F29 ya declarado es decisión del contador (regla 9).
- Cada cliente trae archivos distintos: se confirma columna por columna y se guarda en su carpeta. Lo que no cambia es el formato de la plantilla.
