# Partie VII — Business Process Analysis

Cette partie approfondit la **Business Process Analysis (BPA)** dans HOPEX Aquila/Bizzdesign : architecture de processus, BPMN 2.0, gouvernance, risques/contrôles, performance, mappings cross-layer, analyse, process mining, simulation, automatisation et transformation.

Elle complète les parties précédentes sans les recopier :

```text
Partie V  = Business Architecture intégrée
Partie VI = Capability Architecture détaillée
Partie VII = Process Architecture & Business Process Analysis détaillées
```

## Positionnement à retenir

```text
TOGAF
= méthode / gouvernance d'architecture

ArchiMate
= langage de modélisation

HOPEX
= EAM / repository / analyse / gouvernance / portfolio / transformation

HOPEX
≠ moteur BPM runtime
```

Camunda et Pega sont utilisés dans cette partie uniquement pour expliquer la frontière entre repository d'architecture et moteur/runtime d'orchestration ou de case management.

## 13 chapitres de fond

1. [BPA : rôle, périmètre et méthode](01-bpa-role-scope-method.md)
2. [BPMN 2.0 : events, activities, gateways et participants](02-bpmn-core-modeling.md)
3. [Exceptions, controls, risks, RACI et KPIs](03-exceptions-controls-risks-kpis.md)
4. [Cross-layer mapping : process ↔ applications/data/architecture](04-process-cross-layer-mapping.md)
5. [Optimisation, simulation, process mining et automation candidates](05-optimization-simulation-process-mining.md)
6. [MayaBank Instant Payment — modèle end-to-end](06-mayabank-instant-payment-reference.md)
7. [Quality gates, anti-patterns et dette de modélisation](07-governance-antipatterns.md)
8. [Process governance operating model, lifecycle, versioning et publication](08-process-lifecycle-governance-workflows.md)
9. [Process performance, KPIs, SLA, throughput et maturity](09-process-performance-maturity.md)
10. [Process analysis methods : gap, impact, bottleneck, redundancy et control weakness](10-process-analysis-methods.md)
11. [HOPEX vs runtime BPM : Camunda, Pega et automation architecture](11-runtime-automation-camunda-pega.md)
12. [MayaBank BPA repository blueprint : objets, relations, matrices et vues](12-mayabank-repository-blueprint.md)
13. [Mission playbook, workshops, deliverables et interview cases](13-mission-playbook-interview-cases.md)

## Annexes

- [24 labs + 40 questions corrigées](90-labs-and-review.md)
- [Sources officielles, faits vérifiés et frontière pédagogique](99-official-sources.md)

## Compétences visées

À la fin de cette partie, vous devez savoir :

- construire un process landscape L0/L1/L2/L3 ;
- distinguer process, capability, value stream et procedure ;
- définir owner, steward, RACI et governance operating model ;
- modéliser un flux BPMN lisible ;
- utiliser pools, lanes, start/intermediate/end events, activities, subprocesses, gateways, sequence flows et message flows ;
- représenter timers, errors, escalations et exceptions sans spaghetti ;
- construire un exception catalogue ;
- relier risks, controls, obligations et audit points ;
- identifier les faiblesses de contrôle et SoD ;
- définir cycle time, lead time, throughput, failure rate, STP et automation rate ;
- construire un KPI design card avec formule/source/owner/target ;
- analyser P50/P95/P99 et bottlenecks ;
- mapper Process ↔ Capability ;
- mapper Process ↔ Organization ;
- mapper Process/Activity ↔ Application ;
- mapper Process ↔ Business Service ;
- mapper Process/Activity ↔ Information/Data ;
- mapper Process ↔ Risk/Control ;
- mapper Process ↔ Initiative ;
- réaliser gap analysis, impact analysis et dependency analysis ;
- analyser redundant steps, handoffs et application redundancy ;
- comprendre event logs, discovered process, conformance et performance mining ;
- comprendre le rôle vérifié du HOPEX Simulation Engine ;
- identifier des automation candidates ;
- expliquer clairement HOPEX vs Camunda/Pega/runtime BPM ;
- construire current / transition / target ;
- bâtir un blueprint repository MayaBank ;
- préparer un Architecture/Process Board ;
- auditer la qualité d'un repository BPA ;
- défendre les choix en entretien.

## Fondations BPA

Cette partie couvre explicitement :

```text
Process Architecture
Process Hierarchy
Process Landscape
End-to-End Processes
Process vs Capability
Process vs Value Stream
Process vs Procedure
Process Ownership
Roles & Responsibilities
```

## BPMN

Les concepts BPMN sont expliqués avec des exemples originaux MayaBank ; la norme n'est pas recopiée.

Couverture :

```text
Pools
Lanes
Start Events
Intermediate Events
End Events
Activities
Tasks
Subprocesses
Gateways
Sequence Flows
Message Flows
Timers
Errors
Escalations
Exceptions
```

## Governance

Le chapitre 08 détaille :

```text
Proposed
→ Draft
→ In Review
→ Approved
→ Published
→ Under Change
→ Retired
```

avec :

- Process Owner ;
- Process Steward ;
- reviewers ;
- RACI ;
- versioning ;
- review triggers ;
- publication ;
- SoD ;
- retirement ;
- governance KPIs.

