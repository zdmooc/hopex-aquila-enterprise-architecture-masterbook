# 11 — HOPEX vs runtime BPM : Camunda, Pega, workflow engines et automation architecture

## 1. La frontière à retenir

```text
HOPEX
= repository d'architecture, modélisation, analyse, gouvernance, portfolio et transformation

Runtime BPM / workflow engine
= exécution d'instances de processus, orchestration de tâches et état runtime
```

Le masterbook ne doit jamais présenter HOPEX comme un moteur runtime BPM comparable à Camunda ou Pega.

## 2. Pourquoi cette confusion arrive

Les mêmes mots apparaissent dans plusieurs mondes :

- process ;
- BPMN ;
- workflow ;
- task ;
- event ;
- role ;
- KPI.

Mais la présence d'un modèle BPMN dans un repository ne signifie pas que ce modèle est directement déployé comme définition exécutable.

## 3. Trois couches distinctes

### Layer A — Enterprise/process architecture

Questions :

- quel processus existe ?
- qui le possède ?
- quelles capabilities supporte-t-il ?
- quelles applications l'implémentent ?
- quels risques/contrôles ?
- quelle cible ?

### Layer B — executable process/orchestration design

Questions :

- quelles étapes sont exécutées ?
- quels workers/services ?
- quels messages ?
- quels timers ?
- quels retries ?
- quel état runtime ?

### Layer C — operational execution

Questions :

- quelle instance est en cours ?
- quel job attend ?
- quel incident runtime ?
- quel retry ?
- quel SLA opérationnel ?

## 4. Camunda — concept vérifié

La documentation publique Camunda 8 décrit un processus modélisé en BPMN, déployé comme `process definition`, puis exécuté sous forme de `process instance`. Elle décrit Zeebe comme le workflow engine qui crée notamment des jobs pour les workers.

Source officielle :

https://docs.camunda.io/docs/components/concepts/processes/

Donc, dans ce masterbook :

```text
Camunda 8
= exemple de process orchestration runtime
```

et non un substitut fonctionnel 1:1 à un repository EAM.

## 5. Pega — concept vérifié

Les pages publiques Pega présentent la plateforme comme une solution de workflow automation/orchestration, avec notamment :

- Case Management & BPM ;
- workflow automation ;
- process orchestration ;
- RPA ;
- process mining ;
- AI/decision capabilities.

Sources officielles :

https://www.pega.com/products/platform/workflow-automation

https://www.pega.com/business-process-orchestration

Dans ce masterbook :

```text
Pega
= exemple de plateforme d'automatisation/orchestration et case management
```

## 6. HOPEX — fait produit vérifié pertinent

Le workspace Postman public MEGA expose pour la solution BPA un endpoint GraphQL permettant de lire/écrire des objets du repository, par exemple des business processes.

Source :

https://www.postman.com/mega-international/mega-international-s-public-workspace/documentation/27vy1fl/hopex-rest-api-v5

Cela confirme la dimension **repository/intégration** ; cela ne transforme pas HOPEX en moteur d'exécution de processus métier.

## 7. Source of truth par type de donnée

Exemple d'architecture de gouvernance :

| Information | Source autoritative possible |
|---|---|
| Process architecture | HOPEX |
| Process Owner | HOPEX / référentiel org selon gouvernance |
| Application mapping | HOPEX |
| Executable BPMN | Camunda repository/deployment pipeline |
| Case definition | Pega |
| Runtime process instance | Camunda/Pega |
| Operational logs | observability/runtime platform |
| Process mining event log | analytics/mining platform |
| CMDB CI | ServiceNow CMDB |

Le choix exact dépend du SI client.

## 8. Architecture pattern — governed model to runtime

```text
Business need
   ↓
HOPEX governed process architecture
   ↓
Solution design
   ↓
Executable workflow/BPMN/case design
   ↓
CI/CD
   ↓
Runtime engine
   ↓
Events / metrics / logs
   ↓
Process mining / observability
   ↓
Feedback to HOPEX governance
```

Il ne faut pas supposer un round-trip automatique si aucun connecteur ou mécanisme n'est vérifié.

## 9. Architecture pattern — Camunda

