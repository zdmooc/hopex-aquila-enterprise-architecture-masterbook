# 09 — IT Transformation Roadmaps

## 1. Du constat à l'action

Une cartographie sans roadmap décrit le problème sans le résoudre.

La chaîne attendue :

```text
Fact
→ Risk / Gap
→ Decision
→ Initiative
→ Target Architecture
→ Milestone
→ Decommissioning
```

## 2. Drivers de transformation IT

Exemples :

- fin de support ;
- dette technique ;
- réduction de coûts ;
- résilience ;
- sécurité ;
- capacité métier nouvelle ;
- cloud/container strategy ;
- data modernization ;
- rationalisation applicative ;
- réduction de l'empreinte environnementale.

## 3. Roadmap centrée objets

Mauvais :

```text
2027: Modernization
2028: Cloud
2029: Optimization
```

Meilleur :

```text
Legacy Payment Hub
→ replace by Payment Orchestrator
→ migration WP-01
→ transition Q2
→ decommission Q4
```

## 4. Work packages / initiatives

Une initiative doit expliciter :

- objectif ;
- scope ;
- applications impactées ;
- technologies impactées ;
- dépendances ;
- target state ;
- owner ;
- milestones ;
- risks ;
- exit criteria.

Les MetaClasses réelles dépendent des solutions HOPEX ; la gouvernance doit utiliser les objets disponibles au lieu de créer systématiquement un métamodèle parallèle.

## 5. Milestones

Exemples MayaBank :

```text
M1 API Gateway ready
M2 Event Platform production-ready
M3 Payment Orchestrator handles 10% traffic
M4 Fraud service migrated
M5 100% payment traffic migrated
M6 Legacy Payment Hub decommissioned
```

Un milestone doit représenter un état vérifiable.

## 6. Dépendances de roadmap

```text
Platform readiness
→ application migration
→ data migration
→ consumer cutover
→ legacy decommission
```

Ignorer ces dépendances produit des roadmaps irréalistes.

## 7. Application roadmap

| Application | Current | Target | Action | Horizon |
|---|---|---|---|---|
| Legacy Payment Hub | active | retired | replace | 2027 |
| Payment Orchestrator | emerging | strategic | invest | 2027 |
| Batch Adapter | contain | retired | remove | 2028 |
| Fraud Engine | mainstream | strategic | modernize | 2027 |

Les dates sont pédagogiques et non des données réelles.

## 8. Technology roadmap

```text
WAS
Deprecated
→ migrate workloads
→ remove platform

OpenShift
Preferred
→ expand adoption
→ standardize GitOps/observability
```

## 9. Coexistence plan

Une roadmap complète doit montrer le temps où deux architectures coexistent.

```text
Legacy only
→ Dual run
→ Target primary + legacy fallback
→ Target only
```

## 10. Data migration

Questions :

- source et target ?
- format transformation ?
- historique ?
- synchronization during coexistence ?
- reconciliation ?
- rollback ?
- archive ?

Le traitement détaillé des données viendra en Partie IX.

## 11. Decommission plan

Checklist :

```text
all consumers migrated
no current flows
no regulatory retention blocker
archive complete
licenses terminated
infra released
monitoring removed
CMDB updated
HOPEX lifecycle updated
```

## 12. Green IT

Un gain d'infrastructure n'est réel qu'après décommission.

```text
new platform deployed
≠ carbon/cost gain achieved

legacy removed
→ resources released
→ measurable gain
```

La roadmap doit inclure l'arrêt réel des ressources.

## 13. Architecture gates

Exemple :

```text
Gate 0 — scope validated
Gate 1 — target architecture approved
Gate 2 — platform readiness
Gate 3 — migration readiness
Gate 4 — cutover
Gate 5 — legacy exit
```

Les gates peuvent être gérés hors HOPEX ; le repository doit au minimum conserver la traçabilité vers les objets et états.

## 14. Priorisation

Critères :

- risk urgency ;
- business value ;
- dependency unlock ;
- cost ;
- resource availability ;
- regulatory deadline ;
- technology EOL ;
- complexity.

## 15. Cas MayaBank

```text
2026 Q4
Target approved

2027 Q1
API Gateway + Event Platform

2027 Q2
Payment Orchestrator pilot

2027 Q3
Fraud + notification migration

2027 Q4
100% traffic target

2028 Q1
Legacy decommission
```

Chronologie purement pédagogique.

## 16. Anti-patterns

- roadmap par PowerPoint sans liens repository ;
- dates sans owner ;
- `Retire` sans decommission project ;
- target sans milestone ;
- plateforme cible planifiée après les applications qui en dépendent ;
- absence de coexistence ;
- aucun exit criterion.

## 17. Entretien

**Quelle différence entre target architecture et roadmap ?**  
La target décrit l'état souhaité ; la roadmap décrit les transformations et états intermédiaires permettant de l'atteindre.

**Quand une migration est-elle finie ?**  
Quand la cible est opérationnelle et que les dépendances legacy prévues pour suppression sont effectivement décommissionnées.
