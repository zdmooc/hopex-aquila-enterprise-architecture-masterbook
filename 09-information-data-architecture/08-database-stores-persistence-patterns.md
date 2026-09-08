# 08 — Database Architecture, Stores & Persistence Patterns

## 1. Database architecture in enterprise context

L’objectif n’est pas de recopier le DDL. Il faut comprendre :

- rôle du store ;
- data ownership ;
- consistency model ;
- availability ;
- scalability ;
- lifecycle ;
- coupling ;
- replication ;
- recovery ;
- technology risk.

## 2. Relational database

Appropriée lorsque :

- transactions structurées ;
- relations fortes ;
- contraintes d’intégrité ;
- SQL/reporting ;
- cohérence transactionnelle importante.

Exemple MayaBank : Payment Operational Store.

## 3. Document store

Approprié pour :

- structures flexibles ;
- agrégats documentaires ;
- évolution de schema maîtrisée.

Ne pas choisir uniquement parce que « NoSQL scale mieux ».

## 4. Key-value

Utile pour :

- cache ;
- session ;
- lookup très rapide ;
- idempotency keys.

Il ne remplace pas automatiquement la source transactionnelle.

## 5. Event log / streaming

Un event log conserve des faits ordonnés.

Questions :

- retention ;
- partition key ;
- replay ;
- ordering ;
- duplicate delivery ;
- schema evolution ;
- sensitive data.

## 6. Object storage

Approprié à :

- fichiers ;
- archives ;
- datasets ;
- data lake ;
- exports volumineux.

Le bucket physique appartient plutôt à l’architecture technique détaillée ; le repository EA doit documenter le rôle et les dépendances utiles.

## 7. Data warehouse

Optimisé pour analyse structurée, historique et reporting.

Exemple :

```text
Operational Payment Data
→ governed ingestion
→ Payment Warehouse
→ regulatory/management reporting
```

## 8. Data lake / lakehouse

Peut servir analytics, ML et ingestion multi-format.

Architecture à clarifier :

- zones ;
- ownership ;
- catalog ;
- schema ;
- quality ;
- retention ;
- serving layer.

Un lake sans gouvernance peut devenir un data swamp.

## 9. Shared database anti-pattern

```text
App A ─┐
App B ─┼→ same schema/tables
App C ─┘
```

Risques :

- hidden coupling ;
- schema change blast radius ;
- unclear ownership ;
- bypass business rules ;
- release coupling.

Target possible : ownership explicite + service/API/event contracts.

## 10. Database per service

Avantages possibles : autonomie, ownership, déploiement indépendant.

Coûts :

- distributed consistency ;
- duplication ;
- reporting complexity ;
- operations ;
- reconciliation.

Ce n’est pas une règle universelle.

## 11. Replication

Types conceptuels :

- synchronous ;
- asynchronous ;
- logical ;
- physical ;
- CDC.

Documenter surtout :

```text
source authority
lag
failure behavior
conflict handling
RPO implications
```

## 12. Cache

Un cache doit avoir :

- source of truth ;
- invalidation strategy ;
- TTL ;
- stale data tolerance ;
- fallback behavior.

## 13. Read model

CQRS ou projection analytique peut produire des données dérivées.

```text
Payment source
→ event
→ read model
```

Le read model n’est pas authoritative pour toutes les décisions.

## 14. Consistency choices

### Strong consistency

Pertinente pour certaines opérations financières critiques.

### Eventual consistency

Acceptable pour certains consommateurs dérivés comme notification/analytics.

L’architecture doit expliciter où l’incohérence temporaire est acceptable.

## 15. Backup / HA / DR

Pour chaque store critique :

- backup policy ;
- restore test ;
- replication ;
- failure domain ;
- RTO/RPO ;
- data loss behavior.

Les mécanismes techniques précis seront approfondis Partie X.

## 16. Database design modules HOPEX

Le Store MEGA publie des modules de types de données pour différents DBMS, utilisés notamment pour les niveaux physiques et la synchronisation logique/physique. Cela confirme que HOPEX peut modéliser ces niveaux, mais les modules/version exacts doivent être vérifiés selon le DBMS client.

## 17. MayaBank store map

```text
Customer Master Store
Account Core Store
Payment Operational Store
Fraud Feature/Decision Store
Event Streaming
Reconciliation Store
Analytics Store
Reference Data Store
```

## 18. Store × Owner matrix

| Store | Authoritative for | Owner |
|---|---|---|
| Customer Master | Customer profile | Customer domain |
| Core Account DB | Account/balance | Account domain |
| Payment Store | Payment state | Payments domain |
| Fraud Store | Fraud decision evidence | Fraud domain |

## 19. Selection criteria

1. access pattern ;
2. consistency ;
3. volume ;
4. latency ;
5. durability ;
6. query model ;
7. data lifecycle ;
8. operations capability ;
9. compliance ;
10. cost.

## 20. Anti-patterns

- technologie choisie par mode ;
- un DB par microservice sans capacité ops ;
- shared DB non documentée ;
- cache traité comme source ;
- async replication sans analyse RPO ;
- warehouse utilisé comme transaction source ;
- data lake sans ownership/catalog/quality.
