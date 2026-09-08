# 02 — Application Catalog, granularity et modèle canonique

## 1. Pourquoi commencer par un modèle canonique

Une architecture applicative fiable repose sur un catalogue où chaque application représente **un seul actif logique identifiable**.

Sans cette règle, les mêmes systèmes apparaissent sous des noms différents selon :

- projets ;
- équipes ;
- environnements ;
- contrats ;
- technologies ;
- anciens acronymes ;
- variantes locales.

Le résultat est une cartographie inutilisable.

## 2. Application ID Card

Pour MayaBank, chaque application critique doit disposer au minimum de :

| Champ | Exemple |
|---|---|
| Canonical Name | Payment Orchestrator |
| Short Name | PAY-ORCH |
| Purpose | Orchestration of instant-payment execution |
| Business Domain | Payments |
| Application Owner | Payments IT |
| Business Owner | Payments Product |
| Criticality | Critical |
| Lifecycle | Production |
| Hosting Model | OpenShift |
| Main Interfaces | REST / Events |
| Key Data | Payment Execution State |
| Target Direction | Strategic / modernize |

Les noms de champs réels sont à aligner au métamodèle client.

## 3. Les pièges de granularité

### Trop haut

```text
Application = Payments
```

Trop vague pour comprendre responsabilités et impacts.

### Trop bas

```text
Application = payment-validation-service-pod-7d8b9
```

Trop technique et instable pour un repository d’EA.

### Niveau utile

```text
Application = Payment Orchestrator
```

avec éventuellement une décomposition contrôlée vers des composants si nécessaire.

## 4. Application, module et composant

Une application peut regrouper plusieurs modules cohérents lorsqu’ils partagent :

- une responsabilité commune ;
- un cycle de vie coordonné ;
- un ownership commun ;
- une gouvernance commune.

Créer des objets séparés lorsque les éléments ont :

- des owners différents ;
- des cycles de vie indépendants ;
- des consommateurs indépendants ;
- des déploiements réellement autonomes ;
- des responsabilités métier clairement distinctes.

## 5. SaaS et progiciels

Pour un SaaS, l’application reste un actif logique du SI même si l’infrastructure n’est pas exploitée par MayaBank.

Exemple :

```text
Fraud SaaS Platform
Provider = external vendor
Hosting = SaaS
Data exchange = API
Business owner = Fraud
```

Ne pas créer un faux serveur ou cluster pour représenter ce que l’entreprise ne maîtrise pas.

## 6. COTS / package

Distinguer :

```text
Business application
Core Banking Platform

Software product / package
Vendor Product X

Version
X.Y
```

La relation application ↔ produit logiciel permet de changer de version ou de package sans perdre l’identité métier de l’application.

## 7. Application interne développée sur mesure

Exemple :

```text
Payment Orchestrator
Type = Custom application
Runtime = Java
Platform = OpenShift
Repository = source-code repository reference
```

Le dépôt Git n’est pas l’application elle-même dans le repository d’EA.

## 8. Application partagée

Certaines applications ont un scope transversal :

- IAM ;
- API Management ;
- Event Streaming ;
- Notification ;
- Observability.

Elles doivent être modélisées comme services partagés, sans être artificiellement dupliquées dans chaque domaine.

## 9. Application composite

Une application composite peut agréger plusieurs capacités internes.

Exemple :

```text
Digital Banking Platform
├─ Customer Access
├─ Payment Initiation
├─ Profile Management
└─ Secure Messaging
```

La décomposition doit répondre à un besoin concret d’analyse.

## 10. Legacy application

Ne pas réduire une application legacy à :

```text
Legacy = bad
```

Documenter :

- responsabilité actuelle ;
- utilisateurs ;
- dépendances ;
- données critiques ;
- technologies ;
- contraintes de sortie ;
- risques ;
- coûts ou valeur dans les parties portfolio ;
- trajectoire cible.

## 11. Shadow IT

Lorsqu’une application non gouvernée est découverte :

1. créer ou identifier l’objet canonique ;
2. déterminer owner et scope ;
3. qualifier risques/données ;
4. décider intégration au portefeuille, migration ou retrait ;
5. éviter de la supprimer du modèle uniquement parce qu’elle n’est pas conforme.

Le repository doit représenter la réalité avant de représenter la cible.

