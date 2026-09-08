# 05 — Integration Architecture : synchronous, asynchronous et découplage

## 1. Pourquoi l’intégration est au cœur de l’architecture applicative

Une application isolée est rarement le problème principal.

La complexité se concentre souvent dans :

- les dépendances ;
- les contrats ;
- l’ordre des appels ;
- les timeouts ;
- les retries ;
- les transformations ;
- les synchronisations de données ;
- les erreurs distribuées.

L’Application Architecture doit donc rendre l’intégration explicite.

## 2. Point-to-point

```text
A → B
A → C
A → D
B → C
B → D
C → D
```

Avantage : simplicité locale.

Risque : complexité globale qui croît rapidement.

Questions :

- contrats gouvernés ?
- ownership ?
- duplication de transformation ?
- sécurité cohérente ?
- observabilité end-to-end ?

## 3. API-centric

```text
Consumer
→ API Management
→ Provider API
```

Objectifs :

- exposition contrôlée ;
- security policies ;
- consumer management ;
- versioning ;
- analytics ;
- throttling ;
- documentation.

API Management n’est pas un substitut à une bonne frontière fonctionnelle.

## 4. Event-driven

```text
Producer
→ Event Streaming
→ Consumers
```

Utiliser lorsque :

- le producer ne doit pas attendre tous les consumers ;
- plusieurs consumers réagissent au même fait ;
- replay/history apporte de la valeur ;
- découplage temporel recherché.

Ne pas utiliser Kafka uniquement pour « moderniser » une architecture.

## 5. Command vs event

Command :

```text
DoSomething
```

Event :

```text
SomethingHappened
```

Exemple :

```text
Command
SendCustomerNotification

Event
PaymentStatusChanged
```

Confondre les deux produit des architectures difficiles à raisonner.

## 6. Orchestration

Un orchestrateur connaît la séquence de coordination.

MayaBank :

```text
Payment Orchestrator
→ Fraud
→ Funds
→ Clearing
→ State Update
```

Avantages :

- visibilité du workflow ;
- gestion d’état ;
- contrôle des timeouts ;
- gestion explicite des compensations.

Risques :

- orchestrateur monolithique ;
- trop de logique métier centralisée ;
- SPOF logique ;
- couplage à tous les domaines.

## 7. Choreography

```text
PaymentAccepted
→ Fraud reacts
→ FraudApproved
→ Clearing reacts
```

Avantages : découplage et autonomie.

Risques :

- logique globale difficile à voir ;
- debugging complexe ;
- cycles événementiels ;
- ownership du process diffus.

L’architecture peut combiner orchestration et event-driven communication.

## 8. ESB / mediation

Un ESB historique peut centraliser :

- routing ;
- transformation ;
- protocol mediation ;
- orchestration.

Ne pas le considérer automatiquement comme dette.

Analyser :

- volume de logique métier dans l’ESB ;
- support/lifecycle ;
- performance ;
- central bottleneck ;
- stratégie cible API/event.

## 9. Anti-corruption layer

Lors d’une migration legacy :

```text
New Domain
→ ACL/Adapter
→ Legacy Contract
```

Objectif : empêcher le modèle legacy de contaminer la cible.

## 10. Canonical data model

Un modèle canonique global peut réduire certaines transformations mais devenir trop centralisé.

Approche pragmatique :

- concepts métier stables partagés ;
- contrats explicites ;
- mapping local contrôlé ;
- éviter un modèle universel impossible à faire évoluer.

## 11. Synchronous chain risk

Exemple :

```text
Channel
→ API Gateway
→ Payment Orchestrator
→ Fraud
→ Core Account
→ Clearing
```

La disponibilité end-to-end est inférieure à celle de chaque composant pris isolément.

Une chaîne synchrone longue augmente :

- latency ;
- failure propagation ;
- timeout complexity ;
- retry storms.

## 12. Asynchronous boundary

Découpler les tâches non nécessaires au résultat financier immédiat :

