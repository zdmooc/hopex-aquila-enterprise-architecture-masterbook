# Partie XII — Enterprise Cartography & Dependency Analysis

Cette partie approfondit la **cartographie d’entreprise et l’analyse des dépendances** dans Bizzdesign Hopex / HOPEX Aquila.

Elle transforme le repository en graphe exploitable pour :

- comprendre les dépendances directes et transitives ;
- analyser les impacts de panne ou de changement ;
- identifier hubs, cycles, bridges et SPOF logiques ;
- relier technologie → application → process → capability ;
- construire des recovery dependency chains ;
- planifier migrations et decommissioning ;
- gouverner la qualité et la confiance des relations ;
- exploiter le cas fil rouge **MayaBank**.

---

# Positionnement dans le masterbook

```text
Partie XI
Relationships, Diagrams, Matrices & Views
→ qualité et représentation des relations

Partie XII
Enterprise Cartography & Dependency Analysis
→ exploitation du graphe pour analyse et décision

Partie XIII
IT Business Management & Application Portfolio
→ valeur, coût, santé, rationalisation du portefeuille

Partie XIV
IT Portfolio Management & Transformation Roadmaps
→ initiatives, dépendances de transformation et trajectoires

Partie XV
Reports, Dashboards, Analysis & Decision Support
→ indicateurs, reporting, décision
```

La Partie XII ne répète donc pas la Partie XI : elle passe du **lien représenté** au **réseau de dépendances analysé**.

---

# Objectifs

À la fin de cette partie, vous devez savoir :

- raisonner en graphe `nodes + typed edges` ;
- distinguer association et dépendance ;
- distinguer direct/transitive dependency ;
- construire des règles de traversal ;
- utiliser 1-hop / 2-hop / n-hop de façon contrôlée ;
- comprendre BFS et DFS comme concepts d’analyse ;
- distinguer functional, technical, runtime, data, security et external dependency ;
- distinguer hard, soft, optional et fallback dependency ;
- construire un critical dependency path ;
- construire un business impact chain ;
- analyser blast radius direct et transitive ;
- détecter hubs et shared dependencies ;
- comprendre cycles et strongly connected components ;
- comprendre bridges et articulation points ;
- identifier les candidats SPOF/choke points ;
- construire un recovery dependency graph ;
- déterminer un minimum viable service ;
- utiliser le graph pour RTO/RPO et PRA ;
- analyser interface deprecation ;
- analyser technology retirement ;
- analyser site exit / vendor exit ;
- définir migration units et transition dependencies ;
- intégrer data lineage et control dependencies ;
- exploiter degree, reachability et centrality comme signaux ;
- segmenter la cartographie par domaine ;
- mettre en place une gouvernance fédérée ;
- construire un Architecture Board dependency pack.

---

# Chapitres

## 01 — Enterprise Cartography : rôle, périmètre et méthode

[Ouvrir](01-enterprise-cartography-role-scope-method.md)

Couvre :

- cartographie vs diagramme ;
- graph model ;
- nodes/edges ;
- layers business/application/data/technology ;
- direct/transitive ;
- traversal method ;
- baseline MayaBank ;
- product facts vs graph-analysis best practices.

---

## 02 — Graph Model, Traversal, Scope & Depth

[Ouvrir](02-graph-model-traversal-scope-depth.md)

Couvre :

- typed node/edge sets ;
- forward/reverse traversal ;
- BFS/DFS ;
- k-hop neighborhood ;
- max depth ;
- scope business/geography/environment ;
- confidence filters ;
- stop conditions ;
- external boundary objects ;
- path explosion ;
- orphan/dead-end paths.

---

## 03 — Dependency Taxonomy

[Ouvrir](03-dependency-taxonomy-direct-transitive-runtime-business.md)

Couvre :

- direct/transitive ;
- functional/technical ;
- runtime/build/deployment ;
- data/control ;
- organizational/supplier/geographic/network/identity ;
- synchronous/asynchronous ;
- hard/soft/optional/fallback ;
- current/target/temporary dependency ;
- dependency register.

---

## 04 — Criticality & Critical Dependency Paths

[Ouvrir](04-criticality-critical-path-business-impact.md)

Couvre :

- object vs dependency criticality ;
- business impact chain ;
- hard-stop vs degraded path ;
- criticality propagation ;
- shared critical dependencies ;
- RTO/RPO context ;
- critical dependency register.

Le terme `critical dependency path` est explicitement distingué du `critical path` de planification projet.

---

