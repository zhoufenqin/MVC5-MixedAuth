# Assessment Overview

This directory contains supplementary architectural analysis documents generated alongside the core AppCAT assessment report. Each document provides a specific perspective on the MixedAuth application to support modernization planning.

## Supplementary Documents

| Document | Description |
|---|---|
| [Architecture Diagram](./architecture-diagram.md) | High-level application architecture (layers, technology stack, data flow) and detailed component relationship diagram (controllers, services, data access, infrastructure) |
| [Dependency Map](./dependency-map.md) | Visual map of all external NuGet package dependencies grouped by functional category, with version/compatibility risk analysis |
| [API & Service Communication Contracts](./api-service-contracts.md) | Inventory of all HTTP endpoints, request/response types, communication patterns, security posture, and a sequence diagram of key authentication flows |
| [Data Architecture](./data-architecture.md) | Database configuration, ASP.NET Identity entity model (ER diagram), repository methods, caching strategy, and data classification/sensitivity analysis |
| [Configuration Inventory](./configuration-inventory.md) | Comprehensive inventory of all configuration sources, build profiles, runtime properties, secrets handling, and framework/runtime versions |
| [Business Workflows](./business-workflows.md) | End-to-end documentation of core authentication workflows (Forms login, Windows Authentication, account management), business rules, and decision logic |

## How to Use These Documents

- **For migration planning**: Start with the [Architecture Diagram](./architecture-diagram.md) and [Dependency Map](./dependency-map.md) to understand the current technology stack and identify modernization targets.
- **For API compatibility analysis**: See [API & Service Communication Contracts](./api-service-contracts.md) for the full endpoint inventory and security posture.
- **For data migration**: See [Data Architecture](./data-architecture.md) for the entity model, schema management approach, and PII/sensitivity classification.
- **For configuration management**: See [Configuration Inventory](./configuration-inventory.md) for all property keys, build profiles, and secrets handling gaps.
- **For functional regression testing**: See [Business Workflows](./business-workflows.md) for the core authentication flows and business rules to validate after migration.
