flowchart TD
    S["Daily Scheduler"] --> O["Import Coordinator"]
    O --> Q["Job Queue"]
    Q --> W["Fetch Workers"]
    W --> A["Third-party REST API"]
    W --> R["Raw Object Storage"]
    R --> V["Validate and Normalize"]
    V --> D["Staging Tables"]
    D --> C{"Reconciliation passes?"}
    C -->|Yes| P["Atomic Publish"]
    C -->|No| F["Quarantine / Failed Run"]
