# 12 — MayaBank : modèle applicatif de référence complet

## 1. Objectif

Ce chapitre rassemble le cas fil rouge Application Architecture dans un modèle cohérent, exploitable pour :

- apprendre HOPEX ;
- préparer un entretien ;
- simuler une mission banque ;
- construire des matrices ;
- pratiquer impact analysis ;
- produire current/target ;
- préparer les Parties IX et X.

Toutes les données MayaBank sont fictives.

## 2. Domaine fonctionnel

Périmètre : `Instant Payments`.

Capabilities principales :

```text
Customer Access
Identity & Access
Payment Initiation
Payment Execution
Fraud Prevention
Account Servicing
Clearing
Customer Communication
Reconciliation
Observability
```

## 3. Applications de référence

### A01 — Digital Channel

Responsabilité : interaction client web/mobile et initiation de paiement.

Expose/consomme :

- customer UI ;
- Payment Initiation API ;
- Payment Status API ;
- IAM services.

### A02 — API Management

Responsabilité : exposition contrôlée et gouvernance des APIs.

N’assume pas la logique métier du paiement.

### A03 — IAM

Responsabilité : authentication, authorization et service identities selon architecture sécurité.

### A04 — Payment Orchestrator

Responsabilité :

```text
validate execution request
maintain execution state
coordinate fraud/funds/clearing
manage timeout/technical retry policy
expose payment execution status
publish status changes
```

### A05 — Fraud Decision Service

Responsabilité : produire une décision de fraude à partir du contexte reçu.

### A06 — Core Account Service

Responsabilité : exposer les services nécessaires sur compte/fonds et opérations de core banking dans le scope retenu.

### A07 — Clearing Gateway

Responsabilité : adapter et sécuriser la connexion au réseau/système de clearing.

### A08 — Event Streaming

Responsabilité : plateforme de distribution d’événements.

### A09 — Notification Service

Responsabilité : livraison multicanale des notifications.

### A10 — Reconciliation Service

Responsabilité : détecter les écarts entre états/transactions attendus et observés.

### A11 — Observability Platform

Responsabilité : collecte/corrélation metrics, logs, traces et signaux opérationnels.

### A12 — Legacy Payment Hub

Responsabilité actuelle : orchestration historique des paiements.

Cible : retrait après migration.

## 4. Application catalog

| ID | Application | Domain | Current/Target | Criticality |
|---|---|---|---|---|
| A01 | Digital Channel | Customer | both | High |
| A02 | API Management | Integration | target | Critical |
| A03 | IAM | Security | both | Critical |
| A04 | Payment Orchestrator | Payments | target | Critical |
| A05 | Fraud Decision Service | Fraud | target | Critical |
| A06 | Core Account Service | Accounts | both | Critical |
| A07 | Clearing Gateway | Payments | target | Critical |
| A08 | Event Streaming | Integration | target | Critical |
| A09 | Notification Service | Shared | target | High |
| A10 | Reconciliation Service | Operations | target | High |
| A11 | Observability Platform | Platform | target | High |
| A12 | Legacy Payment Hub | Payments | current/sunset | Critical |

## 5. Capability × Application Matrix

| Capability | A01 | A03 | A04 | A05 | A06 | A07 | A09 | A10 |
|---|---|---|---|---|---|---|---|---|
| Customer Access | X |  |  |  |  |  | X |  |
| Identity & Access |  | X |  |  |  |  |  |  |
| Payment Initiation | X |  | X |  |  |  |  |  |
| Payment Execution |  |  | X |  | X | X |  |  |
| Fraud Prevention |  |  | X | X |  |  |  |  |
| Account Servicing |  |  | X |  | X |  |  |  |
| Clearing |  |  | X |  |  | X |  |  |
| Customer Communication | X |  |  |  |  |  | X |  |
| Reconciliation |  |  |  |  | X | X |  | X |

## 6. Process Activity × Application

