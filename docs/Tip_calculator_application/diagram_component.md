```markdown
```mermaid
flowchart TB
    %% Define subgraphs for each layer
    subgraph Frontend
        FE_UI[User Interface]
        FE_Logic[Client-side Logic]
    end
    
    subgraph Backend
        BE_API[API Server]
        BE_Logic[Business Logic]
    end
    
    subgraph Data
        DB[Database]
    end
    
    subgraph External
        PaymentGateway[Payment Gateway]
    end

    %% Define relationships and dependencies
    FE_UI --> FE_Logic
    FE_Logic --> BE_API
    BE_API --> BE_Logic
    BE_Logic --> DB
    BE_Logic --> PaymentGateway

    %% User interactions
    user((User)) --> FE_UI
    FE_UI --> user
```
```
This diagram shows the components of a tip calculator application organized by layer, with arrows indicating dependencies and interactions. The frontend layer contains the user interface and client-side logic, the backend layer handles the API and business logic, the data layer consists of a database, and an external payment gateway is also depicted.