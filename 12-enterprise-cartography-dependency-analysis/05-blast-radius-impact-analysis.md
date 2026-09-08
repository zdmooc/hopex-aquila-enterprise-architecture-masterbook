# 05 — Blast Radius & Impact Analysis

## 1. Définition

Le blast radius décrit **l’étendue potentielle des impacts d’un changement, d’une panne ou d’une dégradation à partir d’un objet du repository**.

Exemples de points de départ :

- application ;
- interface ;
- plateforme ;
- technologie ;
- data object ;
- site ;
- fournisseur ;
- contrôle ;
- initiative.

---

## 2. Blast radius ≠ nombre de voisins

Un objet avec 50 relations n’a pas nécessairement un blast radius plus important qu’un objet avec 3 relations.

La gravité dépend notamment :

```text
Criticality
Dependency type
Fallback
Business exposure
Data sensitivity
Regulatory exposure
Recovery complexity
Confidence
```

---

## 3. Analyse en couches

Pour un composant technique :

```text
Technology / Platform
↓
Applications
↓
Processes
↓
Capabilities
↓
Business Services
↓
Customers / Operations / Compliance
```

Pour une application :

```text
Application
├→ Consumers
├→ Interfaces
├→ Data
├→ Processes
├→ Capabilities
├→ Platforms
└→ Initiatives
```

---

## 4. Blast radius direct

Relations 1-hop seulement.

Exemple :

```text
Event Streaming Platform
→ Payment Orchestrator
→ Notification Service
→ Reconciliation Service
```

Cela répond à : `qui consomme directement cette plateforme ?`

---

## 5. Blast radius transitive

```text
Event Streaming
→ Notification
→ Customer Notification Process
→ Customer Communication Capability
```

L’impact métier apparaît après plusieurs hops.

---

## 6. Horizontal blast radius

Impact sur des objets du même niveau.

Exemple :

```text
API Management outage
→ Payment Orchestrator
→ Customer Portal
→ Fraud APIs
```

---

## 7. Vertical blast radius

Impact cross-layer :

```text
Technology
→ Application
→ Process
→ Capability
```

C’est souvent la vue la plus utile pour l’Architecture Board.

---

## 8. Blast radius par environnement

```text
PROD outage
≠ UAT outage
```

Toujours filtrer le contexte d’exécution si les relations de déploiement le permettent.

---

## 9. Blast radius fonctionnel

Question :

> Si Fraud Decision Service n’est plus disponible, quelles fonctions sont touchées ?

Chemin :

```text
Fraud Decision Service
→ consumer applications
→ activities/processes
→ capabilities
```

---

## 10. Blast radius technologique

Question :

> Si une version Java sort du support, quels éléments sont concernés ?

```text
Java version
→ platforms / applications
→ business processes
→ transformation initiatives
```

---

## 11. Blast radius data

Question :

> Si la définition de Payment Status change, qui doit être revu ?

```text
Payment Status
→ producers
→ consumers
→ APIs/events
→ stores
→ reports/processes
```

---

## 12. Blast radius sécurité

Question :

> Quel est l’impact d’un compromis de l’IAM ?

```text
IAM
→ applications using identity
→ privileged operations
→ critical processes
→ business services
```

La cartographie ne remplace pas une threat model détaillée.

---

## 13. Blast radius fournisseur

```text
External Provider
→ supplied service
→ applications
→ business services
```

Utile pour concentration fournisseur et continuité.

---

## 14. Blast radius géographique

```text
Site / Region
→ platforms
→ applications
→ services
```

Permet d’analyser la perte d’un datacenter ou d’une région cloud.

---

## 15. Impact dimensions

Pour chaque objet impacté, conserver pédagogiquement :

```text
Impact type
Distance
Criticality
Fallback
Confidence
Owner
Required action
```

---

## 16. Distance comme indicateur

Exemple :

```text
Distance 1 = direct
Distance 2 = indirect close
Distance 3+ = wider business exposure
```

La distance ne suffit pas à mesurer la gravité.

---

## 17. Weighted blast radius — pratique pédagogique

On peut calculer un score de priorisation :

```text
Weight = criticality × dependency strength × confidence
```

