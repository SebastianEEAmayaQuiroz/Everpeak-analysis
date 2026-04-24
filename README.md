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

```bash
# Clonar el repositorio
git clone https://github.com/SebastianEEAmayaQuiroz/everpeak-analysis.git

# Instalar dependencias
pip install pandas numpy matplotlib seaborn

# Abrir Jupyter
jupyter notebook Notebooks/everpeak_analysis.ipynb