## 12. Environnement ≠ application

Mauvais :

```text
PAY-ORCH-DEV
PAY-ORCH-UAT
PAY-ORCH-PROD
```

comme trois applications distinctes.

Préférer :

```text
Application
Payment Orchestrator

Deployments
DEV
UAT
PROD
```

sauf si les variantes sont réellement des produits fonctionnels distincts.

## 13. Région ≠ application

Même règle pour :

```text
Payment Orchestrator France
Payment Orchestrator Germany
```

Ne créer deux applications que si responsabilités, versions, fonctionnel ou ownership justifient cette distinction.

## 14. Duplicate detection

Avant création, comparer :

```text
Name
Aliases
Acronym
Business domain
Owner
Purpose
Provider/vendor
Lifecycle
Known integrations
```

Un workflow de création d’application devrait intégrer cette vérification.

## 15. Naming convention MayaBank

Nom fonctionnel lisible :

```text
Payment Orchestrator
Fraud Decision Service
Clearing Gateway
Notification Service
```

Éviter les noms uniquement techniques :

```text
APP00394
MYSVC01
NEWPAY2
FOO-PROD
```

L’identifiant technique peut exister comme attribut séparé.

## 16. Ownership

Distinguer selon le besoin :

- Business Owner ;
- Application Owner ;
- Technical Owner ;
- Operational Owner ;
- Data Owner ;
- Vendor/Provider.

Un seul champ `Owner` peut masquer des responsabilités différentes.

## 17. Criticality

La criticité doit être fondée sur l’impact, pas sur la visibilité politique de l’application.

Dimensions possibles :

- impact client ;
- impact financier ;
- impact réglementaire ;
- disponibilité requise ;
- données sensibles ;
- dépendance d’autres services.

Les méthodes exactes seront reprises dans les parties portfolio/risk.

## 18. Lifecycle

Une séquence pédagogique :

```text
Idea
→ Planned
→ Build
→ Production
→ Restricted Change
→ Sunset
→ Retired
```

Les statuts réels doivent être vérifiés dans l’environnement HOPEX client.

## 19. Catalogue minimal viable

Pour démarrer une mission :

```text
Application
+ purpose
+ domain
+ owner
+ lifecycle
+ criticality
+ key business mappings
+ key dependencies
```

Ne pas demander 150 attributs dès la première campagne.

## 20. Qualité du catalogue

Mesures utiles :

- % applications avec owner ;
- % avec purpose ;
- % avec lifecycle ;
- % avec business mapping ;
- % avec dependency mapping ;
- doublons détectés ;
- objets sans revue depuis > 12 mois.

## 21. Cas MayaBank — catalogue de départ

| Application | Domain | Purpose | Criticality |
|---|---|---|---|
| Digital Channel | Customer | Initiate customer interactions | High |
| API Management | Integration | Secure/expose APIs | Critical |
| IAM | Security | Authentication/authorization | Critical |
| Payment Orchestrator | Payments | Coordinate payment execution | Critical |
| Fraud Decision Service | Fraud | Produce fraud decision | Critical |
| Core Account Service | Core Banking | Account and funds services | Critical |
| Clearing Gateway | Payments | Connect clearing network | Critical |
| Notification Service | Shared | Send customer notifications | High |
| Reconciliation Service | Operations | Detect discrepancies | High |
| Event Streaming | Integration | Event distribution platform | Critical |

## 22. Fait produit vérifié

Les pages publiques Bizzdesign Hopex de l’offre Enterprise Architecture mentionnent explicitement `Application Catalog & Lifecycle` et `Application Architecture Modeling`. Le playbook public d’application rationalization insiste également sur l’inventaire des applications, lifecycles, échanges, technologies, capabilities, ownership et workflow de contrôle.

Ces éléments confirment le principe du catalogue connecté ; ils ne définissent pas à eux seuls le métamodèle détaillé de chaque client.

## 23. Checklist

Avant de considérer un catalogue exploitable :

1. objets canoniques ;
2. aliases gérés ;
3. owner défini ;
4. purpose compréhensible ;
5. domain défini ;
6. lifecycle défini ;
7. criticality qualifiée ;
8. environnements non dupliqués comme applications ;
9. liens métier présents ;
10. revue périodique organisée.
