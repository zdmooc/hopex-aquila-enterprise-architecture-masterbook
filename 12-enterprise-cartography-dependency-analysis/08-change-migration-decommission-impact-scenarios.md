# 08 — Change, Migration & Decommission Impact Scenarios

## 1. La cartographie au service du changement

La valeur d’un dependency graph apparaît lorsqu’il permet de répondre avant le changement :

```text
Who is affected?
What must move first?
What can move independently?
What must coexist?
What must be tested?
What can be retired safely?
```

---

## 2. Change object

Le point de départ d’un changement peut être :

- application ;
- interface ;
- data model ;
- platform ;
- technology version ;
- site ;
- vendor ;
- control ;
- business process.

---

## 3. Change Impact Card

```text
Change
Reason
Source object
Target date
Current state
Target state
Direct consumers
Transitive impacts
Critical dependencies
Owners
Test scope
Migration actions
Fallback/Rollback
Residual risks
```

---

## 4. Application replacement

Exemple :

```text
Legacy Payment Gateway
→ replaced by
Payment Orchestrator + Clearing Gateway
```

L’analyse doit couvrir :

- interfaces entrantes ;
- interfaces sortantes ;
- business processes ;
- data ownership ;
- technologies ;
- operational procedures ;
- controls ;
- external partners.

---

## 5. Interface deprecation

Question : retirer `Payment API v1`.

```text
API v1
→ consumers
→ consumer owners
→ supported processes
→ migration status
→ target API
```

Créer un register :

| Consumer | Owner | Criticality | Migration status | Target |
|---|---|---|---|---|
| Channel A | Digital | High | In progress | API v2 |
| Partner B | Partnership | High | Not started | API v2 |

---

## 6. Technology upgrade

Exemple : upgrade OpenShift.

```text
OpenShift release
→ clusters/platforms
→ hosted applications
→ operators/add-ons
→ storage/network dependencies
→ test scope
```

Ne pas limiter l’impact aux applications directement hébergées si des services partagés sont aussi affectés.

---

## 7. Technology retirement

```text
Deprecated Technology
→ platforms
→ applications
→ processes
→ business owners
→ initiatives
```

Cela permet de transformer une date d’obsolescence en portefeuille de remédiation.

---

## 8. Database migration

Exemple : Oracle → PostgreSQL pour une application compatible.

Analyser :

- application CRUD ;
- schema dependencies ;
- batch ;
- reporting ;
- interfaces ;
- stored procedures ;
- backup/DR ;
- operational tooling ;
- data migration ;
- reconciliation.

---

## 9. Shared database split

```text
App A ─┐
App B ─┼→ Shared DB
App C ─┘
```

Avant découpage :

1. identifier tables/entities par responsabilité ;
2. identifier cross-schema reads ;
3. identifier transactions multi-domaines ;
4. identifier batch/reporting ;
5. définir target ownership ;
6. créer transition data flows.

---

## 10. Event migration

Exemple : ancien bus → Event Streaming Platform.

Analyser :

```text
producers
consumers
schemas
ordering
replay
retention
security
monitoring
coexistence
```

---

## 11. Cloud migration

Point de départ : application.

Dependency graph :

```text
Application
→ interfaces
→ data stores
→ network zones
→ IAM
→ shared files
→ batch
→ on-prem systems
→ external partners
```

Un simple score `cloud ready` ne remplace pas cette cartographie.

---

## 12. OpenShift migration

Pour un workload :

- runtime compatibility ;
- persistent storage ;
- network flows ;
- certificates ;
- secrets ;
- observability ;
- database connectivity ;
- HA ;
- DR ;
- scheduling/capacity.

Le graphe permet d’identifier les dépendances qui restent on-prem.

---

## 13. Site exit

Question : fermer un datacenter.

```text
Site
→ platforms
→ deployments
→ applications
→ data stores
→ network dependencies
→ business services
```

Puis classer :

```text
Move
Retire
Replace
Externalize
Unknown
```

---

## 14. Vendor exit

```text
Vendor
→ products/services
→ platforms
→ applications
→ business processes
```

Inclure :

- licence ;
- support ;
- skills ;
- data export ;
- proprietary protocols ;
- migration tooling.

---

## 15. Regulatory change

Point de départ : obligation/requirement ou contrôle.

```text
Requirement
→ Processes
→ Controls
→ Applications
→ Data
→ Evidence
```

Le dependency graph aide à identifier le change scope.

---

## 16. Data classification change

Exemple : une information passe `Internal` → `Restricted`.

Analyser :

```text
Information
→ stores
→ interfaces/events
→ applications
→ users/organizations
→ external parties
```

Puis vérifier chiffrement, accès, logs et retention selon politiques réelles.

---

## 17. M&A / carve-out

Pour séparer une entité :

