# 02 — Application Architecture

## 1. L’application comme objet d’architecture

Une application ne doit pas être définie uniquement par son nom ou son serveur. Dans le repository, elle doit être décrite par son rôle durable dans le SI.

Exemple MayaBank :

```text
Application : Payment Orchestrator
Domain      : Payments
Owner       : Payments Domain
Criticality : Critical
Lifecycle   : Strategic
Current     : active
Target      : retained / modernized
```

## 2. Questions à poser pour chaque application

- quel besoin ou processus supporte-t-elle ?
- quelles capacités métier sert-elle ?
- quels services expose-t-elle ?
- quelles interfaces possède-t-elle ?
- quelles applications appelle-t-elle ?
- quelles données manipule-t-elle ?
- quelles technologies utilise-t-elle ?
- où est-elle déployée ?
- quel est son lifecycle ?
- existe-t-il un plan de remplacement ?

## 3. Granularité

Trop gros :

```text
Payments Platform
```

Trop fin :

```text
payment-api
payment-worker
payment-validator
payment-audit
payment-ui
```

Une granularité utile doit correspondre à un niveau où :

- un owner existe ;
- un lifecycle existe ;
- un impact métier peut être analysé ;
- une décision d’investissement peut être prise.

## 4. Application vs composant technique

Ne pas transformer chaque librairie ou runtime en application.

```text
Payment Orchestrator = application logique
Spring Boot            = technologie
OpenShift              = plateforme
Kafka                   = technologie / plateforme
```

La MetaClass exacte dépend du métamodèle, mais les responsabilités restent distinctes.

## 5. Application et capability

Le mapping application ↔ capability permet de répondre à :

- quelle capability dépend de quelles applications ?
- où existe-t-il trop d’applications pour une même capability ?
- où une capability critique dépend-elle d’une application obsolète ?

Exemple :

```text
Capability: Real-Time Payment Processing
    ↓ supported by
Payment Orchestrator
Fraud Engine
Notification Hub
```

## 6. Application et processus

Une application peut supporter plusieurs processus et un processus peut dépendre de plusieurs applications.

```text
Execute Instant Payment
  ├─ Payment Orchestrator
  ├─ Fraud Engine
  ├─ Customer Identity
  └─ Notification Hub
```

Cette relation permet l’analyse d’impact métier.

## 7. Lifecycle applicatif

Un modèle minimal :

```text
Emerging
Strategic
Mainstream
Contain
Retire
```

Les valeurs réelles sont celles de la configuration HOPEX du client.

Le lifecycle doit servir à décider, pas seulement à colorer un tableau.

## 8. Obsolescence applicative

Une application n’est pas obsolète uniquement parce qu’elle est ancienne.

Critères possibles :

- technologie non supportée ;
- coût élevé ;
- faible maintenabilité ;
- faible alignement métier ;
- risque sécurité ;
- absence de compétences ;
- duplication fonctionnelle ;
- dépendance à un produit en fin de vie.

## 9. Rationalisation

Matrice simple :

| Valeur métier | Santé technique | Décision |
|---|---|---|
| haute | haute | invest |
| haute | faible | modernize |
| faible | haute | tolerate / assess |
| faible | faible | retire |

Le modèle doit rester traçable aux objets du repository.

## 10. Cas MayaBank

### Current

```text
Legacy Payment Hub
Batch Clearing Adapter
Legacy Fraud Adapter
Payment DB
```

### Target

```text
Payment Orchestrator
API Gateway
Event Streaming Platform
Fraud Decision Service
Cloud-native database service
```

### Question d’architecture

Quels éléments sont réellement remplacés, lesquels sont modernisés et lesquels restent en coexistence ?

## 11. Vue recommandée

```text
Capability
   ↓
Business Process
   ↓
Applications
   ↓
Interfaces
   ↓
Technologies
```

Ne montrer que ce qui répond à la question.

## 12. Anti-patterns

- une application par environnement ;
- une application par microservice sans raison de gouvernance ;
- lifecycle renseigné sans date ni owner ;
- application dupliquée parce qu’un diagramme la représente différemment ;
- confondre application logique et produit logiciel ;
- stocker la target comme simple commentaire.

## 13. Questions d’entretien

**Comment rationaliser un portefeuille applicatif ?**  
En croisant valeur métier, santé technique, coût, risque, duplication et lifecycle, puis en reliant chaque décision à une transformation.

**Pourquoi mapper les applications aux capabilities ?**  
Pour raisonner en termes de valeur métier plutôt qu’en inventaire technique.

**Que faut-il protéger pendant une migration ?**  
La traçabilité entre current, transition, target et impacts sur les processus/capabilities.
