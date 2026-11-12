# Modalidad 3: carga directa en el Libro Diario con Claude Code + conector de Sheets

> **Estado de validación: capacidad diseñada, pendiente de validación funcional en una copia de demostración de FIN-06.** Nunca se ha escrito una fila en el Libro Diario de FIN-06 con el conector. Lo único probado con el conector es leer y escribir celdas en Control Total Starter (FIN-03, 2026-11-11) y leer FIN-06 (2026-11-12). Este archivo describe cómo debe hacerse; no afirma que funcione. Etiquetas: **Verificado** · **Documentado** · **Inferido** · **Propuesto** · **Pendiente**.

## 1. Qué es y qué no es

- Es una **carga asistida por IA**: Don Balance interpreta información contable externa (Excel, CSV, TXT, exportaciones de otros sistemas o datos que el usuario escriba en el chat), la traduce al formato de `formato-plantilla.md` y escribe las filas en el Libro Diario con el conector.
- **No es** un importador nativo: «• Importaciones» solo trae RCV, cartola, honorarios y LRE (Documentado). No es un menú de la planilla ni pasa por la lógica de Apps Script.
- **No sustituye a los formularios.** Para facturas que necesitan CxC, CxP y vínculo con el RCV se recomienda siempre el camino nativo (modalidad 2).
- No confundir con Control Total Starter (FIN-03), cuyo Libro Diario sí se llena a mano con el conector (`mcp-vs-chrome.md` §3).

## 2. Cuándo sí y cuándo no

| Caso | Modalidad |
|---|---|
| Facturas de venta o compra con documento | **2 · Formularios** (RCV → «Desde el RCV»). Crean asiento, CxC y CxP y los vínculos |
| Asientos sin documento: apertura, ajustes, traspasos, historial de otro sistema | **3** es posible; para pocos asientos, **2 · Asiento libre** con bandeja es más seguro |
| El usuario quiere escribir él mismo uno o dos asientos | **1 · Manual**, con la guía de `formato-plantilla.md` §9 |
| Hay duda de que el asiento ya exista por otra vía | No cargar. Cruzar primero (`importar-contabilidad-externa.md` paso 4) |
| Ejercicio cerrado (`Config!C49` con fecha) o fechas anteriores al cierre | No cargar |

## 3. Condiciones previas
1. La planilla fue identificada como **FIN-06** (`diagnostico-inicial.md` §4). Si es otra, detenerse.
2. El conector tiene permiso de **escritura** sobre esa planilla (prueba en `conexion-inicial.md` §3, solo en una copia de prueba).
3. El Plan de Cuentas está aplicado y el diagnóstico no mostró descuadres previos.
4. El usuario entendió, con palabras sencillas, que esta modalidad **no está validada** y que **no deja la misma trazabilidad** que los formularios (§9), y dijo «sí» a seguir.

## 4. Fases

### Fase A · Leer la plantilla real (nada se escribe)
Con el conector, antes de proponer nada:
1. Producto y versión (`diagnostico-inicial.md` §4).
2. Empresa (`Config!C8`, `C10`) y que sea la planilla correcta.
3. **Plan de Cuentas vigente:** `P. Cuentas!A6:D2073` (código, nombre, tipo, naturaleza) y la lista `G` (`código | nombre`). Nunca un plan genérico.
4. Naturaleza de cada cuenta (Deudora o Acreedora).
5. Estructura del Libro Diario: cabecera (fila 4), última fila usada y una fila de ejemplo.
6. Tipos de celda: fechas como fecha real, montos como número, cuenta como texto (`formato-plantilla.md` §1).
7. **Maestros** de las dimensiones: `Clientes`, `Proveedores`, `Personal`, `Sucursales`, `Proyectos`, `Centro Gasto`, `Centro Negocio`.
8. Fórmula de cuadre de `AH` (Verificado): `=IF($F5="";"";ROUND(SUMIF(LD_NUM;$F5;LD_DEBE)-SUMIF(LD_NUM;$F5;LD_HABER);2))`.
9. Movimientos existentes: máximo N° de asiento (columna F), rango de fechas y cuentas ya usadas.
10. Fecha de cierre (`Config!C49`) y ejercicio (`C28`, `C29`).

