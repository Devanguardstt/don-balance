# Ficha del producto: Control Total Advance Automatizado (FIN-06)

> Resumen de la Ficha FIN-06 v2 (2026-11-09), hecha desde el uso de punta a punta y desde la lectura del código de Apps Script v7.6.22 (sin ejecutar funciones). **No confundir con Control Total Advance (FIN-05, v7.5), que es otro producto.** Etiquetas: **Confirmado (código)** · **Confirmado (en uso)** · **Documentado (guía)** · **Inferido** · **Pendiente**.

## 1. Qué es
Sistema contable completo para empresas chilenas, en Google Sheets con Apps Script. El usuario carga el RCV del SII y el sistema arma los asientos; registra cobros y pagos con la cartola; contabiliza remuneraciones, honorarios, activos fijos y F29; entrega libros, estados financieros, PDF, renta, cierre del año y un dashboard web. Una copia por empresa. **El usuario elige y revisa; el formulario arma el asiento y lo escribe solo cuando el usuario confirma.**

- **Versión:** 7.6.22 (la copia se llama «Control Total PRO Advance v7.6.22»). La versión no aparece en las hojas ni siempre en el título de la copia: cómo comprobarla está en `diagnostico-inicial.md` §4. Si resulta otra (se probó una 7.6.23), avisarlo: algunas pantallas o mensajes pueden diferir.
- **Funciona solo en Google Sheets**, en navegador de escritorio (Windows y macOS; no probado en tablet ni celular).

## 2. Qué NO hace (decirlo con claridad)

| Pregunta del cliente | Respuesta |
|---|---|
| ¿Se conecta al SII o al banco? | **No.** El cliente importa sus archivos |
| ¿Presenta o paga el F29, el F22 o las DJ? | **No.** Registra lo declarado y deja antecedentes de apoyo; declarar y pagar es del usuario |
| ¿Acepta la cartola de cualquier banco? | **Solo Excel de Mercado Pago.** Otro banco: el cuadro avisa y no importa; Vanguard adapta la cartola como servicio aparte |
| ¿Calcula sueldos y liquidaciones? | **No.** Contabiliza remuneraciones ya calculadas (a mano o desde el LRE de la DT) |
| ¿Los asientos se hacen solos? | El sistema los **propone**; cada lote lo confirma el usuario. Nada corre solo ni programado |
| ¿Renta Presunta? | El sistema no la determina |
| ¿Varios usuarios a la vez? | Hay bloqueos, pero el uso simultáneo **no se probó** |
| ¿Envía correos? | No |
| ¿Reemplaza a un ERP? | No es software homologado ni emite documentos tributarios |
| ¿Importa asientos de otro sistema? | **No tiene un importador nativo.** «• Importaciones» solo trae RCV, cartola, honorarios y LRE. Don Balance puede hacer una **carga asistida** con el conector de Sheets (modalidad 3), pero está **diseñada y pendiente de validación**: `carga-directa-mcp.md` |

## 2b. Tres modalidades de registro de asientos
1. **Manual directo** en la hoja Libro Diario (`formato-plantilla.md` §9).
2. **Formularios nativos** de Apps Script (menús «•»): Desde el RCV, Registrar a mano, Asiento libre, Remuneraciones, Honorarios, Activos fijos, F29, Renta y cierre. Conservan la trazabilidad completa.
3. **Carga asistida directa** con Claude Code y el conector de Sheets (`carga-directa-mcp.md`): **diseñada, pendiente de validación en copia de demo**, sin la trazabilidad de los formularios. No es un importador del producto.

## 3. Qué incluye (Confirmado)
- **Plan de cuentas:** Editor en 3 etapas; la estructura sugerida deja 41 subgrupos y 79 cuentas e instala 43 asignaciones para los módulos.
- **Importar:** RCV compras y ventas (CSV del SII), cartola (Mercado Pago), boletas de honorarios recibidas (.xls/.htm), LRE (.csv/.txt). Importar no contabiliza.
- **Asientos:** desde el RCV (ventas, compras, cobros y pagos), registro manual (ingreso, egreso, cobrar o pagar, traspaso, asiento libre, bandeja), remuneraciones, honorarios, activos fijos y depreciación, F29, renta y cierre, revisar operaciones pendientes, eliminación controlada.
- **Reportes con fórmulas:** Libro Mayor, Mayor Analítico, Balance de 8 columnas, Balance Clasificado, Estado de Resultados, Flujo de Caja, Ratios (19 indicadores más capital de trabajo), IVA Mensual, Resumen Ejecutivo, filtro por dimensión (O1 y O2).
- **PDF:** Estado de Resultados, Situación Financiera, Balance de 8 columnas, Informe Financiero mensual, Determinación de la renta; libro de caja con vista, CSV y PDF. Se guardan en la carpeta principal del Drive.
- **Dashboard web:** no está en los menús; se publica una vez (`primer-uso.md`).
- **Guía de uso** dentro de la planilla («• Guía de uso», con buscador).

## 4. Cómo se protege lo escrito
- Cada operación tiene identidad en `_Registro Asientos` y `_Operaciones`: si se corta la conexión se comprueba antes de repetir.
- Un asiento automático **editado o borrado a mano** queda «en revisión» y ningún módulo lo usa hasta resolverlo.
- Con el libro compartido para edición, un **candado temporal** protege las hojas mientras corre una generación masiva.
- Un cierre del ejercicio (Config C49) bloquea escribir y eliminar con fechas cerradas; se reabre con un motivo.
- El Libro Diario, CxC, CxP y Cartola crecen solos de a 1.000 filas.
- Columnas técnicas del Libro Diario: AH a AR (cuadre, flujo de caja, código, rol). No se tocan.
- El script no guarda datos contables fuera de la planilla. Permisos: Hojas de cálculo, ventanas, Drive, servicio externo (solo para convertir la cartola) y correo del usuario.

## 5. Defectos conocidos (Documentado en «FIN-06 Errores plantilla»)
| Código | Qué pasa | Qué decir |
|---|---|---|
| E-01 | Antes de autorizar el script solo se ve «• Configuración» | Normal: autorizar (`primer-uso.md`) |
| E-02 | Config C35 rechaza 0,25 % de PPM por validación | Rango admitido sin confirmar; consultar a Vanguard |
| E-03 | «Condición de pago» con `30` en vez de `30 días` | Solo vale Contado, 30 días, 60 días, 90 días |
| E-04 | Una fecha inexistente (30/02) se acepta al pegar y luego bloquea el Libro de caja | Revisar fechas antes de pegar |
| E-05 | «Aplicar y guardar cambios» del Plan puede tardar unos 5 minutos en una copia vacía | Esperar sin cerrar ni repetir |
| E-06 | El cuadro del plan dice «40 de 40» y «43 completadas» | Mensaje inconsistente, no un error |

Otros pendientes: la columna «Estado Pago/Cobro» del RCV siempre dice «Pendiente» (duda abierta); no se probaron cierre y apertura del ejercicio, datos reales, otros regímenes ni otros bancos; los factores de actualización del año tributario 2027 se cargan en enero de 2027.

## 6. Cómo responder
- Una función que no aparece aquí ni en las demás referencias: «No consta en la documentación de la planilla» y ofrecer revisar la «• Guía de uso».
- No atribuir a esta planilla nada de FIN-05 ni de Control Total Starter (FIN-03).
- Nunca precios, ofertas ni promesas comerciales: eso lo ve el cliente en la tienda.
