```mermaid
graph TB
    user -->|ssh.cloud.nstu.ru:5980| OCAlmaLinux9.4
    OCAlmaLinux9.4 <--> Nginx
    user <-->|http://217.71.129.139:4775/browser/| Nginx
    OCAlmaLinux9.4 <--> pgAdmin4
    OCAlmaLinux9.4 <--> postgresql
    Nginx <--> |127.0.0.1:5050| pgAdmin4
    pgAdmin4 <--> |127.0.0.1:5432| postgresql
```