Ce lifecycle est une recommandation pédagogique ; la configuration réelle du client doit être vérifiée.

## Performance

Le chapitre 09 traite :

- KPI ;
- SLA ;
- SLO ;
- cycle time ;
- lead time ;
- processing time ;
- waiting time ;
- throughput ;
- failure rate ;
- rework ;
- automation rate ;
- manual intervention ;
- STP ;
- P50/P95/P99 ;
- bottlenecks ;
- process maturity.

## Cross-layer mapping

Matrices et relations principales :

```text
Process ↔ Capability
Process ↔ Organization
Process/Activity ↔ Application
Process ↔ Business Service
Process/Activity ↔ Information/Data
Process ↔ Risk
Process ↔ Control
Process ↔ KPI
Process ↔ Initiative
Application ↔ Platform/Technology
```

## Process analysis

Méthodes opérationnelles :

```text
Gap Analysis
Impact Analysis
Dependency Analysis
Bottleneck Analysis
Handoff Analysis
Redundant Step Analysis
Control Weakness Analysis
SoD Analysis
Application Redundancy Analysis
Automation Opportunity Analysis
Current/Target/Transition Analysis
```

## Process mining et simulation

La partie distingue :

```text
Governed process model
≠
Observed process from event logs
```

Elle couvre :

- Case ID / Activity / Timestamp ;
- variants ;
- loops ;
- conformance ;
- performance ;
- limitations ;
- feedback vers le repository ;
- HOPEX Simulation Engine officiel et ses scénarios what-if.

## Automation

```text
HOPEX
= repository/gouvernance/analyse

Camunda/Pega/runtime engine
= exécution/orchestration selon technologie
```

La partie couvre :

- workflow automation ;
- BPM engines ;
- case management ;
- API automation ;
- event-driven ;
- RPA ;
- decision automation ;
- human tasks ;
- timers/retries ;
- observability ;
- process-mining feedback.

## Cas fil rouge — Execute Instant Payment

Chaîne principale :

```text
Customer
→ Initiate Payment
→ Authenticate
→ Validate Payment
→ Fraud Check
→ Compliance Check
→ Funds Check
→ Reserve Funds
→ Route Payment
→ Clearing
→ Settlement / final status handling
→ Notify Customer
→ Reconciliation
```

Le modèle détaillé est adapté au scope de la Partie VII et ne prétend pas décrire un scheme interbancaire réel.

## Exceptions MayaBank

Le cas couvre notamment :

- invalid request ;
- unauthorized ;
- fraud rejection ;
- compliance rejection ;
- insufficient funds ;
- duplicate payment ;
- clearing reject ;
- clearing timeout ;
- technical failure ;
- notification failure ;
- reconciliation exception ;
- fallback ;
- operational intervention.

## Applications et plateformes reliées

Le blueprint MayaBank relie le processus à :

- Payment Orchestrator ;
- Fraud Decision Service ;
- IAM ;
- API Management ;
- Kafka/Event Streaming ;
- Clearing Gateway/Adapter ;
- Notification Service ;
- Core Account Service ;
- databases/data objects ;
- OpenShift Platform ;
- Observability Platform.

## Livrables MayaBank

- Process Landscape ;
- Process Charter ;
- BPMN Happy Path ;
- BPMN Exceptions ;
- Exception Catalogue ;
- RACI ;
- Activity × Application Matrix ;
- Activity × Data Matrix ;
- Risk × Control Matrix ;
- KPI Catalogue ;
- Current/Target Comparison ;
- Impact Analysis ;
- Transformation Backlog ;
- Repository Blueprint ;
- Governance RACI ;
- Architecture Board One-Pager.

## Labs et questions

Annexe pratique :

```text
24 labs
40 questions corrigées
```

Les labs peuvent être réalisés :

- dans un environnement HOPEX autorisé ;
- ou sur papier/Markdown pour travailler le raisonnement repository sans licence.

## Sources

L'annexe sources sépare :

- MEGA/Bizzdesign/HOPEX Store ;
- workspace Postman officiel ;
- OMG BPMN 2.0.2 ;
- Camunda documentation officielle ;
- Pega documentation/présentation officielle ;
- recommandations pédagogiques ;
- données fictives MayaBank.

## Baseline produit utilisée

Vérifiée au 8 septembre 2026 :

```text
HOPEX Aquila 6.2
Core Back-End : 62.18.0+774
Web Front-End : 62.18.0+143
REST API : 62.18.0+69
BPA GraphQL endpoint : documentation publique vérifiée
Simulation Engine : add-on officiel vérifié
```

Toujours revérifier la licence, les modules, le profil, le métamodèle et les workflows dans l'environnement client.

## Definition of Done — Partie VII

La Partie VII est considérée complète car elle fournit :

- 13 vrais chapitres de fond ;
- un README de synthèse ;
- un cas MayaBank end-to-end ;
- BPMN et exceptions ;
- gouvernance détaillée ;
- process performance ;
- cross-layer mappings ;
- process analysis ;
- process mining/simulation ;
- frontière HOPEX/runtime BPM ;
- blueprint repository ;
- anti-patterns ;
- playbook de mission ;
- 24 labs ;
- 40 questions corrigées ;
- sources officielles séparées des recommandations pédagogiques.
