# 10 — Assessments, Gaps & Business Roadmaps

## 1. Passer du modèle descriptif au modèle décisionnel

Une Business Architecture devient réellement utile lorsqu'elle permet de comparer l'état actuel à l'état cible.

```text
Current State
→ Assessment
→ Gap
→ Option
→ Initiative
→ Target State
```

## 2. Les objets évaluables

Selon le besoin, on peut évaluer :

- capability ;
- value stream ;
- process ;
- business service ;
- organization readiness ;
- information quality ;
- application support ;
- technology support.

Le score doit toujours avoir une définition claire.

## 3. Capability assessment

Exemple :

| Capability | Importance | Maturity | Performance | Risk |
|---|---:|---:|---:|---:|
| Payment Orchestration | 5 | 2 | 3 | 5 |
| Fraud Decisioning | 5 | 4 | 4 | 4 |
| Payment Operations | 4 | 2 | 2 | 4 |

Un score unique « health » peut masquer des problèmes différents ; garder les dimensions utiles à la décision.

## 4. Value Stream assessment

Pour chaque stage :

```text
customer value
lead time
failure rate
manual effort
risk
supporting capability maturity
```

Exemple :

```text
Stage: Confirm Payment
Issue: delayed status propagation
Impact: customer retries + operations workload
```

## 5. Gap

Un gap doit exprimer une différence entre current et target, pas seulement un problème vague.

Faible :

```text
Kafka missing
```

Meilleur :

```text
Current: payment status propagation is synchronous and application-coupled
Target: asynchronous, resilient, shared event distribution
Gap: no shared event distribution capability/platform
```

## 6. Gap categories

- capability gap ;
- process gap ;
- organization/skill gap ;
- information gap ;
- service gap ;
- application gap ;
- technology gap ;
- governance gap ;
- compliance gap.

## 7. Options

Un bon architecture assessment évalue plusieurs options.

Exemple :

```text
Option A: modernize legacy payment hub
Option B: incremental strangler migration
Option C: new target payment platform
```

Critères :

- business value ;
- risk ;
- time-to-value ;
- cost ;
- capability improvement ;
- migration complexity ;
- reversibility.

## 8. Initiative

Une initiative ferme un ou plusieurs gaps.

```text
Initiative: Payment Event Backbone
closes:
- real-time distribution gap
- observability gap partially
- integration coupling gap partially
```

## 9. Business roadmap

Une roadmap doit montrer la progression de capacités et outcomes, pas seulement des dates de projets.

```text
Now
→ stabilize payment operations
→ establish event backbone
→ automate fraud decisions
→ enable multi-site runtime
→ decommission legacy integrations
Target
```

## 10. Dependencies

Exemple :

```text
Event Backbone
must precede
Real-time Notification migration

Target Identity capability
must precede
Partner API expansion
```

Les dépendances métier doivent être reliées aux dépendances IT de la Partie IV.

## 11. Transition states

Une transformation n'est pas un saut direct.

```text
Current
Legacy + point-to-point

Transition 1
Legacy + APIs + initial event backbone

Transition 2
Hybrid orchestration

Target
Domain services + event-driven + resilient platform
```

Chaque transition doit rester opérable.

## 12. Benefits realization

Pour chaque initiative :

```text
expected outcome
measure
baseline
expected target
owner
review date
```

Exemple :

```text
Initiative: Payment Operations Automation
Benefit: lower manual exception handling
Measure: manual touch rate
Baseline: 18%
Target: < 5%
```

## 13. Portfolio prioritization

Questions :

1. quelle capability est stratégique ?
2. quel gap est le plus critique ?
3. quel service/client est touché ?
4. quelle dépendance bloque ?
5. quel risque est réduit ?
6. quel coût legacy peut être retiré ?
7. quel benefit est mesurable ?

## 14. MayaBank roadmap

```text
Wave 1 — Understand & Stabilize
- canonical repository
- capability/process map
- service ownership
- observability baseline

Wave 2 — Decouple
- API rationalization
- event streaming foundation
- status event model

Wave 3 — Resilience
- multi-site runtime
- automated recovery
- fraud decision optimization

Wave 4 — Simplify
- retire point-to-point integrations
- decommission legacy components
- consolidate operations
```

## 15. Anti-patterns

- roadmap = Gantt ;
- gap = nom d'une technologie absente ;
- score sans définition ;
- target sans baseline ;
- initiatives sans outcome ;
- aucune dependency ;
- aucun benefit owner ;
- transformation sans transition state ;
- tout classé priorité 1.

## 16. Entretien

**Comment passer d'une capability map à une roadmap ?**  
En évaluant importance/maturité/performance, en identifiant les gaps vers la cible puis en priorisant des initiatives mesurables qui ferment ces gaps.

**Pourquoi modéliser les transition states ?**  
Parce qu'une cible parfaite mais non atteignable opérationnellement n'est pas une architecture de transformation.