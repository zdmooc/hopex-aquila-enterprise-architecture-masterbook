# 09 — Stakeholders, Drivers, Outcomes & Strategic Alignment

## 1. Business Architecture commence par une décision

Une architecture métier sans stakeholder ni outcome risque de devenir une encyclopédie descriptive.

Le point de départ est :

```text
Stakeholder
→ concern
→ driver
→ objective/outcome
→ impacted capabilities/value streams
→ change initiative
```

## 2. Stakeholders MayaBank

Exemples :

- Retail Customer ;
- Payments Business Director ;
- Operations ;
- Fraud & Risk ;
- Compliance ;
- CIO ;
- Enterprise Architecture ;
- Platform Engineering ;
- Regulators ;
- Payment Schemes.

Chaque stakeholder n'a pas le même concern.

## 3. Concerns

```text
Customer
→ speed, trust, transparency

Operations
→ recoverability, workload, observability

Compliance
→ traceability, control, reporting

CIO
→ cost, resilience, simplification

Business
→ growth, service coverage, time-to-market
```

Les vues HOPEX doivent être construites pour répondre à ces concerns, pas pour montrer tout le repository.

## 4. Drivers

Exemples MayaBank :

```text
Instant payment adoption
Regulatory requirements
Legacy obsolescence
Fraud pressure
Customer expectation 24x7
High operating cost
```

Un driver explique pourquoi le changement devient nécessaire.

## 5. Outcomes

Un outcome doit être observable.

Faible :

```text
Modernize payments
```

Meilleur :

```text
Reduce payment confirmation P95
Increase straight-through processing
Reduce critical legacy dependencies
Achieve multi-site recovery target
```

## 6. Strategic alignment

Bonne chaîne :

```text
Strategic Objective
→ Capability
→ Value Stream
→ Business Service
→ Process
→ Application
→ Technology
→ Initiative
```

Cette chaîne permet d'expliquer pourquoi un investissement technique existe.

## 7. Example — Event Streaming Platform

Mauvaise justification :

```text
We need Kafka because event-driven is modern.
```

Meilleure justification :

```text
Outcome
Faster and more resilient payment status propagation
↓
Capability gap
Real-time payment event distribution
↓
Business impact
Confirmation + Operations + Fraud
↓
Architecture decision
Shared Event Streaming Platform
```

## 8. Objective × Capability

| Objective | Orchestration | Fraud | Ops | Observability |
|---|---:|---:|---:|---:|
| 24x7 resilience | X | X | X | X |
| Faster time-to-market | X | - | - | X |
| Reduce fraud losses | X | X | X | X |

Cette matrice permet d'identifier les capabilities stratégiques.

## 9. Outcome measures

Associer des KPIs :

```text
Outcome: faster payment confirmation
Measure: P95 end-to-end confirmation
Baseline: 12 sec
Target: < 5 sec
```

Sans mesure, la roadmap ne peut pas prouver sa valeur.

## 10. Strategy vs Project

Une initiative n'est pas un objectif.

```text
Objective : Improve payment resilience
Initiative: Deploy active-active payment runtime
```

Confondre les deux empêche d'évaluer plusieurs options pour atteindre le même objectif.

## 11. Prioritization

Évaluer une initiative selon :

- strategic alignment ;
- capability gap closed ;
- customer value ;
- risk reduction ;
- regulatory urgency ;
- cost ;
- dependency ;
- implementation feasibility.

## 12. Architecture decisions

Chaque décision significative devrait pouvoir répondre :

```text
Which stakeholder concern?
Which outcome?
Which capability?
Which gap?
Which option rejected?
Which measure validates success?
```

## 13. MayaBank strategic thread

```text
Driver
Growing instant-payment usage
↓
Outcome
24x7 resilient payment execution
↓
Capabilities
Payment Orchestration + Fraud + Ops
↓
Value Stream
Initiate → Validate → Decide → Execute → Confirm
↓
Gaps
legacy coupling + weak observability + manual exception handling
↓
Initiatives
API simplification + event backbone + runtime resiliency + ops automation
```

## 14. Anti-patterns

- objectifs sans stakeholder ;
- goals non mesurables ;
- initiatives traitées comme des outcomes ;
- aucune trace entre stratégie et application ;
- heatmap capability sans driver ;
- projet technologique auto-justifié ;
- décision non reliée à un gap.

## 15. Entretien

**Comment démontrer l'alignement stratégique ?**  
En maintenant une chaîne de traçabilité entre objectives/outcomes, capabilities, value streams, services/processus, architecture et initiatives.

**Pourquoi cette trace est-elle utile ?**  
Pour prioriser, challenger et éventuellement arrêter un investissement qui ne contribue plus à un outcome métier.