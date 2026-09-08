# 06 — MayaBank Instant Payment : modèle de processus end-to-end

## 1. Objectif

Construire un modèle de référence suffisamment détaillé pour servir :

- d'exercice HOPEX BPA ;
- de support d'entretien ;
- de base de mapping Process/Application/Data/Risk ;
- de support à une architecture cible ;
- de cas de simulation et d'amélioration.

Le cas est fictif.

## 2. Scope

Début : le client soumet une instruction de paiement instantané.

Fin : le client reçoit un statut final ou l'opération est placée dans un traitement d'exception gouverné.

Hors scope :

- détail du ledger comptable ;
- processus KYC complet ;
- règlement interbancaire détaillé ;
- implémentation technique de chaque microservice.

## 3. Participants

```text
Customer
Digital Channel
Payments Domain
Fraud Domain
Clearing Network
Operations
Platform/SRE
```

## 4. Happy path

### P01 — Receive Payment Request

Entrée : Payment Instruction.

Résultat : demande acceptée pour validation.

### P02 — Validate Request

Contrôles :

- mandatory fields ;
- format ;
- payment scheme constraints ;
- duplicate/idempotency key.

### P03 — Authenticate / Authorize

Vérifie que l'action est autorisée selon canal et contexte.

### P04 — Run Fraud Decision

Sortie : Approve / Reject / Review selon règles du cas.

### P05 — Check Account and Funds

### P06 — Create Execution Context

Assure corrélation et état durable du processus.

### P07 — Send Payment to Clearing

### P08 — Wait for Clearing Result

Le modèle doit représenter explicitement :

- success ;
- reject ;
- timeout.

### P09 — Update Payment State

### P10 — Notify Customer

### P11 — Publish Operational/Event Status

### P12 — End

## 5. BPMN logique

```text
Customer
  |
  | Submit Payment
  v
Digital Channel
  |
  v
[Start]
  |
Validate Request
  |
Valid? --No--> Reject Invalid Request --> Notify --> [End]
  |
 Yes
  v
Authenticate / Authorize
  |
Authorized? --No--> Reject Unauthorized --> Notify --> [End]
  |
 Yes
  v
Run Fraud Decision
  |
  +--Reject--> Reject Fraud --> Notify --> [End]
  +--Review--> Manual/Enhanced Review --+
  |                                     |
  +---------------Approve---------------+
                                        v
                              Check Account/Funds
                                        |
                              Funds? --No--> Reject --> Notify --> [End]
                                        |
                                       Yes
                                        v
                              Send to Clearing
                                        |
                             Wait for Response
                                /       |       \
                         Accepted    Rejected   Timeout
                             |          |          |
                         Complete     Reject    Handle Timeout
                             |          |          |
                             +----------+----------+
                                        |
                                Update Status
                                        |
                                Notify Customer
                                        |
                                      [End]
```

## 6. Exception catalogue

### EX01 Invalid Request

Traitement : rejection immédiate, motif structuré.

### EX02 Unauthorized

Traitement : rejection + audit/security event selon politique.

### EX03 Fraud Reject

Traitement : rejection et journalisation de décision.

### EX04 Fraud Review

Traitement : parcours spécifique contrôlé ; attention au SLA instant payment.

### EX05 Insufficient Funds

Traitement : reject.

### EX06 Duplicate

Traitement cible : réponse idempotente plutôt que double exécution.

### EX07 Clearing Reject

Traitement : statut final rejeté avec code.

### EX08 Clearing Timeout

Traitement : retry limité, status inquiry ou exception selon règles.

### EX09 Internal Platform Failure

Traitement : retry/failover/incident selon nature.

### EX10 Notification Failure

Ne doit pas nécessairement annuler un paiement déjà exécuté ; traiter séparément résultat financier et notification.

## 7. Applications

| Activity | Application/Service |
|---|---|
| Receive | Mobile/Web/API Channel |
| Validate/Orchestrate | Payment Orchestrator |
| Fraud | Fraud Decision Service |
| Account/Funds | Core Account Service |
| Clearing | Clearing Adapter |
| Notify | Notification Service |
| Observe | Observability Platform |

## 8. Data objects

