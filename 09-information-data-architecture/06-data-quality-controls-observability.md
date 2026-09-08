# 06 — Data Quality Architecture, Controls & Observability

## 1. Data quality is contextual

Une donnée n’est pas « bonne » de façon absolue. Elle est de qualité si elle est suffisamment adaptée à son usage.

Dimensions fréquentes :

- completeness ;
- validity ;
- uniqueness ;
- consistency ;
- accuracy ;
- timeliness/freshness ;
- integrity.

## 2. Critical Data Elements first

Ne pas essayer de contrôler chaque champ au même niveau.

MayaBank priorise :

```text
PaymentId
EndToEndId
Amount
Currency
Debtor Account
Creditor Reference
Payment Status
Execution Timestamp
Fraud Decision
Clearing Result
```

## 3. Quality rule anatomy

Une règle exploitable contient :

```text
Rule ID
Data element
Definition
Dimension
Formula/test
Threshold
Severity
Owner
Monitoring frequency
Source
Remediation process
```

## 4. Exemple — Amount

```text
DQ-PAY-001
Element : Payment Amount
Rule    : amount > 0 and currency populated
Dimension: validity/completeness
Target  : 100%
Owner   : Payments Data Owner
```

## 5. Exemple — duplicate payment

```text
DQ-PAY-002
Element : EndToEndId + debtor context
Rule    : uniqueness according to payment scheme/idempotency window
Dimension: uniqueness
```

La règle métier exacte dépend du scheme et de l’architecture.

## 6. Preventive controls

Agissent avant propagation :

- schema validation ;
- mandatory fields ;
- type/range validation ;
- reference data check ;
- idempotency ;
- referential integrity.

## 7. Detective controls

Détectent après création :

- reconciliation ;
- anomaly detection ;
- freshness monitoring ;
- duplicate scan ;
- cross-system consistency check.

## 8. Corrective controls

- retry ;
- replay ;
- repair workflow ;
- manual correction ;
- compensation ;
- source-system remediation.

## 9. Data observability

La data observability cherche à détecter rapidement :

```text
Freshness failure
Volume anomaly
Schema drift
Null spike
Distribution change
Pipeline failure
Lineage break
```

HOPEX peut porter architecture, ownership, quality context et impact ; l’observation runtime peut venir d’outils spécialisés.

## 10. Quality score

Éviter une moyenne unique qui masque les problèmes.

Préférer :

```text
Overall score
+ per dimension
+ per critical element
+ trend
+ failed rules
+ business impact
```

## 11. Quality incident workflow

```text
Detection
→ classify severity
→ identify impacted data asset
→ lineage impact
→ assign owner
→ contain
→ remediate
→ validate
→ root-cause action
```

## 12. Business impact

Une mauvaise donnée devient prioritaire si elle impacte :

- paiement ;
- fraude ;
- conformité ;
- reporting réglementaire ;
- customer experience ;
- finance ;
- operational decision.

## 13. Data quality vs application bug

Un défaut peut provenir de :

- source incorrecte ;
- mapping ;
- transformation ;
- race condition ;
- stale cache ;
- schema mismatch ;
- manual input ;
- reference data obsolete.

Le lineage aide à localiser la racine.

## 14. Quality campaigns

Les pages publiques HOPEX Data Governance décrivent des campagnes d’évaluation et de remédiation pour qualité/conformité.

Le détail des workflows doit être vérifié dans l’environnement client.

## 15. DQ dashboard MayaBank

| Data element | Rule | Target | Current | Owner |
|---|---|---:|---:|---|
| PaymentId | not null/unique | 100% | 100% | Payments |
| Currency | ISO code valid | 100% | 99.99% | Reference Data |
| Payment Status | allowed state | 100% | 99.98% | Payments |
| Fraud Decision | populated for eligible payment | 100% | 99.95% | Fraud |

Valeurs pédagogiques.

## 16. Service Level for Data

Pour un dataset analytique :

```text
Freshness < 15 min
Completeness > 99.9%
Schema compatibility = no breaking change without notice
Availability = agreed service window
```

Un data SLA/SLO doit être mesurable et relié à un usage.

## 17. Quality ownership

Le producteur doit corriger les défauts à la source lorsque possible.

Anti-pattern :

```text
Bad source
→ ETL fixes forever
→ consumers never know
```

Target :

```text
Detect
→ root cause
→ fix producer
→ keep defensive controls
```

## 18. Quality gates before migration

Avant migration :

1. baseline qualité ;
2. reconciliation criteria ;
3. mapping validation ;
4. duplicate rules ;
5. error quarantine ;
6. rollback criteria ;
7. post-cutover monitoring.

## 19. Anti-patterns

- score global sans dimensions ;
- règle sans owner ;
- seuil arbitraire ;
- réparer seulement downstream ;
- mesurer sans remédiation ;
- contrôler chaque colonne avec même priorité ;
- data quality séparée du lineage et du business impact.
