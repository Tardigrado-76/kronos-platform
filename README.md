# Proyecto Kronos

[![Backend Architecture](https://img.shields.io/badge/Architecture-Microservices-blue.svg)]()
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Relational%20DB-336791.svg)]()
[![Redis](https://img.shields.io/badge/Redis-Cache%20%26%20Message%20Broker-DC382D.svg)]()

## 📌 Resumen Ejecutivo
**Kronos** es una plataforma backend distribuida diseñada para escalabilidad y alta disponibilidad. Su infraestructura está completamente contenerizada (Docker) orquestando bases de datos relacionales (PostgreSQL), sistemas de caché de alto rendimiento (Redis) y capas de aplicación (Apps).

---

## 🏗️ Arquitectura de la Solución (Mermaid)

```mermaid
flowchart TD
    %% Estilos
    classDef proxy fill:#f59e0b,stroke:#fff,stroke-width:2px,color:#fff;
    classDef backend fill:#10b981,stroke:#fff,stroke-width:2px,color:#fff;
    classDef db fill:#3b82f6,stroke:#fff,stroke-width:2px,color:#fff;
    classDef cache fill:#ef4444,stroke:#fff,stroke-width:2px,color:#fff;

    Client([Peticiones Externas]) --> API[API Gateway / Router]:::proxy
    
    API --> BackendNode[Servicios Backend (Node.js/TS)]:::backend
    
    BackendNode --> DB[(PostgreSQL 16)]:::db
    BackendNode -.-> Cache[(Redis Alpine)]:::cache
    
    Admin[Administradores] --> Adminer[Adminer DB UI]:::db
    Adminer --> DB
```

---

## 📚 Estructura de Componentes

```text
Kronos/
├── apps/                   # Microservicios y módulos de negocio
│   ├── backend/            # Lógica principal del servidor
│   └── frontend/           # Capa de presentación o cliente
├── docker-compose.yml      # Definición de la topología local
├── docker-compose.prod.yml # Definición de topología de producción
├── package.json            # Gestor de dependencias del monorepo
└── README.md               # Documentación ejecutiva
```

---

## 🔐 Seguridad y Rendimiento
1. **Contenerización Estricta:** Uso de imágenes Alpine ligeras y aisladas para reducir drásticamente la superficie de ataque de la infraestructura subyacente.
2. **Topología de Red Aislada:** Redis y PostgreSQL se comunican mediante redes internas de Docker, limitando la exposición pública de los puertos de datos.
