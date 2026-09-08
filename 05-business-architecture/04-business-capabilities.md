# 04 — Business Capabilities

## 1. Définition pratique

Une business capability décrit **ce que l'entreprise doit être capable de faire** pour atteindre ses objectifs, indépendamment de l'organigramme, des processus détaillés et des applications du moment.

Exemples MayaBank :

```text
Customer Identity Management
Payment Initiation
Payment Orchestration
Fraud Decisioning
Payment Clearing
Liquidity Management
Payment Operations
Regulatory Reporting
```

Une capability doit rester compréhensible même si l'organisation ou la technologie change.

## 2. Pourquoi les capabilities sont centrales dans HOPEX

HOPEX met explicitement en avant le business capability mapping et la connexion des capabilities aux applications, technologies et données.

Le bénéfice est de construire un pivot stable :

```text
Strategy
  ↓
Capability
  ├─ Organization
  ├─ Process
  ├─ Application
  ├─ Data
  ├─ Technology
  └─ Initiative
```

## 3. Capability ≠ Process

```text
Capability : Fraud Decisioning
Process    : Evaluate Payment Fraud Risk
```

La capability est l'aptitude.
Le process est une manière de l'exécuter.

## 4. Capability ≠ Function

Une fonction organisationnelle peut évoluer avec la structure.

La capability doit rester relativement stable.

```text
Department : Fraud Operations France
Capability : Fraud Decisioning
```

## 5. Capability ≠ Application

```text
Capability : Payment Orchestration
Application: MayaBank Payment Orchestrator
```

Une capability peut être soutenue par plusieurs applications ; une application peut soutenir plusieurs capabilities.

## 6. Taxonomie et niveaux

Exemple pédagogique MayaBank :

```text
L1 Payments
 ├─ L2 Payment Initiation
 ├─ L2 Payment Processing
 │    ├─ L3 Payment Validation
 │    ├─ L3 Fraud Decisioning
 │    ├─ L3 Payment Routing
 │    └─ L3 Payment Settlement Coordination
 └─ L2 Payment Operations
      ├─ L3 Exception Management
      └─ L3 Payment Investigation
```

Règle : ne pas mélanger plusieurs niveaux de granularité dans la même carte sans les signaler.

## 7. Nommage

Privilégier des noms d'aptitudes métier stables.

Bon :

```text
Payment Orchestration
Customer Authentication
Fraud Decisioning
```

Mauvais :

```text
Kafka
New Payment Project
Team Phoenix
Run Payment Engine
```

## 8. Maturity assessment

Une capability map devient utile quand elle porte des assessments.

Axes possibles :

- strategic importance ;
- current maturity ;
- target maturity ;
- business performance ;
- risk ;
- application fitness ;
- technology health ;
- investment need.

Exemple :

| Capability | Importance | Current | Target | Gap |
|---|---:|---:|---:|---:|
| Payment Orchestration | 5 | 2 | 5 | 3 |
| Fraud Decisioning | 5 | 4 | 5 | 1 |
| Payment Operations | 4 | 2 | 4 | 2 |
| Regulatory Reporting | 4 | 3 | 4 | 1 |

## 9. Heatmaps

Une heatmap doit répondre à une question unique.

Exemples :

```text
Capability maturity
Capability strategic importance
Capability risk exposure
Capability application complexity
Capability investment priority
```

Éviter une seule couleur « globale » dont personne ne comprend le calcul.

## 10. Capability-to-Application Mapping

Exemple :

| Capability | Payment Orchestrator | Fraud Engine | Ops Portal | Kafka |
|---|---:|---:|---:|---:|
| Payment Orchestration | P | S | - | S |
| Fraud Decisioning | - | P | - | S |
| Payment Operations | S | S | P | - |

`P` = primary support, `S` = secondary/supporting.

Cette matrice permet d'identifier :

- capabilities sans support IT clair ;
- applications redondantes ;
- single points of dependency ;
- applications critiques par impact métier ;
- domaines surinvestis.

## 11. Capability-to-Data Mapping

Exemple :

```text
Fraud Decisioning
→ Payment Transaction
→ Customer Risk Profile
→ Fraud Rule Set
```

Cela prépare les analyses Data Architecture de la Partie IX.

## 12. Capability-to-Technology Mapping

Ne pas relier directement chaque capability à chaque serveur.

Préférer des niveaux utiles :

```text
Payment Orchestration
→ Payment Orchestrator
→ Container Platform
→ OpenShift
```

La capability reste business ; la technologie est traversée via les actifs IT pertinents.

## 13. Capability-based planning

Méthode :

```text
Strategic objective
→ impacted capabilities
→ assessments
→ gaps
→ options
→ initiatives
→ investments
→ target maturity
```

Exemple :

```text
Objective: 24x7 instant payment resiliency
↓
Capabilities:
Payment Orchestration
Fraud Decisioning
Payment Operations
Observability
↓
Gaps:
legacy coupling
manual incident detection
single-site dependencies
↓
Initiatives:
event backbone
active-active runtime
operational automation
```

## 14. Reference content

HOPEX peut exploiter des contenus de référence sectoriels. MEGA mentionne notamment les capability maps et service landscape BIAN pour le secteur bancaire, selon les droits/licences nécessaires.

Le masterbook MayaBank n'importe aucun contenu propriétaire BIAN ; il utilise ses propres exemples pédagogiques.

## 15. Anti-patterns

- une capability par application ;
- une capability par équipe ;
- verbes de workflow très détaillés ;
- niveaux L1/L4 mélangés ;
- maturity score sans méthode ;
- heatmap sans décision associée ;
- capability sans owner ;
- capability map jamais reliée au SI ;
- customisation du métamodèle pour chaque taxonomie locale.

## 16. Entretien

**Pourquoi une capability map est-elle stable ?**  
Parce qu'elle décrit les aptitudes de l'entreprise, pas son organisation ou ses systèmes actuels.

**Quel est le principal usage EA ?**  
Relier stratégie, business et IT pour prioriser investissements, transformations et réduction de risques.

La Partie VI approfondira les capability maps, assessments, scénarios, heatmaps et capability-based planning.