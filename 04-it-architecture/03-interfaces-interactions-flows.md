# 03 — Interfaces, Interactions & Application Flows

## 1. Pourquoi les flux sont centraux

Un inventaire d'applications ne suffit pas. Deux applications peuvent paraître indépendantes dans un portefeuille alors qu'elles sont fortement couplées par leurs échanges.

Le graphe de dépendances doit permettre de répondre à :

- qui appelle qui ?
- par quel mécanisme ?
- dans quel sens circule l'information ?
- quelle donnée est échangée ?
- quel protocole ou contrat est utilisé ?
- quel niveau de criticité porte le flux ?
- que se passe-t-il si le fournisseur disparaît ?

## 2. Application ≠ Interface ≠ Flow

Mental model :

```text
Application
  ↓ exposes / consumes
Interface
  ↓ participates in
Flow / Interaction
  ↓ transports
Information / Data
```

Les noms précis des objets HOPEX dépendent du métamodèle installé. Le principe sémantique reste stable.

## 3. Flux fonctionnel vs flux technique

### Flux fonctionnel

```text
Payment Orchestrator
→ Fraud Decision
```

Il exprime une dépendance fonctionnelle.

### Flux technique

```text
HTTPS POST /fraud/decision
OAuth2 client credentials
JSON payload
mTLS
```

Il décrit l'implémentation.

Le repository doit conserver le niveau nécessaire à la décision sans devenir une documentation OpenAPI complète.

## 4. Synchrone vs asynchrone

### Synchrone

```text
Payment API
→ Payment Orchestrator
→ Fraud Engine
← Fraud Decision
```

Points à analyser :

- timeout ;
- latence ;
- retry ;
- circuit breaker ;
- dépendance de disponibilité.

### Asynchrone

```text
Payment Orchestrator
→ PaymentAccepted event
→ Event Streaming Platform
→ Notifications / AML / Analytics
```

Points à analyser :

- topic / channel ;
- producteur ;
- consommateurs ;
- ordre ;
- duplication ;
- replay ;
- rétention ;
- schema compatibility.

## 5. Flow Set / regroupement de flux

Les ressources historiques HOPEX IT Architecture décrivent la possibilité de regrouper plusieurs interactions dans un ensemble de flux pour simplifier les représentations de scénarios.

Le principe est utile :

```text
10 interactions techniques
→ 1 regroupement lisible dans une vue de synthèse
```

Mais une agrégation visuelle ne doit pas supprimer les relations canoniques nécessaires aux analyses.

## 6. Application Environment

Les ressources publiques HOPEX montrent l'usage de diagrammes d'environnement applicatif générés à partir de scénarios de flux.

Objectif :

```text
Application centrale
  ├─ upstream systems
  ├─ downstream systems
  ├─ interfaces
  └─ flows
```

Cette vue est particulièrement utile en analyse d'impact.

## 7. Interface ownership

Une interface doit avoir une responsabilité claire.

Exemple :

```text
Interface : Payment Initiation REST API
Provider  : Payment Orchestrator
Owner     : Payments Domain
Consumers : Mobile Banking, Web Banking
Contract  : OpenAPI / governed externally
Lifecycle : Strategic
```

HOPEX n'a pas besoin de remplacer l'API Management. Il doit conserver la relation d'architecture.

## 8. API Management et HOPEX

Répartition recommandée :

```text
HOPEX
- service / interface logique
- provider
- consumers
- owner
- lifecycle
- capability/process support

API Manager
- OpenAPI
- policies
- quotas
- keys
- runtime analytics
- developer portal
```

Les deux sources peuvent être intégrées si la gouvernance le justifie.

## 9. Kafka et HOPEX

Ne pas créer un objet Application appelé `Kafka` si l'objet représente une technologie.

Modèle pédagogique MayaBank :

```text
Application: Payment Orchestrator
   ↓ publishes
Event Flow: Payment Status Events
   ↓ through
Platform: Event Streaming Platform
   ↓ implemented with
Technology: Kafka
```

Selon le niveau d'analyse, les topics peuvent être modélisés ou rester dans la plateforme d'event governance.

## 10. Criticité des flux

Critères possibles :

- business criticality ;
- confidentiality ;
- integrity ;
- availability ;
- latency target ;
- volume ;
- recovery expectations ;
- regulatory sensitivity.

Éviter un unique champ `Critical = Yes` si plusieurs décisions doivent être prises.

## 11. Dépendance transitive

```text
Mobile Banking
→ Payment API
→ Payment Orchestrator
→ Fraud Engine
→ Identity Service
```

Une panne d'Identity Service peut donc impacter un paiement même si Mobile Banking ne possède aucune relation directe avec lui.

La valeur du repository apparaît dans ce type d'analyse multi-hop.

## 12. Cas MayaBank — Instant Payment

Flux principal :

```text
Customer Channel
→ Payment Initiation API
→ Payment Orchestrator
→ Fraud Decision Service
→ Clearing Connector
→ External Payment Rail
```

Flux asynchrones :

```text
Payment Orchestrator
→ PaymentStatusChanged
→ Event Streaming Platform
→ Notification Hub
→ Analytics
→ AML Monitoring
```

## 13. Anti-patterns

- `Application A connected to Application B` sans sémantique ;
- une relation générique pour tous les échanges ;
- représenter le protocole comme une application ;
- dupliquer un flux par diagramme ;
- stocker tout le payload dans HOPEX ;
- oublier provider/consumer ;
- oublier le lifecycle d'une interface ;
- cacher les dépendances externes.

## 14. Questions d'entretien

**Pourquoi modéliser les flux ?**  
Pour comprendre le couplage, les dépendances et l'impact d'un changement ou d'une panne.

**HOPEX remplace-t-il un API Manager ?**  
Non. Il gouverne l'architecture et la dépendance ; l'API Manager gouverne l'exposition et le runtime API.

**Comment représenter Kafka ?**  
Selon son rôle : comme technologie ou plateforme supportant des échanges, jamais automatiquement comme application métier.
