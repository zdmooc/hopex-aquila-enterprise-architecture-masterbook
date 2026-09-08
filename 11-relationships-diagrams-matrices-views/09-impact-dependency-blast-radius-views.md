# 09 — Impact Views, Dependency Views & Blast Radius

## 1. Objectif

Une impact view répond à :

> Si cet objet change, que faut-il regarder ensuite ?

Elle ne doit pas être confondue avec une simple vue de voisinage.

## 2. Direct impact

```text
Technology X
→ used by
Applications A, B, C
```

Premier niveau de blast radius.

## 3. Transitive impact

```text
Technology X
→ Application A
→ Process P
→ Capability C
→ Business Service S
```

La valeur de l’EAM vient de cette traversée cross-layer.

## 4. Upstream impact

Question :

> De quoi dépend cet objet ?

Exemple :

```text
Payment Orchestrator
← IAM
← OpenShift
← PostgreSQL
← DNS/LB
```

## 5. Downstream impact

Question :

> Qui dépend de cet objet ?

```text
Payment Orchestrator
→ Digital Channel
→ Notification
→ Reconciliation
→ Operations process
```

## 6. Critical path

Toutes les dépendances ne sont pas égales.

Marquer :

- mandatory runtime dependency ;
- optional dependency ;
- asynchronous dependency ;
- degraded-mode dependency ;
- batch dependency.

Le métamodèle exact peut ne pas porter directement ces catégories ; utiliser les concepts disponibles ou des propriétés gouvernées.

## 7. Blast radius

Dimensions :

```text
Number of direct consumers
Number of critical consumers
Business criticality
Process criticality
Data sensitivity
Geographic reach
Recovery dependency
```

## 8. Change impact

Exemple : suppression d’une API v1.

```text
API v1
→ consumers
→ processes
→ migration initiatives
→ target API v2
→ cutover dates
```

## 9. Technology obsolescence

```text
Deprecated Technology
→ Platforms
→ Applications
→ Processes
→ Capabilities
→ Business owners
```

Cette vue transforme une information de lifecycle en décision de transformation.

## 10. Data impact

```text
Business Term / Data Entity
→ Producer
→ Stores
→ Transformations
→ Consumers
→ Reports/Processes
```

Question : que se passe-t-il si le schéma ou la définition change ?

## 11. Risk impact

```text
Critical Asset
→ Risk
→ Control
→ Implementation
```

Puis :

```text
Control weakness
→ affected assets/processes
```

## 12. Initiative impact

```text
Transformation Initiative
→ Applications changed
→ Technologies introduced/retired
→ Capabilities improved
→ Processes affected
```

## 13. Failure-domain impact

Exemple :

```text
Shared Load Balancer
→ API Management
→ Payment Orchestrator
→ Fraud Service
→ customer payment flow
```

Très utile pour révéler un SPOF masqué.

## 14. Dependency confidence

Une impact analysis doit signaler les liens douteux.

Exemple :

```text
Verified dependency
Inferred dependency
Stale dependency
```

Sinon une vue d’impact peut donner une fausse impression d’exhaustivité.

## 15. Depth control

Commencer :

```text
Depth 1
```

Puis :

```text
Depth 2
```

Uniquement si nécessaire.

Une profondeur trop forte crée un graphe illisible et multiplie les faux positifs.

## 16. Cycles

Les architectures réelles contiennent parfois des dépendances circulaires.

Exemple :

```text
A → B → C → A
```

Un cycle peut indiquer :

- couplage ;
- orchestration complexe ;
- shared state ;
- modèle de relation trop générique.

Il doit être analysé, pas seulement dessiné.

## 17. Hub analysis

Un objet ayant de nombreuses relations peut être :

- plateforme partagée stratégique ;
- service central ;
- bottleneck ;
- SPOF ;
- objet sur-modélisé.

Le nombre de liens ne suffit pas à conclure.

## 18. Orphan analysis

Un objet sans relation peut être :

- réellement autonome ;
- mal documenté ;
- obsolète ;
- importé par erreur.

## 19. MayaBank — scénario 1

Retirer `Legacy Payment Gateway`.

Vue :

```text
Legacy Gateway
→ interfaces
→ consumers
→ process activities
→ capabilities
→ technologies
→ target replacement
→ migration wave
```

## 20. MayaBank — scénario 2

Kafka unavailable.

```text
Event Streaming Platform
→ PaymentStatusChanged
→ Notification
→ Reconciliation
→ Analytics
```

Puis distinguer :

- payment execution core path ;
- asynchronous side effects ;
- degraded mode.

## 21. MayaBank — scénario 3

OpenShift upgrade.

```text
OpenShift version
→ clusters/platform
→ applications
→ critical processes
→ test scope
→ rollout waves
```

## 22. Impact view template

```text
Object under change
Affected direct objects
Affected transitive objects
Criticality
Confidence
Current/Target
Owner
Required decision
```

## 23. Anti-patterns

- afficher toutes les relations sans filtrer leur sens ;
- profondeur illimitée ;
- impact présenté comme exhaustif alors que les données sont incomplètes ;
- oublier les relations target ;
- confondre correlation et dependency ;
- conclure SPOF uniquement parce qu’un objet a beaucoup de liens.

## 24. Questions d’entretien

**Quelle différence entre dependency map et impact analysis ?**  
La dependency map décrit les liens ; l’impact analysis les traverse pour répondre à un scénario de changement ou de défaillance.

**Pourquoi qualifier les relations critiques ?**  
Parce qu’une dépendance asynchrone tolérant une panne n’a pas le même impact qu’une dépendance synchrone obligatoire.

**Pourquoi limiter la profondeur ?**  
Pour conserver pertinence, lisibilité et confiance dans l’analyse.