### Fase B · Interpretar y normalizar
Procedimiento de `importar-contabilidad-externa.md` (pasos 1 a 3 y 5): mirar el archivo, traducir columnas, separar Debe y Haber, agrupar por comprobante, mapear cuentas al plan del cliente y terceros a los maestros. Las equivalencias de cuentas con poca certeza **las confirma el usuario**; las confirmadas pueden guardarse en `mapeo-cuentas.md` (`memoria-cliente.md`). Si la información viene del chat y no de un archivo, se trata igual: se estructura y se muestra al usuario antes de seguir.

### Fase C · Prevalidación (todo debe cumplirse antes de escribir)
- [ ] Todas las cuentas existen en el plan vivo y están escritas como `código | nombre`.
- [ ] Todas las fechas son válidas (dd/mm/aaaa, sin 30/02) y caen **dentro del ejercicio** y después de la fecha de cierre, si la hay.
- [ ] Cada asiento está bien agrupado (mismo N° en todas sus líneas).
- [ ] **Debe = Haber en cada asiento.**
- [ ] Los totales coinciden con los del archivo original o con lo que dijo el usuario.
- [ ] No hay duplicados: ni dentro del lote ni contra el Libro Diario (misma fecha, monto y glosa; mismo documento).
- [ ] No se reproducen **facturas o movimientos ya contabilizados por otra vía** (formularios, RCV, otra carga).
- [ ] Los nombres de terceros coinciden **exactos** con los maestros; un tercero nuevo se propone agregar al maestro (escritura a mano permitida), no se inventa.
- [ ] Las dimensiones existen en su maestro y no van en líneas de Banco o Caja.
- [ ] No quedan importes sin clasificar ni cuentas sin confirmar.
- [ ] Ningún valor se ajustó ni se inventó.

**Si algo falla:** no corregirlo por cuenta propia ni «redondear» para que cuadre. Mostrar las diferencias (qué, cuánto, en qué línea) y pedir una decisión. Lo excluido queda registrado como excluido.

### Fase D · Autorización
Mostrar al usuario, en lenguaje simple:
- cantidad de asientos y de líneas, y rango de fechas;
- cuentas principales;
- total Debe y total Haber;
- registros excluidos y por qué;
- advertencias y diferencias pendientes.

Esperar un **«sí» explícito**. Vale **solo para el lote presentado** (reglas 1 y 2). Un cambio al lote pide un nuevo sí.

### Fase E · Escritura
- **Primer lote: un solo asiento**, para que el usuario lo vea en su planilla. Recién después, lotes controlados (**Propuesto:** hasta 20 asientos por lote; ajustar tras las pruebas).
- Usar solo herramientas del conector disponibles. Hoy `update_values` está probado en Starter; `append_values` y `update_formulas` están documentados, no probados (`mcp-vs-chrome.md` §1).
- **Dónde:** en la primera fila vacía después de la última usada de la columna F. No sobrescribir nada.
- **Qué columnas:** `F` a `K` (N° asiento, fecha, cuenta, Debe, Haber, glosa) y `Q` a `X` (dimensiones y observaciones) cuando correspondan. Nada más.
- **Tipos:** números como números, fechas como fechas reales, cuentas y nombres como texto idéntico a la lista. Debe o Haber vacío en la línea que no corresponde.
- **N° de asiento:** nuevo, continuando desde el máximo usado; el mismo número en todas las líneas del asiento.
- **Marca de origen (Propuesto):** en `X` (Observaciones) escribir «Carga asistida Don Balance AAAA-MM-DD, lote n». Sirve para distinguir después estos asientos de los de formularios.
- **Prohibido** (reglas 3 y 5): hojas automáticas protegidas, hojas técnicas ocultas, columnas `AH` en adelante, columnas `A` a `E` (vínculo con cartola, solo lo llena el sistema), asientos creados por formularios, y vínculos de CxC, CxP, RCV o cartola que no existan realmente (no inventar IDs de las columnas `L` a `P`).

### Fase F · Verificación posterior (obligatoria)
Releer con el conector lo escrito y comprobar:
1. Que están todas las líneas esperadas.
2. Que valores, fechas y cuentas coinciden con lo normalizado.
3. Que los N° de asiento son los asignados y se repiten bien.
4. Que Debe y Haber coinciden en cada asiento.
5. Que **`_Cuadre` (AH) es 0,00** en todas las líneas.
6. Que las dimensiones son las esperadas.
7. Que no hay duplicados nuevos.
8. Que los reportes reflejan los movimientos (por ejemplo, Balance General o Libro Mayor de una cuenta del lote).
9. Que los totales registrados coinciden con los del origen.
10. Que las celdas con lista no muestran aviso de dato inválido y que fecha y montos quedaron con el tipo correcto (leer el tipo de celda, no solo el texto).

