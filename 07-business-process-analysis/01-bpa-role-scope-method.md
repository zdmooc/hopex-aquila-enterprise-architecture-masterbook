# 01 — Business Process Analysis : rôle, périmètre et méthode

## 1. BPA n'est pas seulement du dessin BPMN

La Business Process Analysis vise à comprendre, gouverner et améliorer la manière dont le travail est réellement exécuté.

Dans HOPEX, le processus doit être considéré comme un objet du repository relié à :

- une capability ;
- un owner ;
- une organisation ;
- des rôles ;
- des applications ;
- des données ;
- des risques ;
- des contrôles ;
- des KPIs ;
- des initiatives de transformation.

Un diagramme BPMN n'est donc qu'une représentation d'une partie de cette connaissance.

## 2. Questions auxquelles la BPA doit répondre

1. Quel résultat métier produit le processus ?
2. Qui en est responsable ?
3. Quelles étapes créent réellement de la valeur ?
4. Où se trouvent les délais et handoffs ?
5. Quels systèmes supportent chaque étape ?
6. Quelles informations sont créées, lues ou modifiées ?
7. Quels risques et contrôles existent ?
8. Quels événements déclenchent ou interrompent le processus ?
9. Quels scénarios d'exception existent ?
10. Quels KPIs permettent de savoir si le processus fonctionne ?
11. Quelles étapes peuvent être standardisées, automatisées ou supprimées ?
12. Quel est l'impact d'un changement applicatif ou réglementaire ?

## 3. Positionnement actuel de Bizzdesign Hopex

Le positionnement public actuel met en avant :

- une source partagée de modèles de processus ;
- l'analyse et l'optimisation des processus ;
- le suivi de performance via KPIs ;
- le mapping processus ↔ contrôles/régulations ;
- la standardisation des processus ;
- BPMN 2.0 ;
- la connexion aux applications, données, risques et organisation ;
- l'intégration avec des outils de process mining ;
- l'import de modèles Visio vers des modèles BPMN HOPEX ;
- des capacités de simulation via un add-on dédié.

Le détail exact dépend de la licence, des modules et de la configuration.

## 4. Les quatre niveaux de process architecture

### L0 — Enterprise process landscape

Quelques grands domaines :

```text
Manage Customers
Manage Payments
Manage Risk
Manage Finance
Manage Technology
```

### L1 — Process domains

Exemple Payments :

```text
Initiate Payment
Execute Payment
Handle Exception
Investigate Fraud Alert
Reconcile Payment
```

### L2 — End-to-end processes

Exemple :

```text
Execute Instant Payment
```

### L3/L4 — Detailed process design

BPMN détaillé : événements, activités, gateways, messages, exceptions, participants.

Le niveau de détail doit répondre à une décision ou un besoin de gouvernance.

## 5. Process Architecture vs BPMN

Process Architecture :

```text
Catalogue
+ hierarchy
+ ownership
+ lifecycle
+ KPIs
+ relations
```

BPMN :

```text
Flow logic
+ events
+ activities
+ gateways
+ participants
+ messages
```

Un repository mature utilise les deux.

## 6. Méthode en dix étapes

### Étape 1 — définir le scope

Exemple : traitement d'un paiement instantané depuis l'initiation client jusqu'à la confirmation.

### Étape 2 — définir l'outcome

```text
Payment executed or rejected within SLA,
with traceability and fraud control.
```

### Étape 3 — identifier les participants

Customer, Channel, Payment Orchestrator, Fraud, Operations, Clearing.

### Étape 4 — identifier événements et étapes majeures

### Étape 5 — modéliser le happy path

### Étape 6 — ajouter les exceptions significatives

### Étape 7 — relier applications et données

### Étape 8 — relier risques et contrôles

### Étape 9 — définir KPIs et SLAs

### Étape 10 — identifier les opportunités d'amélioration

## 7. Principe « modèle avant automatisation »

Automatiser un mauvais processus accélère le gaspillage.

Avant RPA, workflow ou orchestration :

```text
Understand
→ Simplify
→ Standardize
→ Control
→ Automate
→ Measure
```

## 8. Exemple MayaBank

Process : `Execute Instant Payment`

```text
Start: Customer submits payment
↓
Validate request
↓
Authenticate / authorize
↓
Fraud decision
↓
Funds / account checks
↓
Send to clearing
↓
Receive result
↓
Update payment status
↓
Notify customer
↓
End
```

Exceptions :

- invalid request ;
- fraud suspected ;
- insufficient funds ;
- clearing timeout ;
- duplicate payment ;
- downstream outage.

## 9. Deliverables utiles

- Process Map ;
- BPMN diagram ;
- RACI ;
- Process/Application Matrix ;
- Process/Data Matrix ;
- Risk/Control Matrix ;
- KPI catalogue ;
- exception catalogue ;
- improvement backlog ;
- target process model.

## 10. Questions d'entretien

**Pourquoi un repository de processus plutôt qu'un dossier Visio ?**  
Pour disposer d'objets canoniques réutilisables, reliés aux owners, applications, données, contrôles et KPIs.

**Pourquoi distinguer process architecture et BPMN ?**  
La première structure le paysage et la gouvernance ; le second décrit la logique d'exécution détaillée.

**Quel est le principal risque d'un programme BPA ?**  
Produire beaucoup de diagrammes sans ownership, métriques ni processus de maintenance.