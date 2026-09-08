# 12 — MayaBank Enterprise Cartography & Dependency Reference Model

## 1. Objectif

Ce chapitre consolide un modèle pédagogique complet permettant d’exécuter les analyses de la Partie XII sur un cas bancaire cohérent.

Le modèle relie :

```text
Business
→ Processes
→ Applications
→ Interfaces / Events
→ Information
→ Platforms
→ Technologies
→ Risks / Controls
→ Initiatives
```

Il ne prétend pas refléter un établissement réel.

---

## 2. Business domains

```text
Customer
Payments
Accounts
Fraud & Financial Crime
Operations
Compliance
Data
Shared Technology Platforms
```

---

## 3. Capabilities de référence

### Payments

```text
Payment Initiation
Payment Validation
Payment Execution
Payment Clearing
Payment Reconciliation
Payment Status Management
```

### Fraud

```text
Fraud Detection
Fraud Decisioning
Fraud Investigation
```

### Customer

```text
Customer Identification
Customer Authentication
Customer Communication
```

### Operations

```text
Incident Management
Payment Operations
Reconciliation Operations
```

---

## 4. Process de référence

Process principal :

```text
Execute Instant Payment
```

Sous-chaîne pédagogique :

```text
Receive Payment Request
Authenticate Customer
Validate Payment
Run Fraud Check
Reserve/Debit Funds
Send Clearing Instruction
Receive Clearing Result
Update Payment Status
Publish Payment Event
Notify Customer
Reconcile Payment
```

---

## 5. Applications canoniques

1. Digital Channel
2. API Management
3. IAM
4. Payment Orchestrator
5. Fraud Decision Service
6. Core Account Service
7. Clearing Gateway
8. Event Streaming Platform
9. Notification Service
10. Reconciliation Service
11. Observability Platform
12. Legacy Payment Gateway

---

## 6. External services

```text
External Clearing Service
External Notification Provider
Certificate Authority
Telecom / Network Provider
Optional External Fraud Data Feed
```

---

## 7. Information objects

```text
Customer Identity
Payment Instruction
Payment Execution State
Payment Status
Fraud Context
Fraud Decision
Account Balance
Clearing Instruction
Clearing Result
Reconciliation Item
Notification Request
Audit Evidence
```

---

## 8. Platforms

```text
OpenShift Platform
API Management Platform
IAM Platform
Event Streaming Platform
Relational Database Platform
Observability Platform
Backup & Recovery Platform
Network Services
PKI / Secrets Services
```

---

## 9. Application dependency map

```text
Digital Channel
→ API Management
→ Payment Orchestrator

Payment Orchestrator
├→ IAM
├→ Fraud Decision Service
├→ Core Account Service
├→ Clearing Gateway
└→ Event Streaming

Event Streaming
├→ Notification Service
├→ Reconciliation Service
└→ Analytics/operational consumers
```

---

## 10. Critical synchronous chain

Pédagogique :

```text
Digital Channel
→ API Management
→ Payment Orchestrator
→ Fraud Decision Service
→ Core Account Service
→ Clearing Gateway
→ External Clearing Service
```

Le design réel peut paralléliser ou ordonner différemment certaines étapes.

---

## 11. Asynchronous chain

```text
Payment Orchestrator
→ PaymentStatusChanged
→ Event Streaming
├→ Notification Service
├→ Reconciliation Service
└→ Analytics
```

---

## 12. Data dependency map

```text
Payment Instruction
→ Payment Orchestrator

Customer Identity
→ IAM / Payment / Fraud context

Fraud Decision
→ Fraud Decision Service
→ Payment Orchestrator

Clearing Result
→ Clearing Gateway
→ Payment Orchestrator

Payment Status
→ Notification / Reconciliation / Operations
```

---

## 13. Source-of-truth mapping

Pédagogique :

| Information | Authoritative responsibility |
|---|---|
| Customer Identity | Customer/IAM domain as governed |
| Account Balance | Core Account Service/domain |
| Payment Execution State | Payment Orchestrator |
| Fraud Decision | Fraud Decision Service |
| Clearing Result | Clearing Gateway captures external result |
| Reconciliation Item | Reconciliation Service |

