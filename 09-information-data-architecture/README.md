# Partie IX — Information & Data Architecture

Cette partie approfondit l’**Information & Data Architecture** dans Bizzdesign Hopex / HOPEX Aquila : information concepts, data domains, glossary, conceptual/logical/physical modeling, ownership, lineage, quality, privacy, persistence, master/reference data, integration et architectures current/transition/target.

Elle complète les Parties IV et VIII sans les recopier :

```text
Partie IV
HOPEX IT Architecture transverse

Partie VIII
Application Architecture détaillée

Partie IX
Information & Data Architecture détaillée

Partie X
Technology & Infrastructure Architecture détaillée

Partie XVI
Repository Governance & Data Quality du repository HOPEX
```

Le fil rouge reste **MayaBank — Execute Instant Payment**.

---

# Objectifs

À la fin de cette partie, vous devez savoir :

- distinguer Information, Data, Business Term, Data Entity, Data Store et Data Product ;
- construire des Data Domains ;
- construire un Business Glossary gouverné ;
- gérer synonymes/homonymes ;
- modéliser conceptual/logical/physical ;
- relier business terms aux modèles physiques ;
- utiliser le reverse engineering sans confondre metadata et modèle métier ;
- définir Data Owner / Data Steward / Custodian ;
- identifier Critical Data Elements ;
- construire functional lineage et source-to-target mappings ;
- distinguer functional et technical lineage ;
- réaliser une impact analysis via lineage ;
- définir des règles de data quality ;
- relier qualité et business impact ;
- classifier les données ;
- traiter privacy, minimization, retention et deletion propagation ;
- choisir des persistence patterns selon les besoins ;
- analyser shared database, replication, cache et consistency ;
- définir Master Data / Reference Data / source authority ;
- concevoir APIs, events, batch, CDC et data contracts ;
- préparer une migration et sa reconciliation ;
- construire Current / Transition / Target ;
- défendre une Data Architecture en Architecture/Data Board.

---

# Chapitres

## 01 — Information & Data Architecture : rôle, périmètre et méthode

[Ouvrir](01-information-data-architecture-role-scope-method.md)

Couvre :

- Information vs Data ;
- rôle de l’architecte ;
- frontières avec Application/Technology Architecture ;
- 10 artefacts fondamentaux ;
- méthode en 12 étapes ;
- granularité ;
- MayaBank baseline.

## 02 — Data Domains, Business Glossary et Information Concepts

[Ouvrir](02-data-domains-business-glossary-information-concepts.md)

Couvre :

- Data Domains ;
- Business Terms ;
- preferred terms/aliases ;
- concept maps ;
- ownership ;
- Master vs Reference Data ;
- Data Products ;
- matrices Domain × Information et Information × Owner.

## 03 — Conceptual, Logical & Physical Data Modeling

[Ouvrir](03-conceptual-logical-physical-data-modeling.md)

Couvre :

- conceptual model ;
- logical model ;
- physical model ;
- traceability between levels ;
- database reverse engineering ;
- keys/cardinalities ;
- transactional vs analytical ;
- bounded contexts ;
- API/event schemas ;
- schema evolution.

## 04 — Data Ownership, Stewardship, Governance & Lifecycle

[Ouvrir](04-data-ownership-stewardship-governance-lifecycle.md)

Couvre :

- Data Owner ;
- Data Steward ;
- Custodian ;
- operating model ;
- lifecycle du modèle et de la donnée ;
- change governance ;
- data contracts ;
- policies ;
- Critical Data Elements ;
- federated governance.

## 05 — Data Lineage, Data Flows & Transformation Analysis

[Ouvrir](05-data-lineage-flows-transformation-analysis.md)

Couvre :

- functional vs technical lineage ;
- source-to-target ;
- transformations ;
- batch/event/API/database lineage ;
- confidence ;
- Data Discovery ;
- change impact ;
- root-cause analysis ;
- regulatory traceability.

## 06 — Data Quality Architecture, Controls & Observability

[Ouvrir](06-data-quality-controls-observability.md)

Couvre :

- quality dimensions ;
- CDE ;
- preventive/detective/corrective controls ;
- quality rules ;
- data observability ;
- quality incidents ;
- data SLOs ;
- migration quality gates.

## 07 — Data Classification, Privacy, Security & Retention

[Ouvrir](07-data-classification-privacy-security-retention.md)

Couvre :

- classification ;
- personal/sensitive data ;
- privacy by design ;
- minimization ;
- encryption/access ;
- masking/tokenization ;
- retention ;
- deletion propagation ;
- residency ;
- non-production data.

## 08 — Database Architecture, Stores & Persistence Patterns

[Ouvrir](08-database-stores-persistence-patterns.md)

Couvre :

- relational/document/key-value ;
- event log ;
- object storage ;
- warehouse/lake/lakehouse ;
- shared DB ;
- database per service ;
- replication/cache/read models ;
- consistency ;
- HA/DR context ;
- HOPEX DB design modules.

## 09 — Master Data, Reference Data & Source of Truth

[Ouvrir](09-master-reference-data-source-of-truth.md)

Couvre :

- Source of Truth/System of Record conventions ;
- Master Data ;
- Reference Data ;
- identity resolution ;
- golden record ;
- legitimate vs risky duplication ;
- authoritative matrix ;
- reconciliation ;
- source authority migration.

