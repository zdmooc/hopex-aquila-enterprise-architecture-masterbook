# 12 — MayaBank BPA repository blueprint : objets, relations, vues et data quality

## 1. Objectif

Ce chapitre transforme le cas `Execute Instant Payment` en **blueprint de repository**.

Le but n'est pas d'imposer les noms exacts de MetaClasses HOPEX d'un environnement client. Le métamodèle réel doit être vérifié par l'UI, la documentation disponible et, si autorisé, l'introspection GraphQL/MetaModel présentée en Partie II.

Le blueprint décrit les **concepts à représenter et leurs relations**.

## 2. Principe canonique

```text
One business concept
→ one canonical repository object
→ many views
```

Éviter :

```text
Payment Orchestrator in BPMN
Payment Orchestrator in matrix
Payment Orchestrator in roadmap
```

comme trois objets distincts.

## 3. Process hierarchy MayaBank

```text
L0 MayaBank Process Landscape
└─ L1 Manage Payments
   ├─ L2 Initiate Payment
   ├─ L2 Execute Payment
   │  ├─ L3 Execute Instant Payment
   │  ├─ L3 Execute Scheduled Transfer
   │  └─ L3 Execute Bulk Payment
   ├─ L2 Handle Payment Exception
   └─ L2 Reconcile Payment
```

La taxonomie exacte est pédagogique.

## 4. Core process object card

Pour `Execute Instant Payment` :

```text
Name                Execute Instant Payment
Domain              Payments
Parent              Execute Payment
Owner               Payment Process Owner
Outcome             Final payment status produced
Start               Valid customer instruction submitted
End                 Final status or governed exception state
Criticality         Critical
Lifecycle           Published / Target selon vue
Review cadence      Defined by governance
```

## 5. Activity catalogue

Créer des activités stables et réutilisables lorsque le niveau de détail le justifie :

1. Receive Payment Request
2. Validate Payment
3. Authenticate / Authorize
4. Run Fraud Check
5. Run Compliance Check
6. Check Funds
7. Reserve Funds
8. Create Execution Context
9. Route Payment
10. Submit to Clearing
11. Wait for Clearing Result
12. Update Payment Status
13. Notify Customer
14. Reconcile Payment
15. Handle Payment Exception

## 6. Activity identifiers

Exemple de convention pédagogique :

```text
PAY-ACT-001 Validate Payment
PAY-ACT-002 Authenticate Payment
PAY-ACT-003 Run Fraud Check
```

L'identifiant doit rester stable même si le libellé est légèrement amélioré.

Ne pas inventer un mécanisme d'ID technique HOPEX si le client n'en utilise pas.

## 7. Process ↔ Capability

| Process | Capability |
|---|---|
| Execute Instant Payment | Payment Execution |
| Run Fraud Check | Fraud Detection / Decisioning |
| Handle Payment Exception | Payment Operations |
| Reconcile Payment | Reconciliation |

Le mapping permet de relier performance opérationnelle et investissements de capability.

## 8. Process ↔ Business Service

Exemples :

```text
Instant Payment Service
Payment Status Service
Payment Exception Handling Service
```

Questions :

- quel service est rendu ?
- à quel client/consumer ?
- quel process réalise le service ?
- quels SLA/outcomes ?

## 9. Activity ↔ Application

| Activity | Application/Service |
|---|---|
| Receive Request | Digital Channel / API Management |
| Validate / Orchestrate | Payment Orchestrator |
| Authenticate | IAM |
| Fraud Check | Fraud Decision Service |
| Compliance Check | Compliance Screening Service |
| Funds Check | Core Account Service |
| Clearing | Clearing Gateway / Adapter |
| Notify | Notification Service |
| Observe | Observability Platform |

## 10. Application object rules

Pour chaque application reliée :

- utiliser l'objet canonique de l'architecture applicative ;
- ne pas recréer un objet local dans le process ;
- vérifier owner et lifecycle ;
- distinguer application, application service et technology ;
- éviter le mapping direct à chaque pod/VM.

## 11. Process ↔ Information/Data

Data objects conceptuels :

```text
Payment Instruction
Authentication Context
Fraud Context
Fraud Decision
Compliance Decision
Funds Result
Clearing Request
Clearing Result
Payment Status
Notification Request
Reconciliation Record
Audit Record
```

## 12. Data relationship card

Pour chaque relation Activity ↔ Data :

```text
Activity
Data object
Usage: read/create/update
Criticality
Authoritative source
Data owner/steward
Sensitivity if relevant
```

Le niveau CRUD détaillé n'est utile que s'il sert une question d'architecture ou de governance.

## 13. Process ↔ Organization

Objets :

- Payments ;
- Fraud ;
- Compliance ;
- Operations ;
- Platform/SRE ;
- Customer Operations ;
- Architecture.

Relations possibles selon métamodèle :

```text
Process Owner
Activity responsibility
Participant
Escalation owner
Reviewer
```

