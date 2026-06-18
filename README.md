# Proyecto Final: Teoría de Aprendizaje de Máquinas (TAM)

Este repositorio contiene el pipeline completo de machine learning desarrollado para el proyecto final del curso de Teoría de Aprendizaje de Máquinas. El objetivo principal es la predicción y clusterización de eventos de fallas, clasificándolas según su nivel de impacto (UITI y DURACION) y variables meteorológicas/temporales.

## Autores
* Johan Sebastian Mendieta Dilbert
* Sebastian Torres Gamboa
* Christopher Andres Piedrahita Pavas

## Descripción del Proyecto
El proyecto implementa un enfoque híbrido que combina aprendizaje no supervisado y supervisado para analizar, perfilar y predecir fallas. Se utilizan datos históricos, climáticos y de infraestructura para entrenar un modelo robusto y generalizable. 

El código y su respectiva documentación técnica se encuentran detallados en el notebook `TAM_pipeline_sustentacion_reducido_comentado.ipynb`, el cual abarca desde la limpieza de datos hasta la evaluación final del modelo predictivo.

## Arquitectura y Flujo de Trabajo (Pipeline)

1. **Preprocesamiento y Limpieza de Datos:**
   * Eliminación de datos nulos y duplicados.
   * Creación de variables temporales cíclicas (seno/coseno para horas y meses) para mejorar el entendimiento temporal del modelo.
   * Generación de resúmenes climáticos (media, máximo, mínimo, desviación estándar) para reducir la dimensionalidad de las variables horarias originales.
2. **Partición Temporal:**
   * División del dataset en conjuntos de Entrenamiento (70%), Validación (15%) y Prueba (15%), respetando estrictamente el orden cronológico para simular un escenario real de predicción de eventos futuros.
3. **Clustering Inicial y Subclustering (K-Means):**
   * **K-Means Inicial (K=2):** Separa los eventos de menor impacto de los de alto impacto histórico utilizando las variables objetivo.
   * **Subclustering (K=3):** Profundiza en los eventos de alto impacto para descubrir tres perfiles específicos de fallas graves.
4. **Modelo de Clasificación (XGBoost):**
   * Preprocesamiento con `ColumnTransformer` y `Pipeline` de scikit-learn (Imputación, StandardScaler, OneHotEncoder).
   * Entrenamiento de un modelo `XGBClassifier` multiclase con ajuste de pesos para manejar el desbalance de clases, optimizado con métricas de *log-loss*.

## Estructura del Repositorio

* `TAM_pipeline_sustentacion_reducido_comentado.ipynb`: Notebook principal con el pipeline de ejecución comentado paso a paso.
* `Presentacion.pdf`: Documento de sustentación con el análisis detallado, la justificación algorítmica y los resultados clave del proyecto.
* `README.md`: Este archivo.

## Requisitos y Dependencias

El proyecto está diseñado para ser ejecutado en entornos como Google Colab o de manera local en Jupyter. Las principales librerías utilizadas son:
* `pandas` y `numpy` para la manipulación y análisis de datos.
* `scikit-learn` para el preprocesamiento, particionamiento, clustering (`MiniBatchKMeans`) y métricas de evaluación.
* `xgboost` para el modelo supervisado final.
* `matplotlib` para las visualizaciones.
* `joblib` para el almacenamiento y carga de modelos persistentes.

## Cómo Utilizar

1. Clona este repositorio en tu entorno local o cárgalo en Google Colab.
2. Asegúrate de tener acceso al dataset requerido (`Dataset_Full_Enriched_V1.pkl`).
3. Instala las dependencias necesarias. Si usas Google Colab, la primera celda del notebook detectará e instalará automáticamente `xgboost` en caso de que falte.
4. Ajusta las variables de configuración en la sección de **"1. Instalación, importaciones y configuración"** del notebook (específicamente la ruta de origen de los datos `RUTA_ARCHIVO` y la ruta de destino `CARPETA_SALIDA`).
5. Ejecuta el notebook celda por celda.
