# 12 — MayaBank Relationships, Diagrams, Matrices & Views Reference Model

## 1. Objectif

Ce chapitre fournit un **blueprint visuel complet** pour le cas MayaBank Instant Payment.

Il ne crée pas un nouveau modèle parallèle : il réutilise les objets canoniques définis dans les Parties V à X.

## 2. Scope

```text
Business domain : Payments
Primary process : Execute Instant Payment
State           : Current + Target
Environments    : Enterprise logical + PROD dependency focus
Horizon         : 2026 → target 2028 (pédagogique)
```

## 3. Objets business

### Capabilities

```text
Payment Initiation
Payment Execution
Fraud Prevention
Account Servicing
Clearing & Settlement
Customer Notification
Reconciliation
```

### Process

```text
Execute Instant Payment
```

### Key activities

```text
Receive Request
Validate Request
Authenticate
Run Fraud Decision
Check Funds
Send to Clearing
Receive Clearing Result
Update Payment Status
Notify Customer
Reconcile
```

## 4. Applications

```text
Digital Channel
API Management
IAM
Payment Orchestrator
Fraud Decision Service
Core Account Service
Clearing Gateway
Notification Service
Reconciliation Service
Event Streaming Platform
Observability Platform
Legacy Payment Gateway
```

## 5. Key information

```text
Payment Instruction
Customer Identity
Account
Fraud Context
Fraud Decision
Clearing Request
Clearing Result
Payment Status
Audit Record
```

## 6. Platforms / technologies

```text
OpenShift Platform
API Management Platform
Event Streaming Platform
Database Platform
IAM Platform
Observability Platform
Backup & Recovery
Network / Load Balancing
```

## 7. Transformation objects

```text
Payment Modernization Program
Legacy Gateway Retirement
Event-Driven Status Initiative
Observability Improvement
```

## 8. Core relationship chain

```text
Payment Execution Capability
↑ supported by
Execute Instant Payment
↑ automated by
Payment Orchestrator
├─ consumes → Fraud Decision Service
├─ consumes → Core Account Service
├─ consumes → Clearing Gateway
├─ publishes → PaymentStatusChanged
├─ runs on → OpenShift Platform
└─ owned by → Payments IT
```

## 9. Application cooperation — current

```text
Customer
  ↓
Digital Channel
  ↓
Legacy Payment Gateway
  ├→ Fraud Engine
  ├→ Core Account
  ├→ Clearing Adapter
  └→ Notification
```

Pain points :

- synchronous chain ;
- concentrated responsibility ;
- legacy middleware ;
- unclear ownership of some flows ;
- notification coupled to core execution.

## 10. Application cooperation — target

```text
Customer
  ↓
Digital Channel
  ↓
API Management
  ↓
Payment Orchestrator
  ├→ IAM
  ├→ Fraud Decision Service
  ├→ Core Account Service
  └→ Clearing Gateway
        ↓
Payment Status
        ↓
PaymentStatusChanged
        ↓
Event Streaming
  ├→ Notification Service
  ├→ Reconciliation Service
  └→ Analytics consumers
```

## 11. Business-to-application view

```text
Payment Initiation
→ Digital Channel / API Management

Payment Execution
→ Payment Orchestrator / Core Account / Clearing Gateway

Fraud Prevention
→ Fraud Decision Service

Customer Notification
→ Notification Service

Reconciliation
→ Reconciliation Service
```

## 12. Application-to-data view

```text
Digital Channel
→ creates Payment Instruction

Payment Orchestrator
→ creates/updates Payment Status

Fraud Service
→ creates Fraud Decision

Clearing Gateway
→ creates Clearing Result

Notification
→ reads Payment Status

Reconciliation
→ reads Payment Status + Clearing Result
```

## 13. Application-to-technology view

```text
Payment Orchestrator
→ OpenShift
→ Java runtime
→ PostgreSQL
→ Event Streaming
→ IAM
→ Observability
```

Ne pas montrer chaque node/pod dans cette vue entreprise.

## 14. Critical dependency view

```text
Digital Channel
→ API Management
→ Payment Orchestrator
→ IAM
→ Fraud Decision Service
→ Core Account Service
→ Clearing Gateway
```

Side effects :

```text
PaymentStatusChanged
→ Notification
→ Reconciliation
```

La vue doit distinguer le chemin financier critique et les traitements asynchrones.

## 15. Failure-domain view

```text
External
→ Edge / Load Balancer
→ API Management
→ OpenShift Platform
→ Payment workloads
→ Data services
→ Clearing connectivity
```

Services transverses :

```text
DNS
IAM
PKI/Secrets
Observability
Backup
```

## 16. Current / Target delta

### Retire

```text
Legacy Payment Gateway
legacy point-to-point notification coupling
manual status reconciliation patterns
```

### Add

```text
Payment Orchestrator
Event-driven status
central API Management governance
improved observability
```

### Keep / integrate

```text
Core Account Service
Fraud Decision capability
Clearing connectivity
```

## 17. Transformation view

```text
Wave 1 — Observability & correlation
Wave 2 — API Management + Orchestrator
Wave 3 — Event-driven status + Notification decoupling
Wave 4 — Legacy Gateway retirement
Wave 5 — Optimization / decommission
```

## 18. Matrix 1 — Capability × Application