Exemple conceptuel MayaBank :

```text
HOPEX Process
Execute Instant Payment
       ↓ traces to
Executable orchestration design
       ↓ deployed to
Camunda/Zeebe
       ↓ workers call
Payment APIs / Fraud / Clearing
```

HOPEX porte le contexte entreprise ; Camunda porte l'exécution si ce choix d'architecture est retenu.

## 10. Architecture pattern — Pega

Pega peut être pertinent lorsque le travail comporte :

- case management ;
- human work ;
- routage ;
- SLA de tâches ;
- décisions ;
- interactions multiples ;
- orchestration de systèmes.

Exemple MayaBank :

```text
Payment Exception Case
→ collect evidence
→ assign analyst
→ investigate
→ approve/reject repair
→ close case
```

Cela peut être plus adapté à Pega qu'à un microservice maison si le besoin principal est le case/work management.

## 11. Orchestration vs choreography

### Orchestration

Un composant/process engine coordonne explicitement les étapes.

```text
Orchestrator
→ Fraud
→ Funds
→ Clearing
→ Notification
```

### Choreography

Les services réagissent à des événements sans coordinateur central unique.

```text
PaymentReceived
→ Fraud reacts
→ Status changes
→ Notification reacts
```

Un processus métier peut être gouverné dans HOPEX quelle que soit l'implémentation retenue.

## 12. BPMN design vs executable BPMN

Un BPMN de compréhension métier peut omettre :

- retry technique ;
- headers ;
- connector configuration ;
- worker type ;
- variables runtime ;
- incident handling engine-specific.

Un BPMN exécutable doit souvent préciser des éléments techniques propres à l'engine.

Ne pas forcer une vue HOPEX de haut niveau à devenir une définition exécutable.

## 13. Human task

Questions d'architecture :

- quelle work queue ?
- assignment par rôle/skill ?
- SLA ?
- escalation ?
- four-eyes ?
- claim/reassign ?
- audit trail ?
- absence/vacation ?

Le repository documente la responsabilité et l'intention. Le runtime gère l'instance et son état.

## 14. Timer et timeout

Dans le modèle gouverné :

```text
Wait for Clearing Result
→ response or timeout
```

Dans le runtime :

- timer configuration ;
- retry policy ;
- backoff ;
- incident ;
- compensation ;
- dead-letter/state handling selon technologie.

Les deux niveaux doivent rester traçables.

## 15. Error vs business rejection

Ne pas traduire toute rejection métier en erreur technique du moteur.

Exemple :

```text
Insufficient Funds
= business outcome/rejection
```

Alors que :

```text
Clearing Adapter unavailable
= technical failure
```

Cette distinction est essentielle pour KPI, retry et audit.

## 16. Compensation

Une transaction distribuée n'a pas toujours un rollback ACID global.

Le process peut prévoir :

```text
Reserve funds
→ downstream failure
→ release reservation
```

Le runtime choisit le mécanisme technique : compensation, saga, command/event, workflow step, etc.

## 17. Decision automation

Séparer :

```text
Process orchestration
from
Decision logic
```

Exemple :

```text
Run Fraud Decision
→ Fraud Decision Service
```

Le process utilise la décision ; le détail du modèle de fraude/règles peut rester dans un composant dédié.

## 18. RPA

RPA est utile lorsque :

- pas d'API disponible ;
- application legacy ;
- transition temporaire ;
- volume/ROI justifié.

Risques :

- dépendance UI fragile ;
- dette cachée ;
- credentials ;
- observability limitée ;
- duplication de règles.

Le repository doit signaler une RPA structurante comme dépendance de transformation.

## 19. API-first automation

Si l'activité est automatisée par un service :

```text
Process Activity
→ Business/Application Service
→ API
→ Application
```

La Partie VII reste au niveau process ; les détails API seront approfondis dans les parties d'architecture/intégration.

## 20. Event-driven automation

Exemple :

```text
PaymentStatusChanged
→ Notification Service
→ Customer notification
```

Le modèle process doit montrer l'effet métier utile, pas chaque topic/partition technique.

Les mappings vers Event Streaming/Kafka appartiennent à la couche architecture.