| Activity | Primary Application | Supporting |
|---|---|---|
| Initiate Payment | Digital Channel | API Management |
| Authenticate | IAM | Digital Channel |
| Validate Payment | Payment Orchestrator | — |
| Fraud Check | Fraud Decision Service | Payment Orchestrator |
| Funds Check | Core Account Service | Payment Orchestrator |
| Send Clearing | Clearing Gateway | Payment Orchestrator |
| Maintain Status | Payment Orchestrator | — |
| Notify Customer | Notification Service | Event Streaming |
| Reconcile | Reconciliation Service | Clearing/Core/Event Streaming |

## 7. Application interaction view

```text
Customer
  |
  v
Digital Channel
  |
  v
API Management
  |
  v
Payment Orchestrator
  |       |        |
  v       v        v
IAM     Fraud     Core Account
                   |
Payment Orchestrator
        |
        v
Clearing Gateway
        |
        v
External Clearing Network

Payment Orchestrator
        |
        v
Event Streaming
   |         |           |
   v         v           v
Notify   Reconcile   Analytics/Other Consumers
```

## 8. Interface catalogue

### I01 — Payment Initiation API

Provider : Payment Orchestrator via API Management.

Consumer : Digital Channel.

Information : Payment Instruction.

Style : synchronous API.

### I02 — Fraud Decision API

Provider : Fraud Decision Service.

Consumer : Payment Orchestrator.

Information : Fraud Context / Decision.

Style : synchronous API.

### I03 — Funds Check API

Provider : Core Account Service.

Consumer : Payment Orchestrator.

### I04 — Clearing Submission Interface

Provider/consumer relation : Payment Orchestrator ↔ Clearing Gateway.

Style exact : scenario-dependent API/messaging.

### I05 — Payment Status API

Provider : Payment Orchestrator.

Consumer : Digital Channel.

### I06 — PaymentStatusChanged Event

Producer : Payment Orchestrator.

Broker/platform : Event Streaming.

Consumers : Notification Service, Reconciliation Service, analytics.

## 9. Interface quality attributes

Pour chaque interface :

```text
owner
version
authentication
timeout
error model
idempotency
availability
payload classification
deprecation
```

## 10. Information model

Objets d’information principaux :

```text
Payment Instruction
Authentication Context
Fraud Context
Fraud Decision
Account/Funds Result
Clearing Request
Clearing Result
Payment Execution State
Payment Status
Notification Request
Reconciliation Record
Audit Record
```

## 11. Data responsibility

| Information | Primary responsibility |
|---|---|
| Payment Instruction | Payment Orchestrator |
| Authentication Context | IAM / Channel context |
| Fraud Decision | Fraud Decision Service |
| Account/Funds | Core Account Service |
| Clearing Result | Clearing Gateway ingress + Payment Orchestrator state |
| Payment Status | Payment Orchestrator |
| Notification Record | Notification Service |
| Reconciliation Record | Reconciliation Service |

## 12. Deployment target

```text
Digital/API applications
→ OpenShift / managed edge components

Payment Orchestrator
Fraud Decision Service
Notification Service
Reconciliation Service
→ OpenShift

Event Streaming
→ resilient Kafka/event platform

Core Account Service
→ core banking platform

Clearing Gateway
→ controlled integration zone
```

Les choix détaillés sont pédagogiques et seront approfondis en Partie X.

## 13. OpenShift view

Conceptuellement :

```text
OpenShift PROD
├─ namespace payments
│  └─ Payment Orchestrator
├─ namespace fraud
│  └─ Fraud Decision Service
├─ namespace notifications
│  └─ Notification Service
└─ namespace operations
   └─ Reconciliation Service
```

Un objet namespace n’est pas une application canonique.

## 14. NFR priorities

### Payment Orchestrator

- high availability ;
- low latency ;
- idempotency ;
- strong auditability ;
- multi-site recovery ;
- end-to-end correlation.

### Fraud Decision Service

- strict decision latency ;
- high availability ;
- sensitive data ;
- explainability/audit requirements according to actual use case.

### Notification Service

- asynchronous throughput ;
- retry/replay ;
- channel isolation ;
- personal data controls.

## 15. Critical dependency graph

