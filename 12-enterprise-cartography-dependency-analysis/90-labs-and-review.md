# 90 — Hands-on Labs & 40 Questions Corrigées

# Partie A — 24 Labs

Les labs peuvent être réalisés sur papier, Markdown, Draw.io, tableur, notebook ou repository Hopex selon disponibilité de licence.

Le but est de pratiquer la **méthode**, pas de simuler des écrans non vérifiés.

---

## Lab 01 — Enterprise Context Map

### Objectif

Construire une carte L0 MayaBank avec :

```text
Customer
Payments
Accounts
Fraud
Operations
Compliance
Shared Platforms
External Clearing
```

### Travail

1. identifier les domaines ;
2. limiter à 10–12 objets ;
3. tracer uniquement les dépendances cross-domain majeures ;
4. ajouter owner et scope ;
5. écrire la décision servie.

### Contrôle

La vue doit être compréhensible en moins de 60 secondes.

---

## Lab 02 — Typed Dependency Register

Construire 15 relations en distinguant :

```text
functional
runtime
data
security
external
operational
```

### Contrôle

Aucun `depends on` générique si une sémantique plus précise est possible.

---

## Lab 03 — Direct vs Transitive Dependencies

Point de départ : `Payment Orchestrator`.

### Travail

Lister :

- dépendances 1-hop ;
- 2-hop ;
- impacts métier 3-hop.

### Contrôle

Ne pas enregistrer les liens transitifs comme dépendances directes.

---

## Lab 04 — Traversal Rule Card

Question :

> Quelles capacités métier dépendent d’OpenShift ?

Créer la carte :

```text
Start node
Direction
Allowed relation types
Max depth
Environment
Confidence
Stop conditions
```

---

## Lab 05 — Critical Dependency Path

Construire la chaîne :

```text
Instant Payment Service
→ applications
→ platforms
→ external dependencies
```

Classer chaque dépendance :

```text
STOP
DEGRADED
DELAYED
```

---

## Lab 06 — Hard vs Soft Dependencies

Classifier :

- IAM ;
- Core Account ;
- Fraud Decision ;
- Notification ;
- Analytics ;
- Observability.

### Contrôle

Justifier chaque classification par un effet métier.

---

## Lab 07 — Blast Radius : IAM

Point de départ : `IAM Platform`.

### Produire

1. direct consumers ;
2. indirect processes ;
3. capabilities ;
4. recovery dependencies ;
5. known unknowns.

---

## Lab 08 — Blast Radius : Event Streaming

Analyser une panne Kafka/Event Streaming.

Séparer :

```text
transaction path
notification
reconciliation
analytics
```

### Contrôle

Ne pas conclure que tout le paiement tombe sans vérifier le design.

---

## Lab 09 — Hub Detection

À partir du modèle MayaBank :

```text
IAM
API Management
Event Streaming
Core
OpenShift
```

Pour chacun :

- consumers count ;
- critical consumers ;
- fallback ;
- DR ;
- owner.

---

## Lab 10 — Cycle Detection

Créer un cycle legacy :

```text
Legacy Payment Hub
→ Shared DB
→ Reconciliation Batch
→ Payment Status Update
→ Legacy Payment Hub
```

### Travail

Identifier pourquoi ce cycle complique la migration et proposer 2 stratégies de découplage.

---

## Lab 11 — Bridge / Choke Point

Analyser :

```text
Internal Payments
→ Clearing Gateway
→ External Clearing
```

Questions :

- second path ?
- fallback ?
- capacity ?
- DR ?
- PKI/network dependency ?

---

## Lab 12 — Shared Failure Domain

Supposer :

```text
Payment Orchestrator and Fraud Service
run on different worker pools
but same cluster + DNS + IAM
```

Identifier les failure domains réellement partagés.

---

## Lab 13 — Recovery Dependency Graph

Construire l’ordre de reprise d’Instant Payment.

### Minimum

```text
Network/DNS
IAM/PKI
Data
Runtime platform
Core/Fraud
Orchestrator
Clearing
Async downstream
```

### Contrôle

Expliquer pourquoi consumer avant dependency ne fonctionne pas.

---

## Lab 14 — Minimum Viable Service

Définir ce qui doit être disponible pour exécuter un paiement en mode dégradé.

Séparer :

```text
Required
Can be delayed
Can be disabled
Unknown / needs business decision
```

---

## Lab 15 — Interface Deprecation

Retirer `Payment API v1`.

Créer :

- consumer inventory ;
- owner ;
- criticality ;
- migration status ;
- target interface ;
- retirement condition.

---

## Lab 16 — Technology Obsolescence Blast Radius

