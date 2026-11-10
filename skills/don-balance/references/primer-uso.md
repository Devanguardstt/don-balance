# Primer uso de una copia

> Fuente: guía de Don Balance para Control Total Advance Automatizado v7.6.22, §4. Las menciones «§N» apuntan a otras secciones de esa guía; ../SKILL.md indica en qué archivo está cada una.

## 4. Primer uso de una copia

1. **Hacer la copia:** *Archivo › Crear una copia*, una por empresa. El script viaja con la planilla.
   - Una copia nueva trae **datos de ejemplo** en Config (por ejemplo, razón social «Ejemplo Empresa» y un RUT de muestra). Se reemplazan por los de la empresa real antes de generar informes.
   - Una copia nueva también viene **sin Plan de cuentas aplicado y sin RCV**. Los formularios lo avisan con mensajes naranjos arriba (por ejemplo, «El Plan no tiene cuentas de ingreso activas»): significa que falta el paso de §6.1, no que algo esté roto.
2. **Autorizar el script:** la primera vez que el usuario usa un menú, Google pide permiso.
   - Si aparece **«Google no ha verificado esta aplicación»**, el usuario pulsa *Configuración avanzada › Ir a … (no seguro)*. Es normal en scripts propios de una planilla.
   - **Permisos que pide y para qué los usa:**

     | Permiso | Para qué |
     |---|---|
     | Hojas de cálculo | Leer y escribir la planilla |
     | Mostrar contenido en ventanas | Los formularios |
     | Google Drive | Guardar los PDF y CSV en la carpeta principal de Drive, convertir la cartola Excel en un archivo temporal (después va a la papelera) y revisar con quién está compartido el libro |
     | Conectarse a un servicio externo | Solo para llamar a la API de Google Drive al convertir la cartola |
     | Ver tu correo | Identificar quién hace cada operación |

   - **El sistema no envía correos ni se conecta al SII, al banco ni a otros servicios.**
3. **Dashboard financiero:** es una página web del propio script y **no está en los menús**. Para abrirlo en una copia nueva se publica una vez:
   1. *Extensiones › Apps Script › Implementar › Nueva implementación*.
   2. Tipo: *Aplicación web*.
   3. En «Quién tiene acceso», elige «Solo yo». Con el acceso abierto, cualquiera que tenga la URL ve los estados financieros de la empresa.
   4. *Implementar*. Pide aprobación antes de pulsarlo.
   5. Se abre la URL que termina en `/exec`.

   Si el libro no tiene el Plan aplicado, el Dashboard dice «Faltan datos para mostrar el Dashboard».
4. **No hay tareas automáticas programadas:** nada corre solo por horario. Todo lo inicia el usuario desde un menú. Lo único automático es que el Libro Diario, CxC, CxP y la Cartola crecen de a 1.000 filas cuando se acercan al final.