## 05 — Blast Radius & Impact Analysis

[Ouvrir](05-blast-radius-impact-analysis.md)

Couvre :

- direct/transitive blast radius ;
- horizontal/vertical impact ;
- technology/data/security/vendor/geographic exposure ;
- change impact ;
- incident analysis ;
- confidence-aware results ;
- test scope ;
- MayaBank IAM/Kafka/Legacy Gateway scenarios.

---

## 06 — Cycles, Hubs, Bridges, SPOF & Choke Points

[Ouvrir](06-cycles-hubs-bridges-spof-chokepoints.md)

Couvre :

- cycles ;
- strongly connected components ;
- hubs ;
- in-degree/out-degree ;
- bridge ;
- articulation point ;
- logical SPOF ;
- choke point ;
- shared DB coupling ;
- IAM/API/Kafka hubs ;
- organizational SPOF ;
- vendor concentration.

---

## 07 — Resilience, DR & Recovery Dependency Chains

[Ouvrir](07-resilience-dr-recovery-dependency-chains.md)

Couvre :

- service recovery chain ;
- recovery order ;
- minimum viable service ;
- recovery tiers ;
- RTO/RPO propagation ;
- shared control-plane dependencies ;
- data/event/network/identity recovery ;
- DR evidence ;
- cascading failure ;
- dependency-aware DR tests.

---

## 08 — Change, Migration & Decommission Scenarios

[Ouvrir](08-change-migration-decommission-impact-scenarios.md)

Couvre :

- application replacement ;
- interface deprecation ;
- technology upgrade/retirement ;
- DB migration ;
- shared DB split ;
- cloud/OpenShift migration ;
- site/vendor exit ;
- regulatory/data classification changes ;
- M&A/carve-out ;
- migration sequencing ;
- coexistence ;
- cutover/rollback ;
- decommission readiness.

---

## 09 — Enterprise Landscapes, Domains, Segmentation & Federation

[Ouvrir](09-enterprise-landscapes-domains-segmentation-federation.md)

Couvre :

- enterprise landscapes ;
- domain cartography ;
- shared services ;
- cross-domain dependencies ;
- geographic/legal entity scopes ;
- federated ownership ;
- map hierarchy ;
- context maps ;
- large graph partitioning ;
- community-detection concept ;
- MayaBank domain map.

---

## 10 — Data Flow, Information & Control Dependency Analysis

[Ouvrir](10-data-flow-information-control-dependency-analysis.md)

Couvre :

- information dependency ;
- producer/consumer ;
- functional/technical lineage ;
- schema/event dependencies ;
- source of truth/replica/cache ;
- batch/CDC ;
- quality/freshness/completeness ;
- control/evidence dependencies ;
- privacy/residency/retention ;
- reconciliation and consistency.

---

## 11 — Graph Analytics, Metrics, Queries & Evidence

[Ouvrir](11-graph-analytics-metrics-queries-and-evidence.md)

Couvre :

- degree/in-degree/out-degree ;
- reachability ;
- path length ;
- path diversity ;
- centrality concepts ;
- connected components ;
- completeness/freshness/confidence metrics ;
- dependency debt ;
- query library ;
- graph export boundary ;
- API / graph database as complementary analysis tools.

Les métriques avancées sont présentées comme **méthodes génériques**, pas comme fonctionnalités Hopex natives garanties.

---

## 12 — MayaBank Enterprise Cartography Reference Model

[Ouvrir](12-mayabank-enterprise-cartography-reference-model.md)

Contient :

- 8 business domains ;
- capabilities ;
- process `Execute Instant Payment` ;
- 12 applications canoniques ;
- external services ;
- 12 information objects ;
- 9 platform/service domains ;
- synchronous critical chain ;
- asynchronous chain ;
- source-of-truth mapping ;
- cross-domain dependencies ;
- hubs/bridges/SPOF candidates ;
- current/target ;
- 4 transition states ;
- 4 migration units ;
- 6 impact scenarios ;
- **12 reference views** ;
- **12 reference matrices**.

---

## 13 — Governance, Quality, Anti-Patterns & Mission Playbook

[Ouvrir](13-governance-quality-antipatterns-mission-playbook.md)

Couvre :

- roles/RACI ;
- dependency lifecycle ;
- source hierarchy ;
- evidence/attestation ;
- quality dimensions/rules ;
- architecture board entry/exit criteria ;
- incident feedback loop ;
- discovery governance ;
- conflict resolution ;
- spaghetti map / fake precision / stale graph ;
- mission 4 semaines ;
- 30/60/90-day plan ;
- interview cases ;
- maturity model.