puis agréger les objets impactés.

Ce modèle est pédagogique et ne constitue pas une formule produit Hopex officielle.

---

## 18. Impact register

| Source | Impacted object | Distance | Effect | Severity | Action |
|---|---|---:|---|---|---|
| Kafka | Notification | 1 | delayed notifications | Medium | verify replay |
| Kafka | Reconciliation | 1 | delayed recon | High | capacity test |
| Kafka | Payments Operations | 2 | backlog | High | operational procedure |

---

## 19. Change impact analysis

Pour un changement planifié :

```text
Change Object
→ impacted objects
→ impacted owners
→ required tests
→ required migrations
→ required communications
```

---

## 20. Interface deprecation example

```text
Legacy API v1
→ Consumer A
→ Consumer B
→ Consumer C
```

Puis :

```text
Consumers
→ processes
→ owners
→ migration initiatives
```

Livrable : deprecation impact pack.

---

## 21. Technology upgrade example

```text
OpenShift Upgrade
→ clusters/platforms
→ hosted applications
→ critical services
→ test scope
→ rollback plan
```

---

## 22. Data model change example

```text
Payment Status model change
→ event schema
→ API schema
→ consumers
→ reconciliation
→ reporting
```

---

## 23. Incident analysis

Pendant ou après incident :

```text
Failed component
→ known dependencies
→ observed symptoms
→ missing relationships
```

Les écarts entre repository et incident réel deviennent un backlog de data quality.

---

## 24. Known impact vs suspected impact

Séparer :

```text
Known = supported by verified relationship
Suspected = inferred from weak evidence
```

Le board doit savoir quelle partie de l’impact est certaine.

---

## 25. Impact confidence

Taxonomie pédagogique :

```text
High
Medium
Low
Unknown
```

Elle peut dépendre de :

- source ;
- date ;
- owner validation ;
- discovery evidence ;
- runtime observation.

---

## 26. Impact owner

Tout impact important devrait avoir un owner responsable de :

- confirmer ;
- accepter ;
- mitiger ;
- tester ;
- planifier la remédiation.

---

## 27. Blast radius and test strategy

Le graphe permet de définir un scope de tests :

```text
changed component
→ direct consumers
→ critical process paths
→ data contracts
→ failure modes
```

---

## 28. Blast radius and communication

Un changement d’infrastructure peut nécessiter d’informer :

```text
Application Owners
Business Owners
Operations
Security
Data Owners
Vendor Managers
```

Le repository peut fournir les relations d’ownership nécessaires.

---

## 29. MayaBank — perte de Kafka

### Direct

```text
Payment Orchestrator
Notification Service
Reconciliation Service
```

### Indirect

```text
Customer notification
Operational reconciliation
Analytics freshness
Potential backlog/replay requirements
```

Le paiement principal peut ou non rester exécutable selon le design réel.

---

## 30. MayaBank — perte IAM

```text
IAM
→ API Management
→ Payment Orchestrator
→ Fraud Service
→ operational consoles
```

Si l’identité est un shared dependency sans fallback, le blast radius peut être très important.

---

## 31. MayaBank — retrait Legacy Payment Gateway

Analyse :

```text
Legacy Gateway
→ interfaces
→ consumers
→ process steps
→ business capabilities
→ data flows
→ technologies
→ migration waves
```

Puis classification :

```text
Must migrate
Can retire
Unknown consumer
Temporary coexistence
```

---

## 32. Anti-patterns

- blast radius = nombre de connexions ;
- impact analysis sans temporalité ;
- mélanger known et suspected ;
- oublier les owners ;
- ignorer data/control dependencies ;
- considérer tous les impacts de même gravité ;
- cartographier les impacts sans action associée.

---

## 33. Questions d’entretien

**Qu’est-ce que le blast radius ?**  
L’étendue potentielle des impacts directs et indirects d’un changement ou d’une panne.

**Pourquoi la distance ne suffit-elle pas ?**  
Parce qu’un impact à trois hops peut être plus critique qu’un voisin direct facultatif.

**Comment utiliser le blast radius pour une migration ?**  
Pour identifier consommateurs, processus, owners, données, tests et dépendances à traiter avant le changement.