```text
Payment Orchestrator
├─ IAM
├─ Fraud Decision Service
├─ Core Account Service
└─ Clearing Gateway
```

Event Streaming est critique pour propagation et services downstream, mais la politique cible cherche à éviter qu’une panne de notification ne compromette un paiement finalisé.

## 16. Risk map

| Risk | Application area | Architecture response |
|---|---|---|
| duplicate execution | Payment Orchestrator | idempotency/state machine |
| fraud service unavailable | Fraud/Payments | approved fail policy + resilience |
| clearing timeout | Clearing/Payments | timeout/status inquiry/reconciliation |
| inconsistent state | Payments/Data | state model + reconciliation |
| notification outage | Notification | async event + retry/replay |
| lost traceability | all | correlation + audit logging |
| platform outage | OpenShift/platform | multi-zone/site recovery |

## 17. Current state

```text
Digital Channel
→ Legacy Payment Hub
→ Fraud appliance
→ Core system
→ legacy clearing adapter
→ synchronous notification

Shared DB
Batch reconciliation
VMs
```

## 18. Target state

```text
Digital Channel
→ API Management
→ Payment Orchestrator
   ├→ IAM
   ├→ Fraud Decision Service
   ├→ Core Account Service
   └→ Clearing Gateway

Status changes
→ Event Streaming
→ Notification + Reconciliation + Analytics
```

## 19. Transition state 1

- inventory legacy dependencies ;
- canonical correlation ID ;
- API façade ;
- observability ;
- current application retained.

## 20. Transition state 2

- new orchestrator ;
- adapters to legacy core/clearing ;
- new fraud contract ;
- controlled traffic migration.

## 21. Transition state 3

- event-driven notification ;
- target reconciliation ;
- data separation ;
- legacy consumers migration.

## 22. Transition state 4

- archive/migrate data ;
- remove direct DB ;
- stop batch legacy ;
- retire Legacy Payment Hub.

## 23. Repository relations à maintenir

Pour `Payment Orchestrator` :

```text
supports → Payment Execution capability
supports → Execute Instant Payment process
provides → Payment Initiation / Status services
consumes → Fraud/Funds/Clearing services
produces → PaymentStatusChanged
manages → Payment Execution State
uses → OpenShift / Java / event platform
participates in → Instant Payment business service
impacted by → modernization initiatives
```

La syntaxe exacte des relations dépend du métamodèle HOPEX.

## 24. Matrices obligatoires du cas

1. Application × Capability.
2. Activity × Application.
3. Application × Application dependency.
4. Application × Interface.
5. Application × Information.
6. Application × Data Store.
7. Application × Technology.
8. Application × Platform/Deployment.
9. Application × NFR.
10. Application × Initiative.

## 25. Vues obligatoires

1. Application Landscape.
2. Application Cooperation.
3. Interface/Flow View.
4. Critical Dependency Graph.
5. Deployment View.
6. Data Responsibility View.
7. NFR/Resilience View.
8. Current Architecture.
9. Transition Architecture.
10. Target Architecture.

## 26. Questions de revue

- chaque application a-t-elle une responsabilité unique ?
- les providers/consumers sont-ils identifiés ?
- les flux critiques sont-ils gouvernés ?
- les data owners/sources of truth sont-ils visibles ?
- les dépendances synchrones critiques sont-elles justifiées ?
- les NFR sont-ils tracés jusqu’aux mécanismes ?
- les failure domains sont-ils compris ?
- la cible possède-t-elle une trajectoire de migration ?
- le legacy possède-t-il un plan de retrait réaliste ?

## 27. Critère de réussite

Le modèle est exploitable lorsque l’on peut partir d’une application et répondre, sans reconstituer manuellement plusieurs PowerPoint :

```text
Pourquoi existe-t-elle ?
Qui la possède ?
Qui dépend d’elle ?
De quoi dépend-elle ?
Quelles données porte-t-elle ?
Où tourne-t-elle ?
Quels NFR la structurent ?
Quel est son état actuel ?
Quelle est sa cible ?
Quel changement la transforme ?
```