## 14. Process ↔ Risk

Risks MayaBank :

```text
R01 Unauthorized payment
R02 Fraudulent payment accepted
R03 Duplicate execution
R04 Insufficient funds incorrectly handled
R05 Clearing unavailability
R06 Inconsistent payment state
R07 Lost audit trace
R08 Reconciliation mismatch
R09 Notification failure
R10 Platform outage
```

## 15. Risk ↔ Control

Controls :

```text
C01 Strong authentication / authorization
C02 Real-time fraud decision
C03 Idempotency control
C04 Funds validation
C05 Timeout + resilience procedure
C06 Explicit state management
C07 Correlation / audit logging
C08 Reconciliation
C09 Notification retry/monitoring
C10 HA/DR controls
```

## 16. Control ↔ Activity

Exemple :

```text
C03 Idempotency Control
→ Validate Payment
→ Submit to Clearing
```

Un contrôle peut couvrir plusieurs étapes ; une activité peut avoir plusieurs contrôles.

## 17. Process ↔ KPI

KPI objects proposés :

```text
KPI-STP
KPI-E2E-P95
KPI-CLEARING-TIMEOUT
KPI-MANUAL-REPAIR
KPI-DUPLICATE
KPI-FRAUD-REVIEW
KPI-NOTIFICATION-FAILURE
```

Chaque KPI doit référencer sa définition et sa source.

## 18. Process ↔ Initiative

Initiatives :

```text
INIT-OBS-001 End-to-End Observability
INIT-PAY-002 Payment Orchestrator Modernization
INIT-EVT-003 Event-Driven Status
INIT-REC-004 Reconciliation Automation
INIT-OPS-005 Exception Automation
```

Relation :

```text
Initiative
→ changes activities/process
→ changes applications
→ changes controls
→ expected KPI improvement
```

## 19. Process ↔ Technology

Ne pas lier directement chaque activité à toutes les technologies.

Préférer :

```text
Activity
→ Application
→ Platform
→ Technology
```

Exemples de platforms :

- OpenShift Platform ;
- Kafka/Event Streaming ;
- API Management ;
- Database Platform ;
- Observability Platform.

## 20. Exception catalogue objects

Exceptions structurantes :

```text
Invalid Request
Unauthorized
Fraud Reject
Compliance Reject
Insufficient Funds
Duplicate Payment
Clearing Reject
Clearing Timeout
Technical Failure
Reconciliation Exception
Notification Failure
```

Pour chaque exception :

- trigger ;
- business/technical classification ;
- response ;
- owner ;
- escalation ;
- control ;
- KPI ;
- operational intervention.

## 21. Matrix — Activity × Application

| Activity | API Mgmt | IAM | Orchestrator | Fraud | Core | Clearing | Notification |
|---|---:|---:|---:|---:|---:|---:|---:|
| Receive | X |  | X |  |  |  |  |
| Authenticate |  | X | X |  |  |  |  |
| Fraud Check |  |  | X | X |  |  |  |
| Funds Check |  |  | X |  | X |  |  |
| Clearing |  |  | X |  |  | X |  |
| Notify |  |  |  |  |  |  | X |

## 22. Matrix — Activity × Data

| Activity | Instruction | Fraud Decision | Funds Result | Clearing Result | Status |
|---|---:|---:|---:|---:|---:|
| Validate | R |  |  |  | C/U |
| Fraud | R | C |  |  | U |
| Funds | R |  | C |  | U |
| Clearing | R |  |  | C | U |
| Notify | R |  |  | R | R |

## 23. Matrix — Risk × Control

| Risk | Control | Type |
|---|---|---|
| duplicate | idempotency | preventive |
| fraud | fraud decision | preventive/detective |
| clearing outage | timeout/resilience | corrective |
| state inconsistency | reconciliation | detective |
| lost trace | audit logging | detective |

## 24. Matrix — Process × Organization

| Process/Activity | Payments | Fraud | Compliance | Ops | Platform |
|---|---|---|---|---|---|
| Execute Instant Payment | A/R | C | C | C | C |
| Fraud Check | C | A/R | I | I | I |
| Compliance Check | C | I | A/R | I | I |
| Handle Technical Exception | C | I | I | A/R | R/C |

## 25. Required views

### View 1 — Process Landscape

L0/L1/L2 structure.

### View 2 — BPMN Happy Path

Lisible par métier.

### View 3 — BPMN Exceptions

Timeouts, rejection, fallback.

### View 4 — Process/Application Matrix

Coverage and dependency.

### View 5 — Process/Data Matrix

Information usage.

### View 6 — Risk/Control View

Compliance and operational risk.

### View 7 — RACI

Ownership and responsibilities.

### View 8 — KPI Dashboard

Performance.

### View 9 — Current/Target

Transformation.

### View 10 — Initiative Roadmap

Sequencing.

### View 11 — Impact Analysis

Dependency traversal.

