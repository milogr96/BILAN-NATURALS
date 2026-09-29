\# BILAN NATURALS – Análisis de Clientes y Predicción de Recompra



\*\*Español\*\* | \[English below](#english)



\## Descripción General



Este proyecto fue desarrollado para una empresa de fabricación y venta de alimentos para mascotas. Usa datos históricos de ventas para apoyar decisiones comerciales mediante segmentación de clientes, identificación de clientes inactivos y estimación de probabilidad de recompra.



Se incluyen dos cuadernos Jupyter que implementan los análisis clave:



\- \*\*`Recuperar\_Clientes.ipynb`\*\* – identifica clientes que no han comprado en los últimos 25–366 días, generando un listado para campañas de recuperación.

\- \*\*`Prediccion\_Clientes\_prox\_a\_comprar.ipynb`\*\* – calcula un score dinámico de recompra (basado en frecuencia histórica, recencia y valor promedio de compra) y estima qué clientes están más próximos a realizar una nueva compra.



Ambos cuadernos están diseñados para ejecutarse en Google Colab (o localmente) y producen archivos Excel listos para uso directo del equipo comercial.



\## Contexto y estado actual del proyecto



Este proyecto nació para reemplazar una macro de Excel que la empresa usaba para este mismo análisis y que dejó de funcionar. La lógica de esa macro fue migrada a Python, y de paso se amplió: se agregó un score de recompra ponderado por frecuencia, variabilidad de gasto y valor esperado, algo que la macro original no calculaba.



Posteriormente, la macro de Excel fue reparada y la empresa retomó su uso por continuidad operativa. Este repositorio queda entonces como una solución funcional y validada, documentada como caso de estudio y lista para retomarse si se necesita escalar el análisis (por ejemplo, si la macro vuelve a fallar o si se requiere algo más robusto que Excel).



> \*\*Nota de honestidad técnica:\*\* el "score de recompra" actual es un modelo basado en reglas estadísticas (media y desviación estándar de frecuencia de compra), no un modelo de machine learning entrenado. Es un enfoque válido y explicable, pero se documenta así para evitar expectativas incorrectas.



\## Cómo Ejecutar los Cuadernos



1\. Sube el archivo Excel de ventas a tu Google Drive.

2\. Abre el cuaderno en Google Colab.

3\. Monta tu Drive y actualiza la ruta del archivo (`archivo = "..."`) si es necesario.

4\. Ejecuta todas las celdas – el cuaderno generará y descargará automáticamente el archivo Excel de salida.



\## Explicación detallada de cada Notebook



\### `Recuperar\_Clientes.ipynb`



Identifica clientes inactivos para campañas de recuperación.



1\. \*\*Carga de datos\*\*: monta Google Drive y lee la hoja `Reporte Ventas` del archivo Excel de ventas histórico.

2\. \*\*Limpieza\*\*: normaliza nombres de columnas y convierte la columna `fecha` a formato de fecha, descartando filas sin fecha o sin cliente válido.

3\. \*\*Última compra por cliente\*\*: agrupa por `cliente` y obtiene la fecha máxima de compra (`ultima\_fecha\_compra`).

4\. \*\*Cálculo de inactividad\*\*: calcula `delta\_dias` = días transcurridos entre la fecha actual y la última compra de cada cliente.

5\. \*\*Filtro de recuperación\*\*: selecciona únicamente los clientes con `delta\_dias` entre 25 y 366 días (ni tan recientes que no necesiten campaña, ni tan antiguos que se consideren perdidos).

6\. \*\*Exportación\*\*: genera un Excel con nombre dinámico (incluye el rango de fechas evaluado) y lo descarga automáticamente.

7\. \*\*Función auxiliar `es\_ultimo\_dia\_habil()`\*\*: valida si la fecha de ejecución es el último día hábil del mes, útil si se quiere diferenciar una corrida mensual de una diaria (actualmente solo informativa, no cambia la lógica de filtrado).



\*\*Output\*\*: `Clientes 25-365 dias sin comprar \[rango de fechas].xlsx`



\### `Prediccion\_Clientes\_prox\_a\_comprar.ipynb`



Calcula un score de priorización combinando \*cuándo\* es probable que un cliente recompre y \*cuánto\* vale esa recompra.



1\. \*\*Carga y limpieza\*\*: lee la misma hoja `Reporte Ventas`, convierte `fecha` y `total` a los tipos correctos, y descarta filas incompletas.

2\. \*\*Consolidación de compras\*\*: agrupa por `cliente` + `fecha` para tratar cada combinación como una transacción única, sumando el total gastado, contando ítems y familias de producto distintas.

3\. \*\*Frecuencia real de compra\*\*: calcula, por cliente, el promedio y la desviación estándar de los días transcurridos entre compras consecutivas (`frecuencia\_promedio`, `frecuencia\_std`).

4\. \*\*Clasificación por rangos\*\*: agrupa a los clientes en buckets de frecuencia (1-30 días, 31-60, 61-90, etc.) para segmentación descriptiva.

5\. \*\*Estimación de próxima compra\*\*: proyecta `prox\_compra\_calculada` sumando la frecuencia promedio (con un ajuste de -3 días) a la última fecha de compra.

6\. \*\*Score dinámico de recompra\*\*: `score\_recompra` = días desde la última compra ÷ frecuencia promedio del cliente. Un valor cercano a 1 indica que el cliente está "a tiempo" de comprar según su propio patrón histórico.

7\. \*\*Features de valor\*\*: calcula gasto promedio, desviación del gasto, cantidad promedio de ítems y familia de producto más comprada por cliente.

8\. \*\*Variación de gasto\*\*: `variacion\_gasto` = desviación estándar del gasto ÷ gasto promedio — mide qué tan predecible es el comportamiento de compra del cliente.

9\. \*\*Probabilidad de recompra\*\*: ajusta el `score\_recompra` penalizando a clientes con gasto muy variable (menos predecibles), y lo acota entre 0 y 1 (`prob\_recompra`).

10\. \*\*Valor esperado\*\*: `valor\_estimado` = gasto promedio ajustado por la variabilidad del cliente.

11\. \*\*Score final\*\*: `score\_final` = `prob\_recompra` × `valor\_estimado` — prioriza clientes que combinan alta probabilidad de recompra \*\*y\*\* alto valor económico esperado, no solo uno de los dos factores.

12\. \*\*Filtro final\*\*: selecciona clientes con `prob\_recompra` ≥ 0.35 y `score\_final` por encima de la mediana, ordenados por impacto económico.

13\. \*\*Exportación\*\*: genera un Excel (`CLIENTES PROX A COMPRAR \[fecha].xlsx`) con la lista final priorizada.



\*\*Output\*\*: `CLIENTES PROX A COMPRAR \[fecha de ejecución].xlsx`



\## Metodología (resumen)



\- Se consolidan las compras por cliente y fecha.

\- Se calcula la frecuencia promedio de compra por cliente (media y desviación estándar entre compras).

\- Se estima la próxima fecha de compra esperada y un score de urgencia (`score\_recompra`).

\- Se combina con el valor histórico de compra para priorizar clientes por impacto económico esperado (`score\_final`).



\## Limitaciones conocidas



\- El score no ha sido validado aún con backtesting formal (comparar predicciones contra compras reales posteriores).

\- Sensible a calidad de datos: nombres de cliente inconsistentes (mayúsculas, espacios, duplicados) pueden fragmentar el historial de un mismo cliente.

\- Rutas de archivo y nombre de hoja están hardcodeados; requiere ajuste manual si cambia la estructura del Excel fuente.



\## Tecnologías Utilizadas



\- Python (pandas, numpy, datetime)

\- Google Colab / Jupyter Notebook

\- xlsxwriter (exportación a Excel)

\- Git / GitHub



\## Próximos pasos (roadmap)



\- \[ ] Backtesting histórico para validar precisión del score.

\- \[ ] Migrar de notebook a script parametrizado (`.py` + config).

\- \[ ] Visualizaciones de distribución de score y cobertura de clientes.



\---



<a name="english"></a>

\## English



\## Project Overview



This project was developed for a pet food manufacturing and sales company. It uses historical sales data to support commercial decision-making through customer segmentation, identification of inactive customers, and repurchase probability estimation.



Two Jupyter notebooks implement the core analytics:



\- \*\*`Recuperar\_Clientes.ipynb`\*\* – identifies customers who haven't purchased in the last 25–366 days, generating a targeted list for recovery campaigns.

\- \*\*`Prediccion\_Clientes\_prox\_a\_comprar.ipynb`\*\* – builds a dynamic repurchase score (based on historical frequency, recency, and average purchase value) and estimates which customers are most likely to buy soon.



Both notebooks are designed to run in Google Colab (or locally) and produce Excel files ready for direct use by commercial teams.



\## Background \& Current Status



This project was originally built to replace an Excel macro the company used for this same analysis, which had stopped working. The macro's logic was migrated to Python and extended along the way: a repurchase score weighted by frequency, spending variability, and expected value was added — something the original macro didn't compute.



The Excel macro was later fixed, and the company resumed using it for operational continuity. This repository remains a functional, documented solution and case study, ready to be picked back up if the analysis needs to scale (e.g., if the macro fails again, or something more robust than Excel is required).



> \*\*Technical honesty note:\*\* the current "repurchase score" is a rules-based statistical model (mean and standard deviation of purchase frequency), not a trained machine learning model. It's a valid, explainable approach, documented as such to avoid overstating it.



\## How to Run the Notebooks



1\. Upload the sales Excel file to your Google Drive.

2\. Open the notebook in Google Colab.

3\. Mount your Drive and update the file path (`archivo = "..."`) if necessary.

4\. Run all cells – the notebook will generate and download the output Excel file automatically.



\## Methodology (summary)



\- Purchases are consolidated by customer and date.

\- Average purchase frequency per customer is computed (mean and standard deviation between purchases).

\- The expected next purchase date and an urgency score (`score\_recompra`) are estimated.

\- This is combined with historical purchase value to prioritize customers by expected economic impact (`score\_final`).



\## Known Limitations



\- The score hasn't yet been validated with formal backtesting (comparing predictions against actual subsequent purchases).

\- Sensitive to data quality: inconsistent customer names (casing, whitespace, duplicates) can fragment a single customer's history.

\- File paths and sheet names are hardcoded; manual adjustment is needed if the source Excel structure changes.



\## Technologies Used



\- Python (pandas, numpy, datetime)

\- Google Colab / Jupyter Notebook

\- Git / GitHub



\## Roadmap



\- \[ ] Historical backtesting to validate score accuracy.

\- \[ ] Migrate from notebook to a parameterized `.py` script + config.

\- \[ ] Score distribution and customer coverage visualizations.

