# AndinaRetail S.A.C. — Proyecto de Analítica de Datos

Proyecto desarrollado por el **Grupo 04** para la asignatura **Analítica de Datos** de la Escuela Profesional de Ingeniería de Software de la Universidad Nacional Mayor de San Marcos.

## 1. Descripción

AndinaRetail S.A.C. es una empresa ficticia del sector retail omnicanal peruano que opera mediante tiendas físicas, una plataforma web y una aplicación móvil.

El proyecto desarrolla una solución integral de analítica de datos para:

- Analizar ventas, clientes, tendencias y estacionalidad.
- Identificar patrones y causas relacionadas con el desempeño comercial.
- Predecir la demanda y la respuesta de clientes a campañas.
- Optimizar decisiones de inventario y reabastecimiento.
- Comunicar los resultados mediante tableros en Power BI.

Todos los datos utilizados son sintéticos y fueron generados exclusivamente con fines académicos.

---

## 2. Integrantes y roles

| Integrante | Rol principal |
|---|---|
| GUZMAN NEYRA, PAULO RENATO | Analista Estadístico / Descriptivo |
| HUERTA FIRMA, FREDDY ANTHONY | Analista de Optimización / BI |
| JUSTINO OCMIN, JHAMIR VALERI | Científico de Datos |
| MENDOZA MEZA, PABLO ANDRES | Ingeniero de Datos |
| SANCHEZ SALDAÑA, SERGIO ANTONIO | Líder del Proyecto / Data PM |

La asignación de roles establece una responsabilidad principal, pero todos los integrantes participaron en la revisión e integración del proyecto.

---

## 3. Estructura del repositorio

```text
proyecto_AndinaRetail_G4/
├── .gitignore
├── README.md
└── proyecto-andinaretail/
    ├── datos/
    │   ├── generar_datos.py
    │   ├── tiendas.csv
    │   ├── productos.csv
    │   ├── clientes.csv
    │   ├── ventas.csv
    │   ├── tickets.csv
    │   ├── inventario.csv
    │   ├── data_dictionary.md
    │   ├── 03_predictivo/
    │   └── 04_prescriptivo/
    ├── notebooks/
    │   ├── 01_estadistica.ipynb
    │   ├── 02_descriptivo_diagnostico.ipynb
    │   ├── 03_predictivo.ipynb
    │   └── 04_prescriptivo.ipynb
    ├── docs/
    ├── powerbi/
    ├── presentacion/
    └── requirements.txt
```

---

## 4. Tecnologías utilizadas

- Python 3.11
- Jupyter Notebook / JupyterLab
- pandas, NumPy y SciPy
- Matplotlib y Seaborn
- scikit-learn
- XGBoost y LightGBM
- SHAP
- PuLP
- Faker
- Microsoft Power BI

---

## 5. Requisitos previos

Para ejecutar el proyecto se requiere:

- Python 3.11.
- Git.
- JupyterLab o Jupyter Notebook.
- Miniconda, Anaconda o el módulo `venv` de Python.
- Power BI Desktop para abrir el archivo `.pbix`.

El proyecto puede ejecutarse utilizando un entorno Conda o un entorno virtual `.venv`. Solo se debe elegir una de las dos alternativas.

---

## 6. Instalación y ejecución

### 6.1 Clonar el repositorio

```bash
git clone https://github.com/SergIOSanchez99/proyecto_AndinaRetail_G4.git
cd proyecto_AndinaRetail_G4/proyecto-andinaretail
```

Los siguientes comandos deben ejecutarse desde la carpeta `proyecto-andinaretail`, donde se encuentra el archivo `requirements.txt`.

### 6.2 Crear el entorno de ejecución

#### Opción A — Entorno Conda

Crear y activar el entorno:

```bash
conda create --name andinaretail python=3.11 -y
conda activate andinaretail
```

Registrar el entorno como kernel de Jupyter:

```bash
python -m ipykernel install --user --name andinaretail --display-name "Python 3.11 - AndinaRetail"
```

#### Opción B — Entorno virtual con `venv`

Crear el entorno virtual:

```powershell
py -3.11 -m venv .venv
```

Activarlo desde PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

En el símbolo del sistema de Windows también puede activarse con:

```cmd
.venv\Scripts\activate.bat
```

Si PowerShell bloquea temporalmente la activación del entorno, ejecutar:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

Registrar el entorno como kernel de Jupyter:

```powershell
python -m ipykernel install --user --name andinaretail-venv --display-name "Python 3.11 - AndinaRetail (.venv)"
```