Le modèle exact doit suivre la gouvernance data réelle.

---

## 14. Application → Platform

| Application | Platform |
|---|---|
| Payment Orchestrator | OpenShift |
| Fraud Decision Service | OpenShift |
| Clearing Gateway | OpenShift or governed runtime |
| Notification | OpenShift |
| Reconciliation | OpenShift / data platform |
| Event Streaming | Event Streaming Platform |
| IAM | IAM Platform |
| API Management | API Management Platform |

---

## 15. Platform shared dependencies

```text
OpenShift
→ Network
→ IAM integration
→ Storage
→ DNS
→ Observability
→ Backup/DR where applicable

Event Streaming
→ Network
→ Storage
→ IAM/PKI
→ Observability
```

---

## 16. Cross-domain dependencies

```text
Payments → Fraud
Payments → Accounts
Payments → Customer/IAM
Payments → Compliance Controls
Payments → Operations
Payments → Shared Platforms
Payments → External Clearing
```

---

## 17. Business-to-technology traceability

Example chain :

```text
Real-Time Payment Capability
→ Execute Instant Payment
→ Payment Orchestrator
→ OpenShift Platform
→ Network / Storage / IAM
```

Autre :

```text
Fraud Decisioning Capability
→ Run Fraud Check
→ Fraud Decision Service
→ OpenShift / Fraud Data / IAM
```

---

## 18. Critical dependency register

| Consumer | Dependency | Type | Effect if lost | Fallback |
|---|---|---|---|---|
| Payment Orchestrator | IAM | security/runtime | transaction access blocked | client-defined |
| Payment Orchestrator | Core Account | functional | payment execution blocked | client-defined |
| Payment Orchestrator | Fraud Service | control | fraud decision unavailable | risk-defined |
| Clearing Gateway | External Clearing | external | clearing blocked | scheme-defined |
| Notification | Event Streaming | async | notification delayed | replay possible |
| Reconciliation | Event Streaming/Data | async/data | reconciliation delayed | batch/manual possible |

---

## 19. Hard vs soft dependencies

### Likely hard in teaching model

```text
IAM
Core Account
Fraud Decision
Clearing
```

### Potentially degradable

```text
Notification
Analytics
Some reporting
```

Le statut doit être validé par business/risk.

---

## 20. Hub candidates

```text
IAM
API Management
Event Streaming
OpenShift
Core Account Service
```

Ils sont candidats à revue, pas automatiquement SPOF.

---

## 21. Bridge candidate

```text
Clearing Gateway
```

Il relie potentiellement le domaine interne au clearing externe.

À vérifier :

- nombre de chemins ;
- secondary endpoints ;
- alternate routes ;
- scheme fallback.

---

## 22. SPOF candidates

Questions :

```text
Single IAM control plane?
Single DNS dependency?
Single clearing route?
Single shared DB?
Single certificate path?
Single network ingress?
```

Ne jamais affirmer le SPOF sans analyser le failure mode réel.

---

## 23. Risk/control dependency

Exemple :

```text
Duplicate Payment Risk
→ Idempotency Control
→ Payment Orchestrator
→ Idempotency / Payment State Store
```

Exemple :

```text
Fraud Risk
→ Fraud Decision Control
→ Fraud Decision Service
```

---

## 24. Observability dependency

```text
Payment flow
→ metrics
→ logs
→ traces
→ correlation id
→ operational dashboard
```

Pour incident/recovery : Observability Platform devient dépendance d’exploitation.

---

## 25. Current architecture pédagogique

```text
Digital Channel
→ Legacy Payment Gateway
→ shared integrations
→ Core
→ Legacy Clearing Adapter
→ synchronous downstream notification

Shared DB
VM-heavy deployment
Batch reconciliation
Fragmented observability
```

---

## 26. Target architecture pédagogique

```text
Digital Channel
→ API Management
→ Payment Orchestrator
   ├→ IAM
   ├→ Fraud Decision Service
   ├→ Core Account Service
   └→ Clearing Gateway

PaymentStatusChanged
→ Event Streaming
   ├→ Notification
   ├→ Reconciliation
   └→ Analytics

OpenShift
Governed data
Central observability
Tested DR
```

