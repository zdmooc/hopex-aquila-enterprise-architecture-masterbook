# 11 — Current, Transition et Target Application Architecture

## 1. Pourquoi modéliser trois états

Une architecture cible sans trajectoire est un dessin.

Une architecture actuelle sans cible est un inventaire.

Une architecture de transformation utile relie :

```text
Current
→ Transition states
→ Target
```

## 2. Current state

Le current doit représenter la réalité suffisamment pour expliquer :

- responsabilités ;
- applications ;
- interactions ;
- data stores ;
- technologies structurantes ;
- failure points ;
- dette ;
- contraintes.

Ne pas embellir le legacy.

## 3. Target state

Le target doit être dérivé de drivers explicites :

- business capability ;
- resilience ;
- security ;
- performance ;
- simplification ;
- cloud strategy ;
- data ownership ;
- decommissioning ;
- regulatory needs.

## 4. Transition state

Une transition architecture représente un état cohérent temporaire.

Exemple :

```text
Legacy Payment Hub remains system of record
New Payment Orchestrator handles new channel
Adapter synchronizes status
Notification moved to event-driven service
```

Un état transitoire peut durer des mois ou années : il doit être architecturé.

## 5. Strangler pattern

Principe : déplacer progressivement des responsabilités du legacy vers la cible.

```text
Consumer
→ façade/routing
→ legacy or target
```

Étapes :

1. identifier bounded responsibility ;
2. créer cible ;
3. router nouveaux flux ;
4. migrer données/consumers ;
5. réduire legacy ;
6. retirer.

## 6. Rehost

```text
VM → cloud/containers
```

Avantage : réduction d’un risque infrastructure ou datacenter.

Limite : architecture applicative et dette restent souvent inchangées.

Ne pas appeler automatiquement cela « modernisation ».

## 7. Replatform

Exemple :

```text
Application
→ managed database / container platform
```

avec modifications limitées.

## 8. Refactor

Modifier structure interne pour améliorer :

- modularity ;
- scalability ;
- cloud fit ;
- maintainability ;
- resilience.

## 9. Rearchitect

Changer des responsabilités ou interactions structurantes.

Exemple :

```text
central monolith
→ orchestrator + domain services + events
```

## 10. Replace

Remplacer par package/SaaS/autre produit.

Analyse :

- functional fit ;
- data migration ;
- integration ;
- customization ;
- lock-in ;
- security ;
- operational model.

## 11. Retire

Suppression d’une application devenue inutile après migration des responsabilités et données.

## 12. Consolidate

Plusieurs applications deviennent une cible commune.

```text
Notification A
Notification B
Notification C
→ Enterprise Notification Service
```

Attention aux variantes fonctionnelles réellement nécessaires.

## 13. Decompose

Une application trop large est séparée par responsabilités.

Ne pas décomposer selon les tables ou équipes uniquement.

## 14. Coexistence patterns

### Dual read

Lire legacy et cible pour comparer.

### Dual write

Très risqué ; nécessite ownership et reconciliation.

### Change data capture

Propager changements entre stores pendant migration.

### Adapter

Conserver anciens consumers pendant migration.

### Compatibility API

Cacher temporairement la cible derrière l’ancien contrat.

## 15. Migration risk

Principaux risques :

- consumers oubliés ;
- données incohérentes ;
- business rules cachées ;
- batch jobs oubliés ;
- reports shadow ;
- performance target non testé ;
- rollback impossible ;
- support model immature.

## 16. Cutover strategy

Options :

- big bang ;
- progressive traffic ;
- by customer segment ;
- by product ;
- by region ;
- by use case.

Le choix dépend du domaine et du risque.

## 17. Rollback

Un rollback réaliste doit répondre :

```text
What happens to data written in target?
Can legacy still process it?
How are external side effects handled?
What is the decision point?
```

Pour un paiement déjà envoyé au clearing, « rollback » n’annule pas magiquement l’effet externe.

## 18. Transition dependencies

Chaque wave doit identifier :

- prerequisite ;
- affected applications ;
- interfaces ;
- data migration ;
- control changes ;
- operational readiness ;
- retirement candidate.

## 19. MayaBank current

```text
Digital Channel
→ Legacy Payment Hub
→ Fraud appliance
→ Core Account
→ Clearing adapter
→ synchronous Notification Gateway

Shared Oracle schema
Batch reconciliation
VM deployment
Weak end-to-end correlation
```

Scénario pédagogique.

## 20. MayaBank target

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

OpenShift + governed state stores + observability
```

## 21. Transition 1 — façade et observabilité

- canonical correlation ID ;
- API façade ;
- dependency inventory ;
- current KPI baseline ;
- legacy interfaces retained.

## 22. Transition 2 — new orchestration

- new Payment Orchestrator ;
- Fraud API ;
- Funds API ;
- clearing adapter reused initially ;
- new state model.

## 23. Transition 3 — events and notification

- PaymentStatusChanged event ;
- Notification Service migrated ;
- replay/repair ;
- legacy notification retired.

## 24. Transition 4 — reconciliation and data separation

- target reconciliation ;
- legacy shared DB dependency removed ;
- archive/migrate data ;
- decommission readiness.

## 25. Architecture roadmap

| Wave | Application change | Dependency change | Outcome |
|---|---|---|---|
| 1 | façade/observability | no major functional cutover | visibility |
| 2 | new orchestrator | new fraud/funds APIs | decoupled execution |
| 3 | event notification | remove sync notification dependency | resilience |
| 4 | data/reconciliation | remove shared DB | separation |
| 5 | retire legacy | remove adapters | simplification |

## 26. Decision gates

Avant chaque transition :

- architecture approved ;
- security approved ;
- data migration tested ;
- performance tested ;
- DR/recovery tested ;
- observability ready ;
- consumer migration status known ;
- rollback/compensation understood.

## 27. Mapping dans le repository

Pour chaque objet :

```text
Current application
Target application
Transition initiative
Dependencies affected
Interfaces migrated
Data migrated
Lifecycle milestone
```

Les mécanismes exacts de time periods/roadmaps dépendent de la solution/configuration HOPEX.

## 28. Anti-patterns

- target sans drivers ;
- big bang par défaut ;
- dual write sans reconciliation ;
- migration applicative sans migration data ;
- transition diagram non maintenu ;
- legacy supprimé du repository avant retrait ;
- rehost présenté comme suppression de dette applicative ;
- rollback imaginé comme annulation de tous les effets externes.

## 29. Livrables

- Current Application Architecture ;
- Target Application Architecture ;
- Transition Architecture 1..N ;
- Application Migration Matrix ;
- Interface Migration Plan ;
- Data Coexistence Plan ;
- Decommission Readiness View ;
- Architecture Decision Log.
