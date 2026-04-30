```mermaid
graph TB
    user -->|ssh.cloud.nstu.ru:5980| OCAlmaLinux9.4
    user <-->|http://217.71.129.139:4775/browser/| Nginx
    OCAlmaLinux9.4 <--> Nginx
    OCAlmaLinux9.4 <--> pgAdmin4
    OCAlmaLinux9.4 <--> postgresql
    Nginx <--> |aa| pgAdmin4
    pgAdmin4 <--> |aa| postgresql
```