---

## 27. Current → Target dependency delta

### Dependencies removed

```text
Direct consumer → Legacy Gateway
Shared DB coupling where redesigned
Synchronous notification dependency
```

### Dependencies introduced

```text
API Management
OpenShift
Event Streaming
New IAM/service identity paths
```

Modernization déplace le risque ; elle ne le supprime pas.

---

## 28. Transition state T1

```text
API Management
→ router/façade
├→ Legacy Payment Gateway
└→ Payment Orchestrator for selected flow
```

Nouvelles dépendances temporaires : routing, dual observability.

---

## 29. Transition state T2

```text
Payment Orchestrator active
Legacy Clearing still used through adapter
Event Streaming added for downstream
```

---

## 30. Transition state T3

```text
Clearing Gateway active
Legacy Gateway only residual consumers
Data synchronization temporary
```

---

## 31. Transition state T4

```text
All consumers migrated
Legacy interfaces retired
Legacy data archived/migrated
Legacy Gateway decommissioned
```

---

## 32. Migration units

### Unit A — channel/API

```text
Digital Channel
API Management
```

### Unit B — orchestration/control

```text
Payment Orchestrator
Fraud integration
IAM
```

### Unit C — clearing

```text
Clearing Gateway
Partner connectivity
PKI
```

### Unit D — asynchronous downstream

```text
Event Streaming
Notification
Reconciliation
```

---

## 33. Dependency matrix 1 — Application × Application

| Consumer | API Mgmt | IAM | Orchestrator | Fraud | Core | Clearing | Kafka |
|---|---:|---:|---:|---:|---:|---:|---:|
| Digital Channel | X |  | X via API |  |  |  |  |
| Payment Orchestrator |  | X |  | X | X | X | X |
| Notification |  |  |  |  |  |  | X |
| Reconciliation |  |  |  |  |  |  | X |

---

## 34. Dependency matrix 2 — Application × Information

| Application | Payment Instruction | Payment Status | Fraud Decision | Clearing Result |
|---|---:|---:|---:|---:|
| Orchestrator | C/U | C/U | R | U |
| Fraud Service | R |  | C |  |
| Clearing Gateway | R |  |  | C |
| Notification |  | R |  |  |
| Reconciliation | R | R |  | R |

CRUD pédagogique.

---

## 35. Dependency matrix 3 — Application × Platform

| Application | OCP | IAM | API Mgmt | Kafka | DB | Observability |
|---|---:|---:|---:|---:|---:|---:|
| Orchestrator | X | X | X | X | X | X |
| Fraud | X | X |  |  | X | X |
| Clearing | X | X/PKI |  | X | X | X |
| Notification | X | X |  | X | X | X |

---

## 36. Dependency matrix 4 — Process × Application

| Process activity | Channel | Orchestrator | Fraud | Core | Clearing | Notification |
|---|---:|---:|---:|---:|---:|---:|
| Receive | X | X |  |  |  |  |
| Fraud Check |  | X | X |  |  |  |
| Debit |  | X |  | X |  |  |
| Clear |  | X |  |  | X |  |
| Notify |  |  |  |  |  | X |

---

## 37. Dependency matrix 5 — Risk × Control × Implementation

| Risk | Control | Implementation |
|---|---|---|
| Duplicate payment | Idempotency | Orchestrator + state store |
| Fraud | Fraud decision | Fraud Service |
| Unauthorized payment | Authentication/authorization | IAM + API/Application controls |
| Missing settlement | Reconciliation | Recon Service |

---

## 38. Recovery dependency map

Pédagogique :

```text
Network / DNS / IAM / PKI
→ Data platforms
→ OpenShift
→ Core/Fraud
→ Payment Orchestrator
→ Clearing
→ Event Streaming
→ downstream consumers
```

À adapter selon architecture réelle.

---

## 39. Scenario A — IAM outage

### Direct

```text
API Management
Payment Orchestrator
Fraud Service
Operational access
```

### Business exposure

