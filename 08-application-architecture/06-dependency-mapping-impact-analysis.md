# 06 — Dependency Mapping et Impact Analysis

## 1. Objectif

La cartographie des dépendances doit permettre de répondre rapidement à :

```text
Si cette application change, qui est impacté ?
Si cette interface disparaît, quels consumers cassent ?
Si cette technologie devient obsolète, quels services métier sont exposés ?
Si ce provider tombe, quels processus deviennent indisponibles ?
```

## 2. Dependency graph

Exemple MayaBank :

```text
Digital Channel
      ↓
API Management
      ↓
Payment Orchestrator
  ├→ IAM
  ├→ Fraud Decision Service
  ├→ Core Account Service
  └→ Clearing Gateway
      ↓
Event Streaming
  ├→ Notification Service
  └→ Reconciliation Service
```

Une simple liste d’applications ne permet pas cette analyse.

## 3. Direct dependency

```text
Application A → Application B
```

Exemple : Payment Orchestrator appelle Fraud Decision Service.

Documenter :

- direction ;
- reason ;
- interface ;
- criticality ;
- synchronous/asynchronous ;
- fallback éventuel.

## 4. Transitive dependency

Si :

```text
A → B → C
```

A peut être impactée par C même si aucun lien direct n’existe.

Le repository doit permettre d’explorer plusieurs niveaux sans supposer que toutes les dépendances transitives ont la même criticité.

## 5. Upstream vs downstream

Pour une application :

### Upstream
Ce dont elle dépend.

### Downstream
Ce qui dépend d’elle.

Cette distinction est fondamentale lors d’un incident ou changement.

## 6. Dependency types

Catégories pédagogiques :

- functional dependency ;
- API/interface dependency ;
- data dependency ;
- technology dependency ;
- deployment/platform dependency ;
- organizational/provider dependency ;
- security dependency ;
- operational dependency.

Ne pas réduire toutes ces relations à une flèche unique.

## 7. Business impact chain

Exemple :

```text
Kafka/Event Streaming outage
→ PaymentStatusChanged not propagated
→ Notification Service delayed
→ customer confirmation delayed
→ customer experience degraded
```

Autre chaîne :

```text
Clearing Gateway outage
→ Execute Instant Payment blocked
→ Instant Payment Business Service unavailable
→ regulatory/customer impact
```

## 8. Technology impact chain

```text
Unsupported Java version
→ Payment Orchestrator runtime risk
→ Payment Execution process
→ Instant Payment service
```

Le lien application ↔ technology est donc exploitable au-delà d’un simple inventaire.

## 9. Data impact chain

```text
Payment Status Store schema change
→ Payment Orchestrator
→ Payment Status API
→ Digital Channel
→ Customer Journey
```

## 10. Critical path

Identifier les dépendances sans lesquelles le service ne peut produire son résultat.

Pour Instant Payment :

```text
IAM
Payment Orchestrator
Fraud
Core Account
Clearing Gateway
```

Notification peut être importante sans être sur le chemin financier critique selon le design.

## 11. Optional dependency

Une dépendance peut dégrader le service sans le stopper.

Exemple : analytics en différé.

Qualifier :

```text
Critical
Important
Optional
```

ou modèle client équivalent.

## 12. Dependency blast radius

Question :

> Quel est le rayon d’impact si `Event Streaming` devient indisponible ?

Navigation :

```text
Event Streaming
→ consuming applications
→ business processes/services
→ capabilities
→ customers/stakeholders
```

## 13. Change impact analysis

Scénario : remplacement de `Payment Orchestrator`.

Vérifier :

1. capabilities supportées ;
2. processes/activities ;
3. providers consommés ;
4. downstream consumers ;
5. interfaces exposées ;
6. data stores ;
7. technologies ;
8. deployments ;
9. controls/risks ;
10. projects/initiatives.

## 14. Interface deprecation impact

Avant retrait d’une API :

```text
Interface v1
→ consumers
→ consumer owners
→ business services
→ migration status
→ target date
```

Un consumer inconnu est un risque de production.

## 15. Application decommission impact

Ne jamais retirer une application uniquement parce que son score est faible.

Avant retrait :

- consumers ;
- providers ;
- data ownership ;
- archives ;
- regulations ;
- business capability coverage ;
- scheduled jobs ;
- batch/file integrations ;
- user populations ;
- operational procedures.

La décision portefeuille sera approfondie en Partie XIII.

## 16. SPOF logique

Un SPOF n’est pas seulement un serveur unique.

Exemple :

```text
All payment channels
→ single Payment Orchestrator logical service
```

Même si plusieurs pods existent, une erreur logicielle ou dépendance unique peut créer un SPOF logique.

## 17. Shared platform concentration

```text
Payments
Fraud
Notifications
Customer
→ same OpenShift cluster
```

Le partage peut être rationnel mais crée un domaine de défaillance commun à analyser.

## 18. Dependency confidence

Chaque relation découverte automatiquement ou manuellement devrait avoir une provenance lorsque c’est utile :

```text
Source
Owner declaration
API gateway discovery
CMDB
Code analysis
Network observation
Architecture review
```

et éventuellement une date de validation.

## 19. Stale dependency

Une dépendance non revue depuis plusieurs années peut être plus dangereuse qu’une relation absente car elle donne une fausse confiance.

Mesures :

- last reviewed date ;
- confidence ;
- source ;
- owner.

## 20. Dependency matrix

| Consumer | Provider | Interface | Criticality | Failure effect |
|---|---|---|---|---|
| Payment Orchestrator | Fraud Decision Service | Fraud API | Critical | payment cannot proceed |
| Payment Orchestrator | Core Account Service | Funds API | Critical | payment rejected/delayed |
| Payment Orchestrator | Clearing Gateway | Clearing Interface | Critical | execution blocked |
| Notification Service | Event Streaming | Payment Status Event | High | notification delayed |
| Analytics | Event Streaming | Payment Events | Medium | analytics delayed |

## 21. Scenario — Fraud unavailable

### Immediate

Payment Orchestrator cannot obtain decision.

### Business decision

Do not silently bypass fraud control.

### Options

- fail closed ;
- controlled degraded mode if approved ;
- queue/retry if business SLA permits ;
- operational intervention.

Le choix est une politique métier/security, pas une décision purement technique.

## 22. Scenario — Notification unavailable

Payment financial state remains final.

Target behavior :

```text
Event retained
→ retry
→ dead-letter / repair
→ observability
```

sans rejouer le paiement.

## 23. Heatmap de dépendances

Dimensions possibles :

- business criticality ;
- number of consumers ;
- lifecycle risk ;
- synchronous coupling ;
- data sensitivity ;
- change frequency.

Le score exact relève de la méthode client.

## 24. Anti-patterns

- tout relier à tout ;
- utiliser seulement des dépendances transverses non typées ;
- ignorer batch/file ;
- ignorer direct DB ;
- ne modéliser que le happy path ;
- dépendances sans direction ;
- analyser un retrait sans consumers ;
- considérer multi-pod = absence de SPOF ;
- croire qu’un graph automatiquement découvert est toujours sémantiquement correct.

## 25. Livrables

- Application Dependency Graph ;
- Critical Path View ;
- Upstream/Downstream Analysis ;
- Interface Deprecation Impact ;
- Application Decommission Impact ;
- Technology Obsolescence Blast Radius ;
- Shared Platform Concentration View ;
- Dependency Quality Dashboard.
