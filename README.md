graph TD
    %% Clients
    Client[Next.js Frontend]
    
    %% Infrastructure
    Keycloak[Keycloak Identity Provider]
    Eureka[Netflix Eureka Service Discovery]
    
    %% Gateway
    Gateway[Spring Cloud API Gateway]
    
    %% Microservices
    UserSvc[User Service]
    CatalogSvc[Catalog Service]
    InventorySvc[Inventory Service]
    OrderSvc[Order Service]
    
    %% Databases
    UserDB[(PostgreSQL - Users)]
    CatalogDB[(MongoDB - Food/Search)]
    InventoryDB[(PostgreSQL - Stock)]
    OrderDB[(PostgreSQL - Orders)]

    %% Routing
    Client -->|REST / HTTP| Gateway
    Gateway -->|Auth Check| Keycloak
    
    %% Service Discovery
    Gateway -.->|Resolve IPs| Eureka
    UserSvc -.->|Register| Eureka
    CatalogSvc -.->|Register| Eureka
    InventorySvc -.->|Register| Eureka
    OrderSvc -.->|Register| Eureka
    
    %% API Routing
    Gateway --> UserSvc
    Gateway --> CatalogSvc
    Gateway --> InventorySvc
    Gateway --> OrderSvc
    
    %% DB Connections
    UserSvc --> UserDB
    CatalogSvc --> CatalogDB
    InventorySvc --> InventoryDB
    OrderSvc --> OrderDB
    
    %% Inter-service sync
    OrderSvc -.->|Feign Client| InventorySvc