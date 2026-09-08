# 01 — Enterprise Cartography & Dependency Analysis : rôle, périmètre et méthode

## 1. Objectif

L’Enterprise Cartography transforme le repository d’architecture en **graphe exploitable pour comprendre les dépendances, les impacts, les concentrations de risque et les trajectoires de changement**.

Elle répond à des questions concrètes :

```text
Qu’est-ce qui dépend de quoi ?
Quelle dépendance est directe ou transitive ?
Quels composants concentrent le plus d’impacts potentiels ?
Quels processus seraient touchés si une plateforme disparaît ?
Quel ordre de migration ou de reprise minimise le risque ?
Où sont les cycles, les hubs et les dépendances cachées ?
Quelle donnée manque pour pouvoir décider avec confiance ?
```

Le but n’est pas de produire une immense carte de l’entreprise. Le but est de produire **des cartographies gouvernées qui permettent une analyse de dépendances fiable**.

---

## 2. Frontières avec les parties précédentes

```text
Partie II
Repository, objets, associations et cardinalités

Partie XI
Relations, vues, matrices, filtres et conventions de représentation

Partie XII
Cartographie d’entreprise, traversée du graphe, dépendances et scénarios d’impact

Partie XIII
Application Portfolio Management

Partie XIV
Transformation roadmaps et portefeuille d’initiatives

Partie XV
Dashboards, rapports et decision support
```

Partie XI explique comment représenter les relations.

Partie XII explique comment **les exploiter comme réseau de dépendances**.

---

## 3. Cartographie ≠ diagramme unique

Une cartographie d’entreprise est un **ensemble cohérent de vues dérivées d’un même graphe canonique**.

Exemple :

```text
Repository
├─ Capability Map
├─ Process Map
├─ Application Landscape
├─ Data Flow Map
├─ Technology Map
├─ Dependency Map
├─ Critical Path View
├─ Current / Target Map
└─ Transformation Impact View
```

Créer une seule image de 500 objets n’est pas une stratégie de cartographie.

---

## 4. Graphe d’architecture

On peut représenter conceptuellement le repository comme :

```text
G = (V, E)
```

avec :

```text
V = objets
E = relations gouvernées
```

Exemple MayaBank :

```text
Capability
→ Process
→ Application
→ Interface
→ Application
→ Platform
→ Technology
```

Chaque arête doit posséder une sémantique exploitable.

---

## 5. Node vs edge

### Node

Exemples :

- Business Capability ;
- Business Process ;
- Application ;
- Application Service ;
- Interface ;
- Information ;
- Platform ;
- Technology ;
- Organization ;
- Risk ;
- Control ;
- Initiative.

### Edge

Exemples :

```text
supports
consumes
publishes
owns
runs on
depends on
stores
mitigates
replaces
impacts
```

Le type de relation détermine le sens de l’analyse.

---

## 6. Les quatre niveaux de dépendances

### Niveau 1 — Business

```text
Capability
→ Process
→ Business Service
```

### Niveau 2 — Application

```text
Process
→ Application
→ Application Service
→ Interface
```

### Niveau 3 — Information

```text
Application
→ Information
→ Data Store
```

### Niveau 4 — Technology

```text
Application
→ Platform
→ Technology
→ Infrastructure context
```

Une analyse de changement utile traverse souvent plusieurs niveaux.

---

## 7. Direct vs transitive dependency

### Directe

```text
Payment Orchestrator
→ depends on
Fraud Decision Service
```

### Transitive

```text
Payment Orchestrator
→ Fraud Decision Service
→ IAM Platform
```

Le Payment Orchestrator dépend donc indirectement de l’IAM si le Fraud Service ne peut fonctionner sans lui.

La dépendance transitive doit être calculée ou déduite à partir de relations gouvernées, pas dessinée manuellement partout.

---

## 8. Dependency question first

Avant toute analyse, écrire la question.

Exemples :

```text
Que se passe-t-il si Kafka est indisponible ?

Quelles applications sont impactées si Java 17 doit être remplacé ?

Quels processus utilisent Legacy Payment Gateway ?

Quelles données sensibles transitent par une interface donnée ?

Quels composants doivent être restaurés avant Payment Orchestrator ?
```

La question détermine :

- point de départ ;
- direction de traversée ;
- types de relations ;
- profondeur ;
- filtres ;
- niveau de confiance exigé.

---

## 9. Méthode en douze étapes

1. Définir la décision attendue.
2. Définir le point de départ.
3. Identifier les types de relations autorisées.
4. Définir la direction de traversée.
5. Définir la profondeur maximale.
6. Filtrer par scope organisationnel, métier ou technique.
7. Exclure les liens non fiables ou obsolètes si nécessaire.
8. Identifier dépendances directes et transitives.
9. Détecter cycles, hubs et points de concentration.
10. Traduire les résultats en impact métier/risque/transformation.
11. Faire valider les dépendances critiques par les owners.
12. Publier la vue avec date, hypothèses et limites.

---

## 10. Traversée du graphe

Conceptuellement :

