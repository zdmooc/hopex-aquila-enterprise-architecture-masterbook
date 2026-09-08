# 03 — Business alignment : Capability, Process, Service et Application

## 1. Pourquoi relier l’application au métier

Un catalogue applicatif sans contexte métier répond seulement à :

```text
Quelles applications existent ?
```

Une architecture d’entreprise doit aussi répondre :

```text
Pourquoi existent-elles ?
Quelles capacités supportent-elles ?
Quels processus dépendent d’elles ?
Quels services métier rendent-elles possibles ?
Quel impact métier provoque leur indisponibilité ou leur retrait ?
```

## 2. Chaîne de traçabilité

Modèle conceptuel MayaBank :

```text
Strategic Objective
        ↓
Business Capability
        ↓
Business Process / Business Service
        ↓
Application Service
        ↓
Application
        ↓
Technology / Deployment
```

Toutes les couches ne sont pas obligatoires dans chaque vue, mais le repository doit permettre de naviguer entre elles.

## 3. Capability ↔ Application

Exemple :

| Capability | Application |
|---|---|
| Payment Initiation | Digital Channel |
| Payment Execution | Payment Orchestrator |
| Fraud Prevention | Fraud Decision Service |
| Account Servicing | Core Account Service |
| Payment Clearing | Clearing Gateway |

### Utilité

- mesurer la couverture applicative d’une capability ;
- détecter redondance ou absence de support ;
- analyser l’impact d’une transformation ;
- aligner investissement IT et priorités métier.

## 4. Coverage ≠ ownership

Une application peut supporter une capability sans en être « propriétaire ».

La capability appartient au modèle métier ; l’application est un enableur.

## 5. Process ↔ Application

Exemple `Execute Instant Payment` :

```text
Receive Request          → Digital Channel
Authenticate             → IAM
Validate / Orchestrate   → Payment Orchestrator
Fraud Check              → Fraud Decision Service
Funds Check              → Core Account Service
Clear Payment            → Clearing Gateway
Notify                   → Notification Service
Reconcile                → Reconciliation Service
```

Le mapping activité ↔ application est souvent plus précis que process ↔ application.

## 6. Business Service ↔ Application Service

Exemple :

```text
Business Service
Instant Payment

Application Services
Submit Payment
Get Payment Status
Fraud Decision
Account Availability Check
Clearing Submission
```

Cette chaîne clarifie comment le SI réalise une promesse métier.

## 7. Service consumer/provider

Pour chaque service applicatif critique, identifier :

- provider ;
- consumer(s) ;
- purpose ;
- contract ;
- criticality ;
- availability expectation ;
- data exchanged.

Exemple :

```text
Service
Fraud Decision

Provider
Fraud Decision Service

Consumer
Payment Orchestrator
```

## 8. Many-to-many

Une application peut supporter plusieurs capabilities.

Une capability peut être supportée par plusieurs applications.

Cela crée des matrices utiles mais aussi un risque de sur-mapping.

Règle : ne créer une relation que si elle répond à une analyse connue.

## 9. Business redundancy

Si plusieurs applications supportent la même capability :

```text
Capability: Customer Notification
├─ Legacy SMS Gateway
├─ Email Platform
└─ Notification Service
```

ne pas conclure immédiatement à une duplication inutile.

Vérifier :

- canaux différents ;
- populations différentes ;
- transition en cours ;
- contraintes réglementaires ;
- niveaux de service ;
- localisation.

## 10. Functional scope

Le scope fonctionnel d’une application doit être lisible sans connaître son implémentation.

Exemple `Payment Orchestrator` :

```text
In scope
- validate payment execution request
- maintain execution state
- coordinate fraud/funds/clearing calls
- expose status
- manage technical timeout policy

Out of scope
- authenticate customer identity
- calculate fraud score
- execute core ledger posting
- send SMS directly
```

Cette discipline réduit les chevauchements.

## 11. Responsibility map

| Responsibility | Primary Application | Secondary/Supporting |
|---|---|---|
| Customer authentication | IAM | Digital Channel |
| Payment orchestration | Payment Orchestrator | — |
| Fraud decision | Fraud Decision Service | Payment Orchestrator consumes |
| Funds availability | Core Account Service | — |
| Clearing connectivity | Clearing Gateway | Payment Orchestrator consumes |
| Notification delivery | Notification Service | Event Streaming |

