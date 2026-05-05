# Descripción detallada de los datasets

Este documento describe la estructura, las columnas y el contexto de cada uno de los siete datasets analizados en este repositorio. Todos los datos se encuentran **pseudonimizados**, es decir, los identificadores naturales han sido reemplazados por códigos sintéticos no reversibles del tipo `AFI_xxxxxxxx` (afiliados) y `EMP_xxxxxxxx` (empleadores).

---

## Convenciones generales

| Elemento | Significado |
|----------|------------|
| `CLP` | Pesos chilenos. |
| `UF` | Unidad de Fomento (unidad reajustable según IPC, usada como denominador estable). |
| `AFI_xxxxxxxx` | Identificador pseudonimizado de afiliado (8 dígitos). |
| `EMP_xxxxxxxx` | Identificador pseudonimizado de empleador (8 dígitos). |
| `PERIODO` | Entero de 6 dígitos en formato `YYYYMM`. |
| `Fecha_*` | Fecha en formato `YYYY-MM-DD` o entero `YYYYMMDD` según el dataset. |

---

## 1. `p18.src_cliente_diario` (pseudonimizado)

**Notebook:** `EDA_cliente_diario.ipynb`
**Volumen:** 304.611 registros × 8 columnas
**Granularidad:** un registro por afiliado.

| Columna | Tipo | Descripción |
|---------|------|-------------|
| `AfiFechaNac` | `datetime` | Fecha de nacimiento del afiliado. |
| `AfiTipo` | `str` | Tipo de afiliado (en este dataset, único valor "P"). |
| `AfiRenta` | `float` | Renta declarada del afiliado en CLP (44,6% nulos). |
| `AfiFechaAfiliacion` | `datetime` | Fecha en que el afiliado se incorporó al sistema. |
| `AfiFechaIniBenef` | `datetime` | Fecha de inicio de beneficio. |
| `Estado` | `float` | Código numérico del estado actual del afiliado. |
| `ID_EMP` | `str` | Empleador del afiliado pseudonimizado (puede ser nulo). |
| `ID_AFI` | `str` | Identificador único del afiliado pseudonimizado (clave). |

---

## 2. `p18.src_ctacorriente_diario` (pseudonimizado)

**Notebook:** `EDA_p18_ctacorriente_diario.ipynb`
**Granularidad:** un registro por cuenta corriente.

| Columna | Tipo | Descripción |
|---------|------|-------------|
| `IdCtaCte` | `int` | Identificador de la cuenta corriente. |
| `Saldo` | `float` | Saldo monetario de la cuenta. |
| `FechaIncorporacion` | `datetime` | Fecha de incorporación de la cuenta al sistema. |
| `FechaCesacion` | `datetime` | Fecha de cesación (`NaT` si la cuenta sigue activa). |
| `FechaFacturacion` | `datetime` | Última fecha de facturación. |
| `Estado` | `int/str` | Estado de la cuenta (activa/cesada/etc.). |
| `ID_AFI` | `str` | Afiliado titular pseudonimizado. |

---

## 3. `p18.src_transaccion_diario`

**Notebook:** `EDA_transaccion_diario.ipynb`
**Granularidad:** un registro por movimiento.

Estructura típica de un sistema transaccional con cargos, abonos, conceptos asociados y saldos resultantes. El notebook documenta la estructura completa al cargar el dataset.

---

## 4. `bnf.src_reembolso_medico_diario` (pseudonimizado, desde 2022)

**Notebook:** `EDA_reembolso_medico.ipynb`
**Volumen:** 928.971 registros × 30 columnas
**Granularidad:** un registro por línea de bono.

