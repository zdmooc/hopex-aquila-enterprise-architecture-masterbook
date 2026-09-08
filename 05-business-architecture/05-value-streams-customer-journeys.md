# 05 — Value Streams & Customer Journeys

## 1. Pourquoi modéliser la valeur de bout en bout

Une organisation est souvent structurée en silos, alors que le client traverse plusieurs équipes, processus et systèmes.

Le value stream permet de raisonner sur la progression de la valeur :

```text
Trigger
→ Value Stage 1
→ Value Stage 2
→ Value Stage 3
→ Outcome
```

HOPEX met actuellement en avant la connexion des value streams avec customer journeys, processes, capabilities et strategy.

## 2. Value Stream vs Process

Un value stream décrit les grandes étapes de création de valeur.

Un process décrit l'exécution opérationnelle.

Exemple MayaBank :

```text
Value Stream
Initiate Payment
→ Validate
→ Decide
→ Execute
→ Confirm
```

Process détaillé associé :

```text
Receive order
→ authenticate customer
→ validate format
→ screen fraud
→ route payment
→ book transaction
→ send confirmation
```

Ne pas transformer un value stream en BPMN simplifié.

## 3. Value Stage

Une stage doit représenter un progrès observable de la valeur.

Bon :

```text
Payment Request Validated
Payment Decision Reached
Payment Executed
Customer Informed
```

Faible :

```text
Team A
System B
Call API
Run batch
```

## 4. Customer Journey

Le customer journey part de l'expérience vécue par un stakeholder/client.

Exemple :

```text
Need to pay
→ choose beneficiary
→ enter amount
→ authenticate
→ wait for confirmation
→ verify status
```

Il peut être relié aux value stages, capabilities et processes.

## 5. Journey ≠ Value Stream

Customer Journey :

```text
outside-in
experience and touchpoints
```

Value Stream :

```text
value delivery
enterprise perspective
```

Les deux se complètent mais ne doivent pas être fusionnés artificiellement.

## 6. Touchpoints et channels

Pour MayaBank :

```text
Mobile App
Web Banking
Open Banking API
Call Center
Operations Portal
```

Chaque touchpoint peut être relié à des services et applications sans faire du customer journey un diagramme technique.

## 7. Pain points

Exemple :

```text
Stage: Confirm
Pain point: status delayed after downstream timeout
Impact: customer retries payment
Risk: duplicate instruction perception
```

Puis tracer :

```text
Pain Point
→ Value Stage
→ Process
→ Application dependency
→ Root cause / Initiative
```

## 8. Value Stream × Capability

Une matrice centrale :

| Value Stage | Payment Initiation | Fraud | Orchestration | Ops |
|---|---:|---:|---:|---:|
| Initiate | X | - | X | - |
| Validate | X | X | X | - |
| Decide | - | X | X | - |
| Execute | - | - | X | X |
| Confirm | X | - | X | X |

Elle montre les capabilities nécessaires à chaque stage.

## 9. Value Stream × Process

Permet de relier valeur et exécution.

```text
Validate stage
→ Validate Payment Order
→ Authenticate Customer
→ Screen Payment
```

## 10. Value Stream × Application

Utile pour l'impact métier :

```text
Confirm stage
→ Notification Service
→ Payment Orchestrator
→ Status API
```

Une panne applicative peut ainsi être remontée jusqu'à la valeur client touchée.

## 11. Metrics

Chaque stage peut avoir des mesures :

- lead time ;
- success rate ;
- error rate ;
- customer effort ;
- straight-through processing ;
- cost per transaction ;
- compliance rate.

Exemple MayaBank :

```text
Execute stage
P95 completion time < 5 sec
Availability = 99.99%
Straight-through rate > 98%
```

## 12. Value stream assessment

Analyser :

```text
customer value
performance
risk
capability maturity
process friction
technology dependency
```

Puis prioriser les stages qui créent le plus de friction.

## 13. Exemple de transformation

Current :

```text
Initiate → Validate → Manual Review → Execute → Delayed Confirm
```

Target :

```text
Initiate → Real-time Validate → Automated Decision → Execute → Real-time Confirm
```

Gaps :

- manual fraud review ;
- synchronous point-to-point calls ;
- missing event status model ;
- weak observability.

Initiatives :

- fraud automation ;
- payment orchestration redesign ;
- event streaming ;
- end-to-end monitoring.

## 14. Customer-centric architecture

Question utile :

> Quelles applications et technologies contribuent réellement à une étape du parcours qui compte pour le client ?

Cette question permet de sortir d'un inventaire IT sans contexte métier.

## 15. Reference frameworks

Le Store MEGA publie notamment un framework APQC Cross Industry avec Process Map, Process Categories, Value Streams, stages et performance indicators. Son utilisation dépend du contenu/licence disponible.

Le masterbook ne reproduit pas ce contenu ; il documente seulement le pattern d'utilisation.

## 16. Anti-patterns

- value stream = liste d'applications ;
- stages = équipes ;
- customer journey = process interne ;
- aucune métrique ;
- aucune capability reliée ;
- pain points sans initiative ;
- trente stages trop détaillées ;
- mélanger état actuel et cible sans convention.

## 17. Entretien

**Pourquoi utiliser value stream + capability ?**  
Le value stream montre où la valeur est créée ; la capability montre ce qu'il faut savoir faire pour créer cette valeur.

**Pourquoi relier les applications au value stream ?**  
Pour contextualiser l'impact IT et prioriser les changements selon la valeur métier touchée.