```text
Payment Instruction
Customer / Authentication Context
Fraud Context
Fraud Decision
Account/Funds Result
Clearing Request
Clearing Result
Payment Status
Notification Request
Audit Record
```

## 9. Events et messages

Exemples conceptuels :

```text
PaymentReceived
FraudDecisionProduced
PaymentSubmittedToClearing
ClearingResultReceived
PaymentStatusChanged
CustomerNotificationRequested
```

Ces événements ne sont pas automatiquement des objets BPMN, Kafka ou ArchiMate identiques. Le repository doit expliciter leur niveau.

## 10. Risks and controls

| Risk | Control |
|---|---|
| duplicate execution | idempotency |
| fraudulent payment | fraud decision |
| unauthorized initiation | authentication/authorization |
| clearing unavailability | timeout + retry + resilience procedure |
| inconsistent status | state management + reconciliation |
| lost traceability | correlation/audit logging |
| notification loss | retry/dead-letter/monitoring |

## 11. RACI simplifié

| Area | Accountable | Responsible |
|---|---|---|
| end-to-end payment process | Payments Domain | Payments Operations/Product |
| fraud decision | Fraud Domain | Fraud Service Team |
| clearing integration | Payments Domain | Clearing Integration Team |
| platform recovery | Platform Engineering | SRE |
| business exception | Payments Operations | Operations Analyst |

## 12. KPIs

- end-to-end processing time P50/P95/P99 ;
- STP rate ;
- rejection rate by reason ;
- fraud review rate ;
- duplicate rate ;
- clearing timeout rate ;
- manual repair rate ;
- notification failure rate ;
- service availability.

## 13. Current-state pain points

Scénario pédagogique :

```text
Manual exception handling
Point-to-point integration
Weak correlation IDs
Multiple status stores
Synchronous notification dependency
Limited real-time KPI visibility
```

## 14. Target process principles

1. Idempotency end-to-end.
2. Explicit state machine.
3. Timeouts and compensation modeled.
4. Notification decoupled from financial execution.
5. Fraud decision real-time.
6. Correlation and observability by design.
7. Reconciliation as detective control.
8. Human review only where business value justifies it.
9. Standard error taxonomy.
10. Process ownership end-to-end.

## 15. Current → target

```text
Current
Submit → Validate → Fraud → Clear → Manual Repair → Notify

Target
Submit
→ deterministic validation
→ real-time fraud
→ idempotent orchestration
→ resilient clearing
→ event-driven status
→ automated exception routing
→ customer notification
```

## 16. Process/Application impact scenario

Si Payment Orchestrator migre :

```text
Affected activities
→ Validate
→ Create Execution Context
→ Send to Clearing
→ Update Status

Affected controls
→ idempotency
→ timeout policy
→ audit trail

Affected data
→ Payment Status
→ Correlation Context

Affected KPIs
→ processing time
→ timeout rate
→ repair rate
```

## 17. Transformation backlog

### Wave 1 — Observability

- canonical correlation ID ;
- KPI instrumentation ;
- exception taxonomy.

### Wave 2 — Orchestration

- idempotency ;
- explicit state ;
- timeout handling.

### Wave 3 — Decoupling

- event-driven status ;
- asynchronous notification.

### Wave 4 — Optimization

- reduce manual review ;
- process mining ;
- simulation/capacity optimization.

## 18. Views à construire dans HOPEX

1. Process Landscape — Payments.
2. BPMN — Execute Instant Payment.
3. Process × Application Matrix.
4. Process × Data Matrix.
5. Process × Risk/Control Matrix.
6. RACI.
7. KPI Dashboard.
8. Current vs Target Process.
9. Process Transformation Roadmap.
10. Impact Analysis View.

## 19. Critères de réussite

Le modèle est considéré exploitable lorsque l'on peut répondre sans PowerPoint externe à :

- qui possède le processus ?
- quelles applications le supportent ?
- quelles données sont critiques ?
- où sont les exceptions ?
- quels contrôles couvrent les risques ?
- quels KPIs mesurent le résultat ?
- quel est l'impact d'une migration applicative ?
- quelles étapes doivent changer dans la cible ?