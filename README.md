# 3-Desafio-X-Telecom-2
Desafío de Alura Latam: Telecom X - parte 2

## 🎯 Objetivo del Proyecto

El objetivo principal de este proyecto es desarrollar modelos predictivos capaces de prever qué clientes de Telecom X tienen mayor probabilidad de cancelar sus servicios (churn). Anticipar este comportamiento nos permite implementar estrategias proactivas de retención y reducir la pérdida de clientes.

## 📁 Estructura del Proyecto

Este proyecto se organiza de la siguiente manera:

- `Telecom_X_Prediccion_Cancelaciones.ipynb`: Cuaderno principal de Google Colab que contiene todo el código para la preparación de datos, modelado, evaluación e interpretación de resultados.
- `datos_tratados.csv`: Archivo CSV que contiene el dataset con los datos de clientes utilizado para el análisis y modelado.


## 🛠️ Preparación de Datos

La preparación de los datos para el modelado incluyó los siguientes pasos:

1.  **Carga de Datos:** Se cargó el dataset `datos_tratados.csv` en un DataFrame de pandas.
2.  **Tratamiento de Datos Nulos:** Se eliminaron las filas con valores nulos en la variable objetivo ('Churn') para asegurar la calidad del conjunto de datos.
3.  **Clasificación de Variables:** Las variables se clasificaron en categóricas y numéricas para aplicar el preprocesamiento adecuado.
4.  **Codificación de Variables Categóricas:** Se aplicó One-Hot Encoding a las variables categóricas para convertirlas a un formato numérico binario, eliminando columnas redundantes generadas por el encoder.
5.  **Transformación de la Variable Objetivo:** La variable 'Churn' fue renombrada a 'Canceled_Yes' y transformada a un formato numérico (1 para 'Yes', 0 para 'No').
6.  **Verificación del Desbalance de Clases:** Se analizó la proporción de clientes que cancelaron vs. los que no, identificando un desbalance significativo (aproximadamente 26.6% de cancelaciones).
7.  **Separación en Conjuntos de Entrenamiento y Prueba:** Los datos fueron divididos en conjuntos de entrenamiento y prueba (75% entrenamiento, 25% prueba) utilizando `train_test_split` con `stratify` para mantener la proporción de clases en ambos conjuntos.

## 📊 Análisis de Correlación y Selección de Variables

Se realizó un análisis de correlación para identificar las variables con mayor relación con la cancelación. Se generó una matriz de correlación visualizada con un heatmap. Basado en este análisis y la importancia de las características obtenida de los modelos, se seleccionó un subconjunto de variables explicativas para el modelado.

## 🤖 Modelado Predictivo

Se entrenaron y evaluaron varios modelos de clasificación para predecir la cancelación:

1.  **Modelo Baseline (DummyClassifier):** Un modelo simple que predice la clase mayoritaria, utilizado como referencia para comparar el rendimiento de modelos más complejos.
2.  **Árbol de Decisión:** Un modelo basado en reglas que proporciona interpretabilidad. Se ajustaron parámetros como `max_depth` para controlar la complejidad.
3.  **Random Forest:** Un modelo de conjunto basado en árboles de decisión, conocido por su buen rendimiento. Se utilizó `class_weight='balanced'` para abordar el desbalance de clases.
4.  **XGBoost:** Otro modelo de ensemble potente basado en gradient boosting. Se ajustaron hiperparámetros para optimizar su rendimiento.

Se evaluó el rendimiento de cada modelo utilizando métricas como Accuracy, Precision, Recall, F1-Score y AUC.

## ✨ Optimización con SMOTE y Escalado

Para mejorar la capacidad de los modelos para predecir la clase minoritaria (cancelación), se aplicaron técnicas adicionales:

-   **Normalización (StandardScaler):** Se escalaron las variables numéricas para que tuvieran media cero y varianza unitaria, lo que puede mejorar el rendimiento de algunos algoritmos.
-   **Sobremuestreo (SMOTE):** Se aplicó SMOTE al conjunto de entrenamiento para sintétizar nuevas instancias de la clase minoritaria y equilibrar la distribución de clases.

Se reentrenó el modelo Random Forest con los datos resampleados y escalados, observando un impacto significativo en el Recall para la clase de cancelación.

## 💡 Resultados y Conclusiones

Los factores clave que influyen en la cancelación identificados incluyen:

-   Tipo de contrato (clientes con contratos a corto plazo son más propensos a cancelar).
-   Antigüedad del cliente (clientes con mayor antigüedad son menos propensos a cancelar).
-   Tipo de servicio de Internet (fibra óptica parece asociada con mayor cancelación).
-   Método de pago (cheque electrónico).
-   Cargos mensuales (cargos más altos asociados con mayor cancelación).
-   Ausencia de servicios adicionales (seguridad, soporte técnico).

Se compararon los modelos basándose en las métricas de evaluación, considerando el desbalance de clases. Se discutieron las implicaciones de priorizar Recall (identificar a todos los posibles canceladores) vs. Precision o Accuracy (tener predicciones más exactas). Dada la naturaleza del problema, un alto Recall puede ser crucial para implementar estrategias de retención efectivas.

## 🛠️ Cómo Ejecutar el Cuaderno

Para ejecutar este cuaderno de Google Colab, sigue estos pasos:

1.  Abre el cuaderno `Telecom_X_Prediccion_Cancelaciones.ipynb` en Google Colab.
2.  Haz clic en "Archivo" > "Subir notebook" y selecciona el archivo .ipynb de este proyecto desde tu computadora.
3.  Una vez que el notebook esté abierto en Colab, ejecuta las celdas del notebook secuencialmente. Puedes hacerlo haciendo usando "Entorno de ejecución" > "Ejecutar todas".


Este README proporciona una visión general del proyecto y sus resultados. Para un análisis detallado, por favor, revisa el cuaderno de Google Colab.