**El color del N° de asiento no se lee con el conector.** Si se necesita comprobarlo, verlo en Chrome; si no hay Chrome, decir «no pude comprobar el color» y apoyarse en `_Cuadre`. No afirmar un color que no se observó.

**Nunca declarar una carga exitosa porque el conector respondió bien.** Éxito = Fase F completa. Si una verificación falla: **detener los lotes siguientes**, identificar el problema y proponer una corrección.

## 5. Fallos y recuperación
| Situación | Qué hacer |
|---|---|
| La escritura se cortó o el conector no respondió | **No repetir** (regla 4). Releer el rango y comparar con `normalizado.tsv`. Informar qué líneas están y cuáles faltan |
| Quedó un asiento a medias (`_Cuadre` ≠ 0) | Mostrar las líneas presentes y las que faltan. Con un «sí», completar solo lo que falta. Si es mejor empezar de cero, limpiar solo esas filas (`batch_clear_values`, documentado y **no probado**) y avisar que quedan filas vacías entre asientos |
| Se escribió dos veces | Mostrar los duplicados y proponer limpiar los sobrantes, con «sí» |
| Falla la verificación | Detener, informar, proponer corrección; no seguir con otros lotes |
| Se necesita borrar o corregir un asiento de un formulario | No tocarlo: se corrige desde su formulario (regla 3, `correcciones.md` §9.4) |

Un asiento cargado por esta vía se corrige a mano (no tiene identidad en los formularios): siempre con vista previa y «sí».

## 6. Diferencia de trazabilidad (decirla al usuario)
| | **A · Formularios nativos** | **B · Carga directa con el conector** |
|---|---|---|
| Identidad en `_Registro Asientos` | Sí | No necesariamente |
| Registro de operación en `_Operaciones` | Sí | No necesariamente |
| Vínculos con CxC y CxP | Sí (los crea el formulario) | No |
| Vínculo con documentos del RCV | Sí | No |
| Se elimina desde su formulario («Registradas», «Revisar la eliminación…») | Sí | No: se corrige a mano |
| Aparece en reportes | Sí | Sí (leen el Libro Diario con fórmulas) |

Ambos forman parte del Libro Diario, pero **no tienen la misma trazabilidad ni integración** (**Inferido** desde la Ficha FIN-06; **Pendiente** confirmarlo en la prueba P8).

## 7. Protocolo de pruebas en una copia de demostración
**Solo en una copia de demo, nunca en la planilla real de un cliente.** Antes de cada prueba, copiar la planilla o anotar la última fila usada. Cada prueba termina con la verificación de la Fase F y con la limpieza de lo escrito.

| # | Prueba | Qué se espera | Estado |
|---|---|---|---|
| P1 | Un asiento simple de dos líneas (Bancos contra Capital) | Filas correctas, `_Cuadre` 0, tipos de celda correctos | Pendiente |
| P2 | Un asiento de varias líneas (por ejemplo un asiento de apertura con cinco cuentas) | Mismo N° en todas las líneas, cuadra | Pendiente |
| P3 | Cuentas de distinta naturaleza y clase | Reportes con el signo correcto | Pendiente |
| P4 | Líneas con distintas dimensiones (Cliente, Proveedor, Sucursal…) | La lista de validación las acepta; no van en líneas de Banco o Caja | Pendiente |
| P5 | Asiento descuadrado a propósito | La prevalidación lo detiene antes de escribir | Pendiente |
| P6 | Reportes después de la carga (Libro Mayor, Balance General, Resumen Ejecutivo) | Reflejan los movimientos | Pendiente |
| P7 | El mismo lote otra vez | Se detecta el duplicado y no se escribe | Pendiente |
| P8 | Efecto en los formularios: «Revisar operaciones pendientes», «Registradas» y eliminación | Confirmar si el asiento aparece o no, y cómo se corrige | Pendiente |
| P9 | Escritura interrumpida (cortar un lote a la mitad) | Se detecta el asiento a medias y se recupera sin duplicar | Pendiente |
| P10 | Color del N° de asiento visto en Chrome | Verde si cuadra | Pendiente |

Hasta que P1 a P10 estén cumplidas y registradas, esta modalidad se ofrece **solo con aviso de que no está validada**.
