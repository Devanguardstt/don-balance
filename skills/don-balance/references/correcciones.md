# Correcciones y recuperación

> Fuente: guía de Don Balance para Control Total Advance Automatizado v7.6.22, §9. Las menciones «§N» apuntan a otras secciones de esa guía; ../SKILL.md indica en qué archivo está cada una.

## 9. Correcciones y recuperación

### 9.1 Antes de corregir
1. Ubica el origen de la cifra. Ve del reporte al **Libro Mayor**, luego al **Mayor Analítico** (cuenta en B2) y al asiento del **Libro Diario**.
2. Mira quién lo creó. Si fue un formulario, **corrige desde ese formulario**.
3. Corrige el origen, no el reporte. Una cifra mal ubicada suele venir de la clasificación de una cuenta (Editor del Plan) o de un documento del RCV.

### 9.2 Eliminar asientos (siempre con vista previa y OK)
| Dónde se creó | Cómo se elimina |
|---|---|
| Desde el RCV | Filtrar contabilizados › marcar › «Eliminar asientos de…» |
| Registro manual | Registradas › la operación › «Revisar la eliminación…» |
| F29 | En el período: «Eliminar el pago…» o «Eliminar la liquidación…» |
| Remuneraciones, Honorarios, Activos | En su mes, boleta o ficha: «Eliminar el asiento…» |
| Renta y cierre | «Eliminar el asiento del impuesto» (con el año abierto) o «Eliminar la apertura…» |

Eliminar un asiento **no deshace el pago real en el banco**.

### 9.3 Si una respuesta se pierde
1. **No vuelvas a pulsar.** Cada operación tiene identidad.
2. Usa la comprobación del formulario, por ejemplo «Comprobar si quedó contabilizada».
3. Si se cerró la ventana, usa *• Asientos › Revisar operaciones pendientes*: completa o anula lo que quedó a medias. En *Desde el RCV*, una operación abierta aparece arriba con Continuar, Cancelar el resto y Revisar.
4. **Está resuelto cuando** «Revisar operaciones pendientes» no informa nada y el Libro Diario no tiene el mismo asiento dos veces (busca por glosa o documento).

### 9.4 Un asiento automático editado o borrado a mano
- Queda «en revisión» y el módulo no lo usa.
- Para resolverlo, restablécelo (*Archivo › Historial de versiones*, con permiso del usuario) o elimínalo desde su formulario.
- Si se borró entero, en *Revisar operaciones pendientes* se puede dar de baja su registro.
- Un asiento cargado con el conector (modalidad 3) o escrito a mano no tiene identidad de formulario: no se elimina desde «Registradas» y se corrige a mano, con vista previa y «sí» (`carga-directa-mcp.md` §5).

### 9.5 Problemas frecuentes
| Síntoma | Causa probable | Qué hacer |
|---|---|---|
| Solo aparece «• Configuración» | El script no está autorizado | El usuario autoriza (§4) y recarga |
| N° de asiento en rojo | Debe ≠ haber, casi siempre por un asiento escrito a mano | Ubicar la línea, corregir desde su origen o con un asiento libre de ajuste |
| La celda de la Tasa PPM rechaza el valor | Validación de datos de C35 | Revisar el formato (porcentaje). Si una tasa real no entra, avisar a Vanguard |
| Condición de pago con triángulo rojo en CxC/CxP | Valor fuera de la lista | Usar Contado, 30 días, 60 días o 90 días |
| Fechas inexistentes pegadas en el Libro Diario | Pegar no valida | Corregir la fecha. El Libro de caja las marca como «fecha no válida» |
| La cartola no se importa | No es un Excel de Mercado Pago, o fue editado | Exportar de nuevo sin editar; otros bancos, con Vanguard |
| Un módulo dice «la cuenta X no está en el Plan de Cuentas» | Alguien cambió P. Cuentas a mano | Deshacer, o corregir en el Editor del Plan |
| La tasa de renta (C36) está vacía | No hay regla segura (§8.4) | Decidir con el contador |
| El PDF no se genera | Reportes sin actualizar o un dato de Config faltante | Leer el motivo, corregir y «Reintentar». Revisar *Ver estado de actualización* |
| El IVA de un documento se cuenta dos veces | Documento pegado a mano dos veces en el RCV | Eliminar la fila sobrante antes de contabilizar |
| El Dashboard dice «Faltan datos» | El Plan no está aplicado | Aplicar el Plan (§6.1) |
| No se puede escribir en una fecha | El ejercicio está cerrado (Config C49) | Reabrir con motivo en Renta y cierre, solo si el usuario lo decide |
