# 09 — Process performance, KPIs, SLA, throughput et maturity

## 1. De la documentation à la mesure

Un process model décrit la logique et les responsabilités. Un **performance model** permet de savoir si cette logique produit le résultat attendu.

Le chapitre 03 introduit les KPIs dans le contexte risk/control. Ici, l'objectif est de construire un système de mesure complet et exploitable.

## 2. Les métriques fondamentales

### Cycle Time

Temps entre le début et la fin d'un cas selon les frontières du processus.

Exemple :

```text
Payment request received
→ final payment status produced
```

### Lead Time

Temps total vécu par le demandeur, qui peut inclure attente avant démarrage, traitement et attente après traitement.

### Processing Time

Temps durant lequel une ressource travaille effectivement sur le cas.

### Waiting Time

Temps passé en file d'attente ou en attente d'un événement externe.

### Throughput

Nombre de cas terminés sur une période.

```text
payments / second
cases / hour
requests / day
```

### Failure Rate

```text
failed cases / total cases
```

### Rework Rate

Part des cas qui repassent par une activité déjà exécutée.

### Automation Rate

Part des activités ou cas exécutés sans intervention humaine selon une définition explicite.

### Manual Intervention Rate

Part des cas nécessitant une intervention humaine significative.

### Straight-Through Processing — STP

Part des cas éligibles terminés sans intervention manuelle.

## 3. Ne pas confondre duration et service time

Exemple :

```text
Manual Review
service time = 4 min
waiting time = 17 min
cycle contribution = 21 min
```

Optimiser uniquement le service time peut ne presque rien changer au cycle time.

## 4. P50, P95, P99

Pour les processus à fort volume, une moyenne masque les queues longues.

Exemple pédagogique :

```text
P50 = 650 ms
P95 = 1.8 s
P99 = 4.2 s
```

Une architecture critique doit connaître au moins la distribution nécessaire à son SLA/SLO.

## 5. KPI design card

Chaque KPI doit contenir :

```text
Name
Business question
Definition
Formula
Scope
Population
Exclusions
Unit
Source
Frequency
Owner
Target
Warning threshold
Critical threshold
Data quality rule
Review date
```

Sans définition stable, deux dashboards peuvent afficher le même nom avec des chiffres incompatibles.

## 6. KPI tree

Relier les métriques techniques aux outcomes métier.

Exemple :

```text
Customer payment outcome
├─ STP
├─ End-to-end P95
├─ Rejection rate
├─ Duplicate rate
├─ Clearing timeout rate
└─ Notification success rate
```

Puis relier les indicateurs de composants :

```text
Fraud latency
Payment Orchestrator latency
Clearing Adapter error rate
Kafka consumer lag
Database latency
```

Les métriques techniques expliquent la performance ; elles ne remplacent pas le KPI end-to-end.

## 7. KPI vs SLA vs SLO

### KPI

Mesure de performance.

### SLO

Objectif interne ou opérationnel mesurable.

### SLA

Engagement de service convenu avec conséquences ou responsabilités associées selon le contrat/contexte.

Un KPI peut alimenter un SLO, et un SLO peut soutenir un SLA, mais les trois concepts ne sont pas interchangeables.

## 8. Process boundary et métrique

Avant de calculer un temps, définir :

```text
Start timestamp
End timestamp
Clock type
Excluded states
Timezone
Retry treatment
Duplicate treatment
Cancelled case treatment
```

Sans cela, un P95 n'est pas comparable.

## 9. Event log minimal pour la performance

```text
Case ID
Activity
Timestamp
Lifecycle state
Outcome
```

Attributs utiles :

```text
Channel
Product
Country
Customer segment
Amount bucket
Error code
Application
Team
Correlation ID
```

Le contenu doit respecter les règles de sécurité et de privacy du client.

## 10. Performance by variant

Une moyenne globale peut cacher une variante dégradée.

Segmenter par :

- canal ;
- produit ;
- pays ;
- type de client ;
- montant ;
- exception ;
- application path ;
- heure/jour ;
- version du processus.

## 11. Bottleneck signal

Signaux typiques :

- queue length croissante ;
- waiting time élevé ;
- resource utilization proche de saturation ;
- forte variance ;
- rework loop ;
- handoff lent ;
- SLA breach concentré sur une activité ;
- burst de volume non absorbé.

Un bottleneck doit être confirmé par des données, pas seulement par une impression d'atelier.

## 12. Capacity model

Questions :

```text
Volume peak?
Arrival rate?
Service time?
Parallel capacity?
Queue behavior?
Retry amplification?
External dependency limit?
```

Exemple MayaBank : un timeout clearing peut créer des retries qui amplifient la charge et aggravent l'incident.

## 13. Failure taxonomy

Séparer :

- business rejection ;
- compliance rejection ;
- fraud rejection ;
- technical retryable ;
- technical permanent ;
- timeout ;
- duplicate ;
- reconciliation exception ;
- manual repair ;
- notification failure.

Sinon le `failure rate` mélange des résultats légitimes et des erreurs techniques.

## 14. Automation rate — prudence

Un taux d'automatisation de 100 % n'est pas toujours un objectif.

Une intervention humaine peut être requise pour :

- exception réglementaire ;
- décision discrétionnaire ;
- contrôle quatre yeux ;
- fraude complexe ;
- incident majeur.

