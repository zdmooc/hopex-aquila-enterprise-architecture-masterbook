# 10 — Process analysis methods : gap, impact, bottleneck, redundancy et control weakness

## 1. Objectif

La Business Process Analysis ne se limite pas à décrire un processus. Elle doit permettre de **diagnostiquer**, comparer, prioriser et décider.

Ce chapitre fournit une méthode réutilisable en mission pour analyser :

- gaps ;
- impacts ;
- bottlenecks ;
- redundant steps ;
- handoffs ;
- automation opportunities ;
- control weaknesses ;
- application dependencies ;
- current/target transitions.

## 2. Principe : partir d'une question de décision

Mauvaise question :

```text
Pouvez-vous documenter le process ?
```

Meilleure question :

```text
Pourquoi le P95 dépasse-t-il 4 secondes ?
Quelles étapes dépendent de l'application Legacy X ?
Quels contrôles deviennent invalides avec la cible ?
Quelles activités peuvent être supprimées ou automatisées ?
```

La question détermine les données et relations à modéliser.

## 3. Cadre d'analyse en sept étapes

```text
1. Define question
2. Establish current baseline
3. Identify evidence
4. Traverse repository relationships
5. Diagnose causes/gaps
6. Design target options
7. Prioritize actions and measures
```

## 4. Gap analysis

Comparer :

```text
Current state
vs
Target state
```

Dimensions possibles :

- process step ;
- responsibility ;
- control ;
- automation ;
- application ;
- data ;
- performance ;
- resilience ;
- compliance ;
- maturity.

## 5. Gap register

Exemple :

| Gap | Current | Target | Impact | Initiative |
|---|---|---|---|---|
| duplicate handling | manual | idempotent | high | Orchestrator modernization |
| timeout recovery | operator repair | governed retry/status inquiry | high | Clearing resilience |
| E2E trace | fragmented IDs | canonical correlation | high | Observability |
| notification | sync dependency | async | medium | Event modernization |

## 6. Impact analysis

Question type :

```text
What changes if X changes?
```

Exemple : remplacer `Payment Orchestrator`.

Traversal logique :

```text
Application
→ supported activities
→ processes
→ business services
→ capabilities
→ data
→ risks/controls
→ KPIs
→ initiatives
```

L'analyse doit distinguer :

- impact direct ;
- impact indirect ;
- impact potentiel ;
- dépendance confirmée ;
- relation obsolète à nettoyer.

## 7. Dependency analysis

Construire la chaîne minimale nécessaire.

Exemple :

```text
Execute Instant Payment
→ Send Payment to Clearing
→ Clearing Adapter
→ API Management / connectivity
→ Clearing Network
```

Puis demander :

- dépendance synchrone ?
- fallback ?
- timeout ?
- capacité ?
- SPOF ?
- owner ?
- observability ?

## 8. Bottleneck analysis

Un bottleneck est une contrainte qui limite le throughput ou augmente le cycle time.

Sources :

- queue ;
- service time ;
- external dependency ;
- capacity ;
- manual review ;
- serial approvals ;
- batch ;
- data wait ;
- lock/contention ;
- retry storm.

## 9. Bottleneck worksheet

| Activity | Volume | Service time | Wait time | Capacity | Failure | Evidence |
|---|---:|---:|---:|---:|---:|---|
| Fraud Review | medium | 6m | 18m | 5 analysts | low | work queue |
| Clearing | high | 800ms | 2.2s P95 | external | timeout 0.7% | traces |

Valeurs fictives.

## 10. Handoff analysis

Handoffs critiques :

```text
Team → Team
Application → Application
Channel → Back office
Automated → Manual
Bank → External network
Synchronous → Asynchronous
```

Pour chaque handoff :

- information transférée ;
- owner avant/après ;
- acknowledgement ;
- timeout ;
- error handling ;
- correlation ;
- duplicate handling ;
- SLA.

## 11. Redundant step analysis

Question : l'étape apporte-t-elle une valeur, un contrôle ou une obligation ?

Classifier :

### Value Added

Produit directement le résultat attendu.

### Business Necessary

Ne crée pas directement de valeur client mais reste nécessaire : conformité, contrôle, sécurité.

### Non Value Added

Peut potentiellement être supprimée, fusionnée ou automatisée.

## 12. Duplicate control analysis

Deux contrôles similaires ne sont pas automatiquement redondants.

Comparer :

- risque couvert ;
- moment du contrôle ;
- source de données ;
- indépendance ;
- prévention vs détection ;
- obligation réglementaire.

Exemple :

```text
Fraud screening
≠
Sanctions screening
```

même si les deux renvoient une décision.

## 13. Control weakness analysis

Pour chaque risk :

```text
Risk
→ Control
→ Design effectiveness
→ Operating effectiveness
→ Evidence
→ Residual risk
```

Weaknesses typiques :

- contrôle non relié à l'activité réelle ;
- contrôle manuel non tracé ;
- owner absent ;
- contrôle contourné sur une variante ;
- absence de preuve ;
- contrôle devenu obsolète après migration.

## 14. Segregation of duties analysis

Identifier les activités incompatibles.

Exemple pédagogique :

```text
Create payment repair
+
Approve same payment repair
```

La SoD doit être analysée sur les rôles réels et le workflow, pas seulement sur les titres de poste.

