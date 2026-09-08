# 01 — Application Architecture : rôle, périmètre et méthode

## 1. Objectif

L’Application Architecture décrit **comment les capacités et processus métier sont supportés par un ensemble cohérent d’applications, de services applicatifs, d’interactions et de dépendances**.

Dans ce masterbook, elle n’est ni :

- un simple inventaire d’applications ;
- une CMDB ;
- un catalogue de serveurs ;
- un diagramme de microservices exhaustif ;
- une vue d’infrastructure ;
- une matrice de portefeuille uniquement financière.

Elle sert à répondre à des décisions d’architecture :

```text
Quel système porte quelle responsabilité ?
Quelles applications supportent quel processus/capability ?
Quelles applications échangent quelles informations ?
Où se trouvent les dépendances critiques ?
Quelles responsabilités doivent être découplées ?
Quelles applications doivent évoluer lors d’une transformation ?
Quelle architecture cible permet de réduire couplage et dette ?
```

## 2. Positionnement dans le masterbook

```text
Partie IV
HOPEX IT Architecture
= vue transverse IT : applications + technologies + déploiement + HA/DR + roadmap

Partie VIII
Application Architecture
= approfondissement du modèle applicatif et de ses interactions

Partie IX
Information & Data Architecture
= données, information, modèles et gouvernance data

Partie X
Technology & Infrastructure Architecture
= plateformes, runtimes, compute, network, storage, cloud, OpenShift

Partie XIII
IT Business Management & Application Portfolio
= portefeuille, coûts, valeur, risques, rationalisation
```

La Partie VIII évite donc de transformer l’architecture applicative en exercice APM.

## 3. Application Architecture vs Application Portfolio Management

Application Architecture :

```text
Structure
Responsabilités
Services
Interactions
Interfaces
Dépendances
Déploiements
NFR
Current / Target
```

Application Portfolio Management :

```text
Inventaire
Ownership
Lifecycle
Business value
Technical fitness
Cost
Risk
Rationalization
Investment decision
```

Les deux domaines utilisent le même repository mais répondent à des décisions différentes.

## 4. Application vs capability

Une capability décrit **ce que l’entreprise sait faire**.

Une application décrit **un actif SI qui supporte une partie de cette capacité**.

Exemple MayaBank :

```text
Capability
Payment Execution

supported by

Applications
Payment Orchestrator
Core Account Service
Fraud Decision Service
Clearing Gateway
Notification Service
```

Une capability ne doit pas être renommée avec le nom d’une application.

## 5. Application vs process

Le processus décrit le déroulement du travail.

L’application fournit des fonctions nécessaires aux activités du processus.

```text
Process
Execute Instant Payment

Activity
Run Fraud Check

Application
Fraud Decision Service
```

Le mapping doit être suffisamment précis pour permettre l’impact analysis.

## 6. Application vs service applicatif

Une application est un actif logique gouverné.

Un service applicatif représente une capacité fonctionnelle exposée ou consommable par d’autres acteurs/applications.

Exemple :

```text
Application
Payment Orchestrator

Application services
Validate Payment
Create Payment Execution
Get Payment Status
Cancel Eligible Payment
```

Le modèle exact dépend du métamodèle HOPEX activé chez le client. Dans le masterbook, les termes restent conceptuels lorsqu’une métaclasse précise n’est pas vérifiée.

## 7. Application vs composant logiciel

Ne pas confondre :

```text
Application métier
Payment Orchestrator

avec

software component/runtime
Java service
Spring Boot module
Kafka client
PostgreSQL driver
```

Le niveau composant est utile lorsque la décision d’architecture l’exige, mais ne doit pas polluer les vues d’entreprise.

## 8. Application vs technologie

```text
Application
Payment Orchestrator

Technology / platform
OpenShift
Java
Kafka
PostgreSQL
API Gateway
```

L’application est la responsabilité logique ; la technologie est un moyen de l’implémenter ou de l’exécuter.

## 9. Application vs deployment

Une même application peut être déployée dans plusieurs environnements :

```text
DEV
INT
PREPROD
PROD
DR
```

et éventuellement plusieurs sites/régions.

Le modèle applicatif doit rester distinct de ses instances et déploiements physiques.

## 10. Les six questions fondamentales

