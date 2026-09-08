# 04 — Data Ownership, Stewardship, Governance & Lifecycle

## 1. Pourquoi la gouvernance est structurelle

Une architecture data sans responsabilités devient rapidement obsolète.

Pour chaque domaine ou information critique, il faut savoir :

```text
Who owns?
Who stewards?
Who produces?
Who consumes?
Who approves change?
Who monitors quality?
Who authorizes access?
```

## 2. Rôles

### Data Owner
Accountable sur définition, usage, qualité attendue et décisions structurantes.

### Data Steward
Maintient glossary, règles, qualité documentaire, coordination et remédiation.

### Data Custodian
Responsabilité technique de stockage/exploitation selon l’organisation.

### Data Architect
Structure domaines, modèles, lineage et target architecture.

### Security/Privacy
Valide classification, accès, conservation et traitements sensibles.

### Producer / Consumer Owner
Responsables des systèmes qui produisent ou consomment.

## 3. Operating model

Exemple MayaBank :

```text
Enterprise Data Council
  ↓
Domain Data Owners
  ↓
Data Stewards
  ↓
Application/Data Platform Teams
```

Les décisions quotidiennes doivent rester décentralisées quand possible, avec des règles enterprise partagées.

## 4. Lifecycle d’un data asset

```text
Proposed
→ Defined
→ Reviewed
→ Approved
→ Published
→ Changed
→ Deprecated
→ Retired
```

Les statuts exacts dépendent du client et de la configuration HOPEX.

## 5. Lifecycle de la donnée opérationnelle

À distinguer du lifecycle du modèle :

```text
Create
→ Use
→ Share
→ Transform
→ Archive
→ Delete
```

Cette chaîne doit intégrer :

- retention ;
- legal hold ;
- purge ;
- anonymization/pseudonymization ;
- archival requirements.

## 6. Change governance

Un changement de définition ou de schema doit déclencher :

1. impact analysis ;
2. identification producers/consumers ;
3. classification du breaking change ;
4. plan de migration ;
5. validation owner ;
6. communication ;
7. observation post-change.

## 7. Data contract governance

Un contrat de données devrait documenter :

```text
Owner
Schema
Semantics
Version
Quality objectives
Compatibility rules
Security classification
SLA/SLO if relevant
Retention
Consumer expectations
```

## 8. Governance workflow MayaBank

Exemple pour `Payment Status` :

```text
Change proposed
→ Payments Data Steward review
→ Application impact analysis
→ Data Owner approval
→ Security/Compliance review if needed
→ contract versioning
→ rollout
→ post-change validation
```

## 9. Issue management

Un data issue doit être relié à :

- data asset ;
- impact ;
- owner ;
- severity ;
- root cause ;
- remediation ;
- due date ;
- evidence.

## 10. Data policy

Une politique peut définir :

- naming ;
- classification ;
- minimum quality ;
- encryption ;
- access ;
- retention ;
- sharing ;
- lineage requirements ;
- critical data element rules.

## 11. Critical Data Elements

Tous les champs n’ont pas la même criticité.

Exemples MayaBank :

```text
PaymentId
Amount
Currency
Debtor Account
Creditor Account
Payment Status
Execution Timestamp
Fraud Decision
```

Pour ces éléments, renforcer : ownership, quality, lineage, controls et monitoring.

## 12. Federated governance

Approche :

```text
Enterprise standards
+ domain autonomy
+ shared tooling
+ common controls
```

Éviter deux extrêmes :

- centralisation totale qui bloque les équipes ;
- autonomie totale qui crée des définitions concurrentes.

## 13. Governance matrix

| Object | Accountable | Maintainer | Reviewer |
|---|---|---|---|
| Data Domain | Domain Owner | Data Architect | Data Council |
| Business Term | Data Owner | Steward | SMEs |
| Logical Model | Data Owner | Data Architect | App/Data teams |
| Quality Rule | Data Owner | Steward | Operations |
| Classification | Data Owner | Steward | Security/Privacy |

## 14. Review triggers

Revue obligatoire lors de :

- nouveau règlement ;
- nouvelle application ;
- migration DB ;
- nouvelle API/event ;
- incident data majeur ;
- changement de source of truth ;
- fusion d’entités ;
- changement de retention ;
- décommissionnement.

## 15. Governance KPIs

Exemples :

- % critical data elements avec owner ;
- % glossary terms approved ;
- % data assets avec classification ;
- % critical flows avec lineage ;
- overdue data issues ;
- average remediation time ;
- % schemas avec owner/version policy.

## 16. Anti-patterns

- Data Owner nominal sans décision réelle ;
- steward chargé de tout sans authority ;
- governance board pour chaque petit changement ;
- politique sans contrôle ;
- workflow trop lourd qui pousse les équipes hors outil ;
- données critiques non identifiées ;
- lifecycle documentaire confondu avec retention opérationnelle.

## 17. Mission checklist

1. owners nommés ;
2. stewards actifs ;
3. domains définis ;
4. glossary validé ;
5. critical data identifié ;
6. rules documentées ;
7. lifecycle défini ;
8. change process opérationnel ;
9. issues suivis ;
10. KPIs de gouvernance utilisés.
