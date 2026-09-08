# 04 — Compute, containers, OpenShift et cloud

## 1. Compute architecture

Le compute décrit où et comment les workloads disposent de CPU, mémoire et runtime.

Modèles :

- bare metal ;
- VM ;
- container ;
- managed container platform ;
- serverless ;
- SaaS.

## 2. VM vs container

```text
VM
OS + middleware + application

Container
image + process isolé
running on shared container platform
```

Le choix influence densité, patching, isolation, déploiement et exploitation.

## 3. OpenShift architecture conceptuelle

```text
Cluster
├─ Control Plane
├─ Worker Nodes
├─ Ingress
├─ Networking
├─ Storage integration
├─ Registry
├─ Operators
└─ Observability / security integrations
```

Le masterbook reste conceptuel : la topologie précise dépend de la version et du design client.

## 4. Namespace

Un namespace est une unité logique de segmentation et gouvernance du runtime.

Il peut porter :

- RBAC ;
- quotas ;
- network policies ;
- limits ;
- secrets ;
- workloads.

Namespace ≠ application par principe.

## 5. Worker pools

Des workers peuvent être segmentés par :

- performance ;
- zone ;
- compliance ;
- workload type ;
- GPU ;
- storage affinity.

Le modèle doit expliquer pourquoi la séparation existe.

## 6. Requests / limits / capacity

Architecture de capacité :

```text
Business load
→ application workload profile
→ pod requests/limits
→ namespace quotas
→ cluster capacity
→ infrastructure capacity
```

Éviter le sizing à partir du nombre de pods seul.

## 7. Horizontal scaling

Questions :

- le workload est-il stateless ?
- métrique de scaling ?
- downstream scalable ?
- sessions externalisées ?
- DB capable d’absorber le débit ?

## 8. Stateful workloads

Un workload stateful exige :

- persistence ;
- ordering éventuel ;
- backup ;
- recovery ;
- quorum selon technologie ;
- placement ;
- storage performance.

## 9. Failure domains

```text
Container
→ pod
→ node
→ rack/host
→ availability zone/site
→ region
```

La redondance doit traverser le bon niveau de failure domain.

## 10. Cloud architecture

Distinguer :

```text
Cloud provider
Cloud account/subscription/project
Region
Availability zone
VPC/VNet
Managed service
Workload deployment
```

## 11. Hybrid architecture

MayaBank peut combiner :

```text
On-prem core systems
+ private/container platform
+ public cloud services
+ SaaS
```

Le point critique devient souvent la connectivité et l’identité inter-domaines.

## 12. Shared responsibility

Dans le cloud, clarifier :

- provider responsibility ;
- platform team responsibility ;
- application team responsibility ;
- data owner responsibility.

## 13. Landing zone principles

Une landing zone fournit généralement :

- identity ;
- network ;
- logging ;
- security policies ;
- account structure ;
- tagging ;
- guardrails ;
- cost controls.

## 14. Kubernetes/OpenShift anti-patterns

- un cluster par microservice ;
- un namespace par pod ;
- requests = limits arbitrairement ;
- replicas sans anti-affinity ;
- stateful workload sans backup ;
- autoscaling ignorant la DB ;
- cluster DR sans dépendances externes.

## 15. MayaBank target

```text
Payment workloads
→ OpenShift PROD
→ multi-node
→ isolated namespaces
→ centralized ingress
→ persistent services externalized/managed where appropriate
→ GitOps
→ metrics/logs/traces
```

## 16. Matrix Application × Runtime

| Application | Runtime | State |
|---|---|---|
| Payment Orchestrator | OpenShift | mostly stateless + external state |
| Fraud Service | OpenShift | stateless/service state external |
| Notification | OpenShift | asynchronous |
| Core Account | managed/legacy platform | stateful |
| Event Streaming | Kafka platform | stateful distributed |

## 17. Questions d’entretien

**Pourquoi 3 replicas ne garantissent-ils pas la HA ?**  
S’ils partagent le même failure domain, une panne commune peut les arrêter simultanément.

**Pourquoi un cluster n’est-il pas une application ?**  
Le cluster est une plateforme d’exécution mutualisable ; l’application est un actif logique métier/IT distinct.
