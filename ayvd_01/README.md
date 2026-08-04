# Análisis y Visualización de Datos

Este documento explica cómo crear y configurar el entorno de trabajo `mento_pdis` con Anaconda para realizar análisis y visualización de datos mediante Python, Pandas, NumPy, Matplotlib y Jupyter.

## 1. Requisitos previos

Instalá Anaconda o Miniconda y luego abrí **Anaconda Prompt**.

Verificá la instalación:

```bash
conda --version
```

## 2. Crear el entorno

```bash
conda create -n mento_pdis python=3.12
```

Cuando aparezca:

```text
Proceed ([y]/n)?
```

escribí `y` y presioná **Enter**.

## 3. Activar el entorno

```bash
conda activate mento_pdis
```

La terminal debería comenzar con:

```text
(mento_pdis)
```

## 4. Instalar las bibliotecas

```bash
conda install -c conda-forge numpy pandas matplotlib jupyterlab notebook ipykernel
```

Paquetes incluidos:

| Biblioteca | Uso |
|---|---|
| `numpy` | Operaciones numéricas |
| `pandas` | Lectura y análisis de datos tabulares |
| `matplotlib` | Gráficos y visualizaciones |
| `jupyterlab` | Entorno interactivo de trabajo |
| `notebook` | Compatibilidad con Jupyter Notebook |
| `ipykernel` | Registro del entorno como kernel |

## 5. Registrar el kernel

```bash
python -m ipykernel install --user --name=mento_pdis --display-name "Python (mento_pdis)"
```

Después, dentro de Jupyter, seleccioná:

```text
Kernel → Select Kernel → Python (mento_pdis)
```

## 6. Verificar la instalación

```bash
python --version
```

Debería mostrar Python 3.12.

Verificá las bibliotecas:

```bash
python -c "import numpy, pandas, matplotlib; print('Entorno instalado correctamente')"
```

## 7. Iniciar Jupyter Notebook

```bash
jupyter notebook
```

## 8. Primera prueba

Creá un notebook y ejecutá:

```python
import sys

import matplotlib
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

print("Python:", sys.version.split()[0])
print("NumPy:", np.__version__)
print("Pandas:", pd.__version__)
print("Matplotlib:", matplotlib.__version__)
```

Probá una visualización:

```python
datos = pd.DataFrame(
    {
        "clase": ["Agua", "Salina", "Suelo", "Rocoso"],
        "cantidad": [120, 280, 190, 90],
    }
)

plt.figure(figsize=(8, 4))
plt.bar(datos["clase"], datos["cantidad"])
plt.title("Cantidad de observaciones por clase")
plt.xlabel("Clase")
plt.ylabel("Cantidad")
plt.tight_layout()
plt.show()
```

## 9. Abrir el proyecto

Ubicate en la carpeta del proyecto:

```bash
cd ruta\al\proyecto
jupyter lab
```

Ejemplo:

```bash
cd C:\proyectos\mentodatos_pdis
jupyter lab
```

## 10. Flujo de trabajo diario

```bash
conda activate mento_pdis
cd ruta\al\proyecto
jupyter lab
```

Al terminar:

```bash
conda deactivate
```

## 11. Solución de problemas

### `conda` no se reconoce

Abrí **Anaconda Prompt**. Para inicializar Conda en PowerShell:

```bash
conda init powershell
```

Cerrá y volvé a abrir la terminal.

### El kernel no aparece

```bash
conda activate mento_pdis
python -m ipykernel install --user --name=mento_pdis --display-name "Python (mento_pdis)"
```

### Jupyter usa otro Python

Dentro del notebook:

```python
import sys
print(sys.executable)
```

La ruta debería contener:

```text
anaconda3\envs\mento_pdis
```

### Falta una biblioteca

```bash
conda activate mento_pdis
conda install -c conda-forge nombre_del_paquete
```

## 12. Eliminar el entorno

```bash
conda deactivate
conda env remove -n mento_pdis
```

## Instalación rápida

```bash
conda create -n mento_pdis python=3.12
conda activate mento_pdis
conda install -c conda-forge numpy pandas matplotlib jupyterlab notebook ipykernel
python -m ipykernel install --user --name=mento_pdis --display-name "Python (mento_pdis)"
jupyter lab
```

## Entorno esperado

```text
Nombre: mento_pdis
Python: 3.12
Canal: conda-forge
Interfaz: JupyterLab
Kernel: Python (mento_pdis)
```