Point de départ : une version Java/OpenShift fictive en fin de support.

Tracer :

```text
Technology
→ platforms
→ applications
→ processes
→ initiatives
```

### Contrôle

Ne pas inventer de date de support réelle.

---

## Lab 17 — Data Schema Change

Changer `Payment Status` v1 → v2.

Lister :

- producers ;
- events ;
- APIs ;
- consumers ;
- stores ;
- reports ;
- migration strategy.

---

## Lab 18 — Shared Database Split

Cartographier :

```text
App A / B / C
→ Shared Payment DB
```

Puis définir :

- target ownership ;
- temporary sync ;
- dual-write risk ;
- migration waves.

---

## Lab 19 — Site Exit

Supposer la fermeture de `DC-A`.

Créer une requête logique :

```text
Site
→ deployments
→ platforms
→ applications
→ business services
```

Classer `Move / Retire / Replace / Unknown`.

---

## Lab 20 — External Provider Dependency

Choisir `External Clearing Service`.

Documenter :

- consuming service ;
- connectivity ;
- certificates ;
- SLA/RTO assumptions ;
- alternate path ;
- owner ;
- contract dependency.

---

## Lab 21 — Current / Target Dependency Delta

Comparer :

```text
Legacy Payment Architecture
vs
Target MayaBank Architecture
```

Produire :

```text
Removed dependencies
New dependencies
Temporary dependencies
Risk concentration changes
```

---

## Lab 22 — Migration Units

Regrouper les composants MayaBank en 4 unités de migration.

### Critères

- coupling ;
- data ;
- platform ;
- business window ;
- external provider.

---

## Lab 23 — Dependency Quality Audit

Créer un tableau de 20 relations avec :

```text
Source
Evidence date
Confidence
Owner
Current/Target
Review status
```

Identifier :

- stale ;
- unowned ;
- inferred ;
- conflicting.

---

## Lab 24 — Architecture Board Scenario

Sujet :

> Décommissionnement de Legacy Payment Gateway.

Préparer un pack 10 minutes :

1. current context ;
2. dependency graph ;
3. blast radius ;
4. unknown consumers ;
5. target replacement ;
6. migration waves ;
7. rollback ;
8. decommission evidence ;
9. risks ;
10. decision requested.

---

# Partie B — 40 Questions Corrigées

## Question 1

**Qu’est-ce qu’une Enterprise Cartography ?**

Un ensemble gouverné de cartes et vues dérivées d’un repository canonique permettant de comprendre structure, dépendances et transformations de l’entreprise.

---

## Question 2

**Quelle différence entre cartographie et diagramme ?**

Le diagramme est une représentation ; la cartographie est un système cohérent de représentations reliées au même repository.

---

## Question 3

**Qu’est-ce qu’un nœud ?**

Un objet du graphe : application, capability, process, data, platform, technology, risk, initiative, etc.

---

## Question 4

**Qu’est-ce qu’une arête ?**

Une relation typée entre deux objets, par exemple `supports`, `uses`, `consumes`, `runs on`.

---

## Question 5

**Dépendance directe vs transitive ?**

Directe : relation immédiate. Transitive : dépendance résultant d’une chaîne de relations.

---

## Question 6

**Pourquoi ne pas stocker chaque dépendance transitive comme relation directe ?**

Parce que cela duplique l’information, fausse la sémantique et devient impossible à maintenir.

---

## Question 7

**Qu’est-ce qu’un k-hop neighborhood ?**

L’ensemble des objets atteignables jusqu’à une profondeur `k` depuis un point de départ selon des relations autorisées.

---

## Question 8

**Pourquoi limiter la profondeur ?**

Pour éviter l’explosion du graphe et conserver une analyse pertinente.

---

## Question 9

**BFS vs DFS ?**

BFS explore par niveaux ; DFS suit une branche en profondeur. Ce sont des concepts génériques d’analyse de graphe.

---

## Question 10

**Une association est-elle toujours une dépendance ?**

Non. `owned by` est une relation de responsabilité, pas nécessairement une dépendance runtime.

---

## Question 11

**Functional dependency vs technical dependency ?**

La première concerne une fonction nécessaire au service ; la seconde un moyen d’implémentation/exécution.

---

## Question 12

**Hard vs soft dependency ?**

Hard bloque le service principal ; soft provoque une dégradation ou un retard sans bloquer le résultat essentiel.

---

## Question 13

**Asynchronous signifie-t-il absence de dépendance ?**

Non. Il reste des dépendances au broker, contrat, backlog, ordering, replay et cohérence.

---

## Question 14

**Qu’est-ce qu’un shared dependency ?**

