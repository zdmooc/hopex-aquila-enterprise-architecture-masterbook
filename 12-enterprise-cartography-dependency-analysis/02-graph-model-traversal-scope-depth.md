# 02 — Graph Model, Traversal, Scope & Depth

## 1. Pourquoi formaliser le graphe

Une analyse de dépendances devient vite incontrôlable si l’on ne définit pas :

- quels objets sont dans le graphe ;
- quelles relations sont traversables ;
- dans quel sens ;
- jusqu’à quelle profondeur ;
- avec quels filtres ;
- avec quel niveau de confiance.

Le modèle conceptuel minimal est :

```text
Node
+ typed Edge
+ direction
+ scope
+ temporal state
+ evidence
```

---

## 2. Types de nœuds

Une cartographie d’entreprise MayaBank peut inclure :

### Business

```text
Capability
Value Stream
Business Process
Business Service
Organization
```

### Application

```text
Application
Application Service
Interface
API
Event
Batch Flow
```

### Information

```text
Information Concept
Logical Data Entity
Data Store
Data Product
```

### Technology

```text
Platform
Technology Product
Technology Version
Deployment Context
External Service
```

### Risk / Transformation

```text
Risk
Control
Initiative
Project
Target State
```

---

## 3. Typed edges

Une traversée ne doit pas traiter toutes les relations comme équivalentes.

Exemple :

```text
Application A -- invokes --> Application B
Application A -- runs on --> Platform X
Application A -- owned by --> Org Unit Y
Application A -- uses --> Information Z
```

Ces quatre relations n’ont pas le même sens d’impact.

---

## 4. Traversable edge set

Pour chaque scénario, définir un ensemble de relations autorisées.

Exemple — impact technologique :

```text
Technology
→ used by Platform
→ hosts Application
→ supports Process
→ enables Capability
```

Exemple — incident applicatif :

```text
Application
→ consumed by Application
→ supports Process
→ supports Business Service
```

Exemple — data impact :

```text
Information
→ produced by Application
→ consumed by Application
→ used by Process
```

---

## 5. Traversée forward vs reverse

### Forward

Suivre le sens naturel de consommation ou dépendance.

```text
Channel
→ API Management
→ Payment Orchestrator
→ Core Account Service
```

### Reverse

Chercher les consommateurs ou dépendants.

```text
Core Account Service
← Payment Orchestrator
← Digital Channel
```

Le sens de l’analyse doit être explicite.

---

## 6. Breadth-first vs depth-first

Concepts génériques de graph theory.

### Breadth-first search — BFS

Explore d’abord les voisins proches.

Utile pour :

- blast radius par niveau ;
- dépendances 1-hop, 2-hop, 3-hop ;
- analyse de proximité.

### Depth-first search — DFS

Explore une chaîne jusqu’au bout avant de revenir.

Utile pour :

- rechercher des cycles ;
- explorer une chaîne de dépendance ;
- comprendre une branche précise.

Le masterbook n’affirme pas qu’un bouton Hopex expose directement BFS/DFS ; ce sont des méthodes conceptuelles ou implémentables via API/export.

---

## 7. k-hop neighborhood

Le voisinage d’un objet à profondeur `k` peut être défini pédagogiquement comme :

```text
N1(x) = dépendances directes
N2(x) = dépendances directes + dépendances de niveau 2
Nk(x) = toutes les dépendances jusqu’à profondeur k
```

Exemple :

```text
Kafka Platform
N1 → Payment Orchestrator, Notification, Reconciliation
N2 → Processes supportés
N3 → Capabilities et Business Services
```

---

## 8. Scope fonctionnel

Un graphe doit souvent être limité par :

- domaine métier ;
- ligne de produit ;
- geography ;
- legal entity ;
- environment ;
- lifecycle ;
- criticality ;
- transformation program.

Exemple MayaBank :

```text
Domain = Payments
Environment = PROD
Criticality = High/Critical
Lifecycle = Current
```

---

## 9. Scope temporel

Une cartographie peut porter sur :

```text
Current
Transition 1
Transition 2
Target
Retired
```

Ne jamais traverser automatiquement current et target comme s’ils coexistaient réellement.

---

## 10. Scope par confiance

Une analyse d’Architecture Board peut exclure :

```text
Confidence < Medium
Stale relation
Unverified imported edge
Owner not confirmed
```

Une analyse de découverte peut au contraire les inclure pour identifier les zones d’incertitude.

---

## 11. Edge confidence

Taxonomie pédagogique :

```text
Verified
Observed
Imported
Inferred
Unverified
Stale
```

On peut produire deux graphes :

### Graph A — decision-grade

Uniquement relations Verified / Observed / valid Imported.

### Graph B — discovery

Inclut Inferred / Unverified pour investiguer.

---

## 12. Traversal rule card

Chaque analyse sérieuse devrait documenter :

```text
Question
Start node type
Start node
Direction
Allowed node types
Allowed relation types
Max depth
Temporal scope
Confidence threshold
Environment
Domain scope
Exclusions
Expected output
```