### Downstream

```text
Technology
→ Platforms
→ Applications
→ Processes
→ Capabilities
```

Question : qui est impacté par l’obsolescence de cette technologie ?

### Upstream

```text
Capability
→ Processes
→ Applications
→ Platforms
→ Technologies
```

Question : de quoi dépend cette capacité métier ?

---

## 11. Profondeur de traversée

### 1-hop

Relations directes.

### 2-hop

Dépendances des dépendances.

### n-hop

Chaîne plus large.

Plus la profondeur augmente :

- plus le volume augmente ;
- plus le bruit augmente ;
- plus la qualité des relations devient critique.

Le bon réflexe n’est pas `traverse everything`, mais `traverse enough to answer the decision`.

---

## 12. Cartographie multi-couches

Exemple MayaBank :

```text
Real-Time Payments Capability
↓
Execute Instant Payment
↓
Payment Orchestrator
├─ Fraud Decision Service
├─ Core Account Service
└─ Clearing Gateway
↓
OpenShift / Database / IAM / Kafka
```

Cette vue permet de passer d’un incident technique à un impact métier.

---

## 13. Faits produit vérifiés

Les pages publiques Bizzdesign Hopex consultées en septembre 2026 indiquent notamment que Hopex permet de :

- connecter business, IT, risk et data dans un repository unifié ;
- cartographier les flux de données et les dépendances ;
- identifier risques et impacts cachés ;
- réaliser de l’impact analysis ;
- soutenir des analyses de transformation et de changement ;
- réutiliser les informations dans des vues et rapports.

Des cas clients publics citent explicitement le dependency mapping et l’impact analysis pour planifier des changements.

Ce masterbook ne suppose pas que Hopex expose nativement toutes les métriques de graph theory décrites plus loin.

---

## 14. Best practices vs fonctionnalités produit

### Faits produit

Ce qui est confirmé publiquement :

- repository connecté ;
- dépendances ;
- impact analysis ;
- cartographies et visualisations ;
- données cross-domain.

### Pratiques d’architecture

Les concepts suivants sont utilisés comme méthodes d’analyse :

- n-hop traversal ;
- degree ;
- hub ;
- cycle ;
- bridge ;
- articulation point ;
- blast-radius scoring ;
- dependency confidence.

Ils peuvent être calculés dans Hopex, via API/export, ou avec un outil complémentaire selon les capacités installées.

---

## 15. MayaBank — baseline de cartographie

Périmètre de référence :

```text
Business
Payments / Fraud / Customer / Operations / Compliance

Applications
Digital Channel
API Management
IAM
Payment Orchestrator
Fraud Decision Service
Core Account Service
Clearing Gateway
Event Streaming
Notification Service
Reconciliation Service

Data
Payment Instruction
Payment Status
Fraud Decision
Clearing Result
Customer Identity

Platforms
OpenShift
Event Streaming
Database
IAM
Observability
Backup / DR
```

---

## 16. Artefacts minimum de la Partie XII

1. Enterprise Dependency Map.
2. Business-to-Technology Traceability Map.
3. Direct Dependency View.
4. Transitive Dependency View.
5. Critical Dependency Register.
6. Hub / Concentration Map.
7. Cycle Register.
8. SPOF / Choke Point Map.
9. Blast Radius Analysis.
10. Change Impact View.
11. Recovery Dependency View.
12. Current / Target Dependency Delta.

---

## 17. Definition of Done d’une cartographie

Une cartographie n’est pas terminée tant que :

- le scope n’est pas clair ;
- les relations critiques n’ont pas de source ;
- les objets ne sont pas canoniques ;
- current/target sont mélangés ;
- le sens des flèches n’est pas défini ;
- la profondeur de traversée n’est pas contrôlée ;
- l’analyse ne conduit à aucune décision.

---

## 18. Anti-patterns

- enterprise map de 1 000 objets ;
- liens bidirectionnels sans sémantique ;
- dépendances transitives copiées comme relations directes ;
- graph traversal sans filtres ;
- dépendances techniques considérées comme équivalentes aux dépendances métier ;
- SPOF déclaré uniquement parce qu’un objet apparaît une fois ;
- score de criticité sans source ;
- graphe ignoré dès qu’un diagramme est joli.

---

## 19. Questions d’entretien

**Quelle différence entre cartographie et diagramme ?**  
La cartographie est un système cohérent de vues dérivées d’un repository ; un diagramme n’est qu’une représentation.

**Pourquoi distinguer dépendance directe et transitive ?**  
Parce qu’un changement peut produire des impacts indirects importants sans relation immédiate entre la source du changement et le métier.

**Pourquoi limiter la profondeur de traversée ?**  
Pour éviter l’explosion du graphe et garder une analyse pertinente pour la décision.

**Hopex calcule-t-il nécessairement toutes les métriques de graph theory ?**  
Ce n’est pas affirmé ici. Ces métriques sont des méthodes d’analyse ; leur calcul peut nécessiter API, export ou outillage complémentaire selon l’environnement.
