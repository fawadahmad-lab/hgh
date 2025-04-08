%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#ffd8d8', 'edgeLabelBackground':'#ffffff'}}}%%
flowchart TB
    subgraph CRM_Data_Sources
        A[Salesforce] -->|REST API| B[(CRM Data Pipeline)]
        C[HubSpot] -->|Webhooks| B
        D[Product Docs] -->|PDF/Excel| B
    end

    subgraph Data_Preprocessing
        B --> E[Chunking & Embedding]
        E --> F[(Vector DB\nPinecone)]
        E --> G[(PostgreSQL\nCRM Data)]
    end

    subgraph Real_Time_Inference
        H[Sales Call Audio] --> I[Whisper.cpp\nSTT]
        I --> J[Hybrid Query Engine]
        J -->|Semantic| F
        J -->|SQL| G
        J --> K[Llama 3\nFine-tuned)]
        K --> L[Response Generator]
    end

    subgraph MLOps
        M[MLflow] --> N[Kubernetes]
        O[Prometheus] --> P[Grafana]
        Q[Evidently] --> R[Retrain Trigger]
    end

    subgraph Frontend
        L --> S[Web Dashboard]
        L --> T[Audio Suggestions]
    end

    S --> U[Sales Rep]
    T --> U

    style CRM_Data_Sources fill:#e3f2fd,stroke:#2196f3
    style Data_Preprocessing fill:#bbdefb,stroke:#1565c0
    style Real_Time_Inference fill:#c8e6c9,stroke:#4caf50
    style MLOps fill:#ffecb3,stroke:#ffa000
    style Frontend fill:#d1c4e9,stroke:#7e57c2