```text
Payment initiation/execution
Fraud decisioning
Operations
```

### Questions

- local token validation ?
- cached sessions ?
- service identity ?
- privileged recovery access ?
- multi-site IAM ?

---

## 40. Scenario B — Kafka outage

### Direct consumers/producers

```text
Payment Orchestrator
Notification
Reconciliation
Analytics
```

### Effects

```text
Event publication backlog
Notification delay
Reconciliation delay
Replay/recovery need
```

---

## 41. Scenario C — Clearing outage

```text
External Clearing
→ Clearing Gateway
→ Payment Orchestrator
→ Execute Instant Payment
```

Questions :

- queue allowed ?
- immediate reject ?
- timeout ?
- alternative route ?
- customer status ?

---

## 42. Scenario D — OpenShift outage

```text
OpenShift
→ hosted payment applications
→ payment/fraud/notification functions
→ business services
```

Le blast radius dépend de la répartition réelle des workloads.

---

## 43. Scenario E — Payment Status schema change

```text
Payment Status
→ event schema
→ Notification
→ Reconciliation
→ Operations / Analytics
```

Plan : consumer inventory, compatibility, dual-version, retirement.

---

## 44. Scenario F — Legacy Gateway retirement

```text
Legacy Gateway
→ consumers
→ interfaces
→ data
→ processes
→ target replacements
```

Go/no-go : aucun consumer critique inconnu.

---

## 45. Twelve reference views

1. Enterprise Domain Map.
2. Payment Context Map.
3. Business-to-Technology Traceability.
4. Application Dependency Map.
5. Data Dependency Map.
6. Shared Platform Hub Map.
7. Critical Dependency Path.
8. Blast Radius View.
9. Recovery Dependency View.
10. Current/Target Dependency Delta.
11. Migration Wave Map.
12. Dependency Quality Map.

---

## 46. Twelve reference matrices

1. Domain × Domain Dependency.
2. Capability × Application.
3. Process × Application.
4. Application × Application.
5. Application × Interface.
6. Application × Information.
7. Application × Platform.
8. Platform × Technology.
9. Risk × Control.
10. Dependency × Owner.
11. Dependency × Confidence.
12. Initiative × Impacted Object.

---

## 47. Quality gates

Le modèle MayaBank est considéré exploitable si :

- chaque application critique a un owner ;
- chaque dependency critique a une rationale ;
- external dependencies sont présentes ;
- current/target sont distingués ;
- les dépendances temporaires ont une retirement condition ;
- source/confidence sont suivies ;
- les vues critiques sont revues.

---

## 48. Questions d’Architecture Board

1. Quel est le business service protégé ?
2. Quelles sont les hard dependencies ?
3. Quel shared service concentre le plus de risques ?
4. Où sont les unknown consumers ?
5. Quel path n’a pas de fallback ?
6. Quel élément n’a jamais été testé en DR ?
7. Quelle dépendance temporary risque de devenir permanente ?
8. Quel objet target dépend encore d’un composant retired ?

---

## 49. Definition of Done MayaBank

```text
Traceable
Scoped
Current/Target separated
Critical paths known
Shared dependencies reviewed
External dependencies visible
Recovery order defined
Migration dependencies sequenced
Unknowns explicit
Owners assigned
```

---

## 50. Anti-patterns

- modèle de référence pris pour un produit bancaire réel ;
- criticités pédagogiques copiées sans validation ;
- toutes les plateformes déclarées SPOF ;
- target présenté comme déjà déployé ;
- migration waves utilisées sans dépendances réelles ;
- dependency matrices maintenues séparément du repository.

---

## 51. Questions d’entretien

**Quel est le chemin métier-technique principal MayaBank ?**  
Capability → Process → Payment Orchestrator → services métier critiques → plateformes/technologies.

**Quel est le principal changement architectural du target ?**  
Séparer orchestration, services de domaine et downstream asynchronous, tout en rendant explicites les shared platforms.

**Moderniser réduit-il automatiquement le nombre de dépendances ?**  
Non. On remplace souvent des dépendances legacy par des dépendances de plateformes partagées qu’il faut gouverner et rendre résilientes.
