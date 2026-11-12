# MCP de Google Sheets o Chrome

> Fuente: prueba hecha el 2026-11-11 en una copia de Control Total Starter (FIN-03) con lectura y escritura de celdas, más la lista de herramientas del conector y lo que ya dicen `mapa-sistema.md`, `operar-planilla.md` y `reportes-y-limites.md`. Etiquetas: **Verificado** (probado) · **Documentado** (en la guía o en la lista de herramientas) · **Inferido**.

## 1. Las dos vías

| | Conector (MCP) de Google Sheets | Chrome |
|---|---|---|
| Qué hace | Lee y escribe celdas directo en la planilla, sin abrir el navegador | Abre la planilla con la sesión de Google del usuario y pulsa menús y botones como lo haría él |
| Velocidad y costo | Más rápido y gasta menos tokens (observación del equipo de Vanguard, 2026-11-11) | Más lento y gasta más tokens |
| Llega a | Celdas, fórmulas, hojas y estructura | Todo lo que se ve: menús «•», formularios, botones, PDF, importaciones |
| No puede | Pulsar menús ni botones, ni correr el script de Apps Script (**Inferido** de la lista de herramientas: solo trae operaciones de la API de Sheets) | Nada de lo anterior, pero es lento |

**Herramientas del conector:** `get_spreadsheet`, `get_values`, `update_values` (**Verificado**); `append_values`, `update_formulas`, `batch_clear_values`, `insert_dimension`, `update_spreadsheet`, `copy_sheet_to_another_spreadsheet` (**Documentado**: aparecen en la lista, no se probaron).

## 2. Qué vía usar según la tarea

| Tarea | Vía |
|---|---|
| Leer cifras de cualquier hoja (Libro Diario, Balance, IVA Mensual, CxC, CxP, Config) | **MCP** |
| Revisar el cierre de mes | **MCP + Chrome** (ver §5) |
| Escribir asientos en **Control Total Starter** | **MCP** (ver §3) |
| Generar asientos con documentos o por módulo en **Control Total Advance Automatizado (FIN-06)** | **Chrome**, con los formularios y el botón dorado: modalidad 2 (ver §3) |
| Cargar en el Libro Diario de FIN-06 asientos que vienen de otro sistema o del chat | **MCP**, modalidad 3: `carga-directa-mcp.md`. **Diseñada, pendiente de validación** |
| Descargar informes en PDF o CSV | **Chrome**: menú «• Reportes». Se guardan en la carpeta principal del Drive |
| Importar RCV, cartola o LRE | **Chrome**: menú «• Importaciones» y selector de archivos |
| Editor del Plan de Cuentas, F29, remuneraciones, honorarios, activos fijos, renta y cierre | **Chrome**: son formularios del script |
| Completar Config y maestros | **MCP**, con el «sí» del usuario por cada cambio (**Inferido**; las celdas son de escritura a mano según `mapa-sistema.md`) |
| Comprobar que un asiento quedó bien | **MCP**: leer el N° de asiento y el cuadre después de generarlo en Chrome |
| Dashboard | **Chrome**: es una aplicación web del script |
| Iniciar sesión en Google o autorizar el script | **El usuario**: Claude no escribe claves |

## 3. Starter y Advance no se tratan igual

- **Control Total Starter (FIN-03):** el Libro Diario se llena **a mano** (N° de asiento, fecha, cuenta, debe, haber, glosa, observaciones). Con el conector se puede escribir el asiento en las columnas A a F; la fila siguiente ya trae las fórmulas de cuadre y de flujo. **Verificado** el 2026-11-11: asiento 77 en la copia de onboarding, cuadre 0,00 y roles reconocidos. Cuenta con el formato `código | nombre`, fecha como fecha real y montos como números.
- **Control Total Advance Automatizado (FIN-06)** tiene **tres modalidades de registro** (`SKILL.md`):
  1. **Manual directo** en el Libro Diario, por el usuario (`formato-plantilla.md` §9).
  2. **Formularios nativos** (menús «•»), con Chrome: preparar, vista previa, «sí», botón dorado, esperar y verificar. Es la modalidad por defecto y la única que deja la trazabilidad completa (`_Registro Asientos`, `_Operaciones`, CxC, CxP y vínculos con el RCV).
  3. **Carga directa con el conector**, asistida por Don Balance: `carga-directa-mcp.md`. **Capacidad diseñada, pendiente de validación en una copia de demostración**; nunca se ha escrito una fila en el Libro Diario de FIN-06 con el conector. No reproduce la trazabilidad de los formularios y no sustituye a la modalidad 2 para facturas.
  Fuera del Libro Diario, el conector **lee** y escribe solo las celdas que `mapa-sistema.md` marca como de escritura a mano: celdas amarillas de Config, maestros (rótulos en fila 3, datos desde la fila 4), importes de Remuneraciones en filas que prepara el formulario, y ID, documento, condición y notas de CxC y CxP. Nunca hojas automáticas, hojas técnicas ocultas ni columnas `AH` en adelante.
- Antes de escribir en cualquier planilla, mira el título y la hoja Config para saber **qué producto es**. No atribuyas funciones de un producto a otro.

## 4. Costos y cuidados
- Leer rangos grandes también cuesta: 180 filas del Libro Diario devuelven una respuesta enorme. Pide rangos acotados (por ejemplo las últimas filas y las columnas A a F).
- Cada escritura con el conector va con el «sí» explícito del usuario y se **lee de vuelta** para comprobarla.
- Chrome necesita una sesión de Google abierta. Si aparece la pantalla de acceso, el usuario inicia sesión; Claude no escribe contraseñas.
- **Prueba del PDF (2026-11-11):** por el conector **no se puede** (no tiene operaciones de menús ni de Apps Script: **Inferido**). Por Chrome **no se probó**: el navegador integrado quedó en la pantalla de acceso de Google y se pidió no generar el PDF, solo comprobar si era posible. Que Chrome pueda pulsar el botón es **Documentado** por la guía, no **Verificado**.
- Los PDF y CSV los genera el menú y quedan en el Drive del usuario. Descargarlos a su computador se le pregunta antes, con nombre y tamaño (regla 6).

## 5. Revisión de cierre: qué se lee con el conector
Los 8 puntos del panel («Cierre de mes»):

| Punto | Vía |
|---|---|
| Sin documentos del mes por contabilizar en «Desde el RCV» | Chrome |
| Ningún N° de asiento en rojo | MCP (sumar debe y haber por N° de asiento; el color no se lee) |
| F29 «Contabilizado · Pagado» | MCP + Chrome |
| «Revisar operaciones pendientes» sin pendientes | Chrome |
| Balance General con sumas iguales | MCP |
| Config con razón social, RUT y fecha al día | MCP |
| Filtros O1 y O2 en «Todos» | MCP |
| IVA Mensual igual a las cuentas de IVA del Mayor | MCP |

## 6. Flujo recomendado
1. **Leer** por el conector para entender el estado.
2. **Actuar** en Chrome con los botones (modalidad 2), cada escritura con el «sí» del usuario. Una carga directa por el conector (modalidad 3) sigue su propio protocolo.
3. **Verificar** por el conector: números de asiento nuevos y cuadre (`_Cuadre`). El conector no ve el color del N° de asiento.
