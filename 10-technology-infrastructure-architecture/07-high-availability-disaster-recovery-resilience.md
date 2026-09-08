# 07 — High Availability, Disaster Recovery & Resilience

## 1. Availability vs resilience

```text
Availability
probabilité que le service soit accessible

Resilience
capacité à absorber, isoler et récupérer d’une perturbation
```

Une architecture très disponible peut rester fragile face à certains scénarios communs.

## 2. HA vs DR

```text
HA
continuité face aux pannes locales

DR
reprise après perte majeure d’un site, d’une région ou d’un ensemble de services
```

## 3. RTO

Recovery Time Objective : délai maximal acceptable pour restaurer un service.

## 4. RPO

Recovery Point Objective : perte de données maximale acceptable.

RTO/RPO doivent venir des besoins métier et de risque.

## 5. Failure scenario catalog

Pour MayaBank :

1. pod/process failure ;
2. node failure ;
3. cluster failure ;
4. storage failure ;
5. network partition ;
6. database failure ;
7. Kafka broker/quorum failure ;
8. site failure ;
9. identity service failure ;
10. partner clearing outage ;
11. certificate expiration ;
12. operator error/corruption.

## 6. Redundancy levels

```text
Process
Node
Cluster
Zone
Site
Region
Provider
```

Le niveau doit correspondre au scénario couvert.

## 7. Active/active

Avantages :

- capacité disponible ;
- bascule potentiellement rapide ;
- meilleure tolérance site.

Complexités :

- état partagé ;
- consistency ;
- split brain ;
- routing ;
- coût ;
- opérations.

## 8. Active/passive

Avantages : architecture souvent plus simple.

Risques :

- environnement passif non testé ;
- configuration drift ;
- capacité insuffisante ;
- bascule manuelle longue.

## 9. Application-level resilience

Patterns :

- timeout ;
- retry borné ;
- circuit breaker ;
- bulkhead ;
- idempotency ;
- queue buffering ;
- graceful degradation ;
- compensation.

## 10. Infrastructure-level resilience

- redundant network paths ;
- HA load balancing ;
- multi-node compute ;
- resilient storage ;
- database replication ;
- multi-site backup ;
- independent management path.

## 11. Dependency-aware DR

Un runbook doit respecter l’ordre :

```text
Network/DNS
→ Identity/PKI
→ Storage/Data services
→ Platform control plane
→ Messaging/API platforms
→ Applications
→ External connectivity
```

L’ordre réel dépend de l’architecture.

## 12. DR orchestration

Documenter :

- trigger ;
- decision authority ;
- automated/manual steps ;
- data cutover ;
- routing change ;
- validation ;
- rollback/failback.

## 13. Failover vs failback

Le retour au site nominal est une opération distincte qui comporte ses propres risques.

## 14. Testing strategy

```text
Component failover tests
Platform recovery tests
Application DR tests
Data restore tests
Site loss exercises
Game days / chaos experiments where appropriate
```

## 15. Recovery evidence

Pour chaque service critique conserver :

- date du test ;
- scénario ;
- résultat ;
- RTO réalisé ;
- RPO observé ;
- écarts ;
- actions.

## 16. Resilience matrix

| Layer | Failure | Protection | Residual Risk |
|---|---|---|---|
| Compute | node | replicas/anti-affinity | capacity |
| Network | link | redundant paths | shared gateway |
| Data | DB node | replication | corruption |
| Site | total loss | DR site | recovery time |
| Partner | clearing outage | timeout/retry/status inquiry | external dependency |

## 17. MayaBank payment chain

```text
Customer
→ Edge
→ API Management
→ Payment Orchestrator
→ Core/Fraud/Clearing
→ Status store
→ Event Streaming
```

Le service end-to-end hérite des dépendances de toute la chaîne.

## 18. Resilience anti-patterns

- `multi-AZ` écrit sans topologie prouvée ;
- réplication sans quorum design ;
- backup sans restore test ;
- RTO inférieur au temps réel de redémarrage ;
- DR sans IAM/DNS/certificates ;
- active/passive jamais démarré ;
- failover testé mais pas failback ;
- retries illimités aggravant une panne.

## 19. Questions d’entretien

**Pourquoi un PRA doit-il être dependency-aware ?**  
Parce qu’une application ne peut pas redémarrer correctement si ses services de base, données, réseau ou identité ne sont pas disponibles.

**RPO=0 est-il gratuit ?**  
Non. Il impose généralement des mécanismes de synchronisation/consistance et des compromis de latency, coût et complexité.