```text
Org Unit
→ capabilities
→ processes
→ applications
→ data
→ shared platforms
→ contracts/vendors
```

Les dépendances partagées deviennent la difficulté principale.

---

## 18. Dependency sequencing

Une transformation doit respecter les prérequis.

Exemple :

```text
API Management target
before
Payment Orchestrator migration

Event Streaming target
before
Notification decoupling
```

L’ordre exact dépend du target design.

---

## 19. Dependency DAG — objectif de planification

Pour planifier, on cherche souvent un graphe sans cycle entre grands work packages :

```text
Foundation
→ Data/Integration
→ Applications
→ Cutover
→ Decommission
```

Si cycles existent, il faut les casser ou planifier coexistence/dual-run.

---

## 20. Transition dependencies

Les états temporaires peuvent créer de nouvelles dépendances :

- adapters ;
- replication ;
- dual-write ;
- bridge topics ;
- reverse proxy ;
- sync batch ;
- temporary VPN.

Elles doivent avoir une date de retrait.

---

## 21. Coexistence map

```text
Current Application
↔ synchronization
Target Application
```

Documenter :

- source of truth ;
- conflict resolution ;
- direction ;
- cutover trigger ;
- rollback ;
- retirement condition.

---

## 22. Cutover dependency map

Avant bascule :

```text
Target platform ready
Data migrated
Interfaces migrated
Consumers tested
Operations ready
Monitoring ready
Rollback ready
```

La cartographie transforme ces prérequis en checklist structurée.

---

## 23. Decommission readiness

Une application ne doit pas être retirée si :

- consumer inconnu ;
- interface encore active ;
- data retention non traitée ;
- batch/reporting oublié ;
- owner non validé ;
- dependency confidence faible ;
- rollback/archival non défini.

---

## 24. Decommission evidence

```text
No active consumers
No active interfaces
Data archived/migrated
Controls transferred
Operational jobs stopped
Contracts/licences handled
Monitoring removed
CMDB/runtime cleaned
Owner approval
```

---

## 25. Change wave grouping

Regrouper les objets selon :

- dépendances fortes ;
- domaine ;
- target platform ;
- business window ;
- data coupling ;
- vendor constraints.

---

## 26. Migration cluster

Si A/B/C sont fortement couplés :

```text
A ↔ B ↔ C
```

ils peuvent devoir être migrés ensemble.

La cartographie aide à définir un `migration unit` réaliste.

---

## 27. Strangler dependencies

Pattern :

```text
Consumer
→ façade/router
├→ Legacy
└→ Target service
```

Le graph doit montrer quelles fonctions ont été extraites et quels consommateurs restent legacy.

---

## 28. Rollback dependency

Une migration n’est rollbackable que si :

- data compatible ;
- ancienne interface disponible ;
- routing reversible ;
- schema changes compatibles ;
- backlog maîtrisé.

---

## 29. MayaBank — modernization waves

### Wave 0 — foundations

```text
API Management
IAM
OpenShift
Observability
Event Streaming
```

### Wave 1 — orchestration

```text
Payment Orchestrator
Fraud integration
```

### Wave 2 — clearing

```text
Clearing Gateway
Partner connectivity
```

### Wave 3 — downstream

```text
Notification
Reconciliation
Analytics
```

### Wave 4 — retirement

```text
Legacy Payment Gateway
Legacy shared DB dependencies
```

Séquence pédagogique.

---

## 30. MayaBank — decommission query

Question : peut-on retirer `Legacy Payment Gateway` ?

Minimum :

```text
Consumers = 0 or migrated
Interfaces = retired
Processes = target-supported
Data = migrated/archived
Controls = transferred
Technology = no residual dependency
Owners = approved
```

---

## 31. Architecture Board pack

- source object ;
- direct impacts ;
- transitive impacts ;
- unknowns ;
- criticality ;
- target replacement ;
- migration waves ;
- test scope ;
- rollback ;
- residual risks.

---

## 32. Anti-patterns

- migration plan sans dependency graph ;
- retirer une API après simple email ;
- oublier les batch/reporting ;
- current et target sans coexistence ;
- adapter temporaire sans retirement date ;
- migration par application alors que le coupling impose un cluster ;
- decommission basé sur absence de trafic observé seulement.

---

## 33. Questions d’entretien

**Comment utiliser le graph pour décommissionner une application ?**  
En vérifiant consommateurs, interfaces, processus, données, contrôles, technologies, owners et dépendances résiduelles.

**Pourquoi modéliser les dépendances temporaires ?**  
Parce qu’elles conditionnent la réussite de la transition et deviennent de la dette si elles restent invisibles.

**Qu’est-ce qu’une migration unit ?**  
Un ensemble d’objets suffisamment couplés pour devoir être transformés ou déplacés ensemble.
