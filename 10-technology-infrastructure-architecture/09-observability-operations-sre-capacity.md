# 09 — Observability, Operations, SRE & Capacity

## 1. Observability architecture

Une plateforme observable permet d’expliquer l’état d’un système à partir de signaux exploitables.

Trois familles principales :

```text
Metrics
Logs
Traces
```

auxquelles peuvent s’ajouter events, profiles et synthetic checks.

## 2. Monitoring vs observability

```text
Monitoring
surveille des conditions connues

Observability
permet d’investiguer le comportement à partir des signaux
```

## 3. End-to-end correlation

Pour un paiement :

```text
Request ID
Payment ID
Trace ID
Correlation ID
```

Les identifiants doivent permettre de relier les étapes sans exposer de données sensibles inutilement.

## 4. Metrics architecture

Catégories :

- infrastructure ;
- platform ;
- application ;
- business/service ;
- security.

Éviter des millions de métriques sans modèle d’usage.

## 5. Golden signals

Pour un service :

```text
Latency
Traffic
Errors
Saturation
```

Ils constituent une base utile, à compléter selon le domaine.

## 6. Logs

Gouverner :

- format ;
- severity ;
- correlation ;
- retention ;
- access ;
- masking ;
- cost.

## 7. Distributed tracing

Particulièrement utile lorsque le flux traverse :

```text
API Gateway
→ Payment Orchestrator
→ Fraud
→ Core
→ Clearing
```

Il aide à localiser latency et erreurs dans une chaîne distribuée.

## 8. SLI, SLO, SLA

```text
SLI
mesure observée

SLO
objectif interne du service

SLA
engagement formalisé
```

## 9. Error budget

Concept : marge d’erreur compatible avec le SLO.

Il permet d’arbitrer entre vitesse de changement et fiabilité.

## 10. Alerting

Une alerte de qualité doit être :

- actionable ;
- liée à un symptôme ou risque ;
- routée vers un owner ;
- suffisamment stable ;
- accompagnée d’un runbook si nécessaire.

## 11. Event management

Chaîne :

```text
Signal
→ alert
→ incident
→ diagnosis
→ mitigation
→ recovery
→ postmortem
```

HOPEX ne remplace pas la plateforme d’incident management ; le repository peut relier services critiques, owners et architecture.

## 12. Capacity management

Dimensions :

- CPU ;
- RAM ;
- storage ;
- IOPS ;
- network ;
- Kafka partitions/throughput ;
- DB sessions/IO ;
- license limits ;
- partner limits.

## 13. Headroom

La capacité nominale n’est pas la capacité réellement exploitable.

Prévoir :

- failure reserve ;
- growth ;
- maintenance ;
- burst ;
- scaling lag.

## 14. Performance testing

Types :

- load ;
- stress ;
- endurance ;
- spike ;
- failover under load.

Tester l’end-to-end, pas uniquement un composant isolé.

## 15. Operational readiness review

Avant production :

1. dashboards ;
2. alerts ;
3. runbooks ;
4. on-call ownership ;
5. backup/restore ;
6. capacity ;
7. security monitoring ;
8. DR ;
9. deployment rollback ;
10. dependency map.

## 16. MayaBank observability

```text
Customer request
→ API metrics
→ distributed trace
→ payment state metric
→ fraud latency
→ clearing timeout rate
→ Kafka lag
→ notification failures
```

## 17. Platform health vs business health

```text
CPU healthy
≠ payments successful
```

Toujours compléter les métriques techniques par des indicateurs de service métier.

## 18. Anti-patterns

- dashboard sans owner ;
- alert sur CPU sans symptôme utilisateur ;
- logs sans correlation ID ;
- traces sans sampling strategy ;
- monitoring absent du DR site ;
- capacité = moyenne ;
- aucune marge après perte d’un node/site.

## 19. Questions d’entretien

**Pourquoi mesurer saturation ?**  
Parce qu’un service peut être encore disponible tout en approchant une limite qui dégradera rapidement latency et fiabilité.

**Pourquoi un KPI métier est-il utile à l’infrastructure ?**  
Parce qu’il permet de relier le comportement technique à l’impact réel sur le service rendu.
