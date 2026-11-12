# Primer uso de una copia

> Fuente: guía de Don Balance para Control Total Advance Automatizado v7.6.22, §4. Las menciones «§N» apuntan a otras secciones de esa guía; ../SKILL.md indica en qué archivo está cada una.

## 4. Primer uso de una copia

1. **Hacer la copia:** *Archivo › Crear una copia*, una por empresa. El script viaja con la planilla.
   - Una copia nueva viene **en blanco**, sin datos de ejemplo. Antes de generar informes se completan en Config la razón social (C8) y el RUT (C10), que van en la cabecera de los PDF.
   - Una copia nueva también viene **sin Plan de cuentas aplicado y sin RCV**. Los formularios lo avisan con mensajes naranjos arriba (por ejemplo, «El Plan no tiene cuentas de ingreso activas»): significa que falta el paso de §6.1, no que algo esté roto.
2. **Autorizar el script, con cuidado.** La primera vez que se usa un menú, Google pide permiso. **No se acepta la advertencia a ciegas**: primero se comprueba qué se está autorizando.
   - **Por qué aparece «Google no ha verificado esta aplicación»:** Google lo muestra con los scripts que no pasaron su proceso de verificación. El script de esta planilla es un proyecto privado ligado al libro, no una aplicación publicada (Documentado en la Ficha FIN-06). La advertencia es esperable, pero **no prueba que el script sea seguro**: por eso se verifica antes.
   - **Quién es el propietario:** al hacer *Archivo › Crear una copia*, el script viaja con la planilla y la copia queda a nombre de la cuenta que la hizo (**Inferido** de cómo funcionan los scripts ligados a una hoja; confirmar en *Extensiones › Apps Script*). Lo que importa verificar es **de dónde viene la planilla original**: debe ser la que entregó Vanguard.
   - **Verificar antes de continuar (con el usuario, de a una pregunta):**
     1. «¿La planilla te la entregó Vanguard, desde el enlace o archivo oficial?».
     2. En *Extensiones › Apps Script* (abierto desde esta misma planilla, no desde un enlace aparte), el proyecto se llama «Control Total PRO Advance AppScript» (Documentado en la Ficha). Si el nombre que muestra Google difiere, no seguir y consultar a Vanguard.
     3. La pantalla de permisos pide **solo** los cinco de la tabla de abajo y la cuenta que autoriza es la del usuario.
   - **Pedir la confirmación:** «¿Reconoces esta planilla como la de Vanguard y estás de acuerdo con estos permisos?». Sin un sí, no se continúa.
   - **Detener el procedimiento** si: el usuario no sabe de dónde viene la planilla; el proyecto tiene otro nombre; la pantalla pide permisos distintos o adicionales (por ejemplo enviar correos, leer el contenido del correo, contactos o calendario); o el origen o los permisos no se pueden verificar.
   - **Quién pulsa:** el usuario, no Don Balance (regla 5). Si todo calza: *Configuración avanzada › Ir a «Control Total…» (no seguro)* y *Permitir*.
   - **Permisos que pide y para qué los usa:**

     | Permiso | Para qué |
     |---|---|
     | Hojas de cálculo | Leer y escribir la planilla |
     | Mostrar contenido en ventanas | Los formularios |
     | Google Drive | Guardar los PDF y CSV en la carpeta principal de Drive, convertir la cartola Excel en un archivo temporal (después va a la papelera) y revisar con quién está compartido el libro |
     | Conectarse a un servicio externo | Solo para llamar a la API de Google Drive al convertir la cartola |
     | Ver tu correo | Identificar quién hace cada operación |

   - **El sistema no envía correos ni se conecta al SII, al banco ni a otros servicios** (Confirmado en el código, Ficha FIN-06).
3. **Dashboard financiero:** es una página web del propio script y **no está en los menús**. Para abrirlo en una copia nueva se publica una vez:
   1. *Extensiones › Apps Script › Implementar › Nueva implementación*.
   2. Tipo: *Aplicación web*.
   3. En «Quién tiene acceso», elige «Solo yo». Con el acceso abierto, cualquiera que tenga la URL ve los estados financieros de la empresa.
   4. *Implementar*. Pide aprobación antes de pulsarlo.
   5. Se abre la URL que termina en `/exec`.

   Si el libro no tiene el Plan aplicado, el Dashboard dice «Faltan datos para mostrar el Dashboard».
4. **No hay tareas automáticas programadas:** nada corre solo por horario. Todo lo inicia el usuario desde un menú. Lo único automático es que el Libro Diario, CxC, CxP y la Cartola crecen de a 1.000 filas cuando se acercan al final.
