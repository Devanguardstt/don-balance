# Conexión inicial: Chrome, conector de Sheets y carpeta del cliente

> Se hace una sola vez por computador. Etiquetas: **Verificado** (probado) · **Documentado** · **Pendiente** (completar al grabar el video de conexión).

## 1. Qué se conecta y para qué

| Pieza | Para qué | Quién la instala |
|---|---|---|
| **Claude en Chrome** (extensión) | Abre la planilla con la sesión de Google del cliente y pulsa menús, formularios y botones (PDF, importaciones, botón dorado) | El cliente |
| **Conector de Google Sheets** (MCP) | Lee y escribe celdas sin abrir el navegador: rápido y barato en tokens. Escribir asientos en el Libro Diario con él es la modalidad 3, pendiente de validación (`carga-directa-mcp.md`) | El cliente |
| **Skills** (`don-balance` y las que se sumen) | El conocimiento de la planilla | El cliente (carpeta de skills de Claude Code) |
| **Carpeta del cliente** | Memoria y trazabilidad: qué se hizo, qué cuentas se usan, archivos importados | La crea la skill (ver `memoria-cliente.md`) |

Cuándo usar cada vía de trabajo: `mcp-vs-chrome.md`. Antes de conectar, el cliente debe saber que lo que Don Balance lee se **procesa en la nube** y qué datos no se guardan (`memoria-cliente.md` §6).

## 2. Pasos de instalación

1. **Extensión Claude en Chrome:** instalarla en el Chrome donde el cliente tiene su sesión de Google, e iniciar sesión con la misma cuenta de Claude. **Pendiente:** pasos y pantallas exactas (se completan con el video).
2. **Conector de Google Sheets:** agregarlo como conector de Claude y autorizar la cuenta de Google que es dueña de la planilla. **Pendiente:** nombre exacto del conector y pantallas.
3. **Skill y carpeta de trabajo:**
   1. Crear la carpeta `Documents/Don Balance/` y abrir una terminal en ella.
   2. Ejecutar `npx skills add Devanguardstt/don-balance` y elegir Claude Code. La herramienta descarga la skill desde GitHub y la instala en la carpeta donde se ejecuta (sin opciones, solo para ese proyecto; con `-g`, para todos los proyectos). **Documentado** en la documentación de la herramienta `skills`; **no probado por Vanguard** todavía.
   3. Abrir Claude Code en esa misma carpeta. La skill queda disponible y Don Balance se presenta al primer mensaje (`diagnostico-inicial.md`).
   4. Si la skill no aparece, revisar que Claude Code se abrió en la carpeta donde se instaló.
4. **Carpeta del cliente:** la crea la skill al primer uso, tras pedir permiso (ver `memoria-cliente.md`).

## 3. Pruebas para confirmar que todo quedó conectado

Hacerlas en este orden y contar el resultado al cliente en una línea cada una:

| Prueba | Cómo | Resultado esperado |
|---|---|---|
| Chrome | Listar las pestañas del navegador conectado | Aparece Chrome y la planilla abierta |
| Menús | Esperar ~10 s en la planilla | Se ven los cinco menús «•» (si solo se ve «• Configuración»: `primer-uso.md`) |
| Conector (lectura) | Pedir las hojas de la planilla y leer `Config!C8:C10` | Lista de hojas; razón social y RUT |
| Conector (escritura) | (No se hace durante el diagnóstico inicial.) **Solo en una copia de prueba** y con OK del cliente: escribir una celda vacía y borrarla | Se escribe y se verifica con una lectura |
| Carpeta | Existe la carpeta del cliente con `perfil.md` | Sí |

Con las pruebas en orden, lo siguiente es el diagnóstico de la planilla (`diagnostico-inicial.md`).

## 4. Qué pedirle al cliente que tenga a mano

- La planilla abierta en Chrome, con el script autorizado (`primer-uso.md`).
- Los archivos de sus otros sistemas (Defontana, Nubox, Visual, Excel…) en una carpeta que pueda indicar: ver `importar-contabilidad-externa.md`.
- Nada de claves: la skill nunca pide ni escribe contraseñas, claves del SII ni datos de tarjetas (regla 5).