Un service consommé par plusieurs systèmes/domaines, par exemple IAM ou Event Streaming.

---

## Question 15

**Qu’est-ce qu’un hub ?**

Un nœud très connecté selon un type de relation pertinent ; c’est un signal à analyser.

---

## Question 16

**Un hub est-il automatiquement un SPOF ?**

Non. Il faut analyser HA, fallback, failure domains, critical consumers et recovery.

---

## Question 17

**Qu’est-ce qu’un cycle ?**

Une chaîne de dépendances permettant de revenir au point de départ.

---

## Question 18

**Pourquoi les cycles compliquent-ils la migration ?**

Parce que les composants peuvent devoir évoluer ensemble ou nécessiter des mécanismes de coexistence.

---

## Question 19

**Qu’est-ce qu’un bridge ?**

Une relation structurante dont la suppression peut séparer deux parties du graphe.

---

## Question 20

**Qu’est-ce qu’un SPOF logique ?**

Un mécanisme/service unique dont la perte bloque une fonction même s’il possède plusieurs instances physiques.

---

## Question 21

**Blast radius ?**

Étendue potentielle des impacts directs et indirects d’une panne ou d’un changement.

---

## Question 22

**Pourquoi le nombre de voisins ne suffit-il pas à mesurer le blast radius ?**

Parce que criticité, type de dépendance, fallback, business exposure et confiance influencent la gravité.

---

## Question 23

**Qu’est-ce qu’une critical dependency path ?**

Une chaîne de dépendances dont la rupture menace un résultat métier critique.

---

## Question 24

**Pourquoi préciser qu’il ne s’agit pas du critical path projet ?**

Parce que `critical path` est aussi un terme de planification de projet avec une définition différente.

---

## Question 25

**Comment utiliser le graphe pour le PRA ?**

En partant du service métier, en identifiant hard dependencies, puis en inversant la chaîne pour définir l’ordre de reprise.

---

## Question 26

**Minimum viable service ?**

Sous-ensemble minimal de composants permettant de fournir le service essentiel de façon sûre et conforme.

---

## Question 27

**Pourquoi l’IAM/DNS/PKI sont-ils souvent oubliés ?**

Parce qu’ils sont transverses et hors du diagramme applicatif local, alors qu’ils peuvent être indispensables à l’exécution ou à la reprise.

---

## Question 28

**Pourquoi intégrer les external dependencies ?**

Parce qu’un service interne peut rester indisponible malgré un PRA réussi si le clearing, SaaS, carrier ou autre provider n’est pas accessible.

---

## Question 29

**Comment analyser un retrait d’API ?**

Identifier consumers, owners, processes, criticality, migration status, target contract et condition de retirement.

---

## Question 30

**Qu’est-ce qu’une migration unit ?**

Un ensemble de composants suffisamment couplés pour devoir être transformés ou déplacés ensemble.

---

## Question 31

**Pourquoi modéliser les dépendances temporaires ?**

Parce qu’elles conditionnent la transition et deviennent de la dette si elles ne sont pas retirées.

---

## Question 32

**Pourquoi la data est-elle une dépendance d’architecture ?**

Parce qu’un service peut être techniquement disponible mais incorrect si ses informations sont absentes, stale ou incohérentes.

---

## Question 33

**Source of truth vs replica ?**

La source of truth porte l’autorité ; le replica est une copie destinée à lecture, performance ou résilience.

---

## Question 34

**Qu’est-ce qu’une control dependency ?**

Une dépendance à un contrôle nécessaire pour autoriser, sécuriser ou prouver une opération.

---

## Question 35

**À quoi sert l’in-degree ?**

À mesurer le nombre de relations entrantes selon une sémantique, par exemple le nombre de consumers d’un service.

---

## Question 36

**Centrality = criticité métier ?**

Non. La centrality est une propriété topologique, pas une mesure directe de valeur ou d’impact métier.

---

## Question 37

**Pourquoi la confidence doit-elle apparaître ?**

Parce qu’un résultat basé sur relations inferred/stale ne doit pas être présenté comme équivalent à une dépendance vérifiée.

---

## Question 38

**Hopex remplace-t-il un graph database ?**

Hopex sert ici de repository EAM gouverné. Un graph database peut compléter l’analyse avancée sans devenir une seconde source de vérité.

---

## Question 39

**Comment maintenir la cartographie ?**

Avec owners, evidence, sources automatiques/manuelles, attestations périodiques, triggers de revue et feedback d’incidents.

---

## Question 40

**Règle d’or de la Partie XII ?**

```text
Do not map everything.
Map the dependencies needed to make decisions,
and make their evidence, scope and confidence explicit.
```
