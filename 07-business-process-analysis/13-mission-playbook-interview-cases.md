# 13 — Mission playbook, workshops, deliverables et interview cases BPA

## 1. Objectif

Ce chapitre transforme la Partie VII en playbook utilisable :

- au démarrage d'une mission ;
- en atelier métier/IT ;
- en Architecture Board ;
- en entretien ;
- pour préparer une transformation ;
- pour auditer un repository existant.

Il ne remplace pas les 24 labs de l'annexe ; il décrit une **méthode de mission**.

## 2. Les cinq questions de départ

Avant de modéliser :

1. Quel problème veut-on résoudre ?
2. Quel processus est dans le scope ?
3. Quelle décision le repository devra-t-il permettre ?
4. Quelles sources existent déjà ?
5. Qui est accountable de la validation ?

## 3. Intake de mission

Collecter :

- objectifs métier ;
- transformation/project scope ;
- organisation ;
- process inventory existant ;
- procédures ;
- BPMN/Visio ;
- application inventory ;
- data catalog ;
- risks/controls ;
- KPI/SLA ;
- incidents ;
- roadmaps ;
- process mining/event data si disponible.

## 4. Ne pas importer tout de suite

Un inventaire existant peut contenir :

- doublons ;
- noms incohérents ;
- modèles obsolètes ;
- application aliases ;
- owners partis ;
- versions FINAL2 ;
- procédures mélangées aux processes.

Commencer par profiler et nettoyer.

## 5. Workshop 1 — Scope & outcome

Participants :

- Process Owner ;
- SME ;
- Process Analyst ;
- Architect ;
- Risk/Compliance selon criticité.

Agenda :

```text
Outcome
Start boundary
End boundary
Customer/stakeholder
Major participants
Happy path
Top exceptions
Current pain points
KPIs
```

Livrable : Process Charter.

## 6. Process Charter template

```text
Process Name:
Business Outcome:
Owner:
Scope In:
Scope Out:
Start:
End:
Customers/Stakeholders:
Criticality:
Key Applications:
Key Data:
Top Risks:
Top Controls:
KPIs:
Known Issues:
Target Drivers:
```

## 7. Workshop 2 — Happy path

Règle : ne pas commencer par toutes les exceptions.

Questions :

- quel événement déclenche ?
- quelles étapes changent l'état métier ?
- qui réalise chaque étape ?
- quelle décision change le chemin ?
- quel résultat termine le cas ?

Sortie : BPMN lisible de 10–20 activités maximum au niveau principal lorsque possible.

## 8. Workshop 3 — Exceptions & controls

Pour chaque exception :

```text
Trigger
Classification
Business impact
Automatic handling
Manual handling
Owner
Escalation
Risk
Control
Evidence
KPI
```

Ne pas traiter `manual review` comme réponse universelle.

## 9. Workshop 4 — Cross-layer mapping

Réunir Process Analyst + Solution/Application Architect + Data + Risk.

Construire :

- Activity × Application ;
- Activity × Data ;
- Risk × Control ;
- Process × Organization ;
- Process × Initiative.

Objectif : révéler dependencies et impacts, pas produire un tableau décoratif.

## 10. Workshop 5 — Performance

Sources :

- monitoring ;
- traces ;
- process events ;
- work queues ;
- incidents ;
- business reports.

Questions :

- cycle time ?
- P95/P99 ?
- throughput ?
- failure/rejection taxonomy ?
- STP ?
- manual rate ?
- bottleneck ?
- variants ?

## 11. Workshop 6 — Current → Target

Construire :

```text
Current pain point
→ root cause
→ target principle
→ impacted object
→ initiative
→ KPI expected benefit
```

Exemple :

```text
Manual repair after timeout
→ ambiguous state
→ explicit timeout/status inquiry
→ Payment Orchestrator + Clearing Adapter
→ Clearing Resilience initiative
→ Manual Repair Rate ↓
```

## 12. Workshop 7 — Governance handover

Avant de quitter la mission :

- owner confirmé ;
- steward confirmé ;
- review calendar ;
- publication rules ;
- change process ;
- quality checks ;
- training ;
- backlog ;
- metrics ;
- ownership des relations.

Un repository sans handover redevient rapidement obsolète.

