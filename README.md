
# Español- Spanish
# BILAN NATURALS – Análisis de Clientes y Predicción de Recompra

## Descripción
Proyecto de análisis de datos para empresa de fabricacion y venta de alimentacion para mascotas,
con el objetivo de segmentar clientes, identificar inactivos y predecir probabilidad de recompra mediante Machine Learning.

## Tecnologías utilizadas
- Python (pandas, numpy, datetime, scikit-learn)
- Google Colab / Jupyter Notebook
- GitHub para control de versiones

## Estructura del proyecto
- `data/`: datos de muestra en formato CSV.
- `notebooks/scripts`: análisis exploratorio y desarrollo del modelo, ETL, entrenamiento y segmentación.
- `outputs/`: resultados generados (segmentaciones, métricas)

## Metodología
1. **Extracción y limpieza** de datos comerciales con pandas.
2. **Análisis exploratorio** para entender comportamiento de compra.
3. **Ingeniería de características** (frecuencia, antigüedad, ticket promedio).
4. **Entrenamiento de modelo de clasificación** (Random Forest) para predecir recompra.
5. **Segmentación de clientes** (activos, inactivos, alto potencial).



# Ingles - English

# BILAN NATURALS – Customer Analytics & Repurchase Prediction

## Description
Data analysis project for a commercial business, focused on customer segmentation, 
identification of inactive clients, and prediction of repurchase probability using Machine Learning. 
The project includes ETL processes, exploratory analysis, and automated reporting to support data-driven commercial strategies.

## Technologies Used
- Python (pandas, numpy, datetime, scikit-learn)
- Google Colab / Jupyter Notebook
- Git / GitHub

## Project Structure
- `data/`: Sample or synthetic data.
- notebooks - scripts: Jupyter notebooks with exploratory analysis and model development,for ETL, model training, and segmentation.
 
  - "Prediccion Clientes prox a compar.ipynb": 
  - "Recuperar_Clientes.ipynb": **Script to extract clients with 25–366 days without purchase** (used for recovery campaigns).
- `outputs/`: Results (segmented client lists, metrics, charts).
- `README.md`: Project overview.

## Methodology

### 1. ETL & Exploratory Data Analysis
- Loaded commercial data from Excel using pandas.
- Cleaned and normalized data (date format, missing values, column names).
- Performed exploratory analysis to understand purchase frequency, recency, and monetary value.

### 2. Customer Recovery Script (`Recuperar_Clientes.ipynb`)
- Calculates days since each client’s last purchase.
- Filters clients with delta between **25 and 366 days**.
- Exports a list of these clients to an Excel file named with the date range.
- Runs automatically; can be scheduled to generate lists for commercial teams.




