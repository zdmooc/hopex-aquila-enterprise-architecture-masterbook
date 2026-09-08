# Partie VIII — Application Architecture

Cette partie approfondit l’**Application Architecture** dans Bizzdesign Hopex / HOPEX Aquila : catalogue applicatif, responsabilités, business alignment, services, interfaces, flux, intégration, dépendances, déploiements, NFR, données, lifecycle et architectures current/transition/target.

Elle complète la Partie IV sans la recopier :

```text
Partie IV
HOPEX IT Architecture transverse

Partie VIII
Application Architecture détaillée

Partie IX
Information & Data Architecture détaillée

Partie X
Technology & Infrastructure Architecture détaillée

Partie XIII
Application Portfolio Management / IT Business Management
```

Le fil rouge reste **MayaBank**.

---

## Objectifs

À la fin de cette partie, vous devez savoir :

- construire un Application Catalog canonique ;
- définir la bonne granularité d’une application ;
- distinguer Application, Capability, Process, Service, Component, Technology et Deployment ;
- mapper applications vers capabilities/processes/business services ;
- documenter interfaces, providers, consumers et informations échangées ;
- choisir et expliquer synchronous API, messaging, event-driven, batch et adapters ;
- analyser orchestration vs choreography ;
- identifier couplages point-to-point et shared database ;
- construire un dependency graph et réaliser une impact analysis ;
- analyser le blast radius d’un changement ou d’une panne ;
- modéliser deployment/environments sans transformer HOPEX en CMDB ;
- relier application et OpenShift/cloud de façon utile ;
- construire un NFR catalogue ;
- analyser availability, RTO/RPO, performance, scalability et observability ;
- mapper application ↔ information/data store/source of truth ;
- analyser lifecycle, obsolescence et dette applicative ;
- construire Current / Transition / Target ;
- préparer une migration strangler/replatform/refactor/replace/retire ;
- gouverner la qualité du repository applicatif ;
- défendre une architecture applicative en Architecture Board.

---

# Chapitres

## 01 — Application Architecture : rôle, périmètre et méthode

[Ouvrir](01-application-architecture-role-scope-method.md)

Couvre :

- rôle de l’Application Architecture ;
- frontières avec APM, Data et Technology Architecture ;
- Application vs Capability/Process/Service/Technology/Deployment ;
- méthode de construction ;
- niveaux de vues ;
- MayaBank baseline.

## 02 — Application Catalog, granularity et modèle canonique

[Ouvrir](02-application-catalog-granularity-canonical-model.md)

Couvre :

- Application ID Card ;
- canonical application ;
- aliases ;
- ownership ;
- lifecycle ;
- criticality ;
- SaaS/COTS/custom ;
- shared applications ;
- duplicate detection ;
- environnement ≠ application.

## 03 — Business alignment

[Ouvrir](03-business-alignment-capability-process-service.md)

Couvre :

- Capability ↔ Application ;
- Process/Activity ↔ Application ;
- Business Service ↔ Application Service ;
- functional scope ;
- responsibility maps ;
- business impact chain.

## 04 — Interactions, interfaces, flux et contrats

[Ouvrir](04-interactions-interfaces-flows-contracts.md)

Couvre :

- provider/consumer ;
- interface contract ;
- REST ;
- messaging ;
- batch/file ;
- database coupling ;
- versioning ;
- timeout/retry/idempotency ;
- security context.

## 05 — Integration Architecture

[Ouvrir](05-integration-architecture-patterns.md)

Couvre :

- point-to-point ;
- API-centric ;
- event-driven ;
- command vs event ;
- orchestration ;
- choreography ;
- ESB ;
- adapters ;
- saga/compensation ;
- eventual consistency ;
- API Gateway vs Service Mesh.

## 06 — Dependency Mapping et Impact Analysis

[Ouvrir](06-dependency-mapping-impact-analysis.md)

Couvre :

- upstream/downstream ;
- direct/transitive dependencies ;
- critical path ;
- blast radius ;
- interface deprecation impact ;
- decommission impact ;
- technology/data impact ;
- SPOF logique ;
- dependency confidence.

## 07 — Deployment Architecture

[Ouvrir](07-deployment-architecture-environments-platforms.md)

Couvre :

- logical vs deployment ;
- environments ;
- OpenShift ;
- cloud ;
- on-prem ;
- SaaS ;
- failure domains ;
- multi-site ;
- stateful/stateless ;
- HOPEX vs CMDB.

## 08 — Non-Functional Architecture

[Ouvrir](08-non-functional-architecture-resilience-security-observability.md)

Couvre :

- availability ;
- reliability ;
- resilience ;
- RTO/RPO ;
- performance budget ;
- throughput/scalability ;
- security ;
- trust boundaries ;
- auditability ;
- metrics/logs/traces ;
- SLI/SLO/SLA ;
- operational readiness.

## 09 — Application ↔ Data Architecture

[Ouvrir](09-application-data-responsibilities-consistency.md)