Le bon objectif est l'automatisation **des cas éligibles**, avec contrôle explicite des exceptions.

## 15. Process maturity model

Modèle pédagogique MayaBank :

### Level 1 — Documented

- processus identifiés ;
- diagrammes disponibles ;
- ownership partiel.

### Level 2 — Standardized

- hierarchy commune ;
- naming ;
- owners ;
- lifecycle ;
- variantes gouvernées.

### Level 3 — Connected

- applications ;
- data ;
- risks ;
- controls ;
- capabilities ;
- initiatives reliés.

### Level 4 — Measured

- KPIs fiables ;
- baselines ;
- event data ;
- targets ;
- dashboards ;
- review cadence.

### Level 5 — Continuously Improved

- process mining ;
- conformance ;
- simulation ;
- experimentation ;
- transformation backlog piloté par les données.

Ce modèle n'est pas un modèle de maturité HOPEX officiel.

## 16. Maturity assessment

Pour chaque process critique, noter :

| Dimension | 1 | 3 | 5 |
|---|---|---|---|
| ownership | absent | defined | actively governed |
| modeling | informal | standardized | measured/optimized |
| application mapping | missing | partial | maintained |
| risk/control | isolated | mapped | continuously assessed |
| KPI | anecdotal | defined | reliable & actionable |
| improvement | reactive | roadmap | continuous feedback |

## 17. Current vs target maturity

Exemple :

```text
Execute Instant Payment
Current maturity = 3.2
Target maturity = 4.4
```

Le chiffre n'a de sens que si les dimensions et règles de calcul sont documentées.

## 18. KPI baseline

Avant transformation :

- période stable ;
- définition gelée ;
- anomalies documentées ;
- saisonnalité comprise ;
- population comparable ;
- qualité des données évaluée.

Sinon le gain annoncé peut venir uniquement d'un changement de définition.

## 19. Target setting

Éviter les targets arbitraires.

Sources :

- obligation réglementaire ;
- SLA ;
- benchmark interne ;
- besoin client ;
- capacité technique ;
- economics ;
- risk appetite ;
- target architecture.

## 20. Dashboard layering

### Executive

- outcome ;
- SLA ;
- STP ;
- critical risks ;
- trend.

### Process Owner

- cycle ;
- variants ;
- exceptions ;
- rework ;
- bottlenecks ;
- controls.

### Operations

- queue ;
- current errors ;
- timeout ;
- manual work ;
- incidents.

### Architecture/SRE

- component latency ;
- availability ;
- saturation ;
- dependency health ;
- event lag.

## 21. MayaBank KPI catalogue

| KPI | Formula/definition | Owner | Source conceptuelle |
|---|---|---|---|
| STP | cases without manual action / eligible cases | Payments | process events |
| E2E P95 | start→final status P95 | Payments | correlated timestamps |
| Clearing Timeout Rate | timeout cases / clearing submissions | Operations | clearing events |
| Duplicate Rate | duplicate detected / requests | Payments | idempotency records |
| Manual Repair Rate | repair cases / cases | Operations | work queue |
| Fraud Review Rate | manual fraud review / eligible cases | Fraud | fraud decision events |
| Notification Failure | failed notification / requested | Customer Ops | notification events |

Valeurs et targets doivent venir du contexte réel.

## 22. Exemple de scorecard pédagogique

| KPI | Current | Target | Status |
|---|---:|---:|---|
| STP | 96.8% | 99.5% | gap |
| E2E P95 | 4.5s | <2s | gap |
| clearing timeout | 0.7% | <0.1% | gap |
| manual repair | 2.0% | <0.2% | gap |
| notification success | 98.9% | >99.9% | gap |

Ces chiffres sont fictifs.

## 23. Cause vs symptom

Exemple :

```text
Symptom: P95 high
```

Causes possibles :

- clearing latency ;
- fraud review ;
- database contention ;
- retry storm ;
- serial checks ;
- message backlog ;
- manual handoff.

Le process model permet de relier le symptôme aux étapes et dépendances à investiguer.

## 24. Measurement anti-patterns

- moyenne uniquement ;
- KPI sans formule ;
- changement de population non déclaré ;
- mélange business rejection / technical failure ;
- SLA calculé avec timestamps non corrélés ;
- target sans owner ;
- dashboards sans action associée ;
- mesure d'une activité locale au lieu du cycle end-to-end ;
- métrique technique présentée comme outcome métier.

## 25. Performance review ritual

Cadence recommandée pour un processus critique :

```text
Observe trend
→ explain variance
→ identify root cause
→ assess risk/control impact
→ decide improvement
→ assign initiative
→ measure outcome
```

HOPEX peut porter la connaissance gouvernée ; les données opérationnelles peuvent provenir d'autres systèmes.

## 26. Questions d'entretien

**Pourquoi P95 plutôt que moyenne ?**  
Pour observer la queue de distribution et les cas lents que la moyenne masque.

**Cycle time et processing time ?**  
Le cycle couvre le temps total entre frontières ; le processing time couvre le travail actif.

**Pourquoi un KPI sans source n'est-il pas exploitable ?**  
Parce qu'il n'est ni reproductible ni audit-able.

**Comment mesurer l'automatisation ?**  
Sur une population éligible et avec une définition explicite de l'intervention humaine.