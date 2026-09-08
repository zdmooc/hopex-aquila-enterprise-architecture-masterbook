# 07 — Current, Transition & Target Architecture

## 1. Pourquoi séparer les états

Une architecture cible n'est utile que si elle peut être comparée à l'existant et reliée à un chemin de transformation.

```text
CURRENT
↓ gap analysis
TRANSITION
↓ migration
TARGET
```

Sans cette séparation, HOPEX devient un inventaire ou un dessin de cible sans trajectoire.

## 2. Current architecture

Le current doit répondre à :

- quelles applications existent réellement ?
- quelles technologies sont réellement utilisées ?
- quelles dépendances sont actives ?
- quels environnements sont opérationnels ?
- quelles exceptions existent ?
- quelles données sont suffisamment fiables ?

La qualité du current conditionne la qualité de toute analyse de transformation.

## 3. Target architecture

Une target décrit des choix structurants :

- applications retenues ;
- applications supprimées ;
- services cibles ;
- technologies standards ;
- architecture d'intégration ;
- principes de déploiement ;
- résilience ;
- sécurité ;
- observabilité.

Elle ne doit pas être seulement une palette de technologies modernes.

## 4. Transition architecture

Une transition représente un état temporaire mais exploitable.

Exemple MayaBank :

```text
Transition 1
- Legacy Payment Hub still active
- new API Gateway introduced
- Kafka introduced for non-critical events
- dual write during migration

Transition 2
- Payment Orchestrator active
- legacy adapter retained for one clearing rail
- target observability complete
```

Ces états sont souvent les plus risqués parce qu'ils combinent ancien et nouveau.

## 5. Scenario architecture

Les ressources publiques historiques HOPEX IT Architecture décrivent des diagrammes de scénarios permettant de représenter une application dans plusieurs contextes et ses flux.

Le pattern est utile pour comparer :

```text
Scenario A = current
Scenario B = transition
Scenario C = target
```

Le nom exact du diagramme ou les fonctionnalités d'Aquila doivent être vérifiés dans l'instance du client.

## 6. Baseline vs target objects

Deux stratégies possibles selon le métamodèle et la gouvernance :

### même objet avec temporalité

```text
Application X
Current status = active
Target status = retire
```

### versions/scénarios séparés

Quand l'outil ou la solution fournit des mécanismes dédiés, les états peuvent être représentés dans des contextes distincts.

Ne jamais inventer une méthode de versioning sans connaître la configuration HOPEX.

## 7. Gap analysis

Exemple :

| Current | Target | Gap |
|---|---|---|
| point-to-point | API/event driven | integration modernization |
| WAS | OpenShift | container migration |
| manual DR | automated tested DR | resilience gap |
| shared file | object storage | storage refactoring |
| legacy auth | OIDC/mTLS | security modernization |

## 8. Dependency-aware target

Une target doit conserver les dépendances critiques.

Mauvaise target :

```text
Payment Orchestrator → OpenShift
```

Bonne target :

```text
Payment Orchestrator
├─ Identity Service
├─ Fraud Service
├─ Event Streaming
├─ Database Service
├─ API Gateway
└─ Observability
```

## 9. Target compliance

Chaque target doit pouvoir être confrontée à :

- technology standards ;
- security principles ;
- architecture principles ;
- lifecycle rules ;
- resilience requirements.

## 10. Decision log

Pour une décision majeure :

```text
Decision
Context
Options
Chosen option
Rationale
Trade-offs
Risks
Impacted objects
Review date
```

HOPEX peut porter ou référencer cette information selon la gouvernance en place.

## 11. MayaBank — trajectoire paiement

### Current

```text
Channels
→ Legacy Payment Hub
→ Fraud Adapter
→ Clearing
```

### Transition

```text
Channels
→ API Gateway
→ Payment Orchestrator
→ Legacy Clearing Adapter
→ Kafka for side events
```

### Target

```text
Channels
→ API Gateway
→ Payment Orchestrator
→ Fraud Decision Service
→ Event Platform
→ Clearing Services
```

## 12. Coexistence

Toujours rendre visible :

- double routing ;
- data synchronization ;
- backward compatibility ;
- temporary adapters ;
- duplicated operational controls ;
- exit criteria.

## 13. Decommissioning

Une cible n'est pas atteinte tant que le legacy reste utilisé.

Checklist :

1. consommateurs migrés ;
2. données migrées/archivées ;
3. interfaces fermées ;
4. monitoring arrêté ;
5. licences supprimées ;
6. infrastructure libérée ;
7. repository mis à jour.

## 14. Anti-patterns

- target sans current fiable ;
- target = liste de produits ;
- transition inexistante ;
- coexistence cachée ;
- legacy marqué `retired` trop tôt ;
- aucun exit criterion ;
- gap non relié à une initiative.

## 15. Entretien

**Pourquoi modéliser les transitions ?**  
Parce que le risque opérationnel est souvent maximal pendant la coexistence du legacy et de la cible.

**Qu'est-ce qu'une bonne target ?**  
Un état cohérent, conforme aux standards, traçable aux besoins et suffisamment détaillé pour analyser les dépendances et la migration.
