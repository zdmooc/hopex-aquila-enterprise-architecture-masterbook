# 05 — Deployment Architecture & Environments

## 1. Pourquoi le déploiement compte

Deux applications identiques sur le plan logique peuvent avoir des architectures opérationnelles très différentes.

Questions :

- sur quelle plateforme l'application s'exécute-t-elle ?
- quels environnements existent ?
- quelles dépendances sont partagées ?
- comment la haute disponibilité est-elle obtenue ?
- où se trouvent les SPOF ?
- existe-t-il une différence entre current et target deployment ?

## 2. Référence publique HOPEX

Des release notes HOPEX IT Architecture antérieures documentent un **Application System Deployment Environment** permettant de représenter le contexte d'intégration et les dépendances d'un déploiement, y compris des serveurs de données partagés.

Cette référence confirme le concept de déploiement dans la solution, mais le masterbook ne suppose pas que le nom exact du diagramme ou son écran soit inchangé dans Aquila 6.2.

## 3. Déploiement logique vs instance runtime

```text
Deployment Architecture
= description stable du mode d'hébergement

Runtime instance
= VM / pod / cluster concret observé
```

Exemple :

```text
Payment Orchestrator Deployment Architecture
→ OpenShift Container Platform
→ PostgreSQL service
→ Event Streaming service
→ Identity service
```

Puis le run peut préciser :

```text
cluster OCP-PROD-A
namespace payments-prod
```

## 4. Environnements

Minimum courant :

```text
DEV
TEST / INT
PREPROD
PROD
DR / secondary site
```

Ne pas créer automatiquement une application distincte pour chaque environnement.

## 5. Deployment view

Une vue de déploiement doit montrer :

- application ou application system ;
- platform/services ;
- shared services ;
- network dependencies structurantes ;
- data stores ;
- external endpoints ;
- HA/DR boundaries si utiles.

## 6. Shared services

Exemples :

```text
Identity Platform
API Gateway
Event Streaming Platform
Observability Platform
Secrets Management
DNS / Load Balancing
```

Un shared service crée une dépendance transversale. Il doit donc être visible dans l'analyse d'impact.

## 7. Haute disponibilité

Ne pas modéliser seulement :

```text
HA = Yes
```

Il faut comprendre la mécanique :

- plusieurs replicas ;
- multi-zone ;
- load balancing ;
- database replication ;
- failover ;
- stateless/stateful ;
- quorum ;
- dépendances externes.

## 8. Disaster Recovery

HA ≠ DR.

```text
HA
→ continuité face à une panne locale

DR
→ reprise après perte d'un site / domaine de défaillance majeur
```

Propriétés possibles :

- RTO ;
- RPO ;
- recovery site ;
- recovery pattern ;
- test date.

## 9. Multi-site MayaBank

```text
Site A
  ├─ OpenShift cluster A
  ├─ Event platform A
  └─ DB primary

Site B
  ├─ OpenShift cluster B
  ├─ Event platform B
  └─ DB standby
```

Question :

- active/active ?
- active/passive ?
- quels composants savent réellement basculer ?
- quelles dépendances restent single-site ?

## 10. Current vs target deployment

Current :

```text
WebSphere cluster
Oracle / shared filesystem
physical LB
manual DR
```

Target :

```text
OpenShift
containerized workloads
S3/object storage where relevant
standard observability
automated deployment
managed failover pattern
```

## 11. Couche réseau

Le repository EAM ne doit pas devenir une base NetBox complète.

Conserver seulement :

- zones / trust boundaries ;
- paths critiques ;
- protocoles structurants ;
- dépendances réseau nécessaires à l'analyse.

## 12. Couche stockage

Exemples de décisions :

```text
block storage
file storage
object storage
shared database storage
backup service
```

La technologie doit être liée aux applications et aux exigences de persistance.

## 13. Anti-patterns

- `Prod` modélisé comme application ;
- 1 objet par pod ;
- DR décrit par une note libre ;
- shared platform absente du graphe ;
- vue réseau ultra-détaillée illisible ;
- pas de distinction logique/runtime ;
- current et target superposés sans statut.

## 14. Checklist revue de déploiement

1. application logique identifiée ?
2. plateforme identifiée ?
3. shared services identifiés ?
4. data stores identifiés ?
5. trust boundaries visibles ?
6. SPOF recherchés ?
7. HA explicite ?
8. DR explicite ?
9. current/target distingués ?
10. owner des plateformes identifié ?

## 15. Entretien

**Pourquoi modéliser le déploiement dans un EAM ?**  
Pour relier les choix d'hébergement et de résilience aux applications et à leur impact métier.

**Faut-il importer tous les pods ?**  
Non, sauf besoin spécifique. Le niveau EAM privilégie les dépendances stables nécessaires aux décisions.
