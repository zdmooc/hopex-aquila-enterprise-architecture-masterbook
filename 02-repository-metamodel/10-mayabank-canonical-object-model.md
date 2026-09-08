# 10 — MayaBank Canonical Object Model

## 1. Objectif

Avant tout import massif dans HOPEX, MayaBank définit un **modèle canonique minimal**. Le but est de décider ce que représente chaque objet, qui le possède, comment on l'identifie et quelles relations doivent être maintenues.

Ce chapitre est pédagogique : les noms exacts de MetaClasses et attributs doivent être mappés sur les solutions HOPEX réellement installées.

## 2. Domaines canoniques

```text
Strategy / Capability
Business
Application
Data
Technology
Organization
Transformation
Governance
```

## 3. Capability

Exemples :

```text
CAP-PAY-001 Real-Time Payment Processing
CAP-PAY-002 Fraud Decision
CAP-PAY-003 Clearing & Settlement
CAP-PAY-004 Payment Reconciliation
```

Propriétés gouvernées :

```text
Name
Definition
Owner
Maturity
Strategic importance
Target maturity
Review date
```

Relations :

```text
Capability
→ supported by Business Process
→ supported by Application
→ targeted by Initiative
```

## 4. Business Process

```text
BPR-PAY-001 Execute Instant Payment
BPR-PAY-002 Investigate Fraud Alert
BPR-PAY-003 Reconcile Payment
```

Propriétés :

```text
Owner
Criticality
Frequency/volume class
Lifecycle
Regulatory scope
```

Relations :

```text
Process
→ supports Capability
→ uses Application
→ manipulates Data concept
→ owned by Org-Unit
```

## 5. Application

```text
APP-PAY-001 Payment Orchestrator
APP-PAY-002 Fraud Engine
APP-PAY-003 Clearing Adapter
APP-PAY-004 Notification Service
```

Propriétés :

```text
Owner
Business domain
Lifecycle
Criticality
Business fit
Technical fit
Source system
External key
Review date
```

Relations :

```text
Application
→ supports Process/Capability
→ interfaces with Application
→ uses Software Technology
→ handles Data
→ owned by Org-Unit
→ impacted by Project
```

## 6. Data

Exemples :

```text
DAT-PAY-001 Payment Order
DAT-PAY-002 Payment Transaction
DAT-PAY-003 Fraud Decision
DAT-PAY-004 Settlement Status
```

Gouvernance :

```text
Data owner
Sensitivity
Retention class
Authoritative source
Critical data element flag
```

## 7. Technology

```text
TEC-PLT-001 Container Platform
TEC-PLT-002 Event Streaming Platform
TEC-DB-001 PostgreSQL Technology
TEC-API-001 API Management Platform
```

Séparer :

```text
Technology standard/product
vs
runtime CI instance
```

Le second peut rester dans ServiceNow si le besoin HOPEX ne nécessite pas ce niveau.

## 8. Organization

```text
ORG-PAY-001 Payments Business
ORG-IT-001 Payments IT
ORG-PLT-001 Platform Engineering
ORG-SEC-001 Cybersecurity
```

Relations :

```text
Org-Unit
→ owns Application
→ owns Process
→ owns Capability
→ stewards Data
```

## 9. Transformation

```text
PRJ-PAY-001 Instant Payment Modernization
PRJ-PAY-002 Event Streaming Adoption
PRJ-PAY-003 Legacy Payment Retirement
```

Relations :

```text
Project/Initiative
→ impacts Application
→ improves Capability
→ retires Technology
→ closes architecture gap
```

## 10. Graph canonique

```text
Goal / Strategy
      ↓
Capability
      ↓
Business Process
      ↓
Application
   ↙       ↘
Data      Technology
   ↘       ↙
 Organization
      ↓
Transformation / Roadmap
```

## 11. Cas complet

```text
Capability
Real-Time Payment Processing
        ↓
Process
Execute Instant Payment
        ↓
Application
Payment Orchestrator
  ├─ uses Fraud Engine
  ├─ uses Event Streaming Platform
  ├─ handles Payment Transaction
  └─ owned by Payments IT
        ↓
Project
Instant Payment Modernization
```

## 12. Source-of-truth matrix

| Objet/donnée | Source proposée |
|---|---|
| Capability | HOPEX / EA |
| Process | HOPEX / Process governance |
| Application logique | HOPEX ou référentiel applicatif gouverné |
| CI runtime | ServiceNow CMDB |
| Technology standard | HOPEX / Technology governance |
| Cost | Finance |
| Owner identity | Directory/HR + governance |
| Project status | PPM |

## 13. Règles de création

Chaque objet doit avoir au minimum :

```text
canonical type
canonical name
owner/steward
source
identity/key strategy
review policy
```

## 14. Règles de relation

Chaque relation doit répondre à :

```text
What does it mean?
Who owns it?
What is the source?
How is it maintained?
Which analysis uses it?
```

## 15. Critères de publication

Un objet ne devient pas « trusted » simplement parce qu'il existe.

Proposition MayaBank :

```text
Draft
→ Identified
→ Enriched
→ Validated
→ Published/Trusted
→ Retired
```

Ce workflow est pédagogique et devra être adapté aux statuts natifs/processus HOPEX disponibles.

## 16. Première matrice d'impact

```text
Application × Capability
Application × Technology
Application × Org-Unit
Process × Application
Data × Application
Project × Application
```

Ces matrices deviendront des livrables des parties suivantes.

## 17. Anti-pattern

Ne jamais construire MayaBank ainsi :

```text
3000 Applications
0 owner
0 relation
0 lifecycle
```

Mieux vaut 100 objets gouvernés et reliés que 3000 lignes importées sans contexte.

## 18. Questions d'entretien

**Par quoi commencer dans un nouveau repository ?**  
Par définir le modèle canonique minimal, les sources maîtres, les owners et les usages d'analyse avant l'import massif.

**Quelle relation apporte le plus de valeur ?**  
Cela dépend du concern ; pour une rationalisation applicative, Application→Capability, Application→Technology, owner et lifecycle sont souvent structurants.
