# 10 — Data Flow, Information & Control Dependency Analysis

## 1. Pourquoi les dépendances data doivent être intégrées à la cartographie

Une application peut continuer à répondre techniquement tout en fournissant un service métier incorrect si ses données sont absentes, périmées ou incohérentes.

La dependency analysis doit donc intégrer :

```text
Information
Data Producers
Data Consumers
Interfaces / Events
Stores
Transformations
Controls
Quality Rules
Retention / Classification
```

---

## 2. Information dependency

Exemple :

```text
Payment Orchestrator
→ requires
Account Balance
```

Le besoin métier est indépendant du stockage technique.

---

## 3. Producer dependency

```text
Payment Status
← produced by
Payment Orchestrator
```

Si le producer change, tous les consumers doivent être identifiés.

---

## 4. Consumer dependency

```text
Payment Status
→ consumed by
Notification
Reconciliation
Analytics
Operations
```

Cette vue permet d’évaluer un changement de sémantique ou schema.

---

## 5. Data lineage as dependency graph

```text
Source Information
→ Producer
→ Interface/Event
→ Transformation
→ Store
→ Consumer
→ Business Use
```

Le lineage fonctionnel de la Partie IX devient ici un chemin de dépendance analysable.

---

## 6. Functional lineage vs technical lineage

### Functional

```text
Customer Identity
→ Payment Fraud Check
```

### Technical

```text
CUSTOMER.ID
→ API payload customerId
→ Kafka field partyId
→ FRAUD_REQUEST.PARTY_ID
```

La cartographie entreprise privilégie le niveau utile à la décision.

---

## 7. Transformation dependency

Une transformation data peut être critique :

```text
Payment Instruction
→ mapping
→ Clearing Message
```

Si le mapping est incorrect :

- rejet ;
- mauvaise donnée ;
- non-conformité ;
- reconciliation issue.

---

## 8. Schema dependency

Consumers peuvent dépendre :

- field presence ;
- type ;
- allowed values ;
- ordering ;
- semantics ;
- version.

Une API compatible techniquement peut être incompatible sémantiquement.

---

## 9. Event schema dependency

```text
PaymentStatusChanged v1
→ Notification
→ Reconciliation
→ Analytics
```

Avant évolution v2 :

1. identifier consumers ;
2. identifier version support ;
3. définir coexistence ;
4. tester replay ;
5. planifier retirement v1.

---

## 10. Source-of-truth dependency

```text
Payment Status
→ authoritative source
Payment Orchestrator
```

Les replicas ne doivent pas être interprétés comme sources indépendantes.

---

## 11. Replica dependency

```text
Primary Store
→ replication
Read Replica
→ consumer
```

Une panne du primary peut affecter le replica selon mode de réplication.

---

## 12. Cache dependency

Un cache peut être :

- optimization only ;
- necessary for latency ;
- unavailable fallback to source ;
- effectively hard dependency under load.

La criticité dépend du comportement réel.

---

## 13. Batch dependency

```text
T-1 Payment Data
→ nightly batch
→ reconciliation/reporting
```

La dépendance est temporelle et peut produire un impact retardé.

---

## 14. CDC dependency

Change Data Capture ajoute :

- source log ;
- CDC connector ;
- stream ;
- consumer ;
- offset/checkpoint.

Chaque composant peut devenir un maillon du lineage technique.

---

## 15. Data quality dependency

Un processus dépend parfois d’une règle qualité :

```text
Payment Instruction
→ must satisfy
Mandatory IBAN / Amount / Currency rules
```

Une donnée disponible mais invalide reste inutilisable.

---

## 16. Freshness dependency

Exemple :

```text
Fraud Profile
must be < threshold age
```

Si la donnée est trop ancienne, le service peut devoir refuser, dégrader ou appliquer une règle spécifique.

Le seuil exact vient du métier/risk.

---

## 17. Completeness dependency

Une décision peut nécessiter plusieurs attributs.

```text
Fraud Check
→ Customer Identity
→ Device Context
→ Payment Amount
→ Beneficiary Context
```

L’absence d’un seul peut modifier la décision.

---

## 18. Control dependency

```text
Payment Execution
→ requires
Authorization Control
Fraud Control
Duplicate Control
```

La perte d’un contrôle ne doit pas être confondue avec simple baisse de performance.

---

## 19. Control implementation dependency

