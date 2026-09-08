# 11 — Current, Transition & Target Infrastructure Architecture

## 1. Pourquoi plusieurs états

Une target architecture seule ne montre pas comment l’entreprise peut y arriver sans interrompre les services existants.

Il faut représenter :

```text
Current
→ Transition State 1
→ Transition State 2
→ Target
```

## 2. Current state

Documenter :

- sites/régions ;
- plateformes ;
- runtimes ;
- network zones ;
- storage ;
- HA/DR ;
- observability ;
- security controls ;
- technologies obsolètes ;
- dépendances communes.

## 3. Target drivers

Exemples MayaBank :

- résilience ;
- réduction des composants obsolètes ;
- standardisation ;
- automation/IaC ;
- OpenShift ;
- meilleure observabilité ;
- séparation des failure domains ;
- simplification des flux réseau ;
- réduction de l’empreinte infrastructure.

## 4. Migration patterns

### Rehost
Déplacer sans changement majeur du runtime applicatif.

### Replatform
Changer plateforme avec adaptations limitées.

### Refactor
Modifier davantage application/runtime.

### Replace
Remplacer par un autre service/produit.

### Retire
Supprimer.

## 5. Infrastructure coexistence

Pendant transition :

```text
Legacy VM estate
+ OpenShift estate
+ shared databases
+ dual network paths
+ dual observability
```

La période de coexistence peut augmenter temporairement la complexité et le coût.

## 6. Dependency sequencing

Ordre possible :

```text
Landing zone / network
→ Identity / PKI
→ Observability
→ OpenShift platform
→ Storage / DB services
→ Event Streaming / API
→ Applications
→ Decommission legacy
```

## 7. Data gravity

Migrer compute sans analyser les données peut créer :

- latency ;
- coûts réseau ;
- dépendance cross-site ;
- difficulté de DR.

## 8. Strangler infrastructure

Pendant un strangler applicatif :

```text
Legacy platform
↔ API/Event integration
↔ New platform
```

La connectivité et l’observabilité doivent couvrir les deux mondes.

## 9. Dual-run risk

Risques :

- double coût ;
- données incohérentes ;
- routage ambigu ;
- certificats multiples ;
- support partagé ;
- troubleshooting complexe.

## 10. Cutover readiness

Checklist :

1. capacity validated ;
2. connectivity validated ;
3. identity/certificates ready ;
4. data migration tested ;
5. observability ready ;
6. rollback path ;
7. DR validated ;
8. owners/on-call ready ;
9. security approval ;
10. decommission criteria defined.

## 11. Decommission

Retirer une infrastructure signifie aussi :

- DNS cleanup ;
- firewall rules removal ;
- routes ;
- certificates ;
- storage ;
- backup schedules ;
- monitoring ;
- licenses ;
- CMDB/EA updates.

## 12. Current MayaBank

```text
Single-site-heavy VM estate
Legacy middleware
Point-to-point network flows
Mixed monitoring
Manual deployment
Shared file/storage dependencies
Partial DR
```

## 13. Transition 1

```text
Build OpenShift platform
Centralize observability
Establish API Management
Establish Kafka/Event Streaming
Connect legacy core
```

## 14. Transition 2

```text
Move payment services
Externalize state
Harden multi-site recovery
Reduce legacy messaging
Automate deployments
```

## 15. Target

```text
Standardized platform services
OpenShift for suitable workloads
Resilient data services
Governed network zones
Centralized identity/secrets
End-to-end observability
Tested DR
IaC/GitOps operations
```

## 16. Transition matrices

### Platform × State

| Platform | Current | Transition | Target |
|---|---|---|---|
| Runtime | VM | VM + OCP | OCP/managed |
| Messaging | legacy + Kafka | dual | Kafka/event platform |
| Observability | fragmented | centralized rollout | end-to-end |
| DR | partial | expanded | tested multi-site |

## 17. Architecture Decision Records

Chaque étape structurante doit expliquer :

- decision ;
- context ;
- options ;
- rationale ;
- consequences ;
- review date.

## 18. Anti-patterns

- target sans transition ;
- migration de compute sans données ;
- double-run sans date de fin ;
- decommission = éteindre VM uniquement ;
- nouveaux services dépendant encore de SPOF legacy ;
- rollback non testé.

## 19. Questions d’entretien

**Pourquoi la transition architecture est-elle un livrable d’architecture ?**  
Parce que les risques et dépendances réels apparaissent souvent pendant la coexistence entre ancien et nouveau.

**Pourquoi décommissionner est-il une activité d’architecture ?**  
Parce qu’il faut supprimer proprement les dépendances, données, flux, licences et contrôles afin de réellement réduire la complexité.
