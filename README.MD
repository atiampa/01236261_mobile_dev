graph TD
    %% Components
    Client[Client/Browser]
    ShoppingServer[Shopping Server]
    AuthService[Auth Service]
    BackendService[Backend Service]
    API[API]
    ConfigStore[Config File/Store]
    S3Bucket[AWS S3 Bucket]
    BackendDB[Backend Database]
    Agent[Agent]

    %% Data Flows
    Client -->|View/Create Orders| ShoppingServer
    ShoppingServer -->|Orders| AuthService
    ShoppingServer -->|Order API Keys| API
    ShoppingServer -->|Configurations| ConfigStore
    AuthService -->|Users| BackendDB
    AuthService -->|UI Resources| S3Bucket
    BackendService --> AuthService
    BackendService --> Agent
    Agent -->|UI (static)| AuthService

    %% Boundaries
    subgraph LocalBoundary1 [Local Boundary (-3)]
        ShoppingServer
        AuthService
        BackendService
        ConfigStore
    end

    subgraph ExternalBoundary [External Boundary]
        Client
        API
    end

    subgraph StorageBoundary [Storage Boundary]
        S3Bucket
        BackendDB
    end
