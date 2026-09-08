# 12 — MayaBank Technology & Infrastructure Reference Model

## 1. Objectif

Construire un modèle technologique de référence cohérent avec les Parties VII–IX afin de relier :

```text
Business
→ Process
→ Application
→ Data
→ Technology
→ Infrastructure
→ Risk / Control
→ Transformation
```

Le cas est fictif et les dimensions chiffrées éventuelles sont pédagogiques.

## 2. Technology domains

```text
Compute & Container
Network & Edge
Integration & Messaging
Data Platforms
Identity & Security
Observability
Automation
Backup & Recovery
Cloud / Datacenter
```

## 3. Platform catalog

| Platform | Purpose | Criticality | Main Consumers |
|---|---|---:|---|
| OpenShift Platform | container runtime | Critical | Payments/Fraud/API |
| API Management | API exposure/control | Critical | Channels/Partners |
| Event Streaming | asynchronous integration | Critical | Payments/Notification/Reconciliation |
| IAM Platform | identities/tokens | Critical | all digital services |
| Database Platform | relational persistence | Critical | Payment/Core/Reconciliation |
| Observability | metrics/logs/traces | High | all platforms/apps |
| Backup & Recovery | protected copies/restore | Critical | data/platform services |
| GitOps/Automation | deployment/configuration | High | platform/app teams |

## 4. Technology products

Exemple pédagogique :

```text
OpenShift
Java
Kafka
PostgreSQL
Oracle
OIDC/SAML stack
GitOps tooling
Metrics/logs/traces tooling
Enterprise backup tooling
```

Le masterbook ne force pas un vendor lorsqu’il n’est pas nécessaire.

## 5. Application × Platform

| Application | Runtime Platform | Integration | Data |
|---|---|---|---|
| Digital Channel | OpenShift | API Mgmt | Customer/session data |
| Payment Orchestrator | OpenShift | API + Kafka | Payment State DB |
| Fraud Decision Service | OpenShift | API/events | Fraud Store |
| Clearing Gateway | OpenShift/secured integration zone | API/message | audit/status |
| Notification Service | OpenShift | Kafka | notification state |
| Reconciliation Service | OpenShift | Kafka/batch | reconciliation DB |
| Core Account Service | Core/DB platform | secure API | Oracle/Core data |

## 6. Logical deployment view

```text
[Internet / Customer]
        |
     Edge/WAF
        |
  API Management
        |
  +-------------------+
  | OpenShift PROD    |
  |                   |
  | Payment Orch.     |
  | Fraud Service     |
  | Clearing Gateway  |
  | Notification      |
  | Reconciliation    |
  +-------------------+
       |       |
       |       +----> Kafka/Event Streaming
       |
       +------------> Data Services
       |
       +------------> Core Account Platform

Shared:
IAM / PKI / DNS / Observability / Backup
```

## 7. Network zones

```text
External
→ Edge
→ Application
→ Data/Core
→ Management
→ DR/Secondary Site
```

Major flows must be labeled with purpose and security expectations.

## 8. OpenShift logical model

```text
MayaBank OpenShift Platform
├─ PROD cluster(s)
│  ├─ control plane
│  ├─ worker pools
│  ├─ ingress
│  ├─ storage integration
│  └─ observability/security integrations
├─ PREPROD
└─ Non-Prod
```

Le nombre exact de clusters/nodes reste une décision de design et de capacité, pas un fait générique.

## 9. Failure-domain model

```text
Application replica
→ worker node
→ compute failure domain
→ zone/site
→ region/site pair
```

Dependencies common to all replicas:

- DNS ;
- IAM ;
- PKI ;
- load balancing ;
- storage ;
- Kafka ;
- DB ;
- external clearing connectivity.

## 10. Critical path — Instant Payment

```text
Customer
→ Edge
→ API Management
→ Payment Orchestrator
→ IAM/AuthZ context
→ Fraud Decision Service
→ Core Account Service
→ Clearing Gateway
→ Clearing Network
→ Payment State DB
```

Notification et analytics ne doivent pas nécessairement appartenir au chemin synchrone critique.

## 11. NFR reference

### Payment execution

```text
Availability: very high
Latency: strict end-to-end target
RPO: strict
RTO: strict
Auditability: mandatory
Idempotency: mandatory
```

