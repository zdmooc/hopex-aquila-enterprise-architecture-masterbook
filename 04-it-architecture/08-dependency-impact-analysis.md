# 08 — Dependency & Impact Analysis

## 1. Pourquoi l'analyse d'impact est un use case majeur

Le positionnement public de HOPEX met explicitement en avant l'analyse des impacts business à travers applications et technologies. C'est l'un des bénéfices directs d'un repository connecté.

Question type :

> Si la technologie X disparaît, quels services métier et quelles capacités seront affectés ?

## 2. Impact direct

```text
Technology X
→ Application A
```

Simple, mais insuffisant.

## 3. Impact transitif

```text
Technology X
→ Application A
→ Application B
→ Business Process P
→ Capability C
```

C'est ce chemin multi-niveaux qui donne sa valeur au graphe d'architecture.

## 4. Upstream vs downstream

### Upstream dependency

Ce dont un objet dépend.

```text
Payment Orchestrator
→ Identity Service
→ Directory
```

### Downstream impact

Ce qui dépend de l'objet.

```text
Identity Service
← Payment Orchestrator
← Mobile Banking
```

Les deux sens doivent être compréhensibles.

## 5. Analyse d'un changement applicatif

Changement : retrait de `Legacy Fraud Adapter`.

Questions :

1. qui le consomme ?
2. quels flux passent par lui ?
3. quelle donnée transporte-t-il ?
4. quelle capacité dépend de ces consommateurs ?
5. quelle cible le remplace ?
6. quelles transitions sont nécessaires ?

## 6. Analyse d'une technologie obsolète

```text
Old MQ Runtime
→ Legacy Payment Hub
→ Batch Clearing Adapter
→ End-of-day Settlement Process
```

Le niveau métier donne la priorité réelle de remédiation.

## 7. Analyse de panne

Incident hypothétique : Event Streaming Platform indisponible.

Directement impactés :

- Notification Hub ;
- Analytics consumers ;
- AML event consumers.

Le Payment Orchestrator peut-il continuer le traitement synchrone ? Cela dépend du design. Le repository doit représenter la dépendance de manière assez précise pour ne pas surévaluer ou sous-évaluer l'impact.

## 8. Impact de sécurité

Vulnérabilité critique sur une technologie :

```text
Technology vulnerable
→ Applications using it
→ Internet-exposed interfaces
→ Critical business services
→ Prioritized remediation
```

## 9. Impact réglementaire

Une exigence réglementaire peut nécessiter :

```text
Requirement
→ Processes
→ Applications
→ Data
→ Technologies
```

La couverture complète sera approfondie dans les parties Business/Data/Risk.

## 10. Blast radius

Définition opérationnelle : ensemble des objets potentiellement affectés par la défaillance ou modification d'un objet.

Un blast radius utile doit être filtré :

- relation type ;
- profondeur ;
- environment ;
- lifecycle ;
- criticality.

Sinon l'analyse renvoie tout le repository.

## 11. Critical path

Exemple MayaBank :

```text
Channel
→ API Gateway
→ Payment Orchestrator
→ Fraud Engine
→ Clearing Connector
```

Services transverses :

```text
Identity
Database
Network
Observability
```

L'analyse doit distinguer les dépendances bloquantes des dépendances de support.

## 12. Matrice d'impact

| Source | Dependency | Impact | Criticality | Owner |
|---|---|---|---|---|
| OpenShift | Payment Orchestrator | payment processing | critical | Payments |
| Kafka | Notifications | delayed notifications | medium | Channels |
| Identity | Payment API | cannot authenticate | critical | IAM |

## 13. Questions de gouvernance

- relation vérifiée quand ?
- par quel owner ?
- source automatique ou manuelle ?
- niveau de confiance ?
- relation current ou target ?

Une analyse d'impact est aussi fiable que ses relations.

## 14. Automation

Les capacités d'automatic discovery et auto-mapping mises en avant par l'offre peuvent accélérer la collecte. Elles ne suppriment pas :

- la validation sémantique ;
- l'ownership ;
- la sélection du bon niveau de granularité.

## 15. Cas MayaBank — fin de support WebSphere

```text
WebSphere
→ Legacy Payment Hub
→ Payment Validation
→ Instant Payment Service
→ Real-Time Payment Capability
```

Actions :

1. confirmer les applications réellement dépendantes ;
2. mesurer criticité ;
3. définir target standard ;
4. rattacher migration ;
5. définir date limite ;
6. suivre résorption.

## 16. Anti-patterns

- relations dessinées mais pas stockées ;
- tout relier par relation générique ;
- impact sans direction ;
- aucune distinction current/target ;
- aucune date de revue ;
- discovery accepté sans validation ;
- analyse à 8 niveaux sans filtre.

## 17. Entretien

**De quoi dépend la qualité d'une impact analysis ?**  
De la qualité des objets, de la sémantique des relations, de leur fraîcheur et du périmètre de requête.

**Pourquoi un graphe EAM est supérieur à un inventaire ?**  
Parce qu'il permet de parcourir les dépendances et de relier l'impact technique à l'impact métier.
