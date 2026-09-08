# 08 — Non-Functional Architecture : disponibilité, sécurité, performance et observabilité

## 1. Les NFR structurent le design

Une architecture applicative ne peut pas être définie uniquement par les fonctions.

Deux applications offrant la même fonction peuvent nécessiter des architectures totalement différentes selon :

- disponibilité ;
- performance ;
- sécurité ;
- volume ;
- résilience ;
- auditabilité ;
- recoverability ;
- data sensitivity.

## 2. NFR catalogue

Pour chaque application critique, documenter les NFR réellement structurants.

Catégories :

```text
Availability
Reliability
Performance
Scalability
Security
Privacy
Recoverability
Observability
Auditability
Maintainability
Interoperability
Data integrity
```

## 3. Availability

Exemple pédagogique :

```text
Payment Orchestrator
Target availability: 99.99%
```

Ce chiffre n’a de sens qu’avec :

- période de mesure ;
- exclusions ;
- service boundary ;
- dependencies ;
- maintenance policy.

## 4. End-to-end availability

Si le service dépend de cinq applications synchrones, chaque application peut respecter son SLA individuel tout en laissant le service global sous sa cible.

L’architecture doit donc analyser la **chaîne**.

## 5. Reliability

Mesures possibles :

- success rate ;
- error rate ;
- duplicate rate ;
- data inconsistency rate ;
- retry rate ;
- failed message rate.

## 6. Resilience patterns

Patterns possibles :

- timeout ;
- retry with backoff ;
- circuit breaker ;
- bulkhead ;
- queue ;
- failover ;
- graceful degradation ;
- idempotency ;
- compensation ;
- reconciliation.

Le choix doit correspondre à la sémantique métier.

## 7. Fail open vs fail closed

Exemple Fraud :

```text
Fraud service unavailable
```

Décision possible : `fail closed` pour ne pas exécuter un paiement non contrôlé.

Cette politique doit être validée par le métier/risk et non inventée par l’équipe technique.

## 8. RTO

Recovery Time Objective : durée cible pour rétablir le service après interruption.

## 9. RPO

Recovery Point Objective : perte de données maximale acceptable exprimée en temps.

Pour une application financière, RPO/RTO doivent être reliés à :

- state model ;
- replication ;
- backup ;
- reconciliation ;
- business continuity.

## 10. Active/active ne résout pas tout

Active/active peut améliorer disponibilité mais introduire :

- data consistency complexity ;
- duplicate processing ;
- routing ;
- conflict resolution ;
- operational complexity.

Le pattern doit être justifié.

## 11. Performance budget

Exemple pédagogique pour un paiement :

```text
E2E P95 target < 2 s
```

Répartir un budget :

- ingress/API ;
- orchestration ;
- fraud ;
- account/funds ;
- clearing ;
- persistence ;
- network.

Mesurer le réel plutôt que supposer.

## 12. Throughput

Documenter :

```text
Average TPS
Peak TPS
Burst behavior
Daily volume
Seasonality
```

Une moyenne seule masque les pics.

## 13. Scalability

Questions :

- horizontal ou vertical ?
- stateless ?
- partitionnement ?
- autoscaling signal ?
- downstream capacity ?
- database bottleneck ?
- license constraints ?

Scaler un front-end n’aide pas si le mainframe downstream reste le goulot.

## 14. Security architecture

Pour une application critique :

- authentication ;
- authorization ;
- service identity ;
- secrets ;
- certificates ;
- encryption ;
- audit ;
- vulnerability management ;
- network exposure ;
- privileged access.

## 15. Trust boundaries

Exemple :

```text
Internet
→ Digital Channel
→ API Management
→ Internal Application Zone
→ Core Banking
```

Les changements de zone nécessitent des contrôles adaptés.

## 16. Data sensitivity

Relier l’application aux catégories d’information :

- personal data ;
- payment data ;
- authentication data ;
- fraud indicators ;
- operational logs.

Les détails de Data Architecture seront approfondis en Partie IX.

## 17. Auditability

Pour un paiement, pouvoir reconstruire :

```text
request
identity/context
validation
fraud decision
funds decision
clearing request/result
status transitions
notifications
manual intervention
```

avec timestamps et correlation identifiers.

## 18. Observability

Trois familles classiques :

- metrics ;
- logs ;
- traces.

Ajouter :

- business events ;
- synthetic probes ;
- dependency health ;
- SLO monitoring.

## 19. Correlation ID

Un identifiant end-to-end doit traverser :

```text
Channel
API
Orchestrator
Fraud
Core
Clearing
Events
Notification
```

pour permettre debugging et audit.

## 20. Technical vs business monitoring

Technique :

```text
CPU
memory
pod restart
HTTP 5xx
Kafka lag
```

Métier :

```text
payment success
fraud reject
clearing timeout
manual repair
notification failure
```

Les deux sont nécessaires.

## 21. SLI, SLO, SLA

### SLI
Mesure observée.

### SLO
Objectif interne/service.

### SLA
Engagement formalisé.

Ne pas les utiliser comme synonymes.

## 22. Capacity and dependency

Un service peut respecter ses ressources mais dépasser la capacité d’un provider.

Exemple :

```text
Payment Orchestrator scales x10
Core Account Service capacity x2
```

Le système end-to-end est limité par le provider.

## 23. Degraded mode

Définir explicitement les fonctions qui peuvent continuer.

Exemple :

```text
Analytics unavailable
→ payment continues

Fraud unavailable
→ payment blocked according to approved policy
```

## 24. Operational readiness

Avant go-live :

- dashboards ;
- alerts ;
- runbooks ;
- on-call ;
- backup/recovery tested ;
- DR tested ;
- known failure modes ;
- capacity tested ;
- security checks ;
- dependency owners.

## 25. NFR Matrix MayaBank

| Application | Availability | Performance | Recovery | Security focus |
|---|---|---|---|---|
| Payment Orchestrator | very high | low latency | multi-site | financial integrity |
| Fraud Decision Service | very high | strict decision latency | resilient | sensitive risk data |
| Core Account Service | critical | strict | strong RPO/RTO | account integrity |
| Clearing Gateway | critical | external SLA-bound | failover | payment-network security |
| Notification Service | high | async throughput | replay | personal data |

Valeurs qualitatives pédagogiques.

## 26. NFR traceability

Relier :

```text
Business Service requirement
→ Application NFR
→ Architecture mechanism
→ Operational evidence
```

Exemple :

```text
Instant Payment 24/7
→ Payment Orchestrator high availability
→ multi-zone deployment
→ availability SLI/SLO dashboard
```

## 27. Anti-patterns

- écrire `high availability` sans objectif ;
- confondre replicas et DR ;
- mettre retry partout ;
- ignorer idempotency ;
- autoscaler sans regarder downstream ;
- loguer des données sensibles sans contrôle ;
- monitoring uniquement infrastructure ;
- RTO/RPO sans test ;
- aucune correlation end-to-end.

## 28. Livrables

- NFR Catalogue ;
- Application NFR Matrix ;
- Critical Service Availability Chain ;
- Performance Budget ;
- Resilience Pattern Map ;
- Trust Boundary View ;
- Observability Architecture ;
- Operational Readiness Checklist.