---

# Pratique

## 90 — 24 Labs + 40 Questions Corrigées

[Ouvrir](90-labs-and-review.md)

### Labs

1. Enterprise Context Map.
2. Typed Dependency Register.
3. Direct vs Transitive Dependencies.
4. Traversal Rule Card.
5. Critical Dependency Path.
6. Hard vs Soft Dependencies.
7. IAM Blast Radius.
8. Event Streaming Blast Radius.
9. Hub Detection.
10. Cycle Detection.
11. Bridge / Choke Point.
12. Shared Failure Domain.
13. Recovery Dependency Graph.
14. Minimum Viable Service.
15. Interface Deprecation.
16. Technology Obsolescence Blast Radius.
17. Data Schema Change.
18. Shared Database Split.
19. Site Exit.
20. External Provider Dependency.
21. Current / Target Dependency Delta.
22. Migration Units.
23. Dependency Quality Audit.
24. Architecture Board Scenario.

Puis **40 questions corrigées** couvrant tout le domaine.

---

# Sources

## 99 — Sources officielles & frontière de vérification

[Ouvrir](99-official-sources.md)

Sources principales vérifiées :

- Bizzdesign Hopex product pages ;
- Bizzdesign Hopex French product page ;
- Global Bank customer story ;
- Nordea application management customer story ;
- connected repository customer stories ;
- Enterprise Architecture Repository guidance ;
- Application Rationalization guidance ;
- HOPEX Core Back-End Aquila 6.2 ;
- HOPEX REST API ;
- HOPEX GraphQL.

Baseline visible :

```text
Core Back-End: 62.18.0+774 — 2026-09-03
REST API:      62.18.0+69  — 2026-09-02
GraphQL:       62.18.0+69  — 2026-09-02
```

---

# Product facts vs analytical methods

## Vérifié publiquement pour Hopex

- repository business/IT/risk/data ;
- dependency mapping ;
- data-flow mapping ;
- hidden-impact identification ;
- impact analysis ;
- transformation analysis ;
- repository API access via REST/GraphQL selon modules/licences.

## Méthodes génériques du masterbook

```text
BFS / DFS
k-hop
centrality
betweenness
connected components
SCC
bridges
articulation points
community detection
blast-radius scoring
confidence scoring
```

Elles peuvent nécessiter API/export/outillage complémentaire.

---

# Cas MayaBank — résumé

## Current

```text
Digital Channel
→ Legacy Payment Gateway
→ Core / legacy integrations
→ Legacy Clearing
→ synchronous downstream

Shared DB
VM-heavy
Batch reconciliation
Fragmented observability
```

## Target

```text
Digital Channel
→ API Management
→ Payment Orchestrator
   ├→ IAM
   ├→ Fraud Decision Service
   ├→ Core Account Service
   └→ Clearing Gateway

PaymentStatusChanged
→ Event Streaming
   ├→ Notification
   ├→ Reconciliation
   └→ Analytics

OpenShift
Governed data
Central observability
Tested DR
```

---

# Règles à retenir

```text
Diagram ≠ Cartography
Association ≠ Dependency
Direct ≠ Transitive
High degree ≠ Business criticality
Hub ≠ SPOF automatically
Replica count ≠ Resilience proof
Async ≠ No dependency
Multi-site ≠ DR proof
Current ≠ Target
Temporary dependency needs retirement condition
Graph metric ≠ Decision
Discovery ≠ Verified truth
HOPEX ≠ CMDB
HOPEX ≠ Graph database runtime engine
```

---

# Chiffres de la Partie XII

- 13 chapitres complets ;
- 1 README de synthèse ;
- 1 modèle MayaBank end-to-end ;
- 12 applications de référence ;
- 12 information objects ;
- 12 vues de référence ;
- 12 matrices de référence ;
- 6 scénarios d’impact ;
- 4 migration units ;
- 24 labs ;
- 40 questions corrigées ;
- sources actuelles et frontière produit clairement documentées.

---

# Partie suivante

**Partie XIII — IT Business Management & Application Portfolio**

Elle approfondira :

- application portfolio inventory ;
- business value ;
- technical fitness ;
- functional fit ;
- lifecycle ;
- cost ;
- risk ;
- ownership ;
- rationalization ;
- TIME-like decision models ;
- duplicate applications ;
- cloud readiness ;
- modernization candidates ;
- portfolio governance ;
- MayaBank portfolio case.
