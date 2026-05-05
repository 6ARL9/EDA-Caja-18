# Análisis Exploratorio de Datos — Sector Previsional y Salud

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458.svg)](https://pandas.pydata.org/)
[![Status](https://img.shields.io/badge/Status-Activo-success.svg)]()

Repositorio de **siete análisis exploratorios de datos (EDA)** sobre conjuntos de información pseudonimizados del sector previsional, de beneficios y de salud. Cada notebook constituye un estudio independiente, autocontenido y reproducible, que aplica una metodología homogénea de exploración estadística, visualización y detección de anomalías.

---

## Tabla de Contenidos

1. [Resumen del proyecto](#resumen-del-proyecto)
2. [Objetivo](#objetivo)
3. [Estructura del repositorio](#estructura-del-repositorio)
4. [Notebooks incluidos](#notebooks-incluidos)
5. [Metodología común](#metodología-común)
6. [Tecnologías utilizadas](#tecnologías-utilizadas)
7. [Instalación y uso](#instalación-y-uso)
8. [Fuente de los datos](#fuente-de-los-datos)
9. [Privacidad y ética](#privacidad-y-ética)
10. [Hallazgos representativos](#hallazgos-representativos)
11. [Licencia](#licencia)
12. [Autor](#autor)

---

## Resumen del proyecto

Este repositorio reúne siete cuadernos Jupyter (`.ipynb`) destinados al análisis exploratorio de datasets reales pseudonimizados, organizados en tres subsistemas operativos:

- **P18** — Información transaccional y de padrón de afiliados, cuentas corrientes y operaciones diarias.
- **BNF** — Beneficios mensuales, reembolsos médicos y ventas de tickets de bienestar (carteras de entretenimiento).
- **PEN** — Stock vigente de pensionados, perfiles demográficos y montos de pensión.

Los volúmenes oscilan entre **170 mil y casi 1 millón de registros por dataset**, abarcando ventanas temporales que van desde 2020 hasta 2026. Cada notebook entrega: estadísticas descriptivas completas, análisis de calidad de datos, distribución de variables numéricas y categóricas, evolución temporal, correlaciones, detección de outliers con método IQR, análisis de duplicados y un resumen ejecutivo con hallazgos clave.

## Objetivo

Aplicar una **plantilla EDA reproducible y rigurosa** que permita:

- Caracterizar el comportamiento estadístico de cada dataset.
- Identificar patrones, anomalías y relaciones entre variables.
- Evaluar la calidad de los datos (valores nulos, duplicados, outliers, inconsistencias temporales).
- Generar visualizaciones publicables para soporte de decisiones de negocio.
- Servir como **base sólida para futuros modelos predictivos, dashboards y procesos de ingeniería de características**.

## Estructura del repositorio

```
EDA-Caja-18/
├── EDA_benef_mensual_10101.ipynb       # Beneficios mensuales BNF código 10101
├── EDA_cliente_diario.ipynb            # Padrón de afiliados P18
├── EDA_p18_ctacorriente_diario.ipynb   # Cuentas corrientes diarias P18
├── EDA_reembolso_medico.ipynb          # Reembolsos médicos BNF
├── EDA_transaccion_diario.ipynb        # Transacciones diarias P18
├── EDA_venta_ticket_mensual.ipynb      # Venta de tickets de bienestar BNF
├── EDA_vigente_stock_mensual.ipynb     # Stock vigente de pensionados PEN
├── data/                               # Carpeta sugerida para los CSV (no versionada)
│   └── .gitkeep
├── docs/
│   └── descripcion_datasets.md         # Descripción detallada de cada dataset
├── requirements.txt                    # Dependencias del proyecto
├── .gitignore                          # Exclusiones de Git
├── LICENSE                             # Licencia MIT
└── README.md                           # Este archivo
```

## Notebooks incluidos

### 1. `EDA_cliente_diario.ipynb`

**Dataset:** `p18.src_cliente_diario` (pseudonimizado) — **304.611 registros × 8 columnas**.

Estudio del padrón completo de afiliados del sistema P18. Incluye análisis de la composición demográfica (edades, antigüedad de afiliación), distribuciones de renta (con detección de skewness extremo), cobertura por empleador, estados del afiliado, fechas de inicio de beneficios y validación de consistencia cruzada entre fechas. Hallazgos: el padrón concentra una población mayoritariamente sénior (mediana de edad ≈ 74 años), con renta mediana ≈ 225.000 CLP y antigüedad mediana ≈ 6,4 años.

### 2. `EDA_p18_ctacorriente_diario.ipynb`

**Dataset:** `p18.src_ctacorriente_diario` (pseudonimizado).

Análisis de las cuentas corrientes diarias del sistema P18. Cubre la dinámica de saldos, la distinción entre cuentas activas y cesadas, fechas de incorporación, cesación y facturación, así como detección de anomalías y relaciones cruzadas entre estado y saldo. Pensado como punto de partida para entender el ciclo de vida de las cuentas.

### 3. `EDA_transaccion_diario.ipynb`

**Dataset:** `p18.src_transaccion_diario`.

Exploración de las transacciones diarias del sistema P18, identificando patrones de cargos, abonos y saldos, distribución temporal del flujo, tipos de concepto y detección de movimientos anómalos. Útil como base para detección de fraude o reglas de validación operativa.

### 4. `EDA_reembolso_medico.ipynb`

**Dataset:** `bnf.src_reembolso_medico_diario` (pseudonimizado, desde 2022) — **928.971 registros × 30 columnas**.

Análisis exhaustivo de los reembolsos médicos del subsistema BNF. Contempla 30 variables, incluyendo prestadores, especialidades médicas, montos en pesos y UF, copagos, agencias usuarias y previsión (Fonasa, Isapres, FF.AA.). Calcula la tasa de bonificación (porcentaje del costo cubierto), identifica los principales prestadores y especialidades, y modela el lag de procesamiento entre fecha de bono y fecha de movimiento. Total bonificado en el período: **~25.400 millones CLP**.

### 5. `EDA_venta_ticket_mensual.ipynb`

**Dataset:** `bnf.src_venta_ticket_mensual` (pseudonimizado) — **171.933 registros × 8 columnas**.

Análisis de las ventas mensuales de tickets de bienestar (carteras como Cineplanet, Fantasilandia, Buin Zoo, Gift Cards, etc.). Incluye comportamiento de consumo por cartera, evolución temporal de la recaudación, segmentación de afiliados por nivel de actividad, lag entre transacción y pago, y análisis de duplicados intencionales (compras múltiples). Recaudación acumulada: **~795 millones CLP**.

### 6. `EDA_benef_mensual_10101.ipynb`

**Dataset:** `bnf.src_lm_10101_benef_mensual` (pseudonimizado, desde 2020) — **246.330 registros × 7 columnas**.

Estudio del beneficio mensual BNF código `10101`. Incluye análisis temporal (43 meses cubiertos), distribución del monto del beneficio por tipo de afiliado y tipo de beneficio, cruce bidimensional de las variables tipológicas, y un análisis de **concentración con curva de Lorenz y coeficiente de Gini** para medir desigualdad en la distribución del beneficio. Total entregado: **~5.250 millones CLP** a 85.459 afiliados únicos.

### 7. `EDA_vigente_stock_mensual.ipynb`

**Dataset:** `pen.src_vigente_stock_mensual` (pseudonimizado, desde 2022).

Análisis del stock vigente de pensionados del subsistema PEN. Caracteriza la composición demográfica (edad, género), distribución de tipos de pensión, evolución temporal del padrón activo, distribución de montos de pensión, cobertura geográfica y calidad estructural de los datos.

## Metodología común

Todos los notebooks comparten una **plantilla EDA estandarizada de 13 a 18 secciones**, lo que garantiza consistencia, comparabilidad entre estudios y reproducibilidad:

| Sección | Contenido |
|--------|-----------|
| 1. Importación de librerías | Configuración de pandas, matplotlib, seaborn y opciones de display. |
| 2. Carga del dataset | Lectura del CSV con tipado explícito y parseo de fechas. |
| 3. Vista general | Cabeceras, dimensiones, dtypes, clasificación columna a columna. |
| 4. Valores nulos | Conteo absoluto, porcentual y visualización con umbrales (5%, 20%, 50%). |
| 5. Estadísticas descriptivas | `describe`, asimetría (skewness), curtosis, ceros y negativos. |
| 6. Variables categóricas | Cardinalidad, moda, distribución de las categorías de baja y alta cardinalidad. |
| 7. Variables numéricas | Histogramas, boxplots, escala lineal y logarítmica (`log1p`), tramos. |
| 8. Análisis temporal | Cobertura, volumen mensual, heatmaps año × mes, lags y diferencias. |
| 9. Análisis cruzado | Combinaciones por empleador, agencia, tipo de afiliado, especialidad. |
| 10. Correlaciones | Matriz de correlación con máscara triangular y mapa de calor. |
| 11. Detección de outliers | Método del rango intercuartílico (IQR) por columna. |
| 12. Duplicados | Filas exactas y combinaciones clave de negocio. |
| 13. Resumen ejecutivo | Bloque final con métricas clave de volumen, calidad y negocio. |

## Tecnologías utilizadas

| Categoría | Librería | Uso |
|-----------|----------|-----|
| Lenguaje | **Python 3.10+** | Lenguaje principal del proyecto. |
| Manipulación de datos | **pandas** | Carga, transformación, agregación y análisis. |
| Cómputo numérico | **numpy** | Operaciones matemáticas, percentiles, transformaciones. |
| Visualización | **matplotlib** | Gráficos personalizados, formateo de ejes, anotaciones. |
| Visualización avanzada | **seaborn** | Heatmaps, paletas, estilos uniformes. |
| Notebook | **Jupyter** | Entorno de ejecución interactivo. |

## Instalación y uso

### Requisitos previos

- Python 3.10 o superior.
- Git (opcional, para clonar el repositorio).
- Acceso a los archivos CSV pseudonimizados (no incluidos en el repositorio).

### Pasos

```bash
# 1. Clonar el repositorio
git clone https://github.com/6ARL9/EDA-Caja-18.git
cd EDA-Caja-18

# 2. (Opcional pero recomendado) Crear un entorno virtual
python -m venv .venv
# Windows
.venv\Scripts\activate
# Linux / macOS
source .venv/bin/activate

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Colocar los archivos CSV pseudonimizados en la carpeta data/
#    (los notebooks esperan los CSV junto a sí mismos por defecto;
#    ajustar la variable FILE_PATH si se mueven a data/).

# 5. Lanzar Jupyter
jupyter notebook
```

Una vez abierto Jupyter, cada notebook puede ejecutarse de forma independiente con `Run All`. La ejecución completa de un notebook tarda entre 30 segundos y 3 minutos en función del tamaño del dataset.

## Fuente de los datos

Los datasets corresponden a información operacional del sector previsional y de salud, sometida a un proceso de **pseudonimización** que reemplaza los identificadores naturales (RUT, nombres, razones sociales) por códigos sintéticos del tipo `AFI_xxxxxxxx` (afiliados) y `EMP_xxxxxxxx` (empleadores). Por motivos de confidencialidad, los archivos CSV no se distribuyen en este repositorio público.

Si deseas ejecutar los notebooks con datos propios, basta con producir CSV con la estructura de columnas documentada en `docs/descripcion_datasets.md`.

## Privacidad y ética

Este proyecto adhiere estrictamente a buenas prácticas de tratamiento responsable de datos:

- **Pseudonimización previa:** todos los identificadores personales fueron reemplazados antes de cualquier análisis.
- **No reidentificación:** ningún notebook intenta reconstruir identidades a partir de combinaciones de variables.
- **Datos no versionados:** los CSV están explícitamente excluidos del control de versiones (`.gitignore`).
- **Análisis agregado:** los hallazgos publicados en el resumen ejecutivo son siempre estadísticas agregadas, no individuales.

## Hallazgos representativos

A modo ilustrativo, algunos resultados extraídos de los notebooks:

- **Distribución de renta P18:** asimetría extrema (skewness ≈ 68,8), con outliers que llegan a 75 millones CLP frente a una mediana de 225 mil.
- **Reembolsos médicos:** el 68,4% de los reembolsos pertenecen a Fonasa; la especialidad más recurrente es "Consulta Medicina General" con más de 100 mil registros.
- **Tickets de bienestar:** Cineplanet domina el volumen (12,3% del total) y los pagos se procesan el mismo día en el 99,9% de los casos.
- **Concentración de beneficios (10101):** el coeficiente de Gini calculado sobre el monto total por afiliado revela el grado de desigualdad en la entrega del beneficio.
- **Calidad de datos:** los datasets BNF muestran tasas de nulidad inferiores al 0,001%, mientras que el padrón P18 presenta nulidad concentrada en `ID_EMP` (71%) y `Estado` (58,7%), señalando campos opcionales o derivados.

## Licencia

Este proyecto está licenciado bajo la **Licencia MIT**. Consulta el archivo [LICENSE](LICENSE) para más detalles.

## Autor

**Alexis Rossel Leal**
GitHub: [@6ARL9](https://github.com/6ARL9)

Si te resultó útil este repositorio, considera dejar una estrella en GitHub. Para sugerencias, correcciones o colaboraciones, abre un *issue* o envía un *pull request*.

---

> *Repositorio orientado a portafolio profesional. Construido con metodología EDA reproducible, código comentado y visualizaciones publicables.*
