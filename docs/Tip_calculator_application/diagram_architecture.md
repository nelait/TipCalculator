Certainly! Below is a markdown file containing a Mermaid.js flowchart representing the high-level system architecture for a Tip Calculator application. The diagram includes layers, technology choices, external integrations, and data storage.

```markdown
# Tip Calculator Application Architecture Diagram

```mermaid
flowchart TB
    %% Define subgraphs for different layers
    subgraph User Interface
        direction TB
        UI[User Interface]
    end
    
    subgraph Application Layer
        direction TB
        Logic[Business Logic]
        Calculator[Tip Calculator Service]
    end
    
    subgraph External Integrations
        direction TB
        API[Currency Conversion API]
    end
    
    subgraph Data Storage
        direction TB
        DB[NoSQL Database]
    end

    %% Define relationships between components
    UI -->|User Input: Total Bill| Logic
    Logic -->|Calculate Tip %| Calculator
    Calculator -->|Store Calculation Data| DB
    Logic -->|Optional: Convert Currency| API
    API -->|Fetch Conversion Rates| Logic
    
    %% Add labels for clarity
    classDef interface fill:#f9f,stroke:#333,stroke-width:2px;
    classDef service fill:#bbf,stroke:#333,stroke-width:2px;
    classDef integration fill:#bfb,stroke:#333,stroke-width:2px;
    classDef storage fill:#ffb,stroke:#333,stroke-width:2px;

    %% Apply styles to nodes
    class UI interface;
    class Logic service;
    class Calculator service;
    class API integration;
    class DB storage;
```
```

### Description

- **User Interface Layer:** This layer allows the user to input the total bill amount.
  
- **Application Layer:** 
  - The `Business Logic` component processes the user input and interacts with other services.
  - The `Tip Calculator Service` performs the calculation of different tip percentages based on the total bill.

- **External Integrations:**
  - The application can optionally interact with a `Currency Conversion API` to convert the tip into different currencies if required.

- **Data Storage:**
  - A `NoSQL Database` is used to store calculation data and user preferences, which can be useful for analytics or future enhancements.

This architecture provides a clear separation of concerns across different layers and shows a simple integration with an external service for additional functionality.
