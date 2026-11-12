# Don Balance

Skill para que Claude actúe como **Don Balance**, el agente guía de **Control Total Advance Automatizado** v7.6.22, el sistema contable en Google Sheets de [Vanguard Strategy SpA](https://vanguardstt.com) para empresas chilenas.

Don Balance explica cada paso, lee la planilla contigo y opera los formularios en Chrome. **Nada se contabiliza sin tu aprobación.**

## Qué hace

- Te guía en el mes: importar el RCV y la cartola, contabilizar ventas y compras, cobros y pagos, F29, remuneraciones, honorarios, activos fijos, renta y cierre.
- Revisa asientos que no cuadran, meses incompletos, diferencias de IVA y documentos sin contabilizar.
- Explica la contabilidad y la tributación chilena aplicadas a lo que estás haciendo.
- La primera vez hace un diagnóstico de solo lectura de tu planilla y arma un plan con lo que falta.
- Si lo autorizas, guarda una memoria por empresa en `Documentos/Don Balance/` (nunca claves ni sueldos).
- Puede cargar asientos de otros sistemas (Defontana, Nubox, Excel) con el conector de Google Sheets. Esta función está **pendiente de validación**.

No presenta ni paga nada en el SII, el banco ni Previred.

## Cómo se usa

1. Instala la skill en Claude.
2. Abre tu copia de la planilla en Google Chrome.
3. Dile a Claude: «Actúa como Don Balance en mi planilla».

Para que Claude opere la planilla necesitas Claude en Chrome; para leerla más rápido, el conector de Google Sheets. Sin eso, Don Balance te guía paso a paso y tú haces los clics.

## Instalación

- **Claude (web o escritorio):** comprime la carpeta `skills/don-balance` en un archivo .zip y súbelo en la sección Skills de la configuración de Claude.
- **Claude Code:** `npx skills add Devanguardstt/don-balance`

## Contenido

- `skills/don-balance/SKILL.md`: reglas de Don Balance y qué guía leer en cada caso.
- `skills/don-balance/references/`: la guía completa del sistema, dividida por tema.

## Aviso

Escrita para la versión 7.6.22 del sistema. Las reglas tributarias corresponden a esa versión y pueden cambiar. Esta skill guía el uso del sistema y explica reglas generales: no reemplaza la asesoría del contador responsable de la empresa.

## Licencia

Propietaria. © 2026 Vanguard Strategy SpA. Solo para clientes con licencia de Control Total Advance Automatizado. Ver [LICENSE](LICENSE).
