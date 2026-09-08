# 03 — Exceptions, contrôles, risques, RACI et KPIs

## 1. Un processus exploitable doit aller au-delà du happy path

Un diagramme de processus devient réellement utile lorsqu'il permet de comprendre :

- les exceptions ;
- les responsabilités ;
- les contrôles ;
- les risques ;
- les indicateurs ;
- les engagements de service.

## 2. Catalogue d'exceptions

Chaque processus critique devrait identifier ses principales exceptions.

Exemple `Execute Instant Payment` :

| Exception | Déclencheur | Traitement | Owner |
|---|---|---|---|
| Invalid Request | contrôle de format | reject | Payments |
| Fraud Suspected | score élevé | reject/review | Fraud |
| Insufficient Funds | balance check | reject | Payments |
| Clearing Timeout | timer | retry/escalate | Operations |
| Duplicate | idempotency control | reject/return known status | Payments |
| Platform Outage | monitoring event | incident/failover | Platform |

## 3. Risque vs incident

Un risque décrit une possibilité et son impact potentiel.

Un incident décrit un événement survenu.

```text
Risk
Clearing network unavailable

Control
Timeout + retry + DR procedure

Incident
Actual clearing outage at 14:32
```

Ne pas confondre repository de risques et journal opérationnel d'incidents.

## 4. Controls by design

Un contrôle doit être relié à l'endroit où il agit.

Exemples :

```text
Validate Payment Request
→ schema validation control

Run Fraud Check
→ fraud decision control

Authorize Payment
→ strong authentication / authorization control

Send to Clearing
→ duplicate prevention / idempotency control
```

Les pages produit actuelles de Bizzdesign mettent en avant le mapping des processus aux contrôles et réglementations pour améliorer compliance et auditability.

## 5. Preventive, detective, corrective

### Preventive
Empêche l'erreur.

```text
Input validation
Authorization
Four-eyes principle
```

### Detective
Détecte un problème.

```text
Reconciliation
Monitoring
Anomaly detection
```

### Corrective
Réduit l'impact après détection.

```text
Retry
Manual repair
Compensation
Failover
```

## 6. RACI

RACI permet de clarifier les responsabilités :

- Responsible ;
- Accountable ;
- Consulted ;
- Informed.

Exemple :

| Activity | Payments | Fraud | Operations | Platform |
|---|---|---|---|---|
| Validate Payment | R/A | C | I | I |
| Fraud Decision | C | R/A | I | I |
| Handle Timeout | C | I | R/A | C |
| Restore Platform | I | I | C | R/A |

RACI n'est pas un moteur d'autorisation. Il documente la responsabilité métier/organisationnelle.

## 7. Process Owner vs Activity Owner

Process Owner : responsabilité end-to-end.

Activity Owner : responsabilité locale d'une étape.

Un processus transverse ne doit pas être gouverné seulement par les owners de ses activités.

## 8. KPI architecture

Un KPI utile doit répondre à :

```text
Metric
+ scope
+ formula
+ target
+ source
+ frequency
+ owner
```

Exemples MayaBank :

### Straight-Through Processing Rate

```text
successful payments without manual intervention
/
total eligible payments
```

### End-to-End Processing Time

De réception à statut final.

### Fraud False Positive Rate

### Clearing Timeout Rate

### Manual Repair Rate

### Process Availability

## 9. KPI vs SLA vs SLO

KPI : indicateur de performance.

SLA : engagement contractuel/service.

SLO : objectif de niveau de service.

Ils peuvent être reliés mais ne sont pas interchangeables.

## 10. Exemple de scorecard MayaBank

| KPI | Target | Warning | Critical |
|---|---:|---:|---:|
| STP | ≥ 99.5% | < 99.5% | < 98.5% |
| Processing P95 | < 2s | 2–4s | > 4s |
| Timeout rate | < 0.1% | 0.1–0.5% | > 0.5% |
| Manual repair | < 0.2% | 0.2–1% | > 1% |

Les valeurs sont pédagogiques ; un client doit utiliser ses objectifs réels.

## 11. Control gap analysis

Pour chaque risque majeur :

```text
Risk
↓
Existing control
↓
Control effectiveness
↓
Residual risk
↓
Target control / initiative
```

## 12. Exception architecture

Ne pas traiter toutes les erreurs comme :

```text
Exception → Manual Review
```

Classer :

- business rejection ;
- technical retryable ;
- technical non-retryable ;
- fraud/compliance ;
- timeout ;
- duplicate ;
- reconciliation discrepancy.

## 13. Compensating actions

Dans un processus distribué, certaines erreurs nécessitent compensation plutôt que rollback technique global.

Exemple conceptuel :

```text
Debit reserved
→ downstream fails
→ release reservation
→ update status
→ notify
```

## 14. Auditability

Un processus critique doit permettre de reconstruire :

- qui a fait quoi ;
- quelle décision a été prise ;
- sur quelles données ;
- à quel moment ;
- quel contrôle a été appliqué ;
- quel résultat a été produit.

## 15. Questions de revue

1. Le process owner est-il identifié ?
2. Les activités critiques ont-elles un responsable ?
3. Les exceptions majeures sont-elles modélisées ?
4. Chaque risque critique possède-t-il un contrôle ?
5. Les contrôles sont-ils préventifs/détectifs/correctifs selon le besoin ?
6. Les KPIs sont-ils mesurables avec une source définie ?
7. Les seuils sont-ils gouvernés ?
8. Le modèle distingue-t-il incident, risque et exception ?
9. Les actions de compensation sont-elles claires ?
10. La traçabilité réglementaire est-elle exploitable ?