| Capability | Channel | API Mgmt | Orchestrator | Fraud | Core | Clearing | Notification | Reconciliation |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Payment Initiation | X | X |  |  |  |  |  |  |
| Payment Execution |  |  | X | X | X | X |  |  |
| Fraud Prevention |  |  |  | X |  |  |  |  |
| Notification |  |  |  |  |  |  | X |  |
| Reconciliation |  |  |  |  | X | X |  | X |

## 19. Matrix 2 — Process Activity × Application

| Activity | Main application |
|---|---|
| Receive Request | Digital Channel |
| Validate | Payment Orchestrator |
| Authenticate | IAM / Channel |
| Fraud Decision | Fraud Decision Service |
| Funds Check | Core Account Service |
| Clearing | Clearing Gateway |
| Update Status | Payment Orchestrator |
| Notify | Notification Service |
| Reconcile | Reconciliation Service |

## 20. Matrix 3 — Application × Technology

| Application | OpenShift | Kafka | PostgreSQL | Oracle/Core | IAM | API Mgmt |
|---|---:|---:|---:|---:|---:|---:|
| Payment Orchestrator | X | X | X |  | X | X |
| Fraud Service | X |  |  |  | X | X |
| Core Account |  |  |  | X |  |  |
| Notification | X | X |  |  |  |  |
| Reconciliation | X | X | X | X |  |  |

## 21. Matrix 4 — Application × Information

| Application | Payment Instruction | Payment Status | Fraud Decision | Clearing Result |
|---|---|---|---|---|
| Orchestrator | C/R | C/U/R | R | R |
| Fraud Service | R |  | C |  |
| Clearing Gateway | R |  |  | C |
| Notification |  | R |  |  |
| Reconciliation |  | R |  | R |

## 22. Matrix 5 — Risk × Control

| Risk | Control |
|---|---|
| Duplicate execution | Idempotency |
| Unauthorized initiation | Authentication/Authorization |
| Fraudulent payment | Fraud Decision |
| Clearing timeout | Timeout/Retry/Inquiry |
| Lost traceability | Correlation/Audit |
| Event loss | Durable messaging / monitoring |

## 23. Matrix 6 — Initiative × Object

| Initiative | Main impacted objects |
|---|---|
| Payment Modernization | Legacy Gateway, Orchestrator, API Mgmt |
| Event-Driven Status | Orchestrator, Kafka, Notification, Reconciliation |
| Observability Improvement | All critical payment applications |
| Legacy Retirement | Legacy Gateway + consumers/interfaces |

## 24. Matrix 7 — Application × Owner

| Application | Owner |
|---|---|
| Payment Orchestrator | Payments IT |
| Fraud Service | Fraud IT |
| Core Account | Core Banking IT |
| Clearing Gateway | Payments Integration |
| Event Streaming | Platform Engineering |

## 25. Matrix 8 — Relationship confidence

| Relation family | Target confidence |
|---|---|
| Business support | Verified by domain owner |
| App dependencies | Verified / discovered + validated |
| Deployment | authoritative platform/CMDB source |
| Technology lifecycle | external evidence + internal governance |

## 26. View library MayaBank

### V01 — Executive Payment Transformation
Audience : Steering Committee.

### V02 — Payment Capability/Application
Audience : Business + EA.

### V03 — Instant Payment Process/Application
Audience : Process + Solution Architecture.

### V04 — Application Cooperation Current
Audience : Architects.

### V05 — Application Cooperation Target
Audience : Architects.

### V06 — Application/Data Responsibilities
Audience : Data + Solution Architects.

### V07 — Application/Technology Dependencies
Audience : Technology Architecture.

### V08 — Critical Path & Failure Domains
Audience : SRE / Resilience.

### V09 — Risk/Control Architecture
Audience : Risk / Architecture.

### V10 — Current/Target Delta
Audience : Architecture Board.

### V11 — Transformation Waves
Audience : Program / Architecture.

### V12 — Relationship Quality
Audience : Repository Stewards.

## 27. Visual conventions MayaBank

Pédagogiques :

```text
Top      = business
Middle   = applications
Bottom   = platforms/technologies
Right    = risks/initiatives when needed
Dashed   = target/planned
Label    = relation semantics on critical links
```

Les couleurs ne sont pas définies ici afin de rester compatibles avec les conventions client et l’accessibilité.

## 28. Saved scopes

```text
PAYMENTS-CURRENT-PROD
PAYMENTS-TARGET-2028
PAYMENTS-CRITICAL-DEPENDENCIES
PAYMENTS-LEGACY-RETIREMENT
PAYMENTS-RELATIONSHIP-QUALITY
```

## 29. Review cycle

Chaque vue publiée doit préciser :

- owner ;
- status ;
- snapshot date ;
- scope ;
- known limitations ;
- next review.

## 30. Critères de réussite

Le modèle est exploitable si l’on peut répondre sans reconstruire manuellement un PowerPoint à :

1. quelles applications supportent Payment Execution ?
2. quelles technologies supportent ces applications ?
3. quelles données critiques circulent ?
4. quelles relations sont douteuses ?
5. quel est le blast radius de Legacy Gateway ?
6. que change la cible ?
7. quelles initiatives réalisent la transformation ?
8. quels risques/contrôles sont associés ?
9. quelle vue présenter à chaque stakeholder ?
10. quelle matrice utiliser pour vérifier la couverture ?