## 10 — Data Integration, APIs, Events, Batch & CDC

[Ouvrir](10-data-integration-api-events-batch-cdc.md)

Couvre :

- APIs ;
- events ;
- commands ;
- batch/files ;
- CDC ;
- ETL/ELT ;
- schema registry concept ;
- idempotency ;
- ordering ;
- dead-letter/quarantine ;
- contract compatibility.

## 11 — Current, Transition & Target Data Architecture

[Ouvrir](11-current-transition-target-data-architecture.md)

Couvre :

- current assessment ;
- target principles ;
- four transition states ;
- big-bang/strangler/dual-run ;
- backfill + CDC ;
- migration phases ;
- reconciliation ;
- rollback ;
- decommission readiness.

## 12 — MayaBank Information & Data Reference Model

[Ouvrir](12-mayabank-information-data-reference-model.md)

Contient :

- 5 Data Domains principaux ;
- Information Concept Map ;
- glossary sample ;
- logical Payment model ;
- source-of-truth matrix ;
- Application × Data Domain ;
- CRUD matrix ;
- functional/exception lineage ;
- CDEs ;
- quality rules ;
- classification ;
- stores/contracts ;
- current/target ;
- 4 waves ;
- 12 matrices ;
- 12 vues.

## 13 — Governance Quality, Anti-Patterns & Mission Playbook

[Ouvrir](13-governance-quality-antipatterns-mission-playbook.md)

Couvre :

- repository quality gates ;
- maturity model ;
- anti-patterns ;
- mission 4 semaines ;
- Board pack ;
- interview cases ;
- operational cadence ;
- final checklist.

---

# Pratique

## 90 — 24 labs + 40 questions corrigées

[Ouvrir](90-labs-and-review.md)

Les labs couvrent :

1. Data Domain Map.
2. Business Glossary.
3. Synonym/Homonym Review.
4. Conceptual Model.
5. Logical Payment Model.
6. Physical Mapping.
7. Inter-level Traceability.
8. Source-of-Truth Matrix.
9. Duplicate Authority Analysis.
10. Functional Lineage.
11. Transformation Catalogue.
12. Lineage Impact Analysis.
13. Critical Data Elements.
14. Data Quality Rules.
15. Data Quality Incident.
16. Classification Map.
17. Privacy by Design.
18. Retention Architecture.
19. Store Architecture.
20. Shared Database Refactoring.
21. Data Contract.
22. Current/Target.
23. Migration & Reconciliation.
24. Data Architecture Board.

Puis **40 questions corrigées**.

---

# Sources

## 99 — Sources officielles et frontière de vérification

[Ouvrir](99-official-sources.md)

Sources publiques recoupées en septembre 2026 :

- HOPEX Core Back-End Aquila 6.2 `62.18.0+774` ;
- HOPEX Web Front-End `62.18.0+143` ;
- HOPEX Data Governance public features ;
- HOPEX Information Architecture positioning ;
- HOPEX Data Discovery ;
- HOPEX Data Source Extractor ;
- Database Design Oracle 19c ;
- SQL ANSI Database Design ;
- BCBS 239 sample ;
- Aquila 6.2 CU5 training database.

---

# MayaBank — vue synthétique

## Current

```text
Duplicate customer data
+ shared DB
+ multiple payment statuses
+ batch reconciliation
+ weak glossary
+ limited lineage
+ manual repairs
```

## Target

```text
Governed Data Domains
→ glossary
→ conceptual/logical models
→ authoritative sources
→ versioned APIs/events
→ functional lineage
→ quality controls
→ classified critical data
→ reconciliation
→ governed lifecycle
```

---

# Règles à retenir

```text
Information ≠ Data representation
Data Domain ≠ Application
Business Term ≠ Column
Conceptual Model ≠ Physical Schema
Reverse Engineering ≠ Business Model
Data Owner ≠ DBA automatically
Functional Lineage ≠ Technical Lineage
Data Flow ≠ unlabeled arrow
Source of Truth ≠ every replica
Reference Data ≠ Master Data
Backup ≠ Retention
Cache ≠ Authoritative Source
Event Schema ≠ Enterprise Logical Model
HOPEX ≠ runtime data observability platform
```

---

# Chiffres de la Partie IX

- 13 chapitres complets ;
- 1 README de synthèse ;
- 1 modèle MayaBank Information & Data end-to-end ;
- 5 domaines principaux détaillés ;
- 12 matrices de référence ;
- 12 vues de référence ;
- 24 labs ;
- 40 questions corrigées ;
- sources produit séparées des recommandations ;
- frontière explicite avec les Parties VIII, X et XVI.

---

# Partie suivante

**Partie X — Technology & Infrastructure Architecture**

Elle couvrira :

- compute ;
- network ;
- storage ;
- databases as technologies ;
- middleware ;
- OpenShift/Kubernetes ;
- cloud Azure/AWS/GCP ;
- on-prem ;
- HA/DR ;
- observability ;
- IAM/security infrastructure ;
- capacity/performance ;
- standards/lifecycle ;
- Green IT/FinOps ;
- MayaBank deployment/infrastructure reference model.
