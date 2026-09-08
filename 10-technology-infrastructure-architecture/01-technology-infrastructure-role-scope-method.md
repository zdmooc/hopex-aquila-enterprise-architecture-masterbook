# 01 — Technology & Infrastructure Architecture : rôle, périmètre et méthode

## 1. Objectif

La Technology & Infrastructure Architecture décrit **les plateformes, runtimes, services techniques et infrastructures qui permettent aux applications de fonctionner avec les niveaux de service, de sécurité et de résilience attendus**.

Elle répond notamment à :

- quelles technologies supportent quelles applications ?
- où s’exécutent les workloads ?
- quels failure domains structurent la disponibilité ?
- quelles dépendances réseau, stockage, identité et observabilité existent ?
- quelles technologies sont standard, tolérées, obsolètes ou interdites ?
- quels impacts produit un changement de plateforme ?
- quels composants participent au PRA/PCA ?
- quelles infrastructures peuvent être rationalisées ou modernisées ?

## 2. Frontières du domaine

```text
Partie VIII — Application Architecture
responsabilités applicatives, services, interfaces, dépendances logiques

Partie IX — Information & Data Architecture
information, data domains, lineage, qualité, modèles

Partie X — Technology & Infrastructure Architecture
platforms, runtime, compute, network, storage, cloud, OpenShift, HA/DR

Partie XIII/XIV
portefeuille, coûts, rationalisation et roadmaps
```

## 3. Technology ≠ Application

Exemple MayaBank :

```text
Application
Payment Orchestrator

runs on / uses
OpenShift
Java
Kafka
PostgreSQL
API Management
Observability stack
```

Une application doit pouvoir survivre à un changement de technologie sans perdre son identité métier.

## 4. Technology ≠ Infrastructure instance

```text
Technology Product
Red Hat OpenShift

Technology Service / Platform
MayaBank OpenShift Platform

Deployment / environment
OCP-PROD-EU

Runtime resources
workers / nodes / namespaces / pods
```

Le repository d’EA ne doit pas automatiquement répliquer chaque ressource runtime.

## 5. Les couches d’analyse

### L0 — Technology Landscape
Cloud, container, data, integration, security, observability.

### L1 — Platform Architecture
OpenShift, Kafka, DB, API Management, IAM, monitoring.

### L2 — Deployment Architecture
sites, régions, clusters, zones, environnements, principaux stores.

### L3 — Infrastructure Detail
compute, network, storage, load balancing, backup, replication lorsque nécessaire à une décision.

## 6. Méthode en douze étapes

1. Définir le scope applicatif et métier.
2. Identifier les plateformes critiques.
3. Identifier les technologies et produits.
4. Relier applications ↔ plateformes ↔ technologies.
5. Cartographier compute, network, storage et data services structurants.
6. Identifier les failure domains.
7. Documenter HA, RTO/RPO et dépendances DR.
8. Documenter sécurité et trust boundaries.
9. Relier observabilité et exploitation.
10. Analyser lifecycle, standards et obsolescence.
11. Construire current / transition / target.
12. Vérifier impacts, ownership et qualité du modèle.

## 7. Modèle de responsabilité

Pour chaque plateforme critique :

```text
Purpose
Owner
Consumers
Environments
Criticality
Availability target
RTO / RPO
Key dependencies
Technology products
Lifecycle state
Security zone
Observability
DR mechanism
Target direction
```

## 8. HOPEX comme repository d’architecture

Les pages publiques Bizzdesign Hopex mettent en avant une source de vérité connectée couvrant business, IT, data et risk, ainsi que la gestion du portefeuille technologique. Le masterbook utilise ces capacités pour relier technologies, applications, dépendances et transformations.

HOPEX n’est pas traité comme :

- console Kubernetes ;
- CMDB exhaustive ;
- hypervisor manager ;
- cloud control plane ;
- outil NMS ;
- SIEM ;
- outil de sauvegarde.

## 9. Baseline MayaBank

```text
Channels
→ API Management
→ Payment Orchestrator
→ Fraud / Core / Clearing
→ Event Streaming
→ Notification / Reconciliation

Technology backbone
OpenShift
Kafka
PostgreSQL / Oracle
IAM
Load Balancers
Network zones
Observability
Backup / DR
```

## 10. Principes de qualité

- modéliser une technologie parce qu’elle influence une décision ;
- distinguer produit, version, plateforme et instance ;
- éviter les objets sans owner ;
- relier technologie et applications consommatrices ;
- documenter les failure domains ;
- dater les informations lifecycle ;
- ne pas déduire la résilience d’un simple diagramme ;
- ne pas confondre réplication et sauvegarde.

## 11. Anti-patterns

- technology = application ;
- cluster = application ;
- un objet HOPEX pour chaque pod ;
- diagramme infrastructure sans flux ni zones ;
- PRA déclaré sans RTO/RPO ;
- multi-site sans mécanisme de bascule ;
- produit obsolète sans applications impactées ;
- standards sans owner ni date de revue.

## 12. Questions d’entretien

**Pourquoi séparer plateforme et produit technologique ?**  
Une plateforme est un service exploité et consommé ; un produit technologique est un composant/version utilisé pour la réaliser.

**Pourquoi modéliser les failure domains ?**  
Parce qu’une architecture peut sembler redondante tout en partageant une dépendance unique qui concentre le risque.

**HOPEX remplace-t-il une CMDB ?**  
Non. Le repository d’EA sélectionne les objets et relations utiles à l’analyse d’architecture et de transformation.
