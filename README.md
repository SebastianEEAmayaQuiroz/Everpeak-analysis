# Everpeak-analysis
Análisis completo de datos EverPeak Retail - Limpieza, EDA, detección de outliers y segmentación de clientes
#
# EverPeak Retail Analysis – 

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/SebastianEEAmayaQuiroz/everpeak-analysis/blob/main/notebooks/everpeak_analysis.ipynb)

## 📊 Descripción del Proyecto

Este repositorio contiene el análisis completo de datos del caso **EverPeak–SilverBasket**, realizado durante el Sprint 6 del bootcamp.

El dataset `everpeak_retail` simula datos reales de retail con:
- 2,000 órdenes de clientes
- Valores faltantes (missing data)
- Sentinels (valores centinela como -999, 999)
- Outliers y problemas de calidad

## 🎯 Objetivos del Análisis

1. **Limpiar y preparar** los datos para análisis
2. **Detectar patrones** de missingness (MCAR, MAR, MNAR)
3. **Identificar outliers** con métodos IQR y Z-score
4. **Segmentar clientes** por comportamiento y características
5. **Generar insights** accionables para el equipo de negocio

## 📂 Estructura del Repositorio

everpeak-analysis/

└── Notebooks/ everpeak_analysis.ipynb

└── Data/ everpeak_clean.csv

└── Scripts/ pipeline_clean.py

└── Images/ (gráficos generados)

└── README.md


## 🚀 Cómo ejecutar el análisis

### Opción 1: Google Colab (Recomendado)

1. Haz clic en el badge de arriba: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)]
2. Ejecuta las celdas en orden
3. El notebook cargará automáticamente el dataset

### Opción 2: Local (Jupyter Notebook)

# Clonar el repositorio
git clone https://github.com/SebastianEEAmayaQuiroz/everpeak-analysis.git

# Instalar dependencias
pip install pandas numpy matplotlib seaborn

# Abrir Jupyter
jupyter notebook Notebooks/everpeak_analysis.ipynb

## 📈 Principales Hallazgos

### Limpieza de Datos

| Acción | Detalle |
|--------|---------|
| **Sentinels eliminados** | -999, 999, 0, -1 convertidos a NaN |
| **Columnas numéricas** | customer_age, price, quantity, order_value |
| **Método de imputación** | Mediana para customer_age y price |
| **Columnas de texto limpiadas** | product_category, city, state (strip) |

### Detección de Outliers (order_value)

| Método | Límite Inferior | Límite Superior | Criterio |
|--------|----------------|-----------------|----------|
| **IQR** | Q1 - 1.5 × IQR | Q3 + 1.5 × IQR | Valores fuera de [Q1-1.5×IQR, Q3+1.5×IQR] |
| **Z-score** | media - 3 × std | media + 3 × std | \|z\| > 3 |

### Segmentación de Clientes

| Segmento | Condición | Descripción |
|----------|-----------|-------------|
| **High Volume** | quantity > 22 | Clientes que compran más de 22 unidades |
| **Low Volume** | quantity ≤ 22 | Clientes que compran 22 unidades o menos |
| **Segmentación avanzada** | Edad + Volumen | Sr./Jr. High/Low Volume |
| **Segmentación por pago** | Método + Volumen | card/no_card high/low volume |

---

## 🛠 Tecnologías Utilizadas

| Herramienta | Versión | Propósito |
|-------------|---------|-----------|
| **Python** | 3.9+ | Lenguaje principal |
| **Pandas** | 1.5+ | Manipulación y limpieza de datos |
| **NumPy** | 1.24+ | Operaciones numéricas y arrays |
| **Matplotlib** | 3.7+ | Visualizaciones base |
| **Seaborn** | 0.12+ | Gráficos estadísticos avanzados |
| **Google Colab** | - | Entorno de ejecución en la nube |

---

## 📝 Funciones Clave del Pipeline

```python
def reemplazar_sentinels(df, sentinels, numeric_cols):
    """Reemplaza valores centinela (-999, 999, 0, -1) por NaN"""
    for col in numeric_cols:
        df[col] = df[col].replace(sentinels, pd.NA)
    return df

def convertir_columnas_numericas(df, columnas):
    """Convierte columnas a tipo numérico, errores → NaN"""
    for col in columnas:
        df[col] = pd.to_numeric(df[col], errors="coerce")
    return df

def rellenar_ausentes(df, cols_fill):
    """Convierte a numérico y rellena NaN con la media"""
    for col in cols_fill:
        df[col] = pd.to_numeric(df[col], errors='coerce')
        df[col].fillna(df[col].mean(), inplace=True)
    return df

def step_strip_text(df):
    """Elimina espacios en blanco en columnas de texto"""
    columnas = ["product_category", "city", "state"]
    for col in columnas:
        df[col] = df[col].str.strip()
    return df

def limpiar_df(df):
    """Pipeline principal que orquesta toda la limpieza"""
    valores_erroneos = [-999, 999, 0, -1]
    columnas_numericas = ["customer_age", "price", "quantity", "order_value"]
    
    df = reemplazar_sentinels(df, valores_erroneos, columnas_numericas)
    df = convertir_columnas_numericas(df, columnas_numericas)
    df = rellenar_ausentes(df, ["customer_age", "price"])
    df = step_strip_text(df)
    
    return df
