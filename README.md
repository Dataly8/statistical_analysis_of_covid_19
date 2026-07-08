# COVID-19 Pandemic Statistical Snapshot

*Read this in: [English](#english) | [Español](#español)*

---

## English

Python application to explore COVID-19 pandemic statistics for the state of Ohio (March 2020 – March 2021). It lets you query the data by date range and visualize it through interactive charts.

Final project for the module *"AI-Powered Programming Languages"* of the Master's in Business Intelligence and Data Analytics (IEBS).

### What the application does

- Connects securely to a remote endpoint (CSV) using header authentication, or reads the data from a local file when no credentials are available.
- Lets the user search records by a **date range**.
- Runs in a **loop**: after each query, it asks whether to repeat or exit.
- Offers **two chart types** (interactive, built with Plotly), selectable dynamically:
  - **Line chart**: evolution of positive cases and cumulative hospitalizations.
  - **Bar chart**: new positive cases per day.
- Includes a function to generate an AI image (Azure OpenAI / `gpt-image-2`).

### Analytical decisions

- **Variable choice**: the app plots `positive` (cumulative cases) and `hospitalizedCumulative` (cumulative hospitalizations) because together they tell the story of the contagion's spread: the gap between the two lines reflects the share of cases that required hospitalization.
- **Missing data**: the `recovered` field was not reported by the source in the early dates (it came back empty), so `hospitalizedCumulative` was used instead, as it has complete data across the whole range. Empty fields are converted to `0` to avoid errors.
- **Time ordering**: records are sorted from oldest to newest before plotting, so the time-series lines read correctly.
- **AI image generation**: the function is implemented and replicates the example provided in the assignment. During submission the API returned a 401 error (invalid/expired access credential), so the final image was generated with an equivalent tool.

### Requirements

- Python 3.10 or higher
- Dependencies listed in `requirements.txt`:

```
requests
plotly
openai
```

Install them with:

```bash
pip install -r requirements.txt
```

### How to run

The application can work in **two ways**:

**Option A — with the local data file (recommended for reproducing):** no credentials required. The app detects that no environment variables are set and automatically reads the `CovidResultsCSV.csv` file included in the repository.

```bash
python PROYECTO_Python_Estadistica_Pandemia.py
```

**Option B — with a live API connection:** requires setting the endpoint credentials as environment variables before running.

Windows (PowerShell):

```powershell
$env:COVID_API_URL = "ENDPOINT_URL"
$env:COVID_API_KEY = "YOUR_API_KEY"
python PROYECTO_Python_Estadistica_Pandemia.py
```

macOS / Linux:

```bash
export COVID_API_URL="ENDPOINT_URL"
export COVID_API_KEY="YOUR_API_KEY"
python PROYECTO_Python_Estadistica_Pandemia.py
```

> AI image generation additionally uses the `AZURE_OPENAI_ENDPOINT`, `AZURE_OPENAI_API_KEY`, and `AZURE_OPENAI_API_VERSION` variables. If they are not defined, the app continues without generating the image.

### Project structure

```
├── PROYECTO_Python_Estadistica_Pandemia.py   # Main application
├── CovidResultsCSV.csv                        # Data (local reproducible source)
├── requirements.txt                           # Dependencies
├── imagen_pizarra.png                         # AI-generated image
└── README.md
```

### Technologies

- **Python** — application logic
- **requests** — HTTP calls to the endpoint
- **csv / io** — data parsing
- **Plotly** — interactive visualizations
- **Azure OpenAI** — AI image generation

### Author

Marta — Master's in Business Intelligence and Data Analytics (IEBS)

---

## Español

Aplicación en Python para explorar datos estadísticos de la pandemia de COVID-19 en el estado de Ohio (marzo 2020 – marzo 2021). Permite consultar los datos por rango de fechas y visualizarlos mediante gráficos interactivos.

Proyecto final del módulo *"Lenguajes de programación potenciados con IA"* del Máster en Business Intelligence y Análisis de Datos (IEBS).

### ¿Qué hace la aplicación?

- Se conecta de forma segura a un endpoint remoto (CSV) mediante autenticación por cabecera, o lee los datos de un archivo local si no hay credenciales.
- Permite buscar registros por un **rango de fechas** introducido por el usuario.
- Funciona en un **bucle**: tras cada consulta, pregunta si se desea repetir o salir.
- Ofrece **dos tipos de gráfico** interactivos (Plotly), elegibles dinámicamente:
  - **Líneas**: evolución de casos positivos y hospitalizados acumulados.
  - **Barras**: nuevos casos positivos por día.
- Incluye una función para generar una imagen con IA (Azure OpenAI / `gpt-image-2`).

### Decisiones analíticas

- **Elección de variables**: se representan `positive` (casos acumulados) y `hospitalizedCumulative` (hospitalizados acumulados) porque juntos cuentan la historia de la expansión del contagio: la distancia entre ambas líneas refleja la proporción de casos que requirió ingreso hospitalario.
- **Datos faltantes**: el campo `recovered` no fue reportado por la fuente en las fechas tempranas (aparecía vacío), por lo que se optó por `hospitalizedCumulative`, con datos completos en todo el rango. Los campos vacíos se convierten a `0` para evitar errores.
- **Ordenación temporal**: los registros se ordenan de fecha más antigua a más reciente antes de graficar, para que las líneas temporales se lean correctamente.
- **Generación de imagen con IA**: la función está implementada y replica el ejemplo facilitado en el enunciado. Durante la entrega, la API devolvió un error 401 (credencial de acceso inválida/caducada), por lo que la imagen final se generó con una herramienta equivalente.

### Requisitos

- Python 3.10 o superior
- Las dependencias listadas en `requirements.txt`:

```
requests
plotly
openai
```

Instálalas con:

```bash
pip install -r requirements.txt
```

### Cómo ejecutar

La aplicación puede funcionar de **dos formas**:

**Opción A — con el archivo de datos local (recomendada para reproducir):** no requiere credenciales. La aplicación detecta que no hay variables de entorno definidas y lee automáticamente el archivo `CovidResultsCSV.csv` incluido en el repositorio.

```bash
python PROYECTO_Python_Estadistica_Pandemia.py
```

**Opción B — con conexión en vivo a la API:** requiere definir las credenciales del endpoint como variables de entorno antes de ejecutar.

Windows (PowerShell):

```powershell
$env:COVID_API_URL = "URL_DEL_ENDPOINT"
$env:COVID_API_KEY = "TU_API_KEY"
python PROYECTO_Python_Estadistica_Pandemia.py
```

macOS / Linux:

```bash
export COVID_API_URL="URL_DEL_ENDPOINT"
export COVID_API_KEY="TU_API_KEY"
python PROYECTO_Python_Estadistica_Pandemia.py
```

> Para la generación de imagen con IA se usan además las variables `AZURE_OPENAI_ENDPOINT`, `AZURE_OPENAI_API_KEY` y `AZURE_OPENAI_API_VERSION`. Si no se definen, la aplicación continúa sin generar la imagen.

### Estructura del proyecto

```
├── PROYECTO_Python_Estadistica_Pandemia.py   # Aplicación principal
├── CovidResultsCSV.csv                        # Datos (fuente local reproducible)
├── requirements.txt                           # Dependencias
├── imagen_pizarra.png                         # Imagen generada con IA
└── README.md
```

### Tecnologías

- **Python** — lógica de la aplicación
- **requests** — llamadas HTTP al endpoint
- **csv / io** — parseo de los datos
- **Plotly** — visualizaciones interactivas
- **Azure OpenAI** — generación de imagen con IA

### Autora

Marta — Máster en Business Intelligence y Análisis de Datos (IEBS)