La carpeta `.venv/` está excluida del repositorio mediante el archivo `.gitignore`.

### 6.3 Instalar las dependencias

Con el entorno seleccionado y activado:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### 6.4 Iniciar JupyterLab

```bash
jupyter lab
```

Luego, ingresar a la carpeta `notebooks/` y seleccionar el kernel correspondiente:

```text
Python 3.11 - AndinaRetail
```

o, si se utilizó `venv`:

```text
Python 3.11 - AndinaRetail (.venv)
```

---

## 7. Orden de ejecución

Los notebooks deben ejecutarse en el siguiente orden:

1. `01_estadistica.ipynb`
2. `02_descriptivo_diagnostico.ipynb`
3. `03_predictivo.ipynb`
4. `04_prescriptivo.ipynb`

En cada notebook se recomienda utilizar:

```text
Kernel → Restart Kernel and Run All Cells
```

El notebook prescriptivo utiliza archivos generados durante la etapa predictiva, por lo que `03_predictivo.ipynb` debe ejecutarse antes que `04_prescriptivo.ipynb`.

---

## 8. Generación de datos sintéticos

Los archivos CSV ya se encuentran incluidos en la carpeta `datos/`.

Para regenerarlos:

```bash
python datos/generar_datos.py
```

El script utiliza semillas fijas para mantener la reproducibilidad.

> La ejecución puede reemplazar los archivos CSV existentes.

---

## 9. Contenido de los notebooks

### Parte 1 — Técnicas estadísticas

`notebooks/01_estadistica.ipynb`

Incluye exploración de datos, estadística descriptiva, valores faltantes, outliers, correlaciones, pruebas de hipótesis e intervalos de confianza.

### Parte 2 — Descriptivo y diagnóstico

`notebooks/02_descriptivo_diagnostico.ipynb`

Incluye tendencias, estacionalidad, Pareto, segmentación RFM, clustering y diagnóstico del margen.

### Parte 3 — Modelos predictivos

`notebooks/03_predictivo.ipynb`

Desarrolla:

- Regresión para predecir demanda.
- Clasificación para predecir respuesta a campañas.
- Validación cruzada.
- Optimización de hiperparámetros.
- Evaluación de modelos.
- Importancia de variables y SHAP.

### Parte 4 — Modelos prescriptivos

`notebooks/04_prescriptivo.ipynb`

Incluye la formulación y resolución de un modelo de optimización de reabastecimiento mediante PuLP, junto con análisis de escenarios y recomendaciones.

---

## 10. Resultados

Los resultados generados se almacenan principalmente en:

```text
datos/03_predictivo/regresion/
datos/03_predictivo/clasificacion/
datos/04_prescriptivo/
```

Estas carpetas contienen predicciones, métricas, importancia de variables, modelos entrenados y resultados de optimización.

---

## 11. Power BI y documentación

Los tableros se encuentran en:

```text
powerbi/AndinaRetail.pbix
powerbi/AndinaRetail_tableros.pdf
```

La documentación complementaria se encuentra en:

```text
datos/data_dictionary.md
docs/bitacora_prompts.md
docs/autoevaluacion.pdf
presentacion/
```

---

## 12. Ejecución en Google Colab

También es posible ejecutar los notebooks en Google Colab:

```python
!git clone https://github.com/SergIOSanchez99/proyecto_AndinaRetail_G4.git
%cd /content/proyecto_AndinaRetail_G4/proyecto-andinaretail
!pip install -r requirements.txt
```

Google Colab utiliza un entorno temporal, por lo que:

- Las dependencias deben instalarse nuevamente en cada sesión.
- Los archivos generados deben descargarse antes de cerrar el entorno.
- Algunas etapas de entrenamiento pueden tardar según los recursos disponibles.

Para una ejecución completa y reproducible se recomienda utilizar Conda o `.venv` de forma local.

---

## 13. Reproducibilidad y consideraciones

La reproducibilidad se mantiene mediante:

- Python 3.11.
- Archivo `requirements.txt`.
- Entorno virtual independiente.
- Semillas fijas.
- Rutas relativas.
- Orden de ejecución documentado.
- Datos sintéticos incluidos.
- Notebooks ejecutados con salidas visibles.

Los datos no representan personas ni empresas reales. Las salidas generadas con inteligencia artificial fueron revisadas y validadas por el equipo.

---

## 14. Cierre del entorno

Para desactivar un entorno Conda:

```bash
conda deactivate
```

Para desactivar un entorno `.venv`:

```bash
deactivate
```