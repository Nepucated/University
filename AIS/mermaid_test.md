```mermaid
graph TB
    user(root, dba) -->|ssh.cloud.nstu.ru:5980| OC AlmaLinux 9.4
    user (root, dba) <-->|http://217.71.129.139:4775/browser/| Nginx
    
    
    Client -->|HTTP запросы<br/>GET/POST/PUT/DELETE| Backend
    Backend -->|SQL запросы| Postgres
    Postgres -->|результаты| Backend
    Backend -->|JSON ответы| Client
    
    style Client fill:#e1f5ff
    style Backend fill:#fff3e0
    style Postgres fill:#f3e5f5
    style Compose fill:#f0f0f0,stroke:#999,stroke-width:2px
```