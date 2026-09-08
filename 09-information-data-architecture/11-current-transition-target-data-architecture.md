# 11 — Current, Transition & Target Data Architecture

## 1. Pourquoi trois états

Une target architecture sans chemin de transition reste théorique.

```text
Current
→ Transition states
→ Target
```

## 2. Current assessment

Pour chaque domaine :

- authoritative source ;
- duplicates ;
- data stores ;
- flows ;
- batch windows ;
- quality issues ;
- ownership ;
- classification ;
- lineage coverage ;
- technology risk.

## 3. MayaBank current

```text
Customer data duplicated CRM/Core
Payment status in multiple stores
Shared DB integrations
Nightly batch reconciliation
Point-to-point files
Limited lineage
Weak glossary
Manual data fixes
Analytics copy with unclear ownership
```

## 4. Pain-point taxonomy

### Semantic
Definitions inconsistent.

### Structural
Schemas/models fragmented.

### Ownership
No accountable owner.

### Integration
Point-to-point/batch dependency.

### Quality
Frequent defects and repair.

### Security
Classification/access unclear.

### Lifecycle
Retention and decommission not governed.

## 5. Target principles MayaBank

1. governed data domains ;
2. glossary aligned with business architecture ;
3. explicit sources of truth ;
4. canonical concepts without forcing one physical schema ;
5. versioned data contracts ;
6. lineage for critical data ;
7. quality controls at source ;
8. classification/privacy by design ;
9. event-driven distribution where useful ;
10. reconciliation for distributed consistency.

## 6. Transition State 1 — Visibility

```text
Inventory
+ glossary
+ owner assignment
+ critical data identification
+ current lineage
```

No major runtime change yet.

## 7. Transition State 2 — Governance

```text
Source-of-truth decisions
+ quality rules
+ classification
+ contract ownership
+ issue workflow
```

## 8. Transition State 3 — Decoupling

```text
shared DB reduction
+ APIs/events
+ reference data service
+ lineage automation
+ reconciliation
```

## 9. Transition State 4 — Optimization

```text
retire duplicate stores
+ reduce batch
+ improve data products
+ automate quality/lineage
+ optimize retention/cost
```

## 10. Migration patterns

### Big-bang
High risk for critical data unless scope small and controllable.

### Strangler
Move producers/consumers progressively.

### Dual run
Old/new sources coexist temporarily.

### Backfill + CDC
Historical load followed by change capture.

### Event-first migration
New event contract becomes distribution mechanism before old store retirement.

## 11. Dual-write risk

```text
App
├→ old DB
└→ new DB
```

Risks : partial failure, ordering, reconciliation, rollback complexity.

Prefer patterns with authoritative source and controlled propagation.

## 12. Data migration phases

1. profiling ;
2. cleansing ;
3. mapping ;
4. rehearsal ;
5. initial load ;
6. delta sync ;
7. reconciliation ;
8. cutover ;
9. hypercare ;
10. old source retirement.

## 13. Reconciliation criteria

Before cutover define :

- record counts ;
- financial totals ;
- key uniqueness ;
- referential consistency ;
- business rule checks ;
- exception threshold.

## 14. Rollback strategy

Rollback must define :

```text
point of no return
write ownership
reverse synchronization
consumer routing
data reconciliation
```

## 15. Target lineage

Target state must show :

```text
source
→ governed contract
→ transformations
→ consumers
→ derived stores
```

## 16. Decommission readiness

Retire a data store only when :

1. no authoritative responsibility remains ;
2. consumers migrated ;
3. historical retention handled ;
4. legal/audit needs preserved ;
5. backup/archive decision made ;
6. monitoring shows no traffic ;
7. owner approves.

## 17. Roadmap dependencies

Data migration must align with :

- application migration ;
- API/event rollout ;
- platform readiness ;
- security controls ;
- operational training ;
- reporting migration.

## 18. Architecture decision record

Pour chaque décision importante :

```text
Context
Options
Decision
Data impacts
Migration impacts
Risks
Controls
Consequences
```

## 19. Anti-patterns

- target = nouveau cloud sans data model ;
- migration sans profiling ;
- dual-write permanent ;
- old master laissé actif ;
- consumers inconnus ;
- lineage créé après cutover ;
- décommission avant retention/audit check.
