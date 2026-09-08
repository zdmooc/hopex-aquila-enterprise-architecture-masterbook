# 05 — Data Lineage, Data Flows & Transformation Analysis

## 1. Pourquoi le lineage

Le lineage répond à :

```text
Where did this data come from?
How was it transformed?
Where is it consumed?
What breaks if it changes?
```

Il est essentiel pour :

- impact analysis ;
- auditability ;
- troubleshooting ;
- quality root-cause analysis ;
- regulatory traceability ;
- migration planning ;
- decommissioning.

## 2. Functional vs Technical Lineage

### Functional lineage

Relie concepts, applications, processus et transformations à un niveau compréhensible par l’architecture et le métier.

### Technical lineage

Descend vers tables, columns, jobs, pipelines et transformations techniques.

Les pages publiques HOPEX distinguent explicitement functional lineage et technical lineage.

## 3. Exemple fonctionnel MayaBank

```text
Customer submits Payment Instruction
        ↓
Digital Channel
        ↓
Payment Orchestrator
        ↓ enrich
Fraud Decision Service
        ↓
Payment Status
        ↓
Clearing Gateway
        ↓
Clearing Result
        ↓
Reconciliation / Notification / Analytics
```

## 4. Transformation nodes

Une transformation doit être nommée par son intention :

```text
Normalize Payment Instruction
Enrich Fraud Context
Map Internal Status to Scheme Status
Aggregate Daily Payment Metrics
```

Éviter :

```text
Transform 1
Job X42
Mapping final2
```

## 5. Source-to-target mapping

Exemple :

| Source | Transformation | Target |
|---|---|---|
| Payment Instruction | validation/normalization | Canonical Payment |
| Fraud Context | scoring | Fraud Decision |
| Clearing Result | status mapping | Payment Status |
| Payment Events | aggregation | Payment KPI Dataset |

## 6. Data flow attributes

Pour un flux critique documenter :

- source ;
- target ;
- information ;
- frequency ;
- volume class ;
- latency requirement ;
- transport mode ;
- security classification ;
- transformation ;
- owner ;
- criticality.

## 7. Batch lineage

Exemple :

```text
Payment Operational DB
→ nightly extract
→ staging
→ reconciliation transformation
→ reconciliation warehouse
```

Questions :

- cutoff time ?
- retries ?
- partial loads ?
- duplicate handling ?
- late-arriving data ?

## 8. Event lineage

```text
Payment Orchestrator
→ PaymentStatusChanged
→ Kafka/Event Streaming
→ Notification
→ Reconciliation
→ Analytics
```

Le topic n’est pas le concept métier. Le lineage doit relier event contract et information transported.

## 9. API lineage

```text
Fraud Consumer
→ POST /fraud-decisions
→ Fraud Service
→ Fraud Decision
```

Documenter :

- request information ;
- response information ;
- transformations ;
- version ;
- owner.

## 10. Database lineage

Technical lineage peut relier :

```text
PAYMENT_TX.AMOUNT
→ ETL expression
→ FACT_PAYMENT.AMOUNT_EUR
```

Mais le niveau enterprise peut se contenter de :

```text
Payment Amount
→ currency normalization
→ Payment Analytics
```

selon la décision à prendre.

## 11. Lineage confidence

Toutes les relations ne sont pas également fiables.

Utiliser si nécessaire :

```text
Verified
Discovered
Inferred
Declared
Unknown
```

Cela évite de présenter une cartographie incomplète comme vérité absolue.

## 12. Automated discovery

HOPEX Data Discovery est un module public MEGA associé à HOPEX Data Governance. Son usage et ses connecteurs doivent être vérifiés selon licence/version.

Principe :

```text
Automated discovery
→ metadata inventory
→ technical lineage
→ contextualization in HOPEX
→ governance validation
```

## 13. Change impact analysis

Question : `Payment Status` change de sémantique.

Analyse :

```text
Payment Status
→ producing applications
→ transformations
→ events/APIs
→ consuming applications
→ reports
→ controls
→ processes
```

## 14. Root cause analysis

Symptôme : KPI de fraude incohérent.

Navigation :

```text
KPI dataset
← transformation
← Fraud Decision event
← Fraud Service
← Fraud Context
← upstream source
```

## 15. Data lineage and regulation

Un lineage exploitable aide à démontrer :

- provenance ;
- traitement ;
- diffusion ;
- stockage ;
- usage.

Il ne prouve pas à lui seul la conformité : policies, controls, lawful basis et evidence restent nécessaires.

## 16. Dendrograms and analysis

Les fonctionnalités publiques HOPEX Data Governance mentionnent des visualisations de transformation et des dendrograms prêts à l’emploi pour analyser les dépendances.

Le masterbook retient le principe d’analyse, pas un écran spécifique qui pourrait varier selon version.

## 17. Lineage quality gates

Pour un flux critique :

1. source identifiée ;
2. target identifié ;
3. information nommée ;
4. transformation documentée ;
5. owner connu ;
6. criticality connue ;
7. confidence connue ;
8. current/target distingués ;
9. pas de rupture silencieuse ;
10. consumer impact disponible.

## 18. Anti-patterns

- lineage = simple flèche applicative ;
- lineage sans transformation ;
- lineage seulement physique sans contexte métier ;
- 100 % de confiance sur metadata non validée ;
- absence de consumer inventory ;
- lineage current mélangé à target ;
- data flow sans information transportée.