### View 12 — Exception Catalogue

Operational governance.

## 26. Viewpoint rule

Une vue répond à une question.

```text
Question
→ objects
→ relationships
→ filter
→ audience
```

Ne pas créer une mega-view montrant tout.

## 27. Data quality rules

### DQ01 — owner completeness

100 % des critical processes ont un owner.

### DQ02 — hierarchy integrity

Aucun process L3 orphelin.

### DQ03 — application canonicality

Aucune application dupliquée pour le même système.

### DQ04 — review freshness

Aucun critical process hors délai de revue.

### DQ05 — risk/control completeness

Chaque critical risk possède au moins un traitement/control documenté ou une décision explicite.

### DQ06 — KPI measurability

Chaque critical KPI possède formule, source, owner et target.

## 28. Naming dictionary

| Type | Convention | Exemple |
|---|---|---|
| Process | Verb + Object | Execute Instant Payment |
| Activity | Verb + Object | Validate Payment |
| Application | Product/System name | Payment Orchestrator |
| Business Service | Noun + Service | Instant Payment Service |
| Risk | Event + impact | Duplicate Payment Execution |
| Control | Action/control noun | Idempotency Control |
| Initiative | Outcome-oriented | End-to-End Observability |

## 29. Tags/classifications pédagogiques

Exemples :

```text
Domain = Payments
Criticality = Critical
Automation = Automated / Human / Hybrid
Lifecycle = Current / Transition / Target
Regulated = Yes/No
Customer-facing = Yes/No
```

Utiliser les classifications standard du client avant de créer du custom.

## 30. GraphQL — frontière vérifiée

Le workspace Postman officiel MEGA documente un endpoint BPA GraphQL et montre un exemple de requête sur `businessprocess`.

Exemple conceptuel issu de ce principe :

```graphql
query {
  businessprocess {
    id
    name
  }
}
```

Ne pas extrapoler les champs/relations disponibles : récupérer le SDL/schema de la version et du profil réellement utilisés.

## 31. Queries d'audit à savoir formuler

Même sans connaître la syntaxe exacte du client, l'architecte doit savoir exprimer :

1. critical processes sans owner ;
2. processes non revus depuis N mois ;
3. processes supportés par application EOL ;
4. activities sans application mapping ;
5. critical risks sans control ;
6. KPIs sans source ;
7. duplicate process names ;
8. retired applications encore reliées à current processes ;
9. target processes sans initiative ;
10. process variants sans parent.

## 32. Import strategy

Pour importer un inventaire existant :

```text
Profile source
→ normalize names
→ match canonical objects
→ detect duplicates
→ dry-run
→ import limited scope
→ quality checks
→ expand
```

Ne jamais bulk-importer un Excel non gouverné directement en production sans règles de matching.

## 33. Ownership de relation

Définir qui maintient quoi.

Exemple :

| Relation | Maintainer |
|---|---|
| Process ↔ Owner | Process Steward |
| Activity ↔ Application | Solution/Enterprise Architecture |
| Process ↔ Risk | Risk/Process Governance |
| Activity ↔ Data | Data + Process |
| Process ↔ Initiative | Transformation/EA |

## 34. Operational intervention blueprint

Pour `Clearing Timeout` :

```text
Exception owner        Payments Operations
Trigger                timeout threshold reached
Automatic action       retry/status inquiry according to policy
Manual trigger          unresolved state
Work item               Payment Exception Case
Evidence                trace + clearing reference + state history
Decision                resolve / reject / escalate
Control                  reconciliation
KPI                      repair rate / age / timeout rate
```

## 35. Fallback blueprint

Fallback n'est pas toujours `use another system`.

Types :

- alternate technical route ;
- queue and retry ;
- status inquiry ;
- degrade non-critical function ;
- human intervention ;
- failover site ;
- reject safely.

Documenter le fallback comme comportement gouverné et mapper ensuite les composants techniques concernés.

## 36. Definition of Done repository

Le modèle MayaBank Partie VII est complet lorsque :

- hierarchy existe ;
- owner existe ;
- BPMN happy path existe ;
- exceptions critiques existent ;
- applications sont reliées ;
- data objects critiques sont reliés ;
- risks/controls sont reliés ;
- KPIs sont définis ;
- initiatives target sont reliées ;
- current/target sont distingués ;
- quality checks passent ;
- audit questions sont répondables.

## 37. Questions d'entretien

**Pourquoi un blueprint repository plutôt qu'un BPMN seul ?**  
Parce que l'analyse d'impact, la gouvernance et la transformation dépendent de relations canoniques réutilisables.

**Comment éviter les doublons d'applications dans les processus ?**  
En liant les activités aux objets applicatifs canoniques déjà gouvernés et en appliquant Search Before Create/matching.

**Jusqu'où mapper la technologie ?**  
Jusqu'au niveau nécessaire à la décision ; généralement Process → Application → Platform avant de descendre vers l'infrastructure.