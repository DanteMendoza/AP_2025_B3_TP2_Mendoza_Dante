# AP_2025_B3_TP2_Mendoza_Dante

## Arquitectura general del sistema
```mermaid
flowchart TB
    subgraph Docker_Compose
        A[Apache Airflow]
        B["MinIO S3"]
        C[MLflow]
        D[FastAPI API]
    end

    A --> B
    A --> C
    D --> C
    B --> E["Data Lake - Crimes Chicago"]
    C --> F["Model Registry"]
    D --> G["Client / App"]
```

## Ciclo de vida del modelo
```mermaid
flowchart LR
    A[Datos en MinIO] --> B[Airflow ETL]
    B --> C[Train/Test Split]
    C --> D[Notebook: Training Models]
    D --> E[MLflow Tracking & Model Registry]
    E --> F[FastAPI Prediction API]
    F --> G[Predicción al usuario]
```

## Pipeline dentro de Airflow (DAG)
```mermaid
flowchart TD
    Start --> Ingest
    Ingest --> Preprocess
    Preprocess --> Train
    Train --> Evaluate
    Evaluate --> Register_Model
    Register_Model --> End
```

# AP_2025_B3_TP2_Mendoza_Dante

## 📌 Arquitectura general del sistema
```mermaid
flowchart TB
    subgraph Docker_Compose
        A[Apache Airflow]
        B["MinIO S3"]
        C[MLflow]
        D[FastAPI API]
    end

    A --> B
    A --> C
    D --> C
    B --> E["Data Lake - Crimes Chicago"]
    C --> F["Model Registry"]
    D --> G["Client / App"]

    %% Estilos
    style A fill:#1f77b4,stroke:#000,stroke-width:2px,color:#fff
    style B fill:#9467bd,stroke:#000,stroke-width:2px,color:#fff
    style C fill:#2ca02c,stroke:#000,stroke-width:2px,color:#fff
    style D fill:#ff7f0e,stroke:#000,stroke-width:2px,color:#fff
    style E fill:#8c564b,stroke:#000,stroke-width:2px,color:#fff
    style F fill:#17becf,stroke:#000,stroke-width:2px,color:#fff
    style G fill:#d62728,stroke:#000,stroke-width:2px,color:#fff
```

## 📌 Ciclo de vida del modelo
```mermaid
flowchart LR
    A["Datos en MinIO"] --> B["Airflow ETL"]
    B --> C["Train/Test Split"]
    C --> D["Notebook: Training Models"]
    D --> E["MLflow Tracking & Model Registry"]
    E --> F["FastAPI Prediction API"]
    F --> G["Predicción al usuario"]

    %% Estilos
    style A fill:#9467bd,stroke:#000,stroke-width:2px,color:#fff
    style B fill:#1f77b4,stroke:#000,stroke-width:2px,color:#fff
    style C fill:#8c564b,stroke:#000,stroke-width:2px,color:#fff
    style D fill:#bcbd22,stroke:#000,stroke-width:2px,color:#fff
    style E fill:#2ca02c,stroke:#000,stroke-width:2px,color:#fff
    style F fill:#ff7f0e,stroke:#000,stroke-width:2px,color:#fff
    style G fill:#d62728,stroke:#000,stroke-width:2px,color:#fff
```

## 📌 Pipeline dentro de Airflow (DAG)
```mermaid
flowchart TD
    Start --> Ingest
    Ingest --> Preprocess
    Preprocess --> Train
    Train --> Evaluate
    Evaluate --> Register_Model
    Register_Model --> End

    %% Estilos
    style Start fill:#1f77b4,stroke:#000,stroke-width:2px,color:#fff
    style Ingest fill:#17becf,stroke:#000,stroke-width:2px,color:#fff
    style Preprocess fill:#ff7f0e,stroke:#000,stroke-width:2px,color:#fff
    style Train fill:#2ca02c,stroke:#000,stroke-width:2px,color:#fff
    style Evaluate fill:#bcbd22,stroke:#000,stroke-width:2px,color:#fff
    style Register_Model fill:#9467bd,stroke:#000,stroke-width:2px,color:#fff
    style End fill:#d62728,stroke:#000,stroke-width:2px,color:#fff
```



