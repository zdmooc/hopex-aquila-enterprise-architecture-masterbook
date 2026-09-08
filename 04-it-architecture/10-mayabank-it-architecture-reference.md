# 10 — MayaBank IT Architecture Reference Model

## 1. Objectif

Ce chapitre assemble les concepts de la Partie IV dans un modèle de référence cohérent. Il ne prétend pas reproduire un métamodèle HOPEX propriétaire exact ; il fournit un **modèle pédagogique à mapper sur les MetaClasses disponibles dans l'instance**.

## 2. Scope fonctionnel

MayaBank modernise son domaine de paiements temps réel.

Capabilities concernées :

```text
Real-Time Payment Processing
Fraud Detection
Customer Authentication
Payment Notification
Operational Monitoring
```

## 3. Applications canoniques

### Payment Orchestrator

```text
Type        : Application
Owner       : Payments Domain
Criticality : Critical
Lifecycle   : Strategic
Target      : retained
Role        : payment orchestration
```

### Fraud Engine

```text
Owner       : Risk Technology
Criticality : Critical
Lifecycle   : Strategic
Role        : fraud decision
```

### Notification Hub

```text
Owner       : Channels
Criticality : High
Lifecycle   : Mainstream
Role        : customer notifications
```

### Legacy Payment Hub

```text
Owner       : Payments Legacy
Criticality : Critical
Lifecycle   : Retire
Target      : decommission
```

## 4. Interfaces

```text
Payment Initiation API
Provider : Payment Orchestrator
Consumers: Mobile Banking, Web Banking

Fraud Decision API
Provider : Fraud Engine
Consumer : Payment Orchestrator

Payment Status Event
Producer : Payment Orchestrator
Consumers: Notification Hub, Analytics, AML
```

## 5. Technologies

```text
Red Hat OpenShift
Category : Container Platform
Status   : Preferred
Owner    : Platform Engineering

Kafka / Event Streaming Technology
Category : Event Streaming
Status   : Preferred
Owner    : Integration Platform

Java LTS
Category : Runtime
Status   : Preferred

Legacy WebSphere
Category : Application Server
Status   : Deprecated
```

## 6. Platforms / shared services

```text
API Management Platform
Event Streaming Platform
Identity Platform
Observability Platform
Database Platform
Secrets Management Platform
```

Ces objets représentent des services/platforms stables de l'architecture, pas des pods individuels.

## 7. Current graph

```text
Mobile Banking
  ↓
Legacy Payment Hub
  ├─ Legacy Fraud Adapter
  ├─ Legacy MQ
  ├─ Oracle Database
  └─ WebSphere
  ↓
Clearing Connector
```

Risques :

- couplage fort ;
- middleware legacy ;
- DR partiellement manuel ;
- difficulté de scalabilité ;
- obsolescence de certains composants.

## 8. Target graph

```text
Mobile Banking / Web Banking
        ↓
API Management Platform
        ↓
Payment Initiation API
        ↓
Payment Orchestrator
  ├─ Fraud Decision API → Fraud Engine
  ├─ Database Service
  ├─ Identity Service
  └─ Payment Status Events
             ↓
      Event Streaming Platform
       ├─ Notification Hub
       ├─ AML Monitoring
       └─ Analytics
```

Runtime :

```text
Payment Orchestrator
→ OpenShift Platform
→ Observability Platform
→ Secrets Management
```

## 9. Current → target mapping

| Current object | Target object | Decision |
|---|---|---|
| Legacy Payment Hub | Payment Orchestrator | replace |
| Legacy Fraud Adapter | Fraud Decision API | replace |
| Legacy MQ | Event Streaming Platform | retire/migrate |
| WAS | OpenShift | migrate |
| manual monitoring | Observability Platform | standardize |

## 10. Transition 1

```text
Channels
→ API Gateway
→ Legacy Payment Hub

New Event Platform
← replicated non-critical events
```

Objectif : introduire les plateformes sans changer le core payment processing.

## 11. Transition 2

```text
Channels
→ API Gateway
→ Payment Orchestrator
→ Legacy Clearing Adapter

Payment status
→ Event Platform
```

Le legacy reste présent seulement là où la cible n'est pas prête.

## 12. Target deployment

```text
Site / Zone A
  ├─ OpenShift workloads
  ├─ API endpoints
  └─ Event platform nodes

Site / Zone B
  ├─ resilient workloads
  ├─ standby/active services
  └─ recovery capacity
```

La topologie exacte dépend des choix d'infrastructure du client.

## 13. Critical dependencies

```text
Payment Orchestrator
→ Identity
→ Fraud Engine
→ Database
→ Clearing
→ API platform
```

Les événements vers notification/analytics peuvent être non bloquants selon le design ; cette sémantique doit être documentée.

## 14. Lifecycle view

```text
Strategic
- Payment Orchestrator
- OpenShift
- Event Platform

Mainstream
- Notification Hub

Contain / Retire
- Legacy Payment Hub
- Legacy MQ
- WebSphere
```

## 15. Technology risk query

Question :

> Quelles capacités sont exposées par WebSphere ?

Parcours :

```text
WebSphere
→ Legacy Payment Hub
→ Instant Payment Process
→ Real-Time Payment Processing Capability
```

## 16. Application rationalization query

Question :

> Quelles applications du domaine Payments ont un faible target fit ?

Filtres :

```text
Domain = Payments
Target status = retire / replace
Criticality >= high
```

Résultat pédagogique : Legacy Payment Hub, legacy adapters.

## 17. Deployment impact query

Question :

> Si Identity Platform est indisponible, quels flux sont bloqués ?

Parcours :

```text
Identity Platform
← Payment API authentication
← Payment Orchestrator
← Channels
```

## 18. Roadmap

```text
M1 target approved
M2 platform foundations ready
M3 orchestrator pilot
M4 fraud migration
M5 full traffic migration
M6 legacy decommission
```

## 19. Gouvernance des objets

| Object family | Owner |
|---|---|
| Applications Payments | Payments Architecture |
| Shared Platforms | Platform Architecture |
| Interfaces | Domain/API owners |
| Technologies | Technology Architecture |
| Lifecycles | Architecture Governance |
| Runtime CIs | ServiceNow / Ops |

## 20. Ce que HOPEX ne doit pas remplacer

```text
OpenAPI details      → API Management / Git
Kafka runtime metrics → Observability
Pods / nodes          → OpenShift / CMDB
Incidents             → ITSM
Source code           → Git
```

HOPEX conserve les relations et décisions d'architecture nécessaires.

## 21. Vues recommandées

1. Application Landscape
2. Payment Application Environment
3. Integration/Flow View
4. Technology Usage Matrix
5. Deployment Architecture
6. Technology Obsolescence Heatmap
7. Current vs Target
8. Transformation Roadmap
9. Critical Dependency View
10. Executive Rationalization View

## 22. Critères de qualité

Le modèle MayaBank est acceptable si :

- aucun doublon applicatif ;
- chaque app critique a un owner ;
- chaque app critique a un lifecycle ;
- chaque technologie critique a un standard status ;
- current et target sont distingués ;
- legacy exit est traçable ;
- les dépendances bloquantes sont identifiées ;
- les vues réutilisent les objets canoniques.
