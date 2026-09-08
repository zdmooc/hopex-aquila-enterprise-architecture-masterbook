# 09 — Application ↔ Data Architecture : responsabilités, stores et cohérence

## 1. Pourquoi relier applications et données

Une application architecture est incomplète si elle montre les appels sans montrer **les informations critiques créées, maîtrisées, lues ou propagées**.

Questions :

```text
Quelle application est source de vérité ?
Qui crée la donnée ?
Qui la consomme ?
Où est-elle persistée ?
Comment est-elle propagée ?
Quelle cohérence est attendue ?
Que se passe-t-il lors d’une migration ?
```

## 2. Application ↔ Information

Exemple :

```text
Payment Orchestrator
creates/maintains
Payment Execution State
```

```text
Fraud Decision Service
produces
Fraud Decision
```

```text
Core Account Service
owns/provides
Account and Funds Information
```

## 3. Source of truth

Le terme doit être explicite.

Une copie analytique n’est pas automatiquement source de vérité.

Exemple :

```text
Payment execution status
System of record = Payment Orchestrator state store
Read model = Customer Status View
Analytics copy = Data Platform
```

## 4. Data ownership vs application ownership

L’Application Owner n’est pas forcément Data Owner.

Distinguer :

- application operational responsibility ;
- data domain ownership ;
- data stewardship ;
- platform ownership.

## 5. CRUD matrix

Une matrice peut utiliser :

```text
C = Create
R = Read
U = Update
D = Delete
```

Exemple :

| Data | Payment Orch. | Fraud | Core Account | Notification |
|---|---|---|---|---|
| Payment Instruction | C/U | R | R | — |
| Fraud Decision | R | C | — | — |
| Account/Funds | R | — | C/U | — |
| Payment Status | C/U | — | — | R |
| Notification Record | — | — | — | C/U |

Le CRUD détaillé n’est utile que si maintenable.

## 6. Data store

Relier une application à ses stores lorsque cela aide à comprendre :

- state ;
- resilience ;
- data lifecycle ;
- coupling ;
- security ;
- migration.

Exemple :

```text
Payment Orchestrator
→ Payment State Store
```

## 7. Database is not data domain

```text
PostgreSQL
```

est une technologie/store.

```text
Payment
```

est un domaine/information concept.

Ne pas confondre architecture data et technologie de stockage.

## 8. Shared database risk

Si deux applications modifient directement les mêmes tables :

- ownership ambigu ;
- coupling de release ;
- schema evolution risquée ;
- sécurité complexe ;
- migration difficile.

Le modèle doit rendre cette dette visible.

## 9. Data replication

Copie nécessaire pour :

- analytics ;
- DR ;
- read model ;
- integration ;
- cache.

Documenter :

```text
source
consumer
mechanism
latency
consistency
retention
purpose
```

## 10. Cache

Un cache introduit :

- staleness ;
- invalidation ;
- fallback ;
- security ;
- capacity.

Il n’est pas source de vérité par défaut.

## 11. Event as data propagation

Exemple :

```text
PaymentStatusChanged
```

permet de propager un changement.

Documenter :

- producer ;
- schema owner ;
- consumers ;
- version ;
- ordering ;
- replay ;
- retention.

## 12. Event sourcing

Ne pas confondre `utiliser Kafka` avec `event sourcing`.

Event sourcing implique que l’état est dérivé d’une séquence d’événements gouvernée comme source de vérité.

C’est un choix structurant, pas un simple transport.

## 13. CQRS

CQRS sépare modèles de commande et de lecture lorsque cela apporte une valeur.

Il ne doit pas être appliqué automatiquement.

Exemple possible :

```text
Command model
Payment execution state

Read model
Customer payment status view
```

## 14. Consistency model

Pour chaque relation critique :

- strong consistency ;
- eventual consistency ;
- acceptable delay ;
- conflict handling ;
- reconciliation.

## 15. Reconciliation

Contrôle détectif essentiel lorsque plusieurs systèmes maintiennent des états liés.

Exemple :

```text
Payment Orchestrator state
vs
Clearing result
vs
Core booking
```

Détecter et traiter les écarts.

## 16. Data lifecycle

Questions :

- combien de temps conserver ?
- archive ?
- purge ?
- legal hold ?
- anonymization ?
- deletion ?

La politique détaillée relève de Data Governance/Compliance ; l’application doit connaître ses responsabilités.

## 17. Data classification

Exemples :

```text
Public
Internal
Confidential
Restricted
```

ou classification client.

Cette classification influence :

- encryption ;
- access ;
- logging ;
- residency ;
- retention.

## 18. PII / sensitive data

Un diagramme applicatif peut montrer que :

```text
Fraud Decision Service
consumes customer/payment context
```

sans recopier chaque attribut personnel.

Le dictionnaire détaillé sera traité en Partie IX.

## 19. Data residency

Pour cloud/SaaS, documenter lorsque requis :

- country/region ;
- replication ;
- backup location ;
- support access ;
- cross-border transfer.

## 20. Migration data impact

Remplacer une application nécessite souvent :

1. identifier source data ;
2. purifier/dédoublonner ;
3. mapper vers target model ;
4. migrate historical data ;
5. synchronize during coexistence ;
6. reconcile ;
7. freeze/cutover ;
8. archive old store ;
9. retire old interfaces.

## 21. Strangler and data

Lors d’un strangler pattern, le code peut être découpé avant les données.

Risque : deux applications utilisent toujours le même schéma legacy.

Une vraie séparation nécessite éventuellement une trajectoire data dédiée.

## 22. MayaBank data responsibility map

| Information | Primary application responsibility | Consumers |
|---|---|---|
| Payment Instruction | Payment Orchestrator | Fraud, Core, Clearing |
| Fraud Decision | Fraud Decision Service | Payment Orchestrator |
| Account Balance/Funds | Core Account Service | Payment Orchestrator |
| Clearing Result | Clearing Gateway / Orchestrator ingest | Payment Orchestrator, Reconciliation |
| Payment Status | Payment Orchestrator | Channel, Notification, Analytics |
| Notification Record | Notification Service | Operations |

## 23. Data dependency impact

Scénario : format `PaymentStatusChanged` change.

Impact :

```text
Schema
→ Event Streaming contract
→ Notification Service
→ Reconciliation Service
→ Analytics
```

L’analyse doit identifier tous les consumers avant évolution.

## 24. Anti-patterns

- base de données = domaine data ;
- plusieurs writers non gouvernés ;
- copie = source of truth ;
- Kafka = event sourcing ;
- cache = master data ;
- replication sans raison ;
- migration applicative sans data migration ;
- data ownership déduit uniquement de l’hébergement.

## 25. Livrables

- Application × Information Matrix ;
- Data Responsibility Map ;
- Application × Data Store Matrix ;
- Shared Database Coupling View ;
- Data Propagation Diagram ;
- Source-of-Truth Register ;
- Migration Data Impact Checklist.

## 26. Frontière avec la Partie IX

La Partie VIII documente **comment les applications utilisent et portent les données**.

La Partie IX approfondira :

- information concepts ;
- data domains ;
- logical/physical models ;
- data dictionary ;
- quality ;
- lineage ;
- governance ;
- database modeling.
