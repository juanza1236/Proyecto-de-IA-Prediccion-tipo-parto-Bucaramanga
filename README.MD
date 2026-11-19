# Predicción y Análisis del Tipo de Parto en Bucaramanga mediante Machine Learning

![Banner del Proyecto](banner.jpeg)

## 1. Objetivo General
Analizar registros de nacidos vivos en Bucaramanga mediante exploración estadística, preparación de datos, modelos de clasificación supervisada y algoritmos de agrupamiento no supervisado. El objetivo de clasificación es `TIPO PARTO`; en la tercera entrega se estudia, además, si las observaciones forman grupos según sus características neonatales, obstétricas y sociodemográficas.

## 2. Dataset y procedencia

**Fuente:** [Datos Abiertos Colombia — 43. Nacidos Vivos en Municipio de Bucaramanga](https://www.datos.gov.co/Salud-y-Protecci-n-Social/43-Nacidos-Vivos-en-Municipio-de-Bucaramanga/x5xp-9w4b).

| Concepto | Resultado almacenado en el notebook |
|---|---:|
| Registros originales | 66.555 |
| Variables originales | 30 (11 cuantitativas y 19 categóricas) |
| Registros empleados para modelado | 51.963 |
| Variables predictoras | 29 |
| Variable objetivo / clases de referencia | `TIPO PARTO` / 3 |

**Distribución de clases en el conjunto de modelado:** Cesárea: 26.263 (50,54 %); Espontáneo: 25.605 (49,28 %); Instrumentado: 95 (0,18 %). Se debe tener en cuenta el gran desbalance de la clase instrumentado al interpretar las métricas de clasificación.

## 3. URL de Procedencia del Dataset
* **Portal Datos Abiertos Colombia:** [43. Nacidos Vivos en Municipio de Bucaramanga](https://www.datos.gov.co/Salud-y-Protecci-n-Social/43-Nacidos-Vivos-en-Municipio-de-Bucaramanga/x5xp-9w4b/data_preview)

## 4. Integrantes
* **José David Caballero Jimenez** — Código: `2235154`
* **Juan Pablo Zarate Jimenez** — Código: `2235161`

## 5. Tecnologías y Bibliotecas Utilizadas
* **Lenguaje y Entorno:** Python 3.11+, Google Colaboratory / Jupyter Notebook
* **Manipulación y Análisis:** `pandas`, `numpy`, `gdown`
* **Visualización:** `matplotlib`, `seaborn`
* **Machine Learning & Deep Learning:** `scikit-learn` (`StandardScaler`, `MinMaxScaler`, `PCA`, `TSNE`, `KMeans`, `DBSCAN`, `NearestNeighbors`, `DecisionTreeClassifier`, `RandomForestClassifier`, `SVC`), `tensorflow` / `keras`

## 6. Metodología Desarrollada
1. **Análisis Exploratorio y Limpieza:** Corrección de codificación UTF-8 (*mojibake*), conversión de variables numéricas, análisis de valores atípicos mediante Rango Intercuartílico (IQR) y codificación de variables categóricas.
2. **Aprendizaje Supervisado (Entrega 2):** Entrenamiento y validación cruzada de Decision Tree, Random Forest, SVM y redes neuronales MLP.
3. **Aprendizaje No Supervisado (Entrega 3):**
   * Comparación de escaladores (`StandardScaler` vs. `MinMaxScaler`).
   * Reducción lineal a 2 componentes mediante **PCA** y exploración no lineal con **t-SNE**.
   * Agrupamiento particional con **K-Means** ($k=3$) y basado en densidad con **DBSCAN** (`eps=0.1541`, `min_samples=10`, justificado mediante gráfico de *k*-distancia).
   * Evaluación mediante *Silhouette Score*, *Davies-Bouldin*, *Calinski-Harabasz*, *ARI* y *NMI*.

## 7. Resultados Principales
* **Escalamiento y PCA:** `StandardScaler` evita el sesgo por magnitud de `PESO (Gramos)` ($\sigma = 507.7\text{ g}$). Los 2 primeros componentes principales explican el **18.86%** de la varianza total (PC1: nivel educativo y edad materna; PC2: paridad y número de embarazos).
* **K-Means ($k=3$):** Alcanza un **Silhouette Score de 0.459** y **Davies-Bouldin de 0.783** en el espacio PCA 2D, segmentando la población en 3 perfiles sociodemográficos/obstétricos equilibrados.
* **DBSCAN (`eps=0.1541`, `min_samples=10`):** Identifica una región densa principal con el **98.29%** de los nacimientos y aísla **788 observaciones (1.52%) como ruido**, correspondientes a perfiles clínicos atípicos.

## 8. Estructura del Repositorio
```text
├── assets/
│   └── Banner_Proyecto.png
├── notebooks/
│   └── Prediccion_tipo_parto.ipynb
├── presentacion/
│   └── Presentacion_Proyecto.pdf
└── README.md
