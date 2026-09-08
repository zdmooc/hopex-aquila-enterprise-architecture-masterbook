# 12 — MayaBank Information & Data Reference Model

## 1. Objectif

Construire un modèle de référence suffisamment riche pour servir :

- de fil rouge HOPEX Information Architecture / Data Governance ;
- de support d’entretien ;
- d’exercice de modélisation ;
- de base de lineage ;
- de support à une transformation payments ;
- de point de jonction avec les Parties VIII et X.

Le cas est fictif.

## 2. Data Domains

### Customer

- Customer ;
- Party ;
- Identity ;
- Contact Point ;
- Consent.

### Account

- Account ;
- Balance ;
- Reservation ;
- Account Status.

### Payment

- Payment Instruction ;
- Payment ;
- Payment Status ;
- Clearing Submission ;
- Clearing Result ;
- Reconciliation Item.

### Fraud

- Fraud Context ;
- Fraud Score ;
- Fraud Decision ;
- Alert.

### Reference Data

- Currency ;
- Country ;
- Payment Scheme ;
- Reason Code ;
- Status Code.

## 3. Information Concept Map

```text
Customer
  ├─ owns ─────────────→ Account
  └─ initiates ────────→ Payment

Payment
  ├─ debits ───────────→ Account
  ├─ assessed by ──────→ Fraud Decision
  ├─ submitted through → Clearing Submission
  ├─ receives ─────────→ Clearing Result
  └─ has ──────────────→ Payment Status History
```

## 4. Business Glossary sample

### Payment

Instruction transformed into an executable payment state governed by the Payments domain.

### Payment Status

Current governed state of the payment within the MayaBank payment lifecycle.

### Fraud Decision

Outcome produced by the fraud decisioning capability for a payment context.

### Clearing Result

Result received from the external clearing participant/scheme for a submitted payment.

## 5. Logical model

### Payment

```text
PaymentId
EndToEndId
DebtorAccountId
CreditorReference
Amount
Currency
RequestedAt
CurrentStatus
Scheme
CorrelationId
```

### FraudDecision

```text
FraudDecisionId
PaymentId
Decision
Score
ReasonCode
DecisionTimestamp
ModelOrRuleVersion
```

### PaymentStatusHistory

```text
StatusEventId
PaymentId
PreviousStatus
NewStatus
ReasonCode
ChangedAt
Source
```

## 6. Source-of-truth matrix

| Information | Authoritative application/store | Key consumers |
|---|---|---|
| Customer | Customer Master | Channel, Fraud, Payments |
| Account/Balance | Core Account Service/Store | Payments |
| Payment state | Payment Orchestrator/Store | Channel, Ops, Analytics |
| Fraud Decision | Fraud Service/Store | Payments, Audit |
| Clearing Result | Clearing Gateway + Payment record | Payments, Reconciliation |
| Currency/Scheme | Reference Data Service | Payments, Fraud |

## 7. Application × Data Domain

| Application | Customer | Account | Payment | Fraud | Ref Data |
|---|---:|---:|---:|---:|---:|
| Digital Channel | R | R | C/R | - | R |
| Payment Orchestrator | R | R | C/U | R | R |
| Fraud Decision Service | R | - | R | C/U | R |
| Core Account Service | - | C/U | R | - | R |
| Clearing Gateway | - | - | R/U | - | R |
| Reconciliation Service | - | R | R | - | R |

## 8. CRUD matrix

| Entity | Channel | Orchestrator | Fraud | Core | Clearing | Reconciliation |
|---|---|---|---|---|---|---|
| Payment | C/R | C/R/U | R | R | R/U | R |
| Fraud Decision | - | R | C | - | - | R |
| Payment Status | R | C/U | - | - | U | R |
| Account | R | R | - | C/R/U | - | R |

La matrice est pédagogique et simplifiée.

## 9. Functional lineage — happy path

```text
Payment Instruction
Channel
→ Normalize/Validate
Payment Orchestrator
→ Enrich Fraud Context
Fraud Service
→ Fraud Decision
Payment Orchestrator
→ Create Clearing Submission
Clearing Gateway
→ Clearing Result
Payment Orchestrator
→ Payment Status
Event Streaming
→ Notification / Reconciliation / Analytics
```

## 10. Exception lineage

### Duplicate