---

## 13. Exemple — upgrade OpenShift

### Question

Quelles capacités métier peuvent être exposées à un upgrade majeur de la plateforme OpenShift ?

### Traversal

```text
Start = OpenShift Platform
Direction = reverse dependency
Relations = hosts / runs on / supports
Max depth = 4
Environment = PROD
Confidence >= Medium
```

### Résultat attendu

```text
OpenShift
→ Payment Orchestrator
→ Execute Instant Payment
→ Real-Time Payments Capability
```

avec branches Fraud, API Management, Notification selon modèle réel.

---

## 14. Exemple — retrait d’une interface

```text
Start = Legacy Payment API v1
Direction = consumer-side
Relations = consumed by / invokes
Max depth = 2
```

Résultat : liste des applications consommatrices directes puis processus associés.

---

## 15. Exemple — donnée sensible

Question : où circule `Customer Identity` ?

```text
Customer Identity
→ produced/managed by
→ applications
→ transported via interfaces/events
→ consumed by processes
→ stored in data stores
```

Le scope de classification vient de la Partie IX.

---

## 16. Stop conditions

Une traversée doit pouvoir s’arrêter lorsque :

- profondeur atteinte ;
- type d’objet terminal atteint ;
- relation hors scope ;
- objet retired ;
- faible confiance ;
- domaine hors périmètre ;
- frontière externe explicitement atteinte.

---

## 17. External dependencies

Une entreprise dépend de services qu’elle ne possède pas :

```text
Clearing Network
Cloud Provider
External Fraud Feed
Certificate Authority
Telecom Provider
SaaS
Partner API
```

Ils doivent être représentés si leur indisponibilité modifie le service rendu.

---

## 18. Boundary object

Pour éviter de modéliser un partenaire entier, utiliser un objet frontière utile :

```text
External Clearing Service
External Identity Provider
Cloud Region
Partner API
```

Le détail interne du partenaire n’est pas nécessaire sauf besoin contractuel ou opérationnel.

---

## 19. Path explosion

Si un hub possède 100 relations et que la profondeur augmente :

```text
1-hop = 100
2-hop = potentiellement milliers
3-hop = inutilisable sans filtres
```

Techniques de maîtrise :

- filtrer par relation ;
- filtrer par criticité ;
- limiter profondeur ;
- regrouper par domaine ;
- utiliser matrices/listes pour le volume ;
- ouvrir un sous-graphe à la demande.

---

## 20. Orphan nodes

Un objet sans relation peut signaler :

- donnée incomplète ;
- objet obsolète ;
- mauvaise granularité ;
- import non relié ;
- actif réellement isolé.

Exemples à auditer :

```text
Critical application with no process
Technology with no consumer
Process with no supporting application
Interface with no provider
```

---

## 21. Dead-end paths

Une chaîne qui s’arrête anormalement peut révéler un trou de modélisation.

```text
Application
→ Platform
→ ???
```

ou :

```text
Process
→ Application
→ no technology/deployment context
```

---

## 22. Duplicate paths

Plusieurs chemins entre deux objets peuvent être légitimes.

Exemple :

```text
Payment Orchestrator
→ Event Streaming
→ Notification

Payment Orchestrator
→ Notification API
```

Il faut distinguer redondance de chemin et duplication de données.

---

## 23. Shortest path — usage prudent

Un shortest path peut être utile pour expliquer le chemin minimal entre deux objets.

Mais le chemin le plus court n’est pas forcément :

- le plus critique ;
- le plus fréquent ;
- le plus risqué ;
- le chemin runtime réellement emprunté.

Ne pas en faire une vérité opérationnelle sans données complémentaires.

---

## 24. MayaBank — règles de traversée de référence

### Business impact

```text
Technology → Platform → Application → Process → Capability
```

### Consumer impact

```text
Interface → Consumer Application → Process
```

### Data impact

```text
Information → Producer/Consumer Applications → Interfaces → Processes
```

### DR order

```text
Business Service → Application → Platform → Dependencies
```

puis inverser pour déterminer l’ordre de restauration.

---

## 25. Anti-patterns

- traverser toute relation disponible ;
- considérer 1-hop et 5-hop comme même niveau d’impact ;
- mélanger target et current ;
- inclure les objets retired par défaut ;
- ignorer la qualité des relations ;
- appeler « dépendance » toute proximité dans un diagramme ;
- ne pas documenter les stop conditions.

---

## 26. Questions d’entretien

**BFS et DFS servent à quoi ?**  
BFS est utile pour explorer par niveau de proximité ; DFS pour explorer une chaîne et détecter certains cycles.

**Pourquoi un max depth ?**  
Pour maîtriser l’explosion du graphe et limiter l’analyse à une distance utile.

**Qu’est-ce qu’un boundary object ?**  
Une représentation contrôlée d’une dépendance externe sans modéliser inutilement tout le système partenaire.

**Pourquoi filtrer par confiance ?**  
Parce qu’une décision critique ne doit pas être basée de la même façon sur une relation confirmée et une relation simplement inférée.
