# 10 — Data Integration, APIs, Events, Batch & CDC

## 1. Data moves through contracts

Une Data Architecture doit documenter non seulement les stores mais aussi les mécanismes de circulation.

```text
API
Event
Message
Batch/File
CDC
Replication
ETL/ELT
```

## 2. API data exchange

API synchrone adaptée lorsqu’un consumer a besoin :

- réponse immédiate ;
- contrôle d’accès central ;
- contrat request/response ;
- source actuelle.

Documenter : schema, owner, version, latency, errors, classification.

## 3. Event-driven exchange

Un event décrit un fait déjà survenu.

```text
PaymentStatusChanged
FraudDecisionProduced
CustomerAddressChanged
```

L’event doit être stable, versionné et relié au concept métier.

## 4. Command vs Event

```text
Command
DoSomething

Event
SomethingHappened
```

Exemple :

```text
Command: ExecutePayment
Event: PaymentExecuted
```

Ne pas nommer un command comme un event pour masquer de l’orchestration.

## 5. Batch / File

Toujours courant en banque.

Documenter :

- producer ;
- consumer ;
- file schema ;
- frequency ;
- cutoff ;
- encryption ;
- acknowledgment ;
- reprocessing ;
- retention.

## 6. CDC

Change Data Capture permet de propager des changements depuis une source.

Questions :

- source tables ;
- ordering ;
- deletes ;
- schema changes ;
- replay ;
- transaction boundaries ;
- PII leakage.

## 7. ETL vs ELT

### ETL

Transform avant chargement cible.

### ELT

Charge puis transforme dans plateforme cible.

Le choix dépend des volumes, plateforme, gouvernance, coût et sécurité.

## 8. Canonical event model

Exemple :

```text
PaymentStatusChanged v2
Header
- eventId
- eventType
- occurredAt
- correlationId
- schemaVersion

Payload
- paymentId
- previousStatus
- newStatus
- reasonCode
```

## 9. Schema Registry concept

Un registry permet de gouverner :

- schemas ;
- versions ;
- compatibility ;
- producers ;
- consumers.

HOPEX peut référencer ce contexte architectural sans forcément remplacer le registry runtime.

## 10. Idempotency

Dans les systèmes distribués :

```text
retry
≠ execute twice
```

Utiliser identifiants/keys et règles métier pour garantir le comportement souhaité.

## 11. Ordering

Ne pas supposer un ordre global.

Questions :

- order par paymentId ?
- partitioning ?
- consumer concurrency ?
- late events ?

## 12. Exactly-once myth

Même si une plateforme offre des garanties techniques, le business effect doit rester idempotent et réconciliable.

## 13. Dead-letter and quarantine

Un message invalide doit avoir :

- reason ;
- owner ;
- retention ;
- repair/replay process ;
- monitoring.

## 14. Data contract compatibility

Types :

- backward compatible ;
- forward compatible ;
- fully compatible ;
- breaking.

Toute évolution doit analyser consumers et historical data.

## 15. MayaBank exchange map

```text
Channel
→ REST Payment Instruction
→ Payment Orchestrator

Payment Orchestrator
→ synchronous Fraud Decision API

Payment Orchestrator
→ clearing message/API

Payment Orchestrator
→ PaymentStatusChanged event
→ Notification / Reconciliation / Analytics
```

## 16. Batch transition

Current :

```text
Nightly payment status export
→ notification/reporting
```

Target :

```text
Real-time event
+ controlled batch fallback/reconciliation
```

## 17. Data integration matrix

| Producer | Contract | Information | Consumer | Mode |
|---|---|---|---|---|
| Channel | Payment API | Payment Instruction | Orchestrator | sync |
| Fraud | Decision API | Fraud Decision | Orchestrator | sync |
| Orchestrator | Status Event | Payment Status | Notification | async |
| Payment DB | Reconciliation extract | Payment | Reconciliation | batch |

## 18. Integration quality gates

1. information defined ;
2. schema versioned ;
3. owner known ;
4. classification known ;
5. consumer inventory ;
6. error behavior ;
7. retry/idempotency ;
8. retention ;
9. observability ;
10. migration policy.

## 19. Anti-patterns

- event = table row dump ;
- CDC sans ownership ;
- file sans schema/version ;
- topic sans business semantics ;
- breaking schema change sans consumer analysis ;
- dual-write sans consistency strategy ;
- ETL réparant éternellement une mauvaise source.
