# INFORME DE CALIDAD DE DATOS

## RESUMEN EJECUTIVO

Los datasets de las plantas solares presentan problemas de completitud en los registros temporales, siendo más severos en la Planta 1 que en la Planta 2. Aunque todos los datasets cubren el mismo período temporal, existen tramos horarios faltantes que afectan la regularidad de las mediciones.

---

## ESTRUCTURA DE DATOS

### Datasets analizados
- **Planta1_Generacion.csv**: Datos de generación eléctrica de inversores
- **Planta2_Generacion.csv**: Datos de generación eléctrica de inversores  
- **Planta1_Sensores.csv**: Datos meteorológicos y ambientales
- **Planta2_Sensores.csv**: Datos meteorológicos y ambientales

### Período de cobertura
- **Fecha inicio**: 15/05/2020
- **Fecha fin**: 17/06/2020
- **Total días**: 34 días
- **Frecuencia esperada**: Mediciones cada 15 minutos (96 registros/día)

---

## HALLAZGOS PRINCIPALES

### ✅ FORTALEZAS

1. **Cobertura temporal consistente**
   - Todos los datasets cubren exactamente el mismo período
   - No faltan días intermedios en ningún dataset
   - Continuidad temporal completa de 34 días

2. **Integridad de identificadores**
   - IDs de planta consistentes en cada dataset
   - Sensor meteorológico único por planta correctamente identificado

### ⚠️ PROBLEMAS IDENTIFICADOS

#### 1. **Pérdida de tramos horarios**

**Planta 1 (Generación y Sensores)**:
- Días con problemas críticos: 20/05/2020, 21/05/2020, 29/05/2020
- Pérdida significativa de registros en estos días específicos
- Afecta tanto a datos de generación como de sensores

**Planta 2**:
- **Generación**: Período problemático del 20/05/2020 al 29/05/2020
- **Sensores**: Sin problemas aparentes de tramos faltantes

#### 2. **Irregularidad por inversor (Planta 2)**

- 4 inversores específicos muestran pérdida de datos superior al resto
- Sugiere posibles fallos específicos de equipos
- Requiere análisis individual por inversor

#### 3. **Potencia_dc_kw de la planta 1 con problemas de calidad**

- **Diagnóstico**: Posible corrimiento del dígito decimal
- **Corrección**: Se ha divido por 10 el campo potencia_dc_kw


---

## IMPACTO EN EL ANÁLISIS

### Limitaciones para el análisis
1. **Series temporales irregulares**: Complicará análisis de tendencias horarias
2. **Comparabilidad entre plantas**: Diferentes patrones de pérdida pueden sesgar comparaciones
3. **Análisis de rendimiento**: Datos faltantes pueden ocultar patrones de fallos reales

### Recomendaciones de tratamiento
1. **No regularizar automáticamente**: Los gaps pueden contener información sobre fallos
2. **Análisis por separado**: Tratar Planta 1 y Planta 2 con enfoques diferenciados
3. **Identificar causas raíz**: Investigar los días/equipos problemáticos específicos

---

## MÉTRICAS DE CALIDAD

| Dataset | Días Completos | Días Incompletos | % Completitud |
|---------|---------------|------------------|---------------|
| Planta1_Generacion | 31 | 3 | 91.2% |
| Planta2_Generacion | Variable por período | Variable | Requiere análisis detallado |
| Planta1_Sensores | 31 | 3 | 91.2% |
| Planta2_Sensores | 34 | 0 | 100% |

---

## SIGUIENTES PASOS

1. **Análisis de causa raíz**: Investigar qué causó las pérdidas en fechas específicas
2. **Mapeo de inversores problemáticos**: Identificar exactamente qué equipos fallan en Planta 2


---

## CONCLUSIÓN

Los datos presentan calidad suficiente para el análisis de detección de anomalías, pero requieren tratamiento cuidadoso de los tramos faltantes. La diferencia en patrones de pérdida entre plantas puede ser indicativa de los problemas operacionales que se busca identificar.
