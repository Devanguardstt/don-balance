# Operar la planilla en Chrome

> Fuente: guía de Don Balance para Control Total Advance Automatizado v7.6.22, §3. Las menciones «§N» apuntan a otras secciones de esa guía; ../SKILL.md indica en qué archivo está cada una.

## 3. Cómo operar la planilla en Chrome

### 3.1 Los menús
El sistema agrega **cinco menús** a la barra de Google Sheets, a la derecha de «Ayuda». Llevan un punto delante para distinguirlos de los de Google.

| Menú | Opciones |
|---|---|
| **• Configuración** | Editor del Plan de Cuentas · Reaplicar protecciones del sistema · (en libros antiguos: Migrar parámetros antiguos a roles) |
| **• Importaciones** | Cargar RCV Compras (CSV) · Cargar RCV Ventas (CSV) · Importar cartola bancaria · Importar Libro de Remuneraciones de RRHH (LRE)… |
| **• Asientos** | Desde el RCV: ventas, compras, cobros y pagos… · Registrar a mano › (Ingreso, egreso o traspaso · Asiento libre) · Procesos mensuales › (Impuestos mensuales (F29) · Remuneraciones · Boletas de honorarios recibidas · Activos fijos y depreciación) · Procesos anuales › Renta y cierre del ejercicio… · Revisar operaciones pendientes |
| **• Reportes** | ▸ Estado de Resultados del ejercicio (PDF) · ▸ Estado de Situación Financiera (PDF) · ▸ Balance de 8 Columnas (PDF)… · ▸ Libro de caja: movimientos de caja y bancos… · ▸ Informe Financiero mensual (PDF) · ▸ Determinación de la renta del ejercicio (PDF) · Ver estado de actualización · Reparar estructura de los reportes |
| **• Guía de uso** | Abre la guía oficial del sistema, con buscador |

**Los menús tardan en aparecer:** al abrir la planilla pueden pasar unos 10 segundos antes de que se vean los cinco. Espera antes de concluir que faltan.

**Si después de esperar solo ves «• Configuración» o no ves ninguno:**
- Puede que el script aún no esté autorizado (§4).
- Si ya está autorizado, recarga la pestaña.

### 3.2 Los formularios
- Casi todo se hace en **ventanas (formularios)** que abre el menú, encima de la planilla.
- Tardan en cargar: en una copia nueva el primer formulario puede demorar **hasta 30 segundos** («Leyendo RCV Ventas, Libro Diario y CxC…»). Espera a que desaparezca el texto de carga antes de actuar y no vuelvas a abrir el menú mientras tanto.
- Se cierran con la **×** de arriba a la derecha. Cerrar sin contabilizar no escribe nada.
- Mientras trabaja, Google muestra arriba «Ejecutando secuencia de comandos»: espera a que termine.
- Los pasos van numerados arriba (por ejemplo *1 · Seleccionar → 2 · Configurar → 3 · Vista previa → 4 · Resultado*).
- Sigue el orden y lee los mensajes del formulario: dicen por qué un documento está bloqueado o qué falta.
- Una lista atenuada significa que viene una actualización. Si tarda, aparece «Volver a pedirla».

**Colores de los botones (son iguales en todos los formularios):**

| Color | Qué hace |
|---|---|
| Azul oscuro | Avanza o revisa. No escribe nada |
| **Dorado** | **Escribe en el Libro Diario. Es el único que contabiliza** |
| Con borde | Guarda datos en una hoja o configuración, sin contabilizar |
| Rojo | Elimina asientos, después de mostrar qué se eliminaría |

**Fechas:** escribe dd/mm/aaaa o abre el calendario con ▾, Alt+↓ o F4. Una fecha que no existe se marca en rojo y no se usa.

### 3.3 Colores de las celdas
- **Amarillo:** lo completa el usuario.
- **Azul claro con ▾:** se elige de una lista.
- **Gris azulado:** lo calcula el sistema. No se escribe.

### 3.4 Leer la planilla
- Para leer cifras, ve a la hoja y lee las celdas. Prefiere leer el texto antes que adivinar desde una imagen.
- Los reportes se recalculan solos con fórmulas a partir del Libro Diario: **no hay que «generarlos»**.
- Si algo se escribió por error, se puede deshacer con Ctrl+Z justo después, o con *Archivo › Historial de versiones*. Pide permiso antes de usar Ctrl+Z y antes de restaurar una versión.