## 21. Runtime observability

Un moteur/runtime doit fournir ou alimenter des données permettant de suivre :

- instance status ;
- duration ;
- error ;
- retry ;
- incident ;
- task queue ;
- SLA ;
- correlation.

Ces données peuvent alimenter process performance/mining, puis la gouvernance HOPEX.

## 22. Process mining feedback

```text
Runtime instances
→ Event logs
→ Process mining
→ discovered variants / performance
→ process analyst
→ HOPEX governed current/target model
```

Le Store MEGA publie un Simulation Engine qui peut importer des descriptions/métriques provenant d'outils de process mining. Cela confirme une logique d'intégration/feedback sans prouver un moteur de mining natif complet.

## 23. Decision matrix

| Besoin dominant | Pattern candidat |
|---|---|
| architecture/process repository | HOPEX |
| orchestration BPMN de services | Camunda-type runtime |
| case management/human work | Pega-type platform |
| simple service integration | application/API orchestration |
| decoupled reactions | event-driven choreography |
| UI legacy sans API | RPA transitionnelle |

Ce tableau est une aide pédagogique, pas une comparaison commerciale exhaustive.

## 24. MayaBank — séparation cible

```text
HOPEX
- Execute Instant Payment
- Process Owner
- capabilities
- applications
- risks/controls
- KPIs
- current/target roadmap

Runtime orchestration
- instance state
- timers
- retries
- worker dispatch
- technical incidents

Kafka/Event Streaming
- domain/integration events

Observability
- traces/logs/metrics

Operations/Case Management
- manual exception work
```

## 25. Cas : clearing timeout

### Dans HOPEX

Documenter :

- exception ;
- owner ;
- risk ;
- control ;
- target behavior ;
- impacted applications ;
- KPI.

### Dans le runtime

Implémenter selon technologie :

- timer ;
- retry ;
- status inquiry ;
- escalation ;
- state transition.

### Dans observability

Mesurer :

- timeout count ;
- retry count ;
- late responses ;
- repair cases.

## 26. Anti-pattern — double modélisation non gouvernée

Même process copié dans :

```text
HOPEX
Confluence
Camunda Modeler
Visio
PowerPoint
```

sans identifier l'autorité de chaque représentation.

Correction : définir la source de vérité et les usages de chaque artefact.

## 27. Anti-pattern — round-trip imaginaire

Ne jamais écrire :

```text
HOPEX model automatically deploys to Camunda
```

ou :

```text
Camunda automatically synchronizes all runtime metadata into HOPEX
```

sans connecteur, API ou développement explicitement vérifié.

## 28. Anti-pattern — engine-driven business architecture

Le fait qu'un moteur supporte un symbole ou pattern ne doit pas déterminer le business process cible.

D'abord le besoin et les règles métier ; ensuite le choix d'implémentation.

## 29. Questions d'entretien

**HOPEX est-il un moteur BPM runtime ?**  
Non dans le positionnement retenu ici : HOPEX est le repository/gouvernance/analyse ; Camunda/Pega illustrent des solutions d'exécution/orchestration.

**Pourquoi conserver un process dans HOPEX si Camunda a déjà le BPMN ?**  
Parce que le repository relie le processus au contexte entreprise : capabilities, applications, data, risks, controls, owners, roadmaps et architecture target.

**Faut-il synchroniser tous les détails runtime dans HOPEX ?**  
Non. Seulement les éléments nécessaires à la gouvernance et aux analyses, avec une frontière de source de vérité explicite.

## 30. Sources publiques

- Camunda 8 Processes : https://docs.camunda.io/docs/components/concepts/processes/
- Camunda BPMN automation guide : https://docs.camunda.io/docs/components/modeler/bpmn/automating-a-process-using-bpmn/
- Pega Workflow Automation : https://www.pega.com/products/platform/workflow-automation
- Pega Business Process Orchestration : https://www.pega.com/business-process-orchestration
- MEGA Public Postman REST API V5 : https://www.postman.com/mega-international/mega-international-s-public-workspace/documentation/27vy1fl/hopex-rest-api-v5
- HOPEX Simulation Engine : https://store.mega.com/modules/details/simulation.engine