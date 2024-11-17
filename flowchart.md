flowchart TD
    subgraph Data Loading
        A[Start] --> B[Load Feature Names]
        B --> C[Load Training Data]
        B --> D[Load Testing Data]
        C --> |"X_train.txt"| E[Raw Training Features]
        C --> |"y_train.txt"| F[Raw Training Labels]
        D --> |"X_test.txt"| G[Raw Testing Features]
        D --> |"y_test.txt"| H[Raw Testing Labels]
    end

    subgraph Feature Processing
        E --> I[Assign Feature Names to Columns]
        G --> I
        I --> J[Feature Standardization]
        J --> |"StandardScaler"| K[Normalized Training Features]
        J --> |"StandardScaler"| L[Normalized Testing Features]
    end

    subgraph Label Processing
        F --> M[Label One-Hot Encoding]
        H --> M
        M --> |"to_categorical"| N[Encoded Training Labels]
        M --> |"to_categorical"| O[Encoded Testing Labels]
    end

    subgraph Sliding Window Transformation
        K --> P[Create Sliding Windows]
        L --> P
        P --> |"window_size=128<br>step_size=64"| Q[Windowed Training Data]
        P --> |"window_size=128<br>step_size=64"| R[Windowed Testing Data]
    end

    subgraph Final Dataset
        Q --> S[Final Training Dataset]
        R --> T[Final Testing Dataset]
        N --> S
        O --> T
        S --> U[Save Processed Data]
        T --> U
        U --> V[End]
    end

    style A fill:#f9f,stroke:#333,stroke-width:2px
    style V fill:#f9f,stroke:#333,stroke-width:2px
    style U fill:#bbf,stroke:#333,stroke-width:2px