Pour chaque application critique, l’architecte doit pouvoir répondre :

1. Quelle responsabilité métier porte-t-elle ?
2. Quels services/fonctions expose-t-elle ?
3. Quelles applications consomme-t-elle ?
4. Quelles données lit-elle, crée-t-elle ou maîtrise-t-elle ?
5. Où et comment est-elle déployée ?
6. Quels NFR structurants conditionnent son design ?

## 11. Méthode de construction en dix étapes

### Étape 1 — définir le scope métier

Exemple : `Instant Payments`.

### Étape 2 — identifier les applications canoniques

Search Before Create dans le repository.

### Étape 3 — attribuer une responsabilité claire

Éviter les applications décrites comme :

```text
Does many payment things
```

Préférer :

```text
Orchestrates instant-payment execution state and coordinates domain services.
```

### Étape 4 — mapper capabilities/processes

### Étape 5 — identifier services et interfaces

### Étape 6 — cartographier interactions et flux

### Étape 7 — relier les données critiques

### Étape 8 — relier technologies et déploiements nécessaires à la décision

### Étape 9 — documenter les NFR structurants

### Étape 10 — produire current, transition et target

## 12. Niveaux de vue recommandés

### L0 — Application Landscape

Domaines et grandes applications.

### L1 — Application Cooperation

Interactions principales entre applications.

### L2 — Application Service / Interface

Services exposés, contrats et responsabilités.

### L3 — Solution Detail

Composants internes, endpoints, topics, stores et déploiements si nécessaire.

Le niveau L3 ne doit pas devenir la norme pour toute cartographie d’entreprise.

## 13. Principe de responsabilité unique

Une application ne doit pas être modélisée seulement par son nom historique.

Documenter :

```text
Purpose
Business scope
Owner
Criticality
Key services
Key consumers/providers
Key data
Lifecycle state
Target direction
```

## 14. Cas MayaBank

Périmètre de référence :

```text
Digital Channel
API Management
IAM
Payment Orchestrator
Fraud Decision Service
Core Account Service
Clearing Gateway
Notification Service
Reconciliation Service
Event Streaming
Observability Platform
```

Objectif : montrer comment un paiement instantané traverse un ensemble d’applications sans confondre process, application, technology et infrastructure.

## 15. Faits produit vérifiés

Les pages publiques Bizzdesign/HOPEX consultées en septembre 2026 confirment que l’offre couvre notamment :

- Application Catalog & Lifecycle ;
- Application Architecture Modeling ;
- Deployment Architecture & infrastructure modeling ;
- repository partagé ;
- assessments, workflows, dashboards et APIs ouvertes selon offres/modules.

Le détail des objets, écrans, profils et licences dépend de la configuration client.

## 16. Bonnes pratiques du masterbook

- modéliser des objets canoniques, pas des copies de formes ;
- écrire une responsabilité avant de dessiner une dépendance ;
- relier chaque application au métier qu’elle supporte ;
- distinguer interaction logique et protocole technique ;
- éviter les diagrammes illisibles ;
- documenter la source des relations importées ;
- faire vivre current et target ensemble pendant une transformation.

## 17. Anti-patterns immédiats

- application = serveur ;
- application = namespace Kubernetes ;
- capability = application ;
- interface = simple trait non gouverné ;
- toute relation = « flow » sans sémantique ;
- un diagramme global de 300 applications ;
- architecture cible sans trajectoire ;
- dépendances déclarées sans provider/consumer ;
- objets dupliqués par projet.

## 18. Questions d’entretien

**Quelle différence entre application architecture et APM ?**  
La première structure responsabilités, services, interactions et dépendances ; l’APM gouverne le portefeuille et les décisions d’investissement/rationalisation.

**Pourquoi séparer application et technology ?**  
Parce que la responsabilité métier/logique doit pouvoir survivre au remplacement d’un runtime ou d’une plateforme.

**À quel niveau modéliser un microservice ?**  
Seulement si la décision requiert ce niveau. Pour une cartographie d’entreprise, l’application ou le service applicatif suffit souvent.

**Quel est le principal risque d’une cartographie applicative ?**  
Accumuler des dépendances non gouvernées et non maintenues qui deviennent rapidement fausses.
