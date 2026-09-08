# 06 — Storage, backup, réplication et data services

## 1. Storage architecture

Le stockage doit être analysé par besoin :

- block ;
- file ;
- object ;
- ephemeral ;
- database-managed ;
- archive.

## 2. Performance dimensions

```text
Capacity
IOPS
Throughput
Latency
Durability
Availability
Retention
Cost
```

Le bon choix dépend du workload.

## 3. Persistent volumes

Sur une plateforme container :

```text
Application
→ PVC
→ Storage Class
→ Storage backend
→ failure domain
```

Le PVC n’est pas une garantie de sauvegarde.

## 4. Block storage

Adapté à certains workloads stateful nécessitant accès bas niveau, faible latency ou semantics spécifiques.

Questions :

- zonal ou replicated ?
- snapshots ?
- encryption ?
- performance tier ?
- failover behavior ?

## 5. File storage

Utile pour partage de fichiers ou applications legacy.

Risques :

- coupling ;
- shared namespace ;
- locking ;
- scaling ;
- SPOF backend.

## 6. Object storage

Patterns :

- documents ;
- archives ;
- data lake objects ;
- backups ;
- immutable artifacts.

S3-compatible ≠ automatiquement AWS S3.

## 7. Backup ≠ replication

```text
Replication
copies current state for availability

Backup
retains recoverable historical state
```

Une corruption répliquée n’est pas protégée par la réplication seule.

## 8. Snapshot ≠ backup

Un snapshot peut contribuer à la stratégie de recovery mais doit être évalué selon :

- indépendance ;
- rétention ;
- immutability ;
- restore procedure ;
- site failure.

## 9. RPO

Recovery Point Objective : perte de données maximale acceptable exprimée dans le temps.

Exemples conceptuels :

```text
Payment execution state: near-zero / strict objective
Analytics: potentially larger objective
```

Les valeurs réelles sont des décisions métier.

## 10. Restore testing

Un backup non testé n’est pas une garantie de recovery.

Mesurer :

- restore time ;
- integrity ;
- dependency restoration order ;
- access controls ;
- evidence.

## 11. Data services

Plateformes possibles :

- relational database service ;
- NoSQL ;
- cache ;
- streaming ;
- object storage ;
- search ;
- warehouse/lakehouse.

La Partie IX traite la donnée ; la Partie X traite ici les services techniques qui la stockent ou la transportent.

## 12. Database HA

Architecture à documenter :

```text
primary
replica(s)
quorum/witness where applicable
failover mechanism
backup
monitoring
network dependencies
```

## 13. Replication patterns

- synchronous ;
- asynchronous ;
- intra-site ;
- cross-zone ;
- cross-region/site.

Le compromis principal : latency, consistency, availability, RPO.

## 14. Storage failure domains

```text
Disk/device
→ storage node/array
→ rack
→ zone/site
→ region
```

Une application multi-zone avec stockage mono-zone n’est pas réellement multi-zone pour son état.

## 15. Encryption

À examiner :

- at rest ;
- in transit ;
- key ownership ;
- rotation ;
- backup encryption ;
- restore permissions.

## 16. Capacity planning

```text
Current volume
Growth rate
Retention
Replication factor
Backup copies
Headroom
Performance tier
```

## 17. MayaBank reference

```text
Payment state → resilient relational store
Event stream → replicated Kafka storage
Documents/archives → object storage
Reconciliation extracts → controlled file/object zone
Backups → independent recovery service
```

## 18. Anti-patterns

- réplication appelée backup ;
- snapshot local = PRA ;
- stockage sans owner ;
- capacité sans croissance ;
- RPO zéro déclaré sans mécanisme synchrone ou contrôle équivalent ;
- restore jamais testé ;
- storage backend unique caché derrière plusieurs PVC.

## 19. Questions d’entretien

**Pourquoi distinguer backup et réplication ?**  
Parce qu’ils couvrent des modes de panne différents : disponibilité du présent vs restauration d’un état antérieur.

**Quel risque avec un stockage mono-zone sous une application multi-zone ?**  
L’état reste exposé à la panne du storage failure domain et peut annuler le bénéfice de la redondance applicative.