Couvre :

- information ownership ;
- source of truth ;
- CRUD ;
- data stores ;
- shared DB ;
- replication/cache ;
- events ;
- eventual consistency ;
- reconciliation ;
- data migration.

## 10 — Lifecycle, standards, obsolescence et dette

[Ouvrir](10-lifecycle-standards-obsolescence-debt.md)

Couvre :

- application vs technology lifecycle ;
- IT-Pedia integration context ;
- standards/exceptions ;
- architecture debt ;
- technology impact ;
- sunset/decommission readiness ;
- modernization drivers.

## 11 — Current, Transition et Target

[Ouvrir](11-current-transition-target-application-architecture.md)

Couvre :

- current baseline ;
- target drivers ;
- transition states ;
- strangler ;
- rehost/replatform/refactor/rearchitect/replace/retire ;
- coexistence ;
- cutover/rollback ;
- MayaBank migration waves.

## 12 — MayaBank Application Model complet

[Ouvrir](12-mayabank-application-reference-model.md)

Contient :

- 12 applications canoniques ;
- catalog ;
- Capability × Application ;
- Activity × Application ;
- interaction view ;
- interface catalogue ;
- data responsibilities ;
- deployment ;
- NFR ;
- risk map ;
- current/target ;
- 4 transition states ;
- 10 matrices ;
- 10 vues de référence.

## 13 — Gouvernance, anti-patterns et mission playbook

[Ouvrir](13-governance-quality-antipatterns-mission-playbook.md)

Couvre :

- rôles ;
- review lifecycle ;
- quality gates ;
- data quality indicators ;
- anti-patterns ;
- mission 4 semaines ;
- Architecture Board ;
- option analysis ;
- cas d’entretien ;
- maturity model.

---

# Pratique

## 90 — 24 labs + 40 questions corrigées

[Ouvrir](90-labs-and-review.md)

Labs :

1. Canonical Application Catalog.
2. Duplicate Detection.
3. Application Granularity.
4. Capability × Application Matrix.
5. Activity × Application.
6. Responsibility Map.
7. Interaction Diagram.
8. Interface Catalogue.
9. Hidden Dependency Hunt.
10. Integration Pattern Review.
11. Synchronous Chain Analysis.
12. Event-Driven Decoupling.
13. Dependency Blast Radius.
14. Interface Deprecation.
15. Deployment View.
16. Shared Failure Domain.
17. NFR Catalogue.
18. Performance Budget.
19. Data Responsibility Map.
20. Shared Database Refactoring.
21. Obsolescence Impact.
22. Current/Transition/Target.
23. Decommission Readiness.
24. Architecture Board.

Puis **40 questions corrigées** couvrant tout le domaine.

---

# Sources

## 99 — Sources officielles et frontière de vérification

[Ouvrir](99-official-sources.md)

Sources publiques vérifiées/recoupées en septembre 2026 :

- HOPEX Core Back-End Aquila 6.2 ;
- HOPEX Enterprise Architecture offer ;
- HOPEX Platform features ;
- Bizzdesign Application Portfolio Management ;
- Application Rationalization playbook ;
- cas client Nordea ;
- training database Aquila ;
- ITPM Excel Import Template ;
- IT-Pedia integration ;
- ArchiMate add-on ;
- ressources communautaires historiques clairement signalées.

---

# Cas MayaBank — résumé

## Current

```text
Digital Channel
→ Legacy Payment Hub
→ Fraud appliance
→ Core
→ Legacy Clearing Adapter
→ synchronous Notification

Shared DB
Batch reconciliation
VM deployment
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
   ├→ Notification Service
   ├→ Reconciliation Service
   └→ Analytics

OpenShift + governed data + observability
```

---

# Règles à retenir

```text
Application ≠ Capability
Application ≠ Server
Application ≠ Namespace
Application ≠ Technology
Application Service ≠ API endpoint automatically
Interface ≠ unlabelled arrow
Kafka topic ≠ Business Event automatically
Database ≠ Data Domain
HOPEX ≠ CMDB
Rehost ≠ full modernization
Target ≠ transformation plan
```

---

# Chiffres de la Partie VIII

- 13 chapitres complets ;
- 1 README de synthèse ;
- 1 modèle applicatif MayaBank end-to-end ;
- 12 applications de référence ;
- 10 matrices de référence dans le blueprint ;
- 10 vues de référence ;
- 24 labs ;
- 40 questions corrigées ;
- sources produit séparées des recommandations ;
- frontière explicite avec les Parties IX, X, XIII et XIV.

---

# Partie suivante

**Partie IX — Information & Data Architecture**

Elle reprendra le fil rouge MayaBank sous l’angle :

- information architecture ;
- data domains ;
- business information ;
- conceptual/logical/physical data models ;
- data dictionary ;
- data ownership/stewardship ;
- lineage ;
- data quality ;
- database architecture ;
- data flows ;
- data lifecycle ;
- privacy/classification ;
- HOPEX Information Architecture.
