# Mapa del sistema

> Fuente: guía de Don Balance para Control Total Advance Automatizado v7.6.22, §5. Las menciones «§N» apuntan a otras secciones de esa guía; ../SKILL.md indica en qué archivo está cada una.

## 5. Mapa del sistema

### 5.1 Hojas
| Grupo | Hojas | ¿Se escribe a mano? |
|---|---|---|
| Base | **Config** · **P. Cuentas** · **Libro Diario** | Config: sí (celdas amarillas). P. Cuentas: no (usa el Editor). Libro Diario: lo escriben los formularios; a mano solo con cuidado |
| Respaldo tributario | **RCV Compras** · **RCV Ventas** | No: se importan |
| Automáticas (candado) | Libro Mayor · Mayor Analítico · Balance General (8 columnas) · Balance Clasificado · Estado Resultados · Flujo de Caja · Ratios Financieros · IVA Mensual · Resumen Ejecutivo | **Nunca** |
| Cobros, pagos y banco | **CxC** · **CxP** · **Cartola Bancaria** | CxC/CxP: ID, documento, condición y notas. El resto son fórmulas. Cartola: se importa |
| Maestros | Clientes · Proveedores · Personal · Sucursales · Proyectos · Centro Gasto · Centro Negocio | Sí. Rótulos en la fila 3; datos desde la fila 4 |
| Procesos | F29 · Remuneraciones · Rem Configuración · Activos Fijos · AF Configuración · AF Arrastre | Remuneraciones: los importes por concepto. El resto, desde su formulario |
| Registro | Historial PDFs | No |
| Técnicas ocultas | `_Registro Asientos`, `_Operaciones`, `_Preferencias`, `_Honorarios`… | **Nunca** |

### 5.2 Libro Diario: columnas
Cabecera en la fila 4; los datos empiezan en la fila 5. Cada línea del asiento es una fila.

| Columna | Contenido |
|---|---|
| A:E | Vínculo con la cartola: banco, fecha, descripción, referencia y monto del movimiento |
| **F** | **N° Asiento**: verde si el asiento cuadra (debe = haber), **rojo si no cuadra** |
| G | Fecha |
| H | Cuenta |
| I | Debe |
| J | Haber |
| K | Glosa |
| L | Libro Compra (documento del RCV de compras) |
| M | Libro Venta (documento del RCV de ventas) |
| N | CxC |
| O | CxP |
| P | Referencia del movimiento bancario |
| Q:W | Dimensiones: Cliente, Proveedor, Personal, Sucursal, Proyecto, Centro de Gasto, Centro de Negocio. Nunca van en líneas de Banco o Caja |
| X | Observación |
| AH en adelante | Técnicas: no tocar |

### 5.3 Config: celdas clave
| Celda | Qué es |
|---|---|
| Filas 8 a 23 | Datos de la empresa. Razón social (C8) y RUT (C10) bastan para empezar; van en la cabecera de los PDF |
| C15 | Régimen tributario: Pro Pyme General, Pro Pyme Transparente, Régimen General (14 A) o Renta Presunta. Debe coincidir con el SII |
| C26 / C27 | Año fiscal y mes de inicio (casi siempre 1) |
| C28 / C29 | Inicio y término del ejercicio. Se calculan solos |
| C30 | Fecha de corte (opcional). Vacía: los informes llegan al último mes con movimientos |
| C35 | **Tasa PPM** de la empresa (código 115 del F29) |
| C36 | **Tasa impuesto a la renta**. La propone el sistema; no se escribe |
| C37 | Impuesto a la renta en informes: «Solo el contabilizado» o «Estimado si no hay impuesto contabilizado» |
| C49 | Fecha de cierre contable. La escribe el cierre del ejercicio |
| Filas 40 a 45 | Datos para el pie de los PDF (responsable, cargo, lugar, fecha) |
