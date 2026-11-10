# Conocimiento tributario chileno

> Fuente: guía de Don Balance para Control Total Advance Automatizado v7.6.22, §8. Las menciones «§N» apuntan a otras secciones de esa guía; ../SKILL.md indica en qué archivo está cada una.

## 8. Conocimiento tributario chileno (según la versión 7.6.22)

> Reglas tal como las trae el sistema, con sus fuentes. **El usuario o su contador confirma su situación.** Si una norma cambió después de esta versión, dilo y no la apliques sin confirmación.

### 8.1 IVA y F29 (mensual)
| Código | Significado |
|---|---|
| 538 | Débito fiscal del mes |
| 504 | Remanente de crédito del mes anterior, reajustado |
| 537 | Total de créditos (crédito del mes + 504) |
| 89 | IVA determinado a pagar |
| 77 | Remanente para el mes siguiente |
| 62 | PPM del mes (ingresos del mes × tasa PPM de Config C35, la del código 115) |
| 48 | Impuesto único de los trabajadores (lo reconoce Remuneraciones) |
| 151 | Retención de honorarios (la reconoce Honorarios) |
| 91 | Total a pagar |
| 756 / 755 | Postergación del IVA / monto postergado |

- La hoja **IVA Mensual** estima el F29 desde los libros.
- **Se contabiliza lo declarado**, no la estimación. Si hay diferencia se pide el motivo.
- El remanente no es gasto ni ingreso: es crédito a favor que pasa al mes siguiente.
- **Postergación del IVA:** se marca en lo declarado. El IVA por pagar se reconoce igual y se paga con el giro, aparte.

### 8.2 PPM
- Es el anticipo mensual del impuesto anual, con la tasa del código 115 (Config C35).
- Los PPM pagados, **reajustados**, son crédito en el F22.
- **Tasa PPM (C35)** y **tasa de renta (C36)** son cosas distintas:
  - La PPM la pone el usuario.
  - La de renta la propone el sistema y solo sirve para estimar en los informes.

### 8.3 Regímenes y base imponible
| Régimen (Config C15) | Base | Impuesto de primera categoría (IDPC) en la empresa |
|---|---|---|
| Régimen General (art. 14 A) | **Devengada**: resultado con agregados, deducciones y corrección monetaria | Sí |
| Pro Pyme General (art. 14 D N° 3) | **Percibida/pagada**: ingresos percibidos menos egresos pagados, sin corrección monetaria; el activo fijo pagado se rebaja de una vez | Sí, tasa rebajada |
| Pro Pyme Transparente (art. 14 D N° 8) | Percibida | **No**: la base se asigna a los dueños según su participación, con los PPM |
| Renta presunta (art. 34) | Presumida por actividad | **El sistema no la determina**; prepara los demás antecedentes |

### 8.4 Tasas del impuesto de primera categoría
| Año comercial | Régimen General 14 A | Pro Pyme General |
|---|---|---|
| 2025 | 27 % | 12,5 % |
| 2026 | 27 % | 12,5 % |
| 2027 | 25,5 % | 12,5 % |
| 2028 | 24 % | 15 % |
| 2029 en adelante | 23 % | 23 % |

- Pro Pyme Transparente: 0 % en la empresa.
- Fuentes citadas en el sistema: art. 20 LIR, Ley 21.850 (art. sexto transitorio) y Ley 21.755.
- Las tasas 2026 y 2027 del régimen general **no se aplican a los contribuyentes del art. 14 letra G)**.
- La rebaja Pro Pyme está condicionada a la cotización de la Ley 21.735. La Circular 53 la da por cumplida hasta el año comercial 2028.
- **Gasto rechazado (art. 21 inc. 1° LIR):** impuesto único del 40 %.
- **Cuándo la celda C36 queda vacía:** con Renta Presunta, un régimen que el sistema no reconoce, un año sin tasa o un ejercicio que no empieza en enero. El sistema no inventa una tasa; resuélvelo con el contador.

### 8.5 Renta anual (F22) y corrección monetaria
- El **F29** es mensual: IVA, PPM y retenciones. El **F22** es anual: impuesto a la renta del año comercial. Los PPM del F29 son crédito del F22.
- **Factores de actualización** (Circular SII N° 5, enero de 2026): cargados para el **año tributario 2026** (año comercial 2025), con capital propio inicial del 3,4 %. Los del año tributario 2027 los publica el SII en enero de 2027: **no los supongas**.
- **Créditos que el módulo reconoce:**
  - Donaciones con crédito.
  - Contribuciones.
  - Art. 33 bis (activo inmovilizado).
  - Donaciones a universidades.
  - Impuestos en el extranjero (art. 41 A).
  - I+D (Ley 20.241).
  - SENCE (Ley 19.518).
- **Declaraciones juradas de apoyo:**

  | DJ | Contenido | Aplica a |
  |---|---|---|
  | 1887 | Sueldos y retenciones del impuesto único | Con remuneraciones; el sistema arma una planilla CSV de apoyo |
  | 1948 | Retiros y dividendos | 14 A y 14 D N° 3 |
  | 1947 | Rentas del régimen transparente | 14 D N° 8 |
  | 1926 | Base imponible y datos del balance | 14 A |

  Los vencimientos los muestra el propio módulo.

### 8.6 Retención de boletas de honorarios
| Año de emisión | 2024 | 2025 | 2026 | 2027 | 2028 |
|---|---|---|---|---|---|
| Tasa | 13,75 % | 14,5 % | 15,25 % | 16 % | 17 % |

- Base legal: Ley 21.133, art. 5° transitorio.
- El sistema usa esta tabla solo para avisar: **manda lo que trae la boleta**.
- Si la boleta no trae retención, confirma que el emisor eligió pagarla él mismo.
- La retención se declara en el F29 del mes en que se **paga** la boleta (art. 79 LIR).
