# Memoria y trazabilidad del cliente

> Lo que el cliente conversa con Claude no se guarda solo. Esta carpeta es lo que hace que la skill «aprenda» sus nombres de cuentas, sus formatos y su historia. Etiquetas: **Propuesto** salvo lo marcado.

## 1. Dónde

`~/Documents/Don Balance/<empresa>/` en el equipo donde corre Claude Code (una carpeta por planilla). Verificar antes dónde corre Claude Code: si es un equipo local, la carpeta queda ahí; si fuera un entorno remoto o en la nube, la carpeta quedaría en ese entorno y no en el computador del cliente (ver §6). Al primer uso, dentro del diagnóstico inicial (`diagnostico-inicial.md` §4), preguntar: «¿Creo la carpeta Don Balance en tus Documentos para ir guardando lo que hagamos?». Sin un sí explícito, no se crea nada y se trabaja sin memoria.

```
Don Balance/<empresa>/
  perfil.md             planilla, versión (o «sin comprobar»), régimen, tipo de usuario, sistemas de origen, ruta a los archivos
  diagnostico.md        resultado del diagnóstico inicial por ítem y tareas pendientes (ver diagnostico-inicial.md)
  mapeo-cuentas.md      nombre en otro sistema → cuenta del plan (lo aprendido)
  formatos/<sistema>.md cómo viene cada archivo (columnas, separadores, fechas)
  terceros.md           alias de clientes y proveedores → nombre exacto en los maestros
  bitacora.md           una línea por sesión: fecha, qué se hizo, asientos, pendientes
  importaciones/AAAA-MM-DD_<origen>/
    original.<ext>      copia del archivo recibido
    normalizado.tsv     lo que se cargó o se iba a cargar
    cruce.md            informe de cruce (ver importar-contabilidad-externa.md)
```

**Crear la carpeta (solo después del sí del usuario):**
1. La carpeta base es `Documents/Don Balance/`. Lo más simple es que el cliente **abra Claude Code dentro de esa carpeta** (`conexion-inicial.md` §2): entonces `Don Balance/` es la carpeta de trabajo y las carpetas por empresa se crean dentro de ella. Si Claude Code se abrió en otra carpeta, decirlo y pedir un sí para crear `~/Documents/Don Balance/`; Claude Code puede pedir además su propio permiso para escribir fuera de la carpeta de trabajo (**Inferido**).
2. Crear `<empresa>/` (nombre de la razón social, sin símbolos) con solo `perfil.md`, `diagnostico.md` y `bitacora.md`. Lo demás (`mapeo-cuentas.md`, `terceros.md`, `formatos/`, `importaciones/`) se crea **cuando haga falta**, no antes: no se dejan carpetas vacías «por si acaso».
3. Decir al usuario qué se creó y dónde.
4. **Esta carpeta es la memoria de Don Balance.** No es la «memoria» interna de Claude Code ni se instala con la skill: la skill (instrucciones) queda en la carpeta de skills de Claude Code; los datos de cada empresa quedan aquí.

## 2. Al comenzar cada sesión

1. Leer `perfil.md`, `diagnostico.md`, `mapeo-cuentas.md` y las últimas líneas de `bitacora.md`. Si no hay `diagnostico.md`, es primera vez: `diagnostico-inicial.md`.
2. Comprobar con el conector que la planilla abierta es la del perfil (nombre y RUT de Config). Si no coincide, preguntar antes de seguir.
3. Retomar los pendientes de la última sesión.

## 3. Al terminar cada sesión

Agregar a `bitacora.md` una línea: fecha · qué se hizo · N° de asientos creados · qué quedó pendiente. Si se aprendió una cuenta o un formato, actualizar `mapeo-cuentas.md` o `formatos/`.

## 4. Formato de `mapeo-cuentas.md`

| Origen | Nombre o código en el otro sistema | Cuenta de la planilla | Confirmó | Fecha |
|---|---|---|---|---|
| Defontana | Deudores por Venta | 1-12-01 \| Clientes | Usuario | 2026-11-12 |

