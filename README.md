# NYC Taxi Data Pipeline 🚖

Este proyecto construye un pipeline de datos de principio a fin usando datos de la NYC Taxi & Limousine Commission (TLC)
y datos de clima de **Open-Meteo**.

## 🎯 Objetivo
Analizar cómo el clima afecta la demanda de taxis en la ciudad de Nueva York y construir un dashboard interactivo para visualizar los resultados.

## 🏗️ Arquitectura Inicial
- **Extracción:** Datos de viajes de taxi (NYC TLC) + clima (API Open-Meteo)
- **Transformación:** Limpieza, feature engineering y combinación de datasets
- **Carga:** Almacenamiento en PostgreSQL
- **Orquestación:** Apache Airflow
- **Visualización:** Dashboard interactivo con Streamlit

## 📂 Estructura de Proyecto
```plaintext
data-pipeline-nyc-taxi/
├── data/
│   ├── raw/        # Datos crudos
│   └── processed/  # Datos procesados
├── etl/            # Scripts de extracción, transformación y carga
├── notebooks/      # Análisis exploratorio (EDA)
├── tests/          # Pruebas unitarias
├── README.md
└── requirements.txt
```

## 🧩 Componentes del Pipeline

```mermaid
flowchart TD
    A[NYC TLC Data] -->|Descarga| B[Extract: Taxi Trips]
    A2[Open-Meteo API] -->|Llamadas API| B2[Extract: Weather Data]

    B --> C[Raw Storage: data/raw/]
    B2 --> C

    C --> D[Transform: Limpieza + Enriquecimiento]
    D -->|Join clima + viajes| E[Processed Data: data/processed/]

    E --> F[Load: PostgreSQL]
    F -->|Tablas: trips_fact + weather_dim| G[Data Warehouse]

    G --> H[Airflow DAG]
    H -->|Automatización diaria| G

    G --> I[Dashboard: Streamlit]
    I -->|KPIs + Visualizaciones| J[Usuario/Stakeholder]