```text
Payment Instruction
→ idempotency check
→ known PaymentId/status
→ no second execution
```

### Clearing timeout

```text
Submission
→ timeout
→ status inquiry / retry policy
→ exception state
→ reconciliation
```

### Data inconsistency

```text
Payment Store
≠ Clearing result
→ reconciliation discrepancy
→ operations repair workflow
```

## 11. Critical Data Elements

| CDE | Why critical | Main quality dimension |
|---|---|---|
| PaymentId | correlation/idempotency | uniqueness |
| Amount | financial value | accuracy/validity |
| Currency | processing/routing | validity |
| DebtorAccountId | debit target | accuracy |
| PaymentStatus | customer/ops truth | consistency |
| FraudDecision | risk control | completeness/traceability |
| ClearingResult | final execution | consistency |

## 12. Data quality rules

```text
PaymentId not null and unique
Amount > 0
Currency in approved reference set
Payment Status follows allowed state transitions
Every eligible payment has a fraud decision
Every clearing submission has final result or governed exception
```

## 13. Classification map

### Restricted/Confidential examples

- Customer Identity ;
- account identifiers ;
- payment details ;
- fraud context ;
- authentication context.

### Internal examples

- architecture classification metadata ;
- non-sensitive reference data governance metadata.

Exact classification à adapter à la politique MayaBank fictive ou au client réel.

## 14. Data stores

```text
Customer Master Store
Core Account Store
Payment Operational Store
Fraud Decision Store
Reference Data Store
Event Streaming
Reconciliation Store
Analytics Store
```

## 15. Data contracts

### Payment API

Carries Payment Instruction.

### Fraud Decision API

Carries Fraud Context / Fraud Decision.

### PaymentStatusChanged

Carries Payment Status Event.

### Reconciliation Extract/Event

Carries execution evidence needed to compare states.

## 16. Current state

```text
CRM/Core duplicate customer attributes
Shared DB reads
Payment status duplicated
Nightly status batch
Manual reconciliation
Weak schema ownership
Limited lineage
```

## 17. Target state

```text
Governed domains
+ authoritative sources
+ glossary
+ data contracts
+ event-driven status distribution
+ functional lineage
+ quality monitoring
+ classified critical data
+ controlled retention
+ reconciliation by design
```

## 18. Transition roadmap

### Wave 1 — Discover

- catalog critical data ;
- glossary ;
- owner/steward ;
- current source mapping.

### Wave 2 — Govern

- CDE ;
- quality rules ;
- classifications ;
- lineage ;
- source-of-truth decisions.

### Wave 3 — Decouple

- remove shared DB dependencies ;
- versioned APIs/events ;
- reference data distribution ;
- reconciliation automation.

### Wave 4 — Optimize

- retire duplicates ;
- reduce batch ;
- automate discovery/lineage ;
- optimize quality and retention.

## 19. 12 reference matrices

1. Domain × Information.
2. Information × Owner.
3. Information × Application.
4. Application × Data Domain.
5. Entity × CRUD Application.
6. Information × Classification.
7. CDE × Quality Rule.
8. Data Flow × Producer/Consumer.
9. Contract × Information.
10. Store × Authoritative Responsibility.
11. Data × Risk/Control.
12. Current Issue × Target Initiative.

## 20. 12 reference views

1. Enterprise Data Domain Map.
2. Payment Information Concept Map.
3. Conceptual Data Model.
4. Logical Payment Model.
5. Source-of-Truth View.
6. Functional Data Lineage.
7. Data Flow Diagram.
8. Data Quality Heatmap.
9. Classification/Privacy View.
10. Current Data Architecture.
11. Target Data Architecture.
12. Data Transformation Roadmap.

## 21. Architecture review questions

- quelle donnée est réellement autoritative ?
- quelle duplication est intentionnelle ?
- quels consumers casseront si le schema change ?
- quel CDE manque de contrôle ?
- où le lineage est-il incomplet ?
- quelles données sensibles transitent inutilement ?
- quelles copies doivent être retirées ?
- quelle migration exige reconciliation ?

## 22. Critères de réussite

Le modèle est exploitable si, depuis une information critique, on peut naviguer vers :

```text
Definition
Domain
Owner
Applications
Processes
Models
Flows
Transformations
Stores
Quality rules
Classification
Risks/controls
Target initiatives
```