## 12. Architecture by bounded responsibility

Sans imposer DDD à HOPEX, l’architecte peut utiliser des responsabilités proches de domaines/bounded contexts pour éviter les applications « fourre-tout ».

Exemple :

```text
Payments
Fraud
Customer
Accounts
Notifications
Compliance
```

Le repository d’EA n’est pas un modèle de code DDD, mais il peut refléter des frontières fonctionnelles utiles.

## 13. Capability heatmap vers application impact

Scénario : `Payment Execution` devient stratégique.

Navigation :

```text
Strategic Capability
→ supported processes
→ supporting applications
→ technologies
→ initiatives
```

Résultat : identifier où investir.

## 14. Process criticality vers application criticality

Une application peut hériter d’une importance élevée parce qu’elle supporte :

- un processus critique ;
- une capability stratégique ;
- un service client 24/7 ;
- une obligation réglementaire.

La criticité ne doit cependant pas être calculée automatiquement sans méthode gouvernée.

## 15. Business service continuity

Pour un service métier `Instant Payment`, la continuité dépend d’une chaîne :

```text
Digital Channel
→ IAM
→ API Management
→ Payment Orchestrator
→ Fraud
→ Core Account
→ Clearing Gateway
```

Une disponibilité élevée du seul orchestrateur ne garantit pas la disponibilité du service end-to-end.

## 16. Service decomposition

Éviter un catalogue de centaines de services sans hiérarchie.

Niveaux possibles :

```text
Business Service
Instant Payment

Application Service
Submit Payment

Technical/API operation
POST /payments
```

Le troisième niveau peut rester dans l’API management/catalogue technique et être référencé plutôt que recopié intégralement dans HOPEX.

## 17. Customer journey ↔ applications

Exemple :

```text
Journey stage
Confirm payment

Business service
Instant Payment

Applications
Digital Channel
Payment Orchestrator
Notification Service
```

Utilité : analyser l’impact client d’une dette ou panne applicative.

## 18. Organization ↔ application

Distinguer :

```text
Business user organization
Application owner organization
Support organization
Provider organization
```

Un seul lien organisationnel peut être insuffisant pour une application critique.

## 19. Product ↔ application

Dans une banque, un produit métier `Instant Payment` peut dépendre de plusieurs applications.

Le produit n’est pas l’application.

Cette distinction est importante lors de :

- fusion d’offres ;
- changement de canal ;
- migration applicative ;
- externalisation.

## 20. MayaBank — matrice de couverture

| Capability | Process | Application principale |
|---|---|---|
| Customer Access | Initiate Payment | Digital Channel |
| Identity & Access | Authenticate Customer | IAM |
| Payment Execution | Execute Instant Payment | Payment Orchestrator |
| Fraud Prevention | Assess Payment Fraud | Fraud Decision Service |
| Account Servicing | Check Funds | Core Account Service |
| Clearing | Route & Clear Payment | Clearing Gateway |
| Customer Communication | Notify Payment Result | Notification Service |
| Financial Control | Reconcile Payment | Reconciliation Service |

## 21. Questions d’analyse

1. Une capability critique n’a-t-elle aucune application cible ?
2. Trois applications couvrent-elles la même responsabilité ?
3. Un processus stratégique dépend-il d’une application sunset ?
4. Une application critique n’a-t-elle aucun owner ?
5. Un service métier dépend-il d’une chaîne sans solution de continuité ?
6. Une transformation métier crée-t-elle une capability non supportée ?

## 22. Anti-patterns

- mapper toutes les applications à toutes les capabilities ;
- utiliser une application comme raccourci pour une capability ;
- relier un processus à une application sans préciser où elle intervient ;
- faire des services applicatifs une copie des endpoints ;
- déduire une ownership métier d’un simple lien technique ;
- dupliquer les mêmes services dans plusieurs diagrammes sans objet canonique.

## 23. Livrables de mission

- Capability × Application Matrix ;
- Process/Activity × Application Matrix ;
- Business Service × Application Service Map ;
- Responsibility Map ;
- Critical Business Service Dependency Chain ;
- Business Impact view pour transformation applicative.
