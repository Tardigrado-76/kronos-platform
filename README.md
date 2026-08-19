# Proyecto Kronos - Fichaje Digital 2025

[![Backend Architecture](https://img.shields.io/badge/Architecture-Microservices-blue.svg)]()
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Relational%20DB-336791.svg)]()
[![Compliance](https://img.shields.io/badge/Compliance-Ley%20Fichaje%202025-DC382D.svg)]()

## 📌 Resumen Ejecutivo
**Kronos** es una plataforma de **software de fichaje digital obligatorio 2025**, diseñada para garantizar el cumplimiento normativo estricto del registro de jornada laboral. Su infraestructura distribuida está completamente contenerizada (Docker) y optimizada para alta disponibilidad, asegurando la trazabilidad inmutable de los marcajes, la gestión de turnos y la interoperabilidad con sistemas de nóminas.

---

## 🏗️ Arquitectura de la Solución (Mermaid)

```mermaid
flowchart TD
    %% Estilos
    classDef proxy fill:#f59e0b,stroke:#fff,stroke-width:2px,color:#fff;
    classDef backend fill:#10b981,stroke:#fff,stroke-width:2px,color:#fff;
    classDef db fill:#3b82f6,stroke:#fff,stroke-width:2px,color:#fff;
    classDef cache fill:#ef4444,stroke:#fff,stroke-width:2px,color:#fff;

    Client([Terminales / App Empleados]) --> API[API Gateway / Router]:::proxy
    
    API --> BackendNode[Core de Fichaje (Node.js/TS)]:::backend
    
    BackendNode --> DB[(PostgreSQL 16 - Registro Inmutable)]:::db
    BackendNode -.-> Cache[(Redis - Gestión de Sesiones)]:::cache
    
    RRHH[Portal RRHH e Inspección de Trabajo] --> Adminer[Adminer / Dashboard UI]:::db
    Adminer --> DB
```

---

## 📚 Estructura de Componentes

```text
Kronos/
├── apps/                   # Microservicios de marcaje y control horario
│   ├── backend/            # Lógica principal del servidor de fichaje
│   └── frontend/           # Capa de presentación (Empleados y RRHH)
├── docker-compose.yml      # Definición de la topología local
├── docker-compose.prod.yml # Definición de topología de producción (Alta Disponibilidad)
├── package.json            # Gestor de dependencias del monorepo
└── README.md               # Documentación ejecutiva
```

---

## 🔐 Cumplimiento y Rendimiento
1. **Cumplimiento Normativo 2025:** Diseñado específicamente para cumplir con las regulaciones laborales de control horario (registro inmutable, retención de datos y exportación legal).
2. **Contenerización Estricta y Seguridad:** Uso de imágenes Alpine ligeras y aisladas. Redis y PostgreSQL se comunican mediante redes internas de Docker para garantizar la privacidad y seguridad de los datos de los empleados.
