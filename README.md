
# Español- Spanish
# BILAN NATURALS – Análisis de Clientes y Predicción de Recompra

## Descripción General
Este proyecto fue desarrollado para una empresa de fabricación y venta de alimentos para mascotas. Utiliza datos históricos de ventas para apoyar la toma de decisiones comerciales mediante segmentación de clientes, identificación de inactivos y predicción de probabilidad de recompra. Se incluyen dos cuadernos Jupyter que implementan los análisis clave:

- **`Recuperar_Clientes.ipynb`** – identifica clientes que no han comprado en los últimos 25–366 días, generando un listado para campañas de recuperación.
- **`Prediccion_Clientes_prox_a_comprar.ipynb`** – calcula un score dinámico de recompra y estima qué clientes están más próximos a realizar una nueva compra, basado en su frecuencia y antigüedad.

Ambos cuadernos están diseñados para ejecutarse en Google Colab (o de forma local) y producen archivos Excel que pueden ser utilizados directamente por equipos comerciales.

## Cómo Ejecutar los Cuadernos

1. Sube el archivo Excel de ventas a tu Google Drive.
2. Abre el cuaderno en Google Colab.
3. Monta tu Drive y actualiza la ruta del archivo si es necesario.
4. Ejecuta todas las celdas – el cuaderno generará y descargará automáticamente el archivo Excel.


## Tecnologías Utilizadas
- Python (pandas, numpy, datetime)
- Google Colab / Jupyter Notebook
- xlsxwriter (para exportar a Excel)
- Git / GitHub

## -----------------------------------------------------------------------------------------

# Ingles - English

# BILAN NATURALS – Customer Analytics & Repurchase Prediction

## Project Overview
This project was developed for a pet food manufacturing and sales company. It uses historical sales data to support commercial decision‑making through customer segmentation, identification of inactive clients, and prediction of repurchase probability. Two Jupyter notebooks implement the core analytics:

- **`Recuperar_Clientes.ipynb`** – identifies customers who have not purchased in the last 25–366 days, generating a targeted list for recovery campaigns.
- **`Prediccion_Clientes_prox_a_comprar.ipynb`** – builds a dynamic repurchase score and estimates which customers are most likely to buy soon, based on their purchase frequency and recency.

Both notebooks are designed to be run in Google Colab (or locally) and produce Excel files that can be directly used by commercial teams.

## How to Run the Notebooks

1. Upload the sales Excel file to your Google Drive.
2. Open the notebook in Google Colab.
3. Mount your Drive and update the file path if necessary.
4. Run all cells – the notebook will generate and download the Excel output automatically.


## Technologies Used
- Python (pandas, numpy, datetime, scikit-learn)
- Google Colab / Jupyter Notebook
- Git / GitHub