| Columna | Tipo | Descripción |
|---------|------|-------------|
| `PERIODO` | `int` | Período `YYYYMM`. |
| `FOLIO_REEMBOLSO` | `int` | Folio que agrupa una solicitud de reembolso. |
| `FOLIO_BONO` | `int` | Folio del bono médico. |
| `FECHA_BONO` | `datetime` | Fecha del bono. |
| `NOMBRE_PRESTADOR` | `str` | Nombre del prestador médico. |
| `ID_TIPO_AFILIADO` / `DSC_TIPO_AFILIADO` | `int` / `str` | Tipo de afiliado (Activo, Pensionado, etc.). |
| `ID_AGENCIA_USUARIO` / `DSC_AGENCIA_USUARIO` | `int` / `str` | Agencia que tramitó. |
| `CUENTA_USUARIO` | `str` | Usuario operacional que tramitó el bono. |
| `FOLIO_CAJA` | `uint64` | Folio del comprobante de caja. |
| `ID_ESTADO_PAGO` / `DSC_ESTADO_PAGO` | `int` / `str` | Estado de pago (Ingresada, Cancelado, etc.). |
| `ID_ESTADO_CAJA` / `DSC_ESTADO_CAJA` | `int` / `str` | Estado en caja. |
| `FECHA_MOVIMIENTO` | `datetime` | Timestamp del movimiento. |
| `TOTAL_BONIFICADO_PESOS` / `_UF` | `int` / `float` | Total bonificado. |
| `ESP_G1`, `ESP_G2`, `ESP_G3` | `int` | Códigos jerárquicos de especialidad/prestación. |
| `ESP_DESCRIPCION` | `str` | Descripción textual de la prestación. |
| `MONTO_BONIFICADO_PESOS` / `_UF` | `int` / `float` | Monto bonificado por la línea. |
| `COPAGO_REEMBOLSO` | `int` | Copago calculado para el reembolso. |
| `COPAGO_REAL` | `int` | Copago efectivo del afiliado. |
| `ID_PREVISION` / `DSC_PREVISION` | `int` / `str` | Sistema previsional (Fonasa, Isapre, FF.AA., etc.). |
| `ID_EMP`, `ID_AFI` | `str` | Empleador y afiliado pseudonimizados. |

---

## 5. `bnf.src_venta_ticket_mensual` (pseudonimizado)

**Notebook:** `EDA_venta_ticket_mensual.ipynb`
**Volumen:** 171.933 registros × 8 columnas
**Granularidad:** un registro por unidad vendida.

| Columna | Tipo | Descripción |
|---------|------|-------------|
| `PERIODO` | `int` | Período `YYYYMM`. |
| `TOTAL` | `int` | Monto del ticket en CLP. |
| `TIPO_CARTERA` | `int` | Código numérico de la cartera. |
| `NTIPO_CARTERA` | `str` | Nombre de la cartera (Cineplanet, Buin Zoo, Fantasilandia, Gift Cards, etc.). |
| `FEC_TRANSAC` | `datetime` | Fecha de la transacción (`YYYYMMDD`). |
| `FECHA_PAGO` | `datetime` | Fecha de pago. |
| `ID_AFI` | `str` | Afiliado pseudonimizado. |

---

## 6. `bnf.src_lm_10101_benef_mensual` (pseudonimizado, desde 2020)

**Notebook:** `EDA_benef_mensual_10101.ipynb`
**Volumen:** 246.330 registros × 7 columnas
**Granularidad:** un registro por entrega del beneficio `10101`.

| Columna | Tipo | Descripción |
|---------|------|-------------|
| `Periodo` | `int` | Período `YYYYMM`. |
| `Version` | `str` | Timestamp de la versión de carga (`DD/MM/YYYY HH:MM`). |
| `Tipo_afiliado` | `float` | Código numérico del tipo de afiliado. |
| `Tipo_Beneficio` | `int` | Sub-tipología dentro del beneficio 10101 (mayoritariamente 8). |
| `Monto_Beneficio` | `int` | Monto entregado en CLP. |
| `Fecha_Otorg_Beneficio` | `int` | Fecha de otorgamiento (`YYYYMMDD`). |
| `ID_AFI` | `str` | Afiliado pseudonimizado. |

---

## 7. `pen.src_vigente_stock_mensual` (pseudonimizado, desde 2022)

**Notebook:** `EDA_vigente_stock_mensual.ipynb`
**Granularidad:** un registro por pensionado vigente y mes.

Captura el estado mensual del padrón de pensionados activos, con variables demográficas, tipo de pensión, monto y cobertura geográfica. La estructura completa se documenta en la primera ejecución del notebook (sección "Vista General").

---

## Notas sobre calidad de datos

- **Tasa de nulidad global típica:** 0,0001% en BNF, 14,2% en P18-cliente (concentrada en `ID_EMP` y `Estado`).
- **Duplicados:** los datasets transaccionales (BNF reembolso, ventas) presentan duplicados intencionales por línea de bono o ticket; los de padrón (P18-cliente) son completamente únicos por `ID_AFI`.
- **Outliers:** las distribuciones de monto suelen presentar skewness extremo (>60), por lo que los notebooks aplican transformaciones logarítmicas (`log1p`) y boxplots con `showfliers=False` para análisis más legibles.
- **Inconsistencias temporales:** se detectan algunos registros con fechas anómalas (afiliaciones con fecha futura, beneficios anteriores a la afiliación). Cada notebook reporta estos casos en su sección de duplicados/anomalías.
