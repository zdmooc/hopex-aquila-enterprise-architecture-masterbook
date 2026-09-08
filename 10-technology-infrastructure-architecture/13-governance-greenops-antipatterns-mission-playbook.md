# 13 — Gouvernance, GreenOps, anti-patterns & mission playbook

## 1. Gouvernance de l’architecture technologique

Une Technology Architecture durable nécessite des responsabilités explicites.

### Technology Owner
Responsable du cycle de vie et de la stratégie d’une technologie.

### Platform Owner
Responsable du service de plateforme réellement exploité.

### Infrastructure Architect
Conçoit topologies, failure domains et dépendances.

### Security Architect
Valide zones, identity, trust boundaries et contrôles.

### SRE / Operations
Porte exploitabilité, observabilité, capacity et recovery.

### Application Architect
Valide les besoins et impacts sur les applications.

## 2. Governance lifecycle

```text
Proposed
→ Architecture Review
→ Approved
→ Implemented
→ Operational Review
→ Periodic Review
→ Deprecated
→ Retired
```

## 3. Quality gates — Technology Object

Obligatoire :

- canonical name ;
- family ;
- owner ;
- status ;
- lifecycle evidence ;
- platforms/applications consuming it ;
- review date.

## 4. Quality gates — Platform

- owner ;
- purpose ;
- consumers ;
- environments ;
- criticality ;
- RTO/RPO ;
- failure domains ;
- security zone ;
- observability ;
- DR principle ;
- lifecycle.

## 5. Quality gates — Deployment View

Refuser si :

- flux non nommés ;
- zones absentes ;
- state placement inconnu ;
- failure domains invisibles ;
- shared dependencies oubliées ;
- environment non indiqué ;
- aucun lien avec application.

## 6. Architecture Review Board

Questions :

1. Quelle décision cette vue soutient-elle ?
2. Quels composants sont critiques ?
3. Quels sont les SPOF ?
4. Quelle panne n’est pas couverte ?
5. Où se trouve l’état ?
6. Quels RTO/RPO ?
7. Comment la capacité est-elle validée après panne ?
8. Quelles technologies sont hors standard ?
9. Comment opère-t-on et observe-t-on ?
10. Quelle trajectoire de retrait ?

## 7. GreenOps / Green IT

L’infrastructure doit être dimensionnée selon le besoin, pas selon la capacité maximale imaginaire.

Axes :

- rightsizing ;
- suppression des environnements inutilisés ;
- mutualisation maîtrisée ;
- autoscaling pertinent ;
- stockage/retention adaptés ;
- réduction des copies inutiles ;
- extinction/decommission réelle ;
- choix de régions/sites selon contraintes et impact ;
- mesure avant optimisation.

## 8. Utilization vs resilience

Optimiser à 100 % d’utilisation détruit la marge nécessaire à :

- panne d’un node ;
- maintenance ;
- burst ;
- croissance ;
- rebalancing.

GreenOps doit donc intégrer le besoin de résilience.

## 9. Capacity efficiency

Métriques :

```text
Requested vs used CPU
Requested vs used memory
Storage allocated vs used
Backup growth
Network utilization
Idle environments
Orphan resources
```

## 10. Carbon-aware architecture

Approche pédagogique :

```text
Workload criticality
× energy/carbon intensity
× execution flexibility
× residency/latency constraints
```

Les workloads critiques temps réel ne se pilotent pas comme des traitements batch flexibles.

## 11. Cost awareness

Dimensions :

- compute ;
- storage ;
- data transfer ;
- licenses ;
- managed services ;
- support ;
- backup ;
- DR duplicate capacity.

FinOps et architecture doivent partager les mêmes objets canoniques de plateforme et de consommation.

## 12. Anti-pattern — Infrastructure wallpaper

Diagramme très détaillé mais sans :

- owner ;
- purpose ;
- flows ;
- NFR ;
- risk ;
- lifecycle.

Correction : réduire le détail et revenir aux décisions.

## 13. Anti-pattern — CMDB copy

Importer des milliers d’instances sans filtre rend le repository illisible.

Correction : définir des règles d’agrégation et de traçabilité vers la CMDB.

## 14. Anti-pattern — Vendor architecture

Dessiner uniquement les icônes d’un fournisseur cloud ne décrit pas :

- pourquoi les services sont utilisés ;
- qui les possède ;
- quelles applications en dépendent ;
- quels NFR sont couverts.

## 15. Anti-pattern — HA by replica count

`replicas=3` ne prouve pas la HA si tous les replicas partagent un même node group, site ou stockage.

## 16. Anti-pattern — DR on paper

Un second site non testé n’est pas un PRA prouvé.

## 17. Anti-pattern — over-engineering

Ajouter multi-region, service mesh, plusieurs caches, plusieurs queues et complexity sans NFR correspondant augmente le risque opérationnel.

## 18. Mission playbook — Semaine 1

### Discover

Collecter :

- application landscape ;
- platform catalog ;
- network zones ;
- sites/cloud accounts ;
- technology inventory ;
- RTO/RPO ;
- incidents majeurs ;
- lifecycle sources ;
- CMDB/cloud exports.

### Livrable

Current Technology Landscape + data quality report.

## 19. Semaine 2

### Connect

Construire :

- Application × Platform ;
- Platform × Technology ;
- Platform × Site ;
- network dependency map ;
- storage/data service map ;
- critical path.

## 20. Semaine 3

### Analyze

- SPOF ;
- obsolescence ;
- DR gaps ;
- capacity risks ;
- security boundaries ;
- operational gaps ;
- GreenOps waste.

## 21. Semaine 4

### Target & Roadmap

- target platform model ;
- transition states ;
- standards ;
- remediation priorities ;
- decommission list ;
- Architecture Board pack.

## 22. Interview case — OpenShift migration

Question : `Une application WAS doit migrer sur OpenShift. Que regardez-vous ?`

Réponse structurée :

```text
Application state
Session/statefulness
CPU/RAM profile
Storage
Network flows
Identity
External dependencies
Database
HA/DR
Observability
Deployment automation
Licensing
Transition coexistence
```

## 23. Interview case — Multi-site

Question : `Deux sites suffisent-ils pour dire que le service est résilient ?`

Non. Il faut analyser routing, state replication, quorum, shared identity/DNS, capacity, recovery process et tests.

## 24. Interview case — EOL technology

Méthode :

```text
Technology EOL
→ platforms
→ applications
→ business criticality
→ options
→ transition
→ exception/remediation plan
```

## 25. Maturity model

### Level 1 — Inventory
Liste de technologies.

### Level 2 — Standards
Owners + lifecycle + status.

### Level 3 — Connected Architecture
Applications/platforms/sites reliés.

### Level 4 — Resilience & Operations
RTO/RPO, failure domains, observability, capacity.

### Level 5 — Continuous Optimization
Lifecycle automation, impact analysis, GreenOps/FinOps, tested resilience.

## 26. Definition of Done

La partie Technology & Infrastructure est mature lorsque les équipes peuvent utiliser le repository pour :

- préparer une migration ;
- mesurer un blast radius ;
- détecter un risque d’obsolescence ;
- comprendre le chemin de panne ;
- concevoir un PRA ;
- prioriser une modernisation ;
- identifier une capacité gaspillée ;
- défendre une décision en Architecture Board.