Una fila por equivalencia. Solo entra lo que el usuario confirmó. Si el plan de la planilla cambia, revisar las filas cuya cuenta ya no exista.

## 5. Qué NO se guarda

- Contraseñas, claves del SII, datos de tarjetas ni tokens.
- Sueldos o remuneraciones individuales (el detalle vive solo en la planilla).
- La skill no envía la carpeta ni su contenido a Vanguard, a mensajes ni a otros servicios. Pero **lo que Don Balance lee o escribe en esta carpeta sí se procesa en la nube** al conversar (ver §6): no existe la garantía de que «nada sale del computador».
- Si un dato no se debe guardar y es necesario para la tarea, se usa en la sesión y no se anota.

## 6. Privacidad y tratamiento de datos
> Describe cómo está diseñada la arquitectura. **No es una garantía legal ni técnica.** Lo que depende de Claude Code, Anthropic, Google o del entorno del cliente se indica como tal; no se promete cifrado, aislamiento, retención, eliminación ni exclusividad de acceso que no se hayan verificado.

**Qué sistemas participan**
- El equipo donde corre **Claude Code** (con la carpeta de memoria).
- **Claude / Anthropic**: el modelo que lee y responde.
- El **conector de Google Sheets** y **Google Sheets / Drive**, donde vive la planilla.
- **Chrome**, con la sesión de Google del usuario.

**Procesamiento, almacenamiento y acceso no son lo mismo**
| | Qué significa aquí |
|---|---|
| **Procesamiento** | Todo lo que Don Balance lee (celdas de la planilla, archivos que el usuario entrega, mensajes, contenido de la carpeta de memoria) pasa a los servicios de Claude para generar la respuesta: es **procesamiento en la nube** |
| **Almacenamiento** | La planilla vive en Google. La memoria de Don Balance son archivos en la carpeta del equipo donde corre Claude Code. Cuánto conservan Anthropic, Google o el servicio de sincronización lo ya procesado **depende de las condiciones y la configuración de cada cuenta**: no está verificado aquí |
| **Acceso** | Quién puede abrir la carpeta (usuarios del equipo, copias de seguridad o sincronización como iCloud o Drive si «Documentos» está sincronizado) y la planilla (botón «Compartir» de Google) lo define el cliente |

**Vanguard Strategy SpA:** esta skill no envía datos a Vanguard y Vanguard **no debe tener acceso operativo** a los datos de un cliente salvo autorización expresa y un mecanismo de acceso configurado para ese fin (por ejemplo, que el cliente comparta algo a propósito). Es un principio de diseño, no una garantía técnica.

**Permisos de acceso:** el conector y Chrome actúan con la cuenta de Google del usuario y solo ven lo que esa cuenta puede ver. Si ve varias empresas, Don Balance trabaja con **una** a la vez.

**Separación entre empresas (medidas de la skill, no aislamiento técnico):**
- Una carpeta por empresa; nunca mezclar `mapeo-cuentas.md`, `terceros.md` ni `importaciones/` entre empresas.
- Al empezar, confirmar la empresa con Config y con `perfil.md`; si no coincide, preguntar.
- No cargar en la misma conversación datos de dos empresas distintas.

**Qué no se guarda:** contraseñas, claves del SII o tributarias, datos de tarjetas, tokens y credenciales de cualquier tipo, ni remuneraciones individuales.

**RUT y datos personales (minimización):** usar solo lo necesario para la tarea. En la memoria queda el RUT de la **empresa** (`perfil.md`); no se guardan RUT de personas ni datos de personal. Cualquier dato personal visto durante una carga se usa en la sesión y no se anota.

**Archivos temporales y conservación:** `importaciones/` guarda copia del archivo original y el `normalizado.tsv`. Conservarlos solo mientras hagan falta: al cerrar el período, ofrecer al usuario borrarlos. No hay borrado automático. Don Balance elimina los temporales que **él mismo** haya creado fuera de la carpeta del cliente, avisando. Borrar archivos del cliente siempre se pregunta antes (regla 2).