### Notification

```text
Asynchronous
Retryable
Can degrade independently from financial execution
```

Les seuils réels sont définis par MayaBank dans une mission réelle.

## 12. Storage map

```text
Payment State
→ resilient relational store

Core Account
→ core DB platform

Kafka
→ replicated event storage

Archives/exports
→ object storage

Backups
→ independent backup/recovery service
```

## 13. HA/DR matrix

| Service | Local HA | DR Principle | Key Dependency |
|---|---|---|---|
| OpenShift | multi-node | secondary site/region design | DNS/network/storage |
| API Mgmt | redundant | secondary endpoint | identity/certs |
| Kafka | replicated | cross-site strategy | quorum/network |
| Payment DB | DB HA | replicated/restorable | storage/network |
| IAM | redundant | DR-capable | directory/PKI |
| Observability | redundant | secondary ingestion/query | storage |

## 14. Security map

```text
External TLS
→ Edge controls
→ API authentication/authorization
→ service identity
→ network segmentation
→ encrypted data services
→ audit logging
```

## 15. Observability map

Signals :

- API latency/error ;
- payment processing P95/P99 ;
- fraud latency ;
- clearing timeout ;
- DB health ;
- Kafka lag ;
- node/cluster saturation ;
- certificate expiration ;
- backup/restore status.

## 16. Technology lifecycle map

| Technology | Status | Direction |
|---|---|---|
| OpenShift | Preferred | expand governed usage |
| Java strategic runtime | Preferred | standardize |
| Kafka | Preferred | event backbone |
| Legacy messaging | Deprecated | migrate |
| Legacy VM middleware | Tolerated/Deprecated | replatform/retire |
| Unsupported DB release | Remediate | upgrade/replace |

Statuts MayaBank pédagogiques.

## 17. Current state

```text
VM-heavy
single-site dependencies
legacy messaging
fragmented monitoring
manual provisioning
shared storage dependencies
partial DR
```

## 18. Target state

```text
Standard platform services
OpenShift where fit
API + event-driven integration
resilient data services
central identity/secrets
central observability
IaC/GitOps
tested DR
```

## 19. Transition waves

### Wave 1 — Foundations
Network, IAM, PKI, observability, automation.

### Wave 2 — Platforms
OpenShift, API Management, Event Streaming, managed data services.

### Wave 3 — Critical workloads
Payment Orchestrator, Fraud, Clearing integration.

### Wave 4 — Resilience
Multi-site recovery, restore testing, capacity under failure.

### Wave 5 — Retirement
Legacy middleware, old VM estates, obsolete products.

## 20. Reference matrices

1. Application × Platform.
2. Platform × Technology Product.
3. Technology × Lifecycle.
4. Platform × Site/Region.
5. Application × Network Zone.
6. Platform × Storage Service.
7. Service × RTO/RPO.
8. Service × Failure Domain.
9. Technology × Standard Status.
10. Technology × Owner.
11. Platform × Security Control.
12. Platform × Observability Signal.

## 21. Reference views

1. Technology Landscape.
2. Platform Landscape.
3. Logical Infrastructure View.
4. OpenShift Platform View.
5. Network Zone View.
6. Data/Storage Infrastructure View.
7. Critical Dependency View.
8. HA/DR View.
9. Security Trust Boundary View.
10. Observability View.
11. Technology Lifecycle Heatmap.
12. Current/Transition/Target View.

## 22. Architecture board questions

- Le critical path est-il explicite ?
- Quels SPOF restent communs ?
- Où se trouve l’état ?
- Le DR couvre-t-il les dépendances ?
- Quelles technologies arrivent en fin de support ?
- La capacité reste-t-elle suffisante après perte d’un failure domain ?
- Les secrets/certificats survivront-ils à une bascule ?
- Qu’est-ce qui sera réellement décommissionné ?

## 23. Criteria of Done

Le modèle est exploitable lorsqu’on peut partir :

```text
Technology
→ Platform
→ Application
→ Process
→ Business impact
```

et dans l’autre sens :

```text
Business Service
→ Applications
→ Platforms
→ Technologies
→ Sites / failure domains
```

sans dépendre d’un PowerPoint externe pour comprendre les relations structurantes.
