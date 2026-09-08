# 13 — Governance Quality, Anti-Patterns & Mission Playbook

## 1. Mission objective

Une mission Information & Data Architecture ne doit pas se terminer par une collection de modèles. Elle doit laisser un **repository gouverné, des décisions, des responsabilités et une trajectoire de transformation**.

## 2. Minimum viable repository

Pour un domaine critique :

```text
Domain
+ glossary
+ owner/steward
+ conceptual model
+ source of truth
+ applications
+ data flows
+ lineage
+ quality rules
+ classification
+ current/target
```

## 3. Quality gates — Data Domain

Refuser publication si :

- scope ambigu ;
- owner absent ;
- overlap non arbitré ;
- aucune information principale ;
- aucune relation avec capabilities/processes/applications.

## 4. Quality gates — Business Term

- preferred name ;
- definition non circulaire ;
- domain ;
- owner ;
- aliases ;
- lifecycle status ;
- examples si utiles.

## 5. Quality gates — Data Model

- niveau explicite ;
- scope ;
- owner ;
- cardinalités ;
- relations ;
- current/target ;
- liens inter-level ;
- pas de duplications injustifiées.

## 6. Quality gates — Lineage

- source ;
- target ;
- information ;
- transformation ;
- owner ;
- confidence ;
- critical flow coverage.

## 7. Quality gates — Quality Rule

- CDE/data element ;
- test/formule ;
- target ;
- source ;
- owner ;
- severity ;
- remediation.

## 8. Quality gates — Classification

- policy/taxonomy ;
- rationale ;
- owner ;
- inheritance rule ;
- handling expectations.

## 9. Data architecture maturity

### Level 1 — Inventory

Databases and files listed.

### Level 2 — Semantics

Domains, glossary, conceptual models.

### Level 3 — Connected Architecture

Applications, processes, lineage, ownership.

### Level 4 — Governed & Measured

CDEs, quality, classification, issues, policies.

### Level 5 — Continuous Transformation

Automated discovery/lineage, data products, target roadmaps, metrics-driven improvement.

## 10. Anti-pattern — database-first enterprise model

Symptom : toutes les discussions commencent par tables et columns.

Correction : partir des concepts, usages et responsibilities.

## 11. Anti-pattern — glossary graveyard

Des milliers de termes sans validation ni usage.

Correction : prioriser les termes critiques reliés aux processus, applications et décisions.

## 12. Anti-pattern — lineage wallpaper

Immense diagramme impossible à analyser.

Correction : views par information critique, consumer, process ou impact scenario.

## 13. Anti-pattern — data lake = governance

Centraliser les données ne crée ni ownership ni qualité.

Correction : domains + contracts + catalog + lineage + controls.

## 14. Anti-pattern — one canonical model to rule them all

Un modèle universel trop abstrait bloque les domaines.

Correction : concepts enterprise + mappings explicites vers bounded contexts.

## 15. Anti-pattern — shared DB hidden integration

Correction : inventorier consumers, créer contracts, planifier découplage.

## 16. Anti-pattern — owner by application team

Un owner data doit représenter la responsabilité data/business appropriée, pas être automatiquement l’équipe qui héberge la table.

## 17. Anti-pattern — quality downstream only

Correction : root-cause et contrôles au producer, avec reconciliation downstream.

## 18. Anti-pattern — every copy is a master

Correction : authoritative-source matrix et purpose des derived copies.

## 19. Anti-pattern — privacy after design

Correction : classification, minimization, access et retention dès le modèle cible.

## 20. Anti-pattern — target cloud = data transformation

Migrer Oracle vers cloud sans clarifier ownership, data model, lineage et quality ne résout pas l’architecture data.

## 21. Mission 4 semaines — Week 1

### Discover

- stakeholders ;
- domains ;
- critical processes ;
- application/data stores ;
- major reports ;
- data incidents ;
- regulatory constraints.

Deliverables : scope + initial data landscape.

## 22. Week 2 — Model & Connect

- glossary ;
- concept maps ;
- current lineage ;
- source-of-truth matrix ;
- CDE list ;
- owners/stewards.

## 23. Week 3 — Analyze

- duplicate authority ;
- quality gaps ;
- shared DB ;
- batch dependencies ;
- sensitive-data flows ;
- technology/lifecycle impacts.

## 24. Week 4 — Target & Govern

- target data architecture ;
- transition states ;
- governance model ;
- quality backlog ;
- migration risks ;
- Architecture/Data Board pack.

## 25. Architecture Board pack

1. business problem ;
2. current data landscape ;
3. key risks ;
4. source-of-truth decisions ;
5. target model ;
6. lineage impacts ;
7. quality/security controls ;
8. transition plan ;
9. unresolved decisions ;
10. recommendation.

## 26. Interview case — duplicate customer master

Question : CRM et Core ont des customer profiles divergents.

Expected reasoning :

```text
Define semantics
→ identify use cases
→ identify authoritative attributes
→ map lineage
→ assess quality
→ define master/ownership
→ migration/sync strategy
→ reconciliation
```

## 27. Interview case — reporting inconsistency

Two regulatory reports show different payment totals.

Approach :

1. compare definitions ;
2. identify source datasets ;
3. trace lineage ;
4. compare transformations ;
5. verify cutoff/reference data ;
6. reconcile CDEs ;
7. fix root cause ;
8. add control.

## 28. Interview case — Kafka schema change

Question : ajouter/changer un field critique.

Approach :

```text
schema owner
→ compatibility
→ consumer inventory
→ classification
→ transformation impact
→ versioning
→ rollout
→ monitoring
```

## 29. Interview case — database migration

Question : Oracle to cloud-managed DB.

Do not answer only infrastructure.

Cover :

- logical model ;
- physical differences ;
- consumers ;
- replication ;
- migration ;
- reconciliation ;
- RPO/RTO ;
- cutover ;
- rollback ;
- lineage update.

## 30. Interview case — sensitive data in analytics

Approach :

- purpose ;
- minimization ;
- classification ;
- masking/tokenization ;
- access ;
- retention ;
- lineage ;
- owner approval.

## 31. Operational review cadence

### Monthly

- critical data issues ;
- schema changes ;
- owner gaps ;
- quality trends.

### Quarterly

- domain review ;
- lineage coverage ;
- target roadmap ;
- obsolete stores/contracts.

### Event-driven

- major incident ;
- regulatory change ;
- new data product ;
- source-of-truth change ;
- decommission.

## 32. Final mission checklist

- canonical domains ;
- glossary ;
- ownership ;
- conceptual/logical models ;
- critical sources ;
- consumer inventory ;
- lineage ;
- CDE/quality ;
- classification ;
- lifecycle ;
- target architecture ;
- transition roadmap ;
- governance cadence.
