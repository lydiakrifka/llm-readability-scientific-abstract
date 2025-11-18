```mermaid
flowchart TD
    A[OpenAlex API] -->|Query by concept ID & year| B[Fetch Abstracts]
    B --> C{Abstract has\ninverted index?}
    C -->|No| B
    C -->|Yes| D[Store Metadata]
    D --> E[Reconstruct Abstract Text]
    E --> F[Save as .txt file]
    F --> G{1000 abstracts\ncollected?}
    G -->|No| B
    G -->|Yes| H[Process Text Files]
    H --> I[Calculate Readability Scores]
    I --> J[ARI Score]
    I --> K[Flesch-Kincaid Grade]
    I --> L[Dale-Chall Score]
    J --> M[Aggregate by Year]
    K --> M
    L --> M
    M --> N[Calculate Mean & SEM]
    N --> O[Save to CSV]
    N --> P[Generate Visualization]
    P --> Q[Plot with Error Bars]
    O --> R[Statistical Analysis]
    Q --> R
    R --> S[Welch's T-Test]
    S --> T[Results & Interpretation]

    style A fill:#e1f5ff
    style I fill:#fff4e1
    style M fill:#e8f5e9
    style P fill:#fce4ec
    style R fill:#f3e5f5