## 15. Application dependency analysis

Construire une matrice Activity × Application.

Puis rechercher :

- application unique sur activité critique ;
- applications multiples pour même activité ;
- legacy dependency ;
- manual bridge entre applications ;
- shadow application ;
- application sans owner ;
- application en end-of-life.

## 16. Redundancy application

Trois applications supportent `Validate Payment`.

Ne pas conclure immédiatement à une rationalisation.

Vérifier :

- pays/canal différent ;
- migration progressive ;
- spécialisation réglementaire ;
- fallback ;
- duplication historique.

## 17. Data dependency analysis

Questions :

- quelle information déclenche l'activité ?
- quelle information est créée ?
- quelle source est autoritative ?
- y a-t-il recopie manuelle ?
- quelle qualité est nécessaire ?
- quel délai de disponibilité ?
- quelle classification/sensibilité ?

## 18. Automation opportunity analysis

Score pédagogique :

| Criterion | 1 | 5 |
|---|---|---|
| volume | faible | très élevé |
| rule stability | instable | stable |
| data availability | faible | excellente |
| human judgement | fort | faible |
| error cost | faible | élevé |
| integration readiness | faible | forte |

Une activité à score élevé est une candidate à **étudier**, pas automatiquement à automatiser.

## 19. Root cause analysis

Ne pas confondre symptôme et cause.

Exemple :

```text
Symptom: Manual Repair Rate = 2%
```

Causes possibles :

- timeout mal géré ;
- duplicate ;
- données invalides ;
- failure downstream ;
- status inconsistency ;
- contrôle trop strict ;
- absence de retry idempotent.

## 20. Five Whys — usage prudent

Les `5 Why` peuvent aider en atelier, mais un problème distribué peut avoir plusieurs causes parallèles.

Compléter avec :

- traces ;
- logs ;
- metrics ;
- event data ;
- incidents ;
- interviews ;
- architecture dependencies.

## 21. Current / target comparison

Comparer sur les mêmes axes :

| Dimension | Current | Target |
|---|---|---|
| orchestration | sync chain | resilient orchestration |
| status | multiple stores | explicit state model |
| timeout | manual | governed handling |
| notification | sync | async |
| traceability | fragmented | canonical correlation |
| repair | high manual | automated routing |

## 22. Transition analysis

Le target ne suffit pas.

Construire :

```text
Current
→ Transition 1
→ Transition 2
→ Target
```

Pour chaque transition :

- process variant temporaire ;
- application coexistence ;
- data sync ;
- controls ;
- rollback/fallback ;
- KPI ;
- decommission criteria.

## 23. Prioritization

Matrice simple :

```text
Business impact
Risk reduction
Customer impact
Compliance urgency
Effort
Dependency
Time to value
```

Éviter de prioriser uniquement selon l'effort technique.

## 24. MayaBank — analyse guidée

### Question

Pourquoi les exceptions `Clearing Timeout` génèrent-elles beaucoup de manual repair ?

### Evidence

- event logs ;
- timeout counts ;
- retry traces ;
- operations queue ;
- status reconciliation ;
- incident history.

### Repository traversal

```text
Clearing Timeout
→ Wait for Clearing Result
→ Payment Orchestrator
→ Clearing Adapter
→ Clearing Network
→ Reconciliation Control
→ Manual Repair activity
```

### Hypothèses

1. timeout trop court ;
2. retry non idempotent ;
3. absence de status inquiry ;
4. résultat tardif non corrélé ;
5. état local incohérent.

### Target options

- explicit timeout state ;
- idempotent retry ;
- status inquiry ;
- delayed result handling ;
- reconciliation automation ;
- observability.

## 25. Analyse de faiblesse de contrôle MayaBank

Risque : duplicate financial execution.

Current controls :

- client reference check ;
- operator review sur certains cas.

Target controls :

- canonical idempotency key ;
- deterministic duplicate response ;
- reconciliation detection ;
- audit trail.

## 26. Deliverables d'analyse

- Gap Register ;
- Impact Map ;
- Dependency Matrix ;
- Bottleneck Report ;
- Handoff Catalogue ;
- Control Weakness Register ;
- Automation Candidate Backlog ;
- Current/Target Comparison ;
- Transition Roadmap ;
- Decision Record.

## 27. Anti-patterns d'analyse

- diagnostiquer sans baseline ;
- conclure sur un atelier sans evidence ;
- cartographier tout le SI au lieu de répondre à la question ;
- confondre correlation et causalité ;
- supprimer un contrôle parce qu'il ralentit ;
- automatiser une activité non nécessaire ;
- ignorer les transitions ;
- traiter une relation repository obsolète comme une vérité.

## 28. Questions d'entretien

**Comment faites-vous une impact analysis ?**  
Je pars d'un objet de changement, traverse les relations canoniques vers activités/processus/services/data/controls, qualifie direct/indirect et valide les relations critiques avec les owners.

**Comment identifiez-vous un bottleneck ?**  
Par les données de queue, temps d'attente, service time, capacité et variantes, puis je relie le signal à l'activité et à ses dépendances.

**Une étape manuelle doit-elle être automatisée ?**  
Seulement après avoir vérifié qu'elle est nécessaire, stable, mesurable, techniquement automatisable et compatible avec les contrôles.