## 13. Deliverable pack — minimum viable mission

1. Process Landscape.
2. Process Charter.
3. BPMN Happy Path.
4. Exception Catalogue.
5. RACI.
6. Process/Application Matrix.
7. Process/Data Matrix.
8. Risk/Control Matrix.
9. KPI Catalogue.
10. Current/Target Comparison.
11. Impact Analysis.
12. Transformation Backlog.
13. Governance RACI.
14. Quality Report.
15. Architecture Board Summary.

## 14. Architecture Board one-pager

Structure :

```text
Decision requested
Business outcome
Current issue
Evidence/KPI
Current process
Target process
Applications impacted
Data impacted
Risks/controls
Transition
Cost/effort order of magnitude
Decision / owner / date
```

## 15. Repository audit — 60 minutes

Échantillonner quelques processus critiques et vérifier :

- owner ;
- parent ;
- review date ;
- application links ;
- risks/controls ;
- KPIs ;
- duplicates ;
- variants ;
- target/initiative links.

Puis chercher les anomalies globales si les fonctions/reportings disponibles le permettent.

## 16. Repository audit — red flags

- milliers de process sans owners ;
- diagrams sans relations ;
- applications créées par les process modelers en doublon ;
- aucune date de revue ;
- aucun mapping risk/control ;
- KPI libres sans source ;
- process variants par pays sans logique ;
- current/target mélangés ;
- modèle dépendant d'une seule personne ;
- bulk import jamais nettoyé.

## 17. Mission case 1 — Clearing timeout

### Situation

Le taux de manual repair augmente après migration.

### Questions à poser

- le timeout a-t-il changé ?
- les retries sont-ils idempotents ?
- un late response est-il corrélé ?
- existe-t-il un status inquiry ?
- quelle activité crée le case manuel ?
- quel control réconcilie ?

### Analyse attendue

```text
Process event
→ activity
→ application dependency
→ state management
→ control
→ KPI
```

### Deliverable

Impact Map + target exception flow.

## 18. Mission case 2 — Fraud false positives

### Situation

STP baisse parce que beaucoup de paiements passent en revue manuelle.

### Analyser

- Fraud Review Rate ;
- False Positive Rate ;
- amount/channel variants ;
- rule/model changes ;
- SLA ;
- manual queue ;
- risk appetite.

### Attention

Réduire la revue manuelle ne doit pas augmenter le risque de fraude de manière non acceptée.

## 19. Mission case 3 — Remplacement Payment Orchestrator

### Question

Quels objets sont impactés ?

### Traversal

```text
Payment Orchestrator
→ activities
→ processes
→ business services
→ data
→ controls
→ KPIs
→ technologies
→ initiatives
```

### Deliverable

Impact Analysis + transition roadmap.

## 20. Mission case 4 — Regulatory change

### Situation

Une nouvelle exigence ajoute un contrôle avant clearing.

### Questions

- quelles populations ?
- quelle activité ?
- quel participant ?
- quelle donnée ?
- quelle application ?
- quel control owner ?
- quel SLA impact ?
- quelle date d'effet ?

### Deliverable

Regulation → Requirement → Control → Activity traceability + change plan.

## 21. Mission case 5 — Process mining révèle un bypass

### Situation

Le mined process montre que certains cas évitent une activité de contrôle.

### Ne pas conclure trop vite

Vérifier :

- log completeness ;
- event naming ;
- technical shortcut légitime ;
- variante autorisée ;
- réel bypass ;
- population affectée.

### Deliverable

Conformance finding + risk assessment + target correction.

## 22. Mission case 6 — SoD weakness

### Situation

La même équipe peut créer et approuver une réparation financière.

### Analyse

```text
Activity
→ role
→ organization
→ permission/workflow runtime
→ control
→ audit evidence
```

Le repository doit documenter la responsabilité ; la vérification des permissions effectives peut nécessiter le système runtime/IAM.

## 23. Mission case 7 — Application redundancy

### Situation

Trois applications sont reliées à `Validate Payment`.

### Démarche

1. qualifier les scopes ;
2. comparer volumes ;
3. identifier target architecture ;
4. vérifier lifecycle ;
5. analyser coûts/risques ;
6. proposer rationalisation ou coexistence justifiée.

## 24. Mission case 8 — Process owner absent

### Situation

Le processus traverse cinq directions et aucun owner n'accepte la responsabilité.

### Réponse architecte

- clarifier outcome ;
- identifier executive sponsor ;
- distinguer activity owners et end-to-end owner ;
- documenter la décision de gouvernance ;
- escalader si nécessaire.

Ne pas inventer un owner dans le repository.

## 25. Interview case — « Dessinez un paiement instantané »

Réponse structurée :

```text
1. Scope
2. Participants
3. Happy path
4. Decisions
5. Exceptions
6. Systems
7. Data
8. Risks/controls
9. KPIs
10. Target improvements
```

L'entretien évalue autant le raisonnement que le BPMN.

## 26. Interview case — « HOPEX sert à quoi ici ? »

Réponse attendue :

HOPEX porte le repository gouverné et les relations permettant de relier processus, owner, capabilities, applications, data, risks, controls, KPIs et initiatives. Le runtime des paiements reste dans les applications/orchestrateurs concernés.

## 27. Interview case — « Capability vs Process ? »

```text
Capability = what the enterprise is able to do
Process = how work is executed to produce an outcome
```

Exemple :

```text
Capability: Payment Execution
Process: Execute Instant Payment
```

## 28. Interview case — « Process vs Value Stream ? »

Le value stream structure la création de valeur du point de vue des stages/outcomes ; le process décrit la logique d'exécution et les responsabilités.

Ils peuvent être reliés mais ne sont pas interchangeables.

## 29. Interview case — « Process vs Procedure ? »

Process : logique stable de travail et résultat.

Procedure : instructions détaillées pour exécuter une activité dans un contexte donné.

```text
Validate Payment
```

peut être une activité de process ;

```text
ouvrir l'écran X, cliquer Y
```

est plutôt une procédure.

## 30. Interview case — « HOPEX vs Camunda ? »

HOPEX : repository/gouvernance/analyse/transformation.

Camunda : exemple de runtime d'orchestration BPMN où des process definitions sont déployées et exécutées en instances.

Les deux peuvent coexister avec des responsabilités différentes.

## 31. Interview case — « HOPEX vs Pega ? »

HOPEX : contexte d'architecture et gouvernance entreprise.

Pega : plateforme de workflow/case management/orchestration selon les produits et usages.

Ne pas répondre par « l'un remplace toujours l'autre ».

## 32. Interview case — « Que faites-vous si le métier veut 200 activités sur le même diagramme ? »

- confirmer l'objectif ;
- structurer niveaux ;
- extraire subprocesses ;
- conserver happy path ;
- séparer exceptions ;
- produire des vues adaptées aux audiences.

## 33. Interview case — « Le process mining dit autre chose que le BPMN »

C'est précisément un résultat à analyser :

```text
Observed
vs
Governed current
vs
Target
```

Qualifier les variantes et la qualité des logs avant de conclure à une non-conformance.

## 34. 30/60/90 jours — exemple de mission

### Jours 1–30

- scope ;
- inventory ;
- governance ;
- critical processes ;
- quick quality audit ;
- MayaBank-like reference model ;
- first matrices.

### Jours 31–60

- detailed cross-layer mapping ;
- risk/control ;
- KPI baselines ;
- impact analysis ;
- current/target ;
- priority backlog.

### Jours 61–90

- governance industrialization ;
- dashboards ;
- automation/mining feedback ;
- training ;
- Architecture Board ;
- handover.

Les délais réels dépendent du scope et de la qualité des données.

## 35. Definition of Done mission

La mission BPA est réellement utile si :

- le repository répond à des questions de décision ;
- les critical processes ont des owners ;
- les modèles sont lisibles ;
- application/data/risk mappings sont canoniques ;
- KPIs sont mesurables ;
- current/target sont distingués ;
- backlog est priorisé ;
- gouvernance est reprise par l'organisation ;
- aucune fonctionnalité HOPEX non vérifiée n'a été promise.

## 36. Règle finale

Le rôle de l'architecte/process analyst n'est pas de produire le maximum de BPMN.

Il est de rendre le fonctionnement de l'entreprise **compréhensible, gouvernable, analysable et transformable**.