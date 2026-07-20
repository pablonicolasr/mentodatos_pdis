<div align="center">

# SalarIA

## M10: Clasificación de la cobertura terrestre en ambientes salares

**Ciencia de Datos y Machine Learning aplicados al análisis de coberturas terrestres del Salar de Olaroz**

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Google Colab](https://img.shields.io/badge/Google-Colab-F9AB00?logo=googlecolab&logoColor=white)](https://colab.research.google.com/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikitlearn&logoColor=white)](https://scikit-learn.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

</div>

---

## Descripción

**SalarIA** es una propuesta de mentoría orientada a la clasificación de la cobertura terrestre en ambientes salares mediante técnicas de **análisis de datos**, **visualización**, **curación de datos** y **aprendizaje automático**.

El área de estudio corresponde al **Salar de Olaroz**, en la provincia de Jujuy, Argentina. Las variables disponibles provienen de un proceso previo de preparación de información satelital Sentinel-2 y de polígonos de referencia etiquetados.

> [!IMPORTANT]
> El trabajo comienza sobre datasets ya conformados y tabulados, disponibles en la carpeta [`tables/`](tables/).

El objetivo no es reconstruir el procesamiento raster, sino aprender a:

- comprender la estructura y el significado de un dataset ambiental;
- analizar variables espectrales, índices y etiquetas;
- identificar problemas de calidad de datos;
- construir visualizaciones relevantes;
- aplicar criterios de curación y preprocesamiento;
- entrenar modelos supervisados y no supervisados;
- evaluar resultados evitando fugas de información;
- comunicar hallazgos de forma clara, reproducible y técnicamente fundamentada.

---

## Objetivos de la mentoría

Al finalizar el recorrido, se espera que los equipos puedan:

1. Interpretar un dataset tabular generado a partir de información satelital.
2. Diferenciar identificadores, coordenadas, bandas, índices, metadatos y etiquetas.
3. Realizar análisis exploratorio univariado, bivariado y multivariado.
4. Detectar valores nulos, infinitos, duplicados, inconsistencias y valores extremos.
5. Diseñar y documentar un proceso de curación de datos.
6. Construir experimentos reproducibles de Machine Learning.
7. Comparar modelos mediante métricas adecuadas para problemas multiclase.
8. Analizar la importancia de las variables y los errores de clasificación.
9. Explorar estructuras internas mediante clustering y reducción de dimensionalidad.
10. Presentar conclusiones con evidencia cuantitativa y visual.

---

## Alcance del trabajo

Se trabajará exclusivamente con **datasets tabulados**.

### No es necesario utilizar

- GDAL;
- Rasterio;
- Google Earth Engine;
- OpenCV;
- Scikit-image;
- herramientas de descarga de Sentinel-2;
- algoritmos de corrección atmosférica;
- generación de mosaicos raster;
- extracción de píxeles desde GeoJSON;
- reproyección o remuestreo de imágenes.

Las carpetas [`raster/`](raster/), [`labels/`](labels/), [`metadata/`](metadata/) y [`scripts/`](scripts/) permiten comprender el origen y la trazabilidad del dataset, pero **no constituyen el punto de partida operativo de los prácticos**.

---

## 🗂️ Estructura del repositorio

```text
mentodatos_pdis/
│
├── apuntes/       # Material teórico y guías de la mentoría
├── labels/        # Etiquetas y polígonos utilizados en la conformación
├── metadata/      # Metadatos del área y de las fuentes de información
├── raster/        # Productos satelitales previamente procesados
├── scripts/       # Scripts utilizados para construir los datasets
├── tables/        # Datasets tabulados para los mentoreados
│
├── LICENSE
└── README.md
```

### Carpeta principal

```text
tables/
├── olaroz_samples_pixels_raw.csv
├── olaroz_samples_pixels.csv
├── olaroz_samples_features.csv
├── olaroz_samples_clean.csv
└── olaroz_samples_balanced.csv
```

---

## Datasets disponibles

Los archivos representan distintas etapas del proceso de conformación y preparación de los datos.

| Archivo | Propósito dentro del flujo |
|---|---|
| `olaroz_samples_pixels_raw.csv` | Tabla inicial obtenida durante la extracción de observaciones. Permite estudiar el estado más próximo a los datos originales. |
| `olaroz_samples_pixels.csv` | Tabla posterior a controles y filtros iniciales. |
| `olaroz_samples_features.csv` | Dataset enriquecido con variables derivadas e índices. Es el punto de partida recomendado para el análisis y la curación. |
| `olaroz_samples_clean.csv` | Versión de referencia luego de un proceso de limpieza y consistencia. Puede utilizarse para comparar decisiones de curación. |
| `olaroz_samples_balanced.csv` | Versión preparada para analizar el efecto del balance de clases y comparar estrategias de modelado. |

> [!NOTE]
> Cada grupo debe conservar los archivos originales sin modificaciones. Los resultados intermedios y las tablas curadas deben guardarse con nombres nuevos.

---

## Cómo interpretar el dataset

Cada fila representa una observación tabular asociada a un píxel extraído dentro de un polígono de referencia.

Según la etapa del dataset, pueden encontrarse los siguientes grupos de variables:

| Grupo | Ejemplos | Función |
|---|---|---|
| Identificación | `sample_id` | Vincular cada píxel con su muestra o polígono de origen. |
| Bandas espectrales | `B02`, `B03`, `B04`, `B08`, entre otras | Representar la respuesta espectral registrada por Sentinel-2. |
| Índices espectrales | `NDVI`, `NDWI`, `MNDWI`, `BSI` | Resumir relaciones entre bandas y facilitar la separación de coberturas. |
| Coordenadas | columnas espaciales disponibles | Ubicar las observaciones y analizar patrones espaciales. |
| Etiquetas | `class_id`, `class_name`, `macro_class` | Definir la clase objetivo para aprendizaje supervisado. |
| Metadatos | `confidence`, `split`, `season`, `source`, entre otros | Aportar contexto y trazabilidad. |

### Conceptos espectrales mínimos

- **NDVI:** asociado principalmente con presencia y vigor de vegetación.
- **NDWI:** utilizado para explorar agua o humedad.
- **MNDWI:** variante orientada a resaltar superficies con agua o humedad.
- **BSI:** indicador relacionado con suelo desnudo y superficies expuestas.

Estos índices deben interpretarse junto con las bandas originales, la clase de cobertura y el contexto ambiental del salar.

---

# Entorno de trabajo

La mentoría puede desarrollarse de dos maneras equivalentes:

1. **PC local:** Python, entorno virtual y JupyterLab, Jupyter Notebook o Visual Studio Code.
2. **Google Colab:** notebook en la nube, sin necesidad de instalación local.

No se requiere GPU. Los modelos clásicos propuestos pueden ejecutarse con CPU.

---

## Opción 1: PC local

### Requisitos recomendados

- Python 3.12 de 64 bits.
- Git.
- 8 GB de RAM como mínimo.
- 16 GB de RAM recomendados.
- Visual Studio Code con las extensiones **Python** y **Jupyter**, o JupyterLab.

### Clonar el repositorio

```bash
git clone https://github.com/pablonicolasr/mentodatos_pdis.git
cd mentodatos_pdis
```

### Crear el entorno virtual en Windows

```bash
py -3.12 -m venv .venv
.venv\Scripts\activate
```

### Crear el entorno virtual en Linux o macOS

```bash
python3.12 -m venv .venv
source .venv/bin/activate
```

### Actualizar `pip`

```bash
python -m pip install --upgrade pip
```

### Instalar las dependencias

```bash
pip install numpy pandas scipy matplotlib seaborn plotly scikit-learn imbalanced-learn joblib openpyxl pyarrow jupyterlab notebook ipykernel
```

### Registrar el kernel

```bash
python -m ipykernel install --user --name m10-salares --display-name "Python - M10 Salares"
```

### Iniciar JupyterLab

```bash
jupyter lab
```

---

## Opción 2: Google Colab

No es necesario activar GPU.

### Clonar el repositorio

```python
!git clone https://github.com/pablonicolasr/mentodatos_pdis.git
%cd mentodatos_pdis
```

### Instalar dependencias adicionales

```python
!pip install -q imbalanced-learn plotly openpyxl pyarrow
```

### Verificar el entorno

```python
import sys
import numpy as np
import pandas as pd
import sklearn

print("Python:", sys.version.split()[0])
print("NumPy:", np.__version__)
print("Pandas:", pd.__version__)
print("Scikit-learn:", sklearn.__version__)
```

### Cargar el dataset principal

```python
from pathlib import Path
import pandas as pd

DATA_DIR = Path("tables")
DATASET = DATA_DIR / "olaroz_samples_features.csv"

df = pd.read_csv(DATASET)

print("Dimensiones:", df.shape)
display(df.head())
```

---

## Dependencias recomendadas

```text
numpy
pandas
scipy
matplotlib
seaborn
plotly
scikit-learn
imbalanced-learn
joblib
openpyxl
pyarrow
jupyterlab
notebook
ipykernel
```

Para registrar las versiones exactas utilizadas:

```bash
pip freeze > environment_freeze.txt
```

---

# Cronograma de actividades

| Fecha | Entrega | Propósito principal |
|---|---|---|
| **07/08/2026** | Práctico 1: análisis y visualización | Comprender el dataset, describir sus variables y comunicar patrones iniciales. |
| **04/09/2026** | Práctico 2: análisis exploratorio y curación | Detectar problemas, justificar decisiones y generar un dataset curado. |
| **02/10/2026** | Práctico 3: aprendizaje supervisado, no supervisado o ambos | Diseñar experimentos, entrenar modelos y evaluar resultados. |
| **31/10/2026** | Video de presentación final | Sintetizar el problema, la metodología, los resultados y las conclusiones. |
| **04/12/2026 y 05/12/2026** | Jornadas de presentación de mentorías | Presentar y defender el trabajo desarrollado. |

---

# Práctico 1 — Análisis y visualización

## Entrega: 07/08/2026

### Dataset sugerido

```text
tables/olaroz_samples_features.csv
```

### Objetivos

- Comprender qué representa cada fila.
- Identificar el significado y el tipo de cada columna.
- Clasificar las variables por función.
- Analizar la distribución de las clases.
- Obtener estadísticas descriptivas.
- Explorar relaciones entre bandas, índices y categorías.
- Generar visualizaciones claras y correctamente rotuladas.

### Visualizaciones mínimas sugeridas

- cantidad de registros por clase;
- histogramas de variables numéricas;
- boxplots por clase;
- matriz de correlaciones;
- gráficos de dispersión entre índices;
- comparación de bandas por cobertura;
- representación espacial mediante las coordenadas disponibles.

### Preguntas orientadoras

- ¿El dataset está balanceado?
- ¿Qué variables presentan mayor dispersión?
- ¿Qué índices parecen separar mejor las clases?
- ¿Existen variables altamente correlacionadas?
- ¿Se observan patrones espaciales?
- ¿Qué clases presentan mayor superposición espectral?

---

# Práctico 2 — Análisis exploratorio y curación

## Entrega: 04/09/2026

### Dataset de entrada recomendado

```text
tables/olaroz_samples_features.csv
```

La finalidad es que cada equipo diseñe su propia estrategia de curación. El archivo `olaroz_samples_clean.csv` debe utilizarse posteriormente como referencia o punto de comparación, no como reemplazo del análisis.

### Controles mínimos

- valores nulos;
- valores infinitos;
- filas duplicadas;
- tipos de datos incorrectos;
- etiquetas inconsistentes;
- variables constantes o casi constantes;
- rangos improbables;
- valores extremos;
- distribuciones asimétricas;
- desbalance de clases;
- correlación excesiva;
- consistencia entre identificadores, etiquetas y metadatos.

### Resultado esperado

Cada grupo debería generar su propio archivo curado:

```text
data/processed/olaroz_samples_curated_grupo_n.csv
```

También debe documentar las decisiones tomadas:

| Problema detectado | Cantidad | Decisión | Justificación |
|---|---:|---|---|
| Valores nulos | ... | ... | ... |
| Infinitos | ... | ... | ... |
| Duplicados | ... | ... | ... |
| Valores extremos | ... | ... | ... |
| Desbalance | ... | ... | ... |

> [!WARNING]
> Un valor no debe eliminarse únicamente por aparecer como atípico en un boxplot. En ambientes salares pueden existir respuestas espectrales extremas que sean ambientalmente válidas.

---

# Práctico 3 — Aprendizaje automático

## Entrega: 02/10/2026

Cada grupo puede desarrollar:

- aprendizaje supervisado;
- aprendizaje no supervisado;
- o una estrategia combinada.

### Dataset principal

```text
data/processed/olaroz_samples_curated_grupo_n.csv
```

Los archivos `olaroz_samples_clean.csv` y `olaroz_samples_balanced.csv` pueden utilizarse para realizar comparaciones controladas.

---

## Aprendizaje supervisado

### Modelos sugeridos

- Regresión logística como línea base.
- Random Forest.
- Extra Trees.
- HistGradientBoosting.

### Métricas mínimas

- F1-macro.
- Balanced accuracy.
- Precision, recall y F1 por clase.
- Matriz de confusión.
- Análisis de errores.
- Importancia de variables o técnicas de interpretación equivalentes.

La exactitud global no debe utilizarse como única medida de rendimiento, especialmente ante clases desbalanceadas.

---

## Aprendizaje no supervisado

### Técnicas sugeridas

- K-Means.
- Gaussian Mixture.
- Clustering jerárquico.
- DBSCAN como exploración complementaria.
- PCA para reducción de dimensionalidad y visualización.

### Evaluación sugerida

- silhouette score;
- análisis de estabilidad;
- interpretación de los grupos;
- comparación posterior con las etiquetas reales;
- Adjusted Rand Index cuando resulte pertinente.

Las etiquetas reales no deben utilizarse para formar los clusters. Solo pueden utilizarse posteriormente para interpretar o evaluar la estructura obtenida.

---

# Regla metodológica fundamental: evitar fuga de información

La columna `sample_id` identifica la muestra o polígono del cual proceden múltiples píxeles.

Los píxeles de un mismo polígono pueden ser muy similares. Si una división aleatoria coloca algunos de esos píxeles en entrenamiento y otros en prueba, el modelo puede obtener resultados artificialmente altos.

## División incorrecta

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.20,
    random_state=42
)
```

## División recomendada por grupos

```python
from sklearn.model_selection import GroupShuffleSplit

splitter = GroupShuffleSplit(
    n_splits=1,
    test_size=0.20,
    random_state=42
)

train_idx, test_idx = next(
    splitter.split(X, y, groups=df["sample_id"])
)

X_train = X.iloc[train_idx]
X_test = X.iloc[test_idx]
y_train = y.iloc[train_idx]
y_test = y.iloc[test_idx]
```

> [!CAUTION]
> La evaluación debe separar grupos completos. Nunca deben mezclarse en entrenamiento y prueba observaciones pertenecientes al mismo `sample_id`.

---

# Selección de variables

No deben utilizarse automáticamente como predictores:

- identificadores;
- etiquetas objetivo;
- descripciones textuales;
- columnas creadas a partir de la clase;
- variables que revelen directamente el conjunto de pertenencia;
- metadatos que provoquen fuga de información.

Ejemplo orientativo:

```python
NON_FEATURE_COLUMNS = [
    "sample_id",
    "class_id",
    "class_name",
    "macro_class",
    "description",
    "confidence",
    "split",
    "notes",
    "season",
    "source",
]

feature_columns = [
    column
    for column in df.columns
    if column not in NON_FEATURE_COLUMNS
]
```

Las coordenadas requieren un análisis especial. Se recomienda comparar:

1. un modelo sin coordenadas;
2. un modelo con coordenadas.

Esto permite evaluar si el algoritmo aprende características espectrales o simplemente memoriza ubicaciones.

---

# Reproducibilidad

Todos los grupos deben:

- utilizar `random_state=42` cuando corresponda;
- conservar intactos los datos originales;
- evitar rutas absolutas;
- utilizar `pathlib` para construir rutas;
- ejecutar cada notebook completo desde cero;
- documentar las decisiones de curación;
- separar identificadores, predictores y etiquetas;
- guardar tablas, figuras y modelos;
- registrar versiones de Python y dependencias;
- dividir los datos respetando `sample_id`;
- comunicar también las limitaciones del análisis.

### Semilla común

```python
import random
import numpy as np

