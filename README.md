# AP_2025_B3_TP2_Mendoza_Dante

## 📌 Arquitectura general del sistema
```mermaid
flowchart TB
    subgraph Docker_Compose
        A[Apache Airflow]
        B["MinIO S3"]
        C[MLflow]
        D[FastAPI]
        H[Postgres DB]
    end

    A --> B
    A --> C
    A <--> H
    C <--> H
    D --> C
    B --> E["Data Lake - Crimes Chicago"]
    C --> F["Registro de modelos"]
    D --> G["Cliente / App"]

    %% Estilos
    style A fill:#1f77b4,stroke:#000,stroke-width:2px,color:#fff
    style B fill:#9467bd,stroke:#000,stroke-width:2px,color:#fff
    style C fill:#2ca02c,stroke:#000,stroke-width:2px,color:#fff
    style D fill:#ff7f0e,stroke:#000,stroke-width:2px,color:#fff
    style E fill:#8c564b,stroke:#000,stroke-width:2px,color:#fff
    style F fill:#17becf,stroke:#000,stroke-width:2px,color:#fff
    style G fill:#d62728,stroke:#000,stroke-width:2px,color:#fff
    style H fill:#7f7f7f,stroke:#000,stroke-width:2px,color:#fff
```

## 📌 Ciclo de vida del modelo
```mermaid
flowchart LR
    A["Datos en MinIO"] --> B["Airflow ETL"]
    B --> C["Train/Test Split"]
    C --> D["Entrenamiento (Notebook/Script)"]
    D --> E["MLflow Tracking"]
    E --> F["MLflow registro de modelos"]
    F --> G["FastAPI Predicción"]
    G --> H["Predicción al usuario"]

    %% Integración con Postgres
    E <---> I["Postgres (Metadatos MLflow)"]

    %% Estilos
    style A fill:#9467bd,stroke:#000,stroke-width:2px,color:#fff
    style B fill:#1f77b4,stroke:#000,stroke-width:2px,color:#fff
    style C fill:#8c564b,stroke:#000,stroke-width:2px,color:#fff
    style D fill:#bcbd22,stroke:#000,stroke-width:2px,color:#fff
    style E fill:#2ca02c,stroke:#000,stroke-width:2px,color:#fff
    style F fill:#17becf,stroke:#000,stroke-width:2px,color:#fff
    style G fill:#ff7f0e,stroke:#000,stroke-width:2px,color:#fff
    style H fill:#d62728,stroke:#000,stroke-width:2px,color:#fff
    style I fill:#7f7f7f,stroke:#000,stroke-width:2px,color:#fff
```


## 📌 Pipeline dentro de Airflow (DAG)
```mermaid
flowchart TD
    subgraph Airflow_DAG
        Start["Start / Trigger DAG"] --> Ingest["Ingest Data"]
        Ingest --> Preprocess["Preprocess Data"]
        Preprocess --> Train["Train Model"]
        Train --> Evaluate["Evaluate Model"]

        Evaluate --> |si es bueno| Register_Model["Register Model"]
        Evaluate --> |si es malo| Train

        Register_Model --> End["Finish / Deploy"]
    end

    %% Estilos
    style Start fill:#1f77b4,stroke:#000,stroke-width:2px,color:#fff
    style Ingest fill:#17becf,stroke:#000,stroke-width:2px,color:#fff
    style Preprocess fill:#ff7f0e,stroke:#000,stroke-width:2px,color:#fff
    style Train fill:#2ca02c,stroke:#000,stroke-width:2px,color:#fff
    style Evaluate fill:#bcbd22,stroke:#000,stroke-width:2px,color:#fff
    style Register_Model fill:#9467bd,stroke:#000,stroke-width:2px,color:#fff
    style End fill:#d62728,stroke:#000,stroke-width:2px,color:#fff
```


