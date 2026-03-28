**Objetivo:**  
Identificar clientes con alta probabilidad de realizar una nueva compra en el corto plazo, basado en su comportamiento histórico.

**Metodología:**
- Consolida compras por cliente y fecha (una compra puede incluir varias líneas de productos).
- Calcula la frecuencia promedio de compra (en días) y su desviación estándar por cliente.
- Determina los días desde la última compra.
- Calcula un **score dinámico de recompra** = `días_ultima_compra / frecuencia_promedio`.
- Filtra clientes con score entre 0.40 y 1.50 (ventana donde es probable que compren).
- Estima una **fecha estimada de próxima compra** basada en la frecuencia promedio.
- Exporta el listado a un archivo Excel ordenado por fecha estimada.

**Salida:**  
Archivo Excel llamado `CLIENTES PROX A COMPRAR [fecha].xlsx` con clientes, fecha de última compra, frecuencia promedio, score de recompra, fecha estimada de próxima compra y métricas adicionales.

--------------

**Purpose:**  
Identify customers with a high probability of making a new purchase soon, based on their historical purchase behavior.

**Methodology:**
- Aggregates purchases per client and per date (one purchase may consist of multiple product lines).
- Calculates average purchase frequency (in days) and standard deviation per client.
- Determines days since the last purchase.
- Computes a **dynamic repurchase score** = `days_since_last / average_frequency`.
- Filters clients with a score between 0.40 and 1.50 (indicating they are in the window where a new purchase is likely).
- Estimates a **next purchase date** based on average frequency.
- Exports the filtered list to an Excel file ordered by estimated next purchase date.

**Output:**  
An Excel file named `CLIENTES PROX A COMPRAR [date].xlsx` containing clients with their last purchase date, average frequency, repurchase score, estimated next purchase date, and additional metrics.