```text
Payment Completed
→ Event
→ Notification
→ Analytics
→ Audit enrichment
```

Ne pas rendre la notification synchrone si son échec ne doit pas annuler le paiement.

## 13. Transaction distribuée

Éviter de supposer qu’un rollback ACID global existe entre domaines autonomes.

Préférer selon contexte :

- local transactions ;
- state machine ;
- idempotency ;
- compensation ;
- reconciliation ;
- eventual consistency.

## 14. Saga concept

Exemple pédagogique :

```text
Reserve Funds
→ Send Clearing
→ failure
→ Release Reservation
```

La saga peut être orchestrée ou chorégraphiée.

Le choix dépend du besoin de contrôle, visibilité et autonomie.

## 15. Eventual consistency

Un statut peut se propager avec délai.

Il faut alors expliciter :

- source of truth ;
- expected convergence time ;
- user experience ;
- repair/reconciliation ;
- duplicate/out-of-order handling.

## 16. API Gateway vs Service Mesh

API Gateway : frontière d’exposition et politiques d’API.

Service Mesh : communication service-to-service dans un environnement distribué.

Les deux peuvent coexister.

Ne pas les modéliser comme équivalents.

## 17. Integration ownership

Pour chaque intégration critique :

```text
Business responsibility
Provider owner
Consumer owner
Integration/platform owner
Operational support
```

## 18. Integration decision record

Documenter les choix structurants :

```text
Decision
Use asynchronous event for payment status propagation

Drivers
Decouple notification from payment execution
Improve scalability
Support multiple consumers

Consequences
Eventual consistency
Schema governance required
Replay/idempotency required
```

## 19. MayaBank — architecture cible

```text
Digital Channel
      |
      v
API Management
      |
      v
Payment Orchestrator
  |      |      |
  v      v      v
Fraud   Core   Clearing

Payment Orchestrator
      |
      v
Event Streaming
   |       |        |
   v       v        v
Notify  Reconcile  Analytics
```

## 20. Matrice pattern par interaction

| Interaction | Pattern | Justification |
|---|---|---|
| Channel → Payment Orchestrator | synchronous API | immediate request acceptance |
| Orchestrator → Fraud | synchronous API | decision required before execution |
| Orchestrator → Core Account | synchronous API | funds required before clearing |
| Payment status → Notification | event | notification should be decoupled |
| Payment status → Analytics | event | independent consumer |
| Reconciliation input | event/batch | depends on source and operational model |

## 21. Migration point-to-point → target

### Wave 1

Inventory interfaces and ownership.

### Wave 2

Stabilize contracts and observability.

### Wave 3

Introduce API/event boundaries.

### Wave 4

Remove legacy direct DB and duplicate integrations.

### Wave 5

Retire obsolete adapters.

## 22. Metrics d’intégration

- number of critical synchronous hops ;
- direct DB dependencies ;
- unsupported interface versions ;
- consumers per interface ;
- event schema compatibility incidents ;
- timeout/error rate ;
- mean recovery time ;
- undocumented flows.

## 23. Anti-patterns

- event-driven partout ;
- API Gateway comme ESB universel ;
- business logic massive dans le middleware ;
- chaines synchrones interminables ;
- retries illimités ;
- shared database sans ownership ;
- consommateurs cachés ;
- schémas événementiels non versionnés ;
- absence de correlation ID ;
- compensation remplacée par « rollback global » imaginaire.

## 24. Questions d’entretien

**Orchestration ou choreography ?**  
Choisir selon besoin de contrôle global, autonomie, visibilité, coupling et gestion d’état ; aucun pattern n’est universellement supérieur.

**Pourquoi découpler la notification d’un paiement ?**  
Parce que l’échec d’un canal de notification ne doit généralement pas inverser un résultat financier déjà validé.

**Quel est le danger d’une longue chaîne synchrone ?**  
Propagation de panne, budgets timeout complexes, latence et retry storms.