RANDOM_STATE = 42

random.seed(RANDOM_STATE)
np.random.seed(RANDOM_STATE)
```

### Guardado de modelos

```python
import joblib

joblib.dump(
    model,
    "models/modelo_final_m10.joblib"
)
```

---

# 📁 Organización recomendada para cada grupo

```text
m10-grupo-n/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   ├── raw/
│   ├── interim/
│   └── processed/
│
├── notebooks/
│   ├── 01_analisis_visualizacion.ipynb
│   ├── 02_eda_curacion.ipynb
│   └── 03_aprendizaje_automatico.ipynb
│
├── reports/
│   ├── figures/
│   └── tables/
│
├── models/
│
└── src/
    ├── data.py
    ├── preprocessing.py
    ├── visualization.py
    └── modeling.py
```

---

# Lista de verificación para las entregas

## Práctico 1

- [ ] El notebook se ejecuta de principio a fin.
- [ ] Se explica qué representa una fila.
- [ ] Se presenta un diccionario o clasificación de variables.
- [ ] Se analiza la distribución de las clases.
- [ ] Los gráficos tienen título, ejes, unidades y explicación.
- [ ] Se incluyen conclusiones basadas en evidencia.

## Práctico 2

- [ ] Se analizan nulos, infinitos y duplicados.
- [ ] Se estudian rangos, distribuciones y valores extremos.
- [ ] Cada decisión de curación está justificada.
- [ ] Se conserva el dataset original.
- [ ] Se exporta una tabla curada propia.
- [ ] Se documentan las limitaciones del proceso.

## Práctico 3

- [ ] Se separan correctamente predictores y objetivo.
- [ ] La división respeta los grupos definidos por `sample_id`.
- [ ] Se construye al menos un modelo de referencia.
- [ ] Se comparan modelos o configuraciones.
- [ ] Se reportan métricas por clase.
- [ ] Se presenta una matriz de confusión o una evaluación equivalente.
- [ ] Se interpretan resultados, errores y limitaciones.
- [ ] El modelo final puede reproducirse y volver a cargarse.

---

# Flujo general de la mentoría

```text
Dataset tabulado conformado
          │
          ▼
Comprensión de variables y etiquetas
          │
          ▼
Análisis y visualización
          │
          ▼
Diagnóstico y curación
          │
          ▼
Dataset curado por el grupo
          │
          ▼
Aprendizaje supervisado y/o no supervisado
          │
          ▼
Evaluación, interpretación y comunicación
```

---

# Mentor

**Pablo Nicolás Ramos**  
Ingeniero en Informática · Diplomado en Ciencia de Datos · Doctorando en Ingeniería

---

# 📄 Licencia

Este proyecto se distribuye bajo la licencia [MIT](LICENSE).

---

<div align="center">

## Comprender los datos. Curar con criterio. Modelar con rigor. Comunicar con claridad.

</div>
