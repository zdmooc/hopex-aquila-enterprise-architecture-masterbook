# 07 — Deployment Architecture : environnements, plateformes et topologies

## 1. Pourquoi modéliser le déploiement

L’architecture applicative décrit la responsabilité logique.

Le deployment model répond à :

```text
Où l’application s’exécute-t-elle ?
Sur quelle plateforme ?
Dans quels environnements ?
Avec quelles dépendances d’infrastructure ?
Quels domaines de défaillance partage-t-elle ?
Comment la topologie change-t-elle entre current et target ?
```

## 2. Séparer logique et physique

```text
Logical
Payment Orchestrator

Deployment
OpenShift Production
Namespace payments-prod
Workloads / services
```

Le namespace n’est pas l’application.

Le pod n’est pas l’application.

Le cluster n’est pas l’application.

## 3. Environnements

Exemple MayaBank :

```text
DEV
INT
TEST
PREPROD
PROD
DR
```

Les noms réels varient selon l’entreprise.

Documenter :

- purpose ;
- hosting ;
- data classification ;
- connectivity ;
- availability expectations ;
- release path.

## 4. Deployment topology

Exemple cible :

```text
Application
Payment Orchestrator
        ↓ deployed on
OpenShift Platform
        ↓
Cluster PROD-A / PROD-B
        ↓
Namespace payments
        ↓
Workloads
```

Le niveau cluster/namespace peut être omis dans une vue d’entreprise et utilisé dans une vue solution.

## 5. OpenShift

Pour une application sur OpenShift, les éléments structurants peuvent inclure :

- cluster ;
- region/site ;
- namespace/project ;
- deployment/workload ;
- service ;
- ingress/route ;
- config/secrets ;
- persistent storage ;
- operators ;
- service mesh ;
- observability ;
- quotas/limits.

HOPEX n’est pas Kubernetes : ne recopier que ce qui est nécessaire à l’analyse d’architecture.

## 6. Cloud

Exemple Azure :

```text
Application
→ Azure landing zone
→ subscription
→ region
→ managed platform
```

Exemple AWS :

```text
Application
→ account
→ region
→ EKS/RDS/MSK/etc.
```

Le cloud resource inventory détaillé doit rester dans les outils cloud/CMDB lorsque c’est plus approprié.

## 7. On-premises

Modéliser selon besoin :

```text
Application
→ middleware/platform
→ virtual/physical infrastructure
→ site/datacenter
```

Éviter de dessiner chaque VM si l’analyse n’en a pas besoin.

## 8. SaaS

Pour SaaS :

```text
Application
Fraud SaaS

Deployment model
Externally hosted / SaaS provider

Known regions/data residency
as contractually relevant
```

Ne pas inventer l’infrastructure interne du fournisseur.

## 9. Environment drift

Une application peut présenter des écarts entre environnements :

```text
PREPROD
Java 21

PROD
Java 17
```

ou :

```text
PREPROD
3 replicas

PROD
8 replicas
```

Certains écarts sont légitimes, d’autres créent un risque de release.

## 10. Deployment dependency

Exemple :

```text
Payment Orchestrator
→ OpenShift
→ Kafka/Event Streaming
→ PostgreSQL
→ Vault/Secrets
→ Observability
```

Une panne de plateforme peut toucher plusieurs applications simultanément.

## 11. Failure domains

Identifier :

- node ;
- rack ;
- datacenter ;
- availability zone ;
- region ;
- cluster ;
- shared middleware ;
- shared database.

La réplication n’a de valeur que si elle traverse les domaines de défaillance pertinents.

## 12. Multi-site

Exemple conceptuel :

```text
Site A
OpenShift PROD-A

Site B
OpenShift PROD-B
```

Questions :

- active/active ou active/passive ?
- routing ?
- data replication ?
- state consistency ?
- failover process ?
- RPO/RTO ?
- operational ownership ?

## 13. Stateless vs stateful

### Stateless

Peut souvent être répliqué plus facilement.

### Stateful

Nécessite de modéliser :

- data store ;
- replication ;
- backup ;
- failover ;
- recovery ;
- consistency.

Ne pas qualifier une application « cloud-native » uniquement parce qu’elle tourne dans un container.

## 14. External dependency

```text
Clearing Gateway
→ External Clearing Network
```

La disponibilité externe fait partie de la chaîne de service même si MayaBank ne la contrôle pas.

## 15. Network zones

Pour une vue sécurité :

```text
Internet / external
DMZ / ingress
Application zone
Data zone
Management zone
```

Le niveau exact doit suivre l’architecture sécurité client.

## 16. Deployment and security

Relier :

- application criticality ;
- data sensitivity ;
- network exposure ;
- secrets/certificates ;
- IAM ;
- logging ;
- runtime policy.

## 17. Deployment and performance

Documenter lorsque structurant :

- expected throughput ;
- latency-sensitive dependencies ;
- autoscaling ;
- resource limits ;
- storage IOPS ;
- region proximity.

## 18. Deployment and cost

Le coût peut être analysé via :

- platform consumption ;
- licenses ;
- environments ;
- capacity ;
- storage ;
- network.

Le modèle FinOps détaillé sera traité plus tard ; ici on conserve seulement les drivers d’architecture.

## 19. Current MayaBank

Scénario pédagogique :

```text
Payment Orchestrator
→ legacy VM platform
→ single primary site

Fraud
→ separate appliance

Notification
→ point-to-point gateway
```

## 20. Target MayaBank

```text
Payment Orchestrator
→ OpenShift multi-zone

Fraud Decision Service
→ OpenShift / external SaaS depending chosen scenario

Event Streaming
→ resilient Kafka platform

Notification Service
→ event-driven shared service
```

## 21. Deployment matrix

| Application | Platform | PROD | DR | State |
|---|---|---|---|---|
| Payment Orchestrator | OpenShift | Site A | Site B | state externalized |
| Fraud Decision Service | OpenShift | Site A | Site B | stateless service + external model/data |
| Core Account Service | Core platform | primary | secondary | stateful |
| Clearing Gateway | Integration platform | Site A | Site B | limited state |
| Notification Service | OpenShift | Site A | Site B | event-driven |

Données pédagogiques.

## 22. Migration dependency

Lors d’un déplacement VM → OpenShift, analyser :

- runtime compatibility ;
- state/session ;
- filesystem assumptions ;
- network ;
- certificates ;
- external dependencies ;
- schedulers ;
- batch ;
- observability ;
- backup ;
- support model.

## 23. HOPEX vs CMDB

HOPEX :

```text
architecture intent
logical application
critical dependencies
target design
impact analysis
```

CMDB :

```text
operational configuration items
instances
runtime relationships
changes/incidents
```

Les deux peuvent être intégrés mais ne doivent pas être confondus.

## 24. Anti-patterns

- créer une application par environnement ;
- mettre tous les pods dans l’EA repository ;
- croire que 3 replicas = DR ;
- modéliser un SaaS comme infrastructure interne connue ;
- ignorer les dépendances shared platform ;
- mélanger topology current et target sans légende ;
- ne pas relier stateful components au plan de recovery.

## 25. Livrables

- Application Deployment Architecture ;
- Application × Platform Matrix ;
- Environment Map ;
- Shared Failure Domain View ;
- Multi-site Deployment View ;
- Current vs Target Hosting Map ;
- VM → OpenShift Migration Dependency Checklist.