```text
Duplicate Payment Risk
→ mitigated by
Idempotency Control
→ implemented by
Payment Orchestrator
→ relies on
Idempotency Store
```

Cette chaîne relie risk, control, application et data store.

---

## 20. Evidence dependency

Certains contrôles exigent des preuves :

- logs ;
- audit trail ;
- decision record ;
- approval ;
- reconciliation evidence.

La perte de la chaîne d’evidence peut créer un impact conformité même si la transaction fonctionne.

---

## 21. Privacy dependency

Une donnée Restricted peut imposer :

```text
Encryption
Access Control
Retention
Audit Logging
Data Residency
```

La classification pilote des contrôles, pas seulement une couleur.

---

## 22. Data residency dependency

```text
Data Domain
→ permitted locations
→ stores/platforms
```

Un projet cloud doit vérifier les contraintes réelles du client.

---

## 23. Retention dependency

Un retrait d’application doit traiter :

- data archive ;
- legal hold ;
- audit evidence ;
- purge ;
- downstream reporting.

Les durées ne doivent pas être inventées.

---

## 24. Reconciliation dependency

Dans les paiements :

```text
Internal Payment State
↔ External Clearing State
```

Un service peut être techniquement disponible tout en nécessitant reconciliation après incident.

---

## 25. Consistency dependency

Patterns :

```text
Strong consistency
Eventual consistency
Compensating correction
Manual reconciliation
```

Le choix influence l’impact d’une panne partielle.

---

## 26. Dual-write risk

Pendant transition :

```text
Application
→ writes Legacy DB
→ writes Target Store
```

Risques :

- divergence ;
- partial success ;
- ordering ;
- rollback complexity.

La cartographie doit marquer cette dépendance temporaire.

---

## 27. Data flow impact query

Question : modifier `Payment Status`.

```text
Payment Status
→ producers
→ events/APIs
→ consumers
→ stores
→ reports/processes
→ owners
```

---

## 28. Data outage impact query

Question : perte du `Payment State Store`.

```text
Store
→ applications using it
→ functions/processes
→ recovery mechanisms
→ reconciliation needs
```

---

## 29. Data breach exposure map

Point de départ : information compromise.

```text
Information
→ stores
→ interfaces
→ applications
→ organizations
→ external parties
```

Cette vue aide l’investigation de portée ; elle ne remplace pas incident response/security tooling.

---

## 30. MayaBank — Payment Status lineage

```text
Payment Orchestrator
→ creates Payment Status
→ PaymentStatusChanged event
→ Event Streaming
├→ Notification Service
├→ Reconciliation Service
└→ Analytics
```

Le modèle doit aussi montrer le system of record et les stores si utile.

---

## 31. MayaBank — Fraud Decision dependency

```text
Payment Orchestrator
→ sends Payment Context
→ Fraud Decision Service
→ reads Fraud/Customer context
→ returns Fraud Decision
→ Payment Orchestrator
```

La décision devient à la fois data object et control dependency.

---

## 32. MayaBank — Clearing Result

```text
Clearing Gateway
→ receives Clearing Result
→ updates Payment execution state
→ triggers downstream event
→ Reconciliation consumes result
```

---

## 33. Data dependency register

| Information | Producer | Consumers | Criticality | Quality dependency | Owner |
|---|---|---|---|---|---|
| Payment Status | Orchestrator | Notification, Recon | Critical | timeliness/consistency | Payments |
| Fraud Decision | Fraud Service | Orchestrator | Critical | freshness/validity | Fraud |
| Clearing Result | Gateway | Orchestrator, Recon | Critical | completeness | Payments |

Pédagogique.

---

## 34. Anti-patterns

- data flow = application arrow only ;
- store considéré comme information ;
- lineage sans transformation ;
- consumer inconnu ;
- source of truth non défini ;
- event schema changé sans cartographie consumers ;
- contrôle modélisé comme commentaire ;
- data availability confondue avec data quality.

---

## 35. Questions d’entretien

**Pourquoi intégrer la data au dependency graph ?**  
Parce qu’un service peut être disponible mais incorrect si les données nécessaires sont absentes, périmées ou incohérentes.

**Quelle différence entre source of truth et replica ?**  
La source de référence porte l’autorité ; le replica est une copie pour un usage spécifique.

**Pourquoi un contrôle est-il une dépendance ?**  
Parce qu’une opération peut être interdite ou non conforme si le contrôle requis n’est pas exécuté ou prouvé.
