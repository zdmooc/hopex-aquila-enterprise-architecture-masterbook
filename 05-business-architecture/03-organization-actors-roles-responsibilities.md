# 03 — Organization, Actors, Roles & Responsibilities

## 1. Pourquoi l'organisation appartient à la Business Architecture

L'organisation permet de relier les décisions, responsabilités et capacités aux personnes ou unités qui les portent.

Elle répond à :

```text
Who owns?
Who performs?
Who decides?
Who is accountable?
Who must be consulted?
```

Mais elle ne doit jamais devenir l'unique structure du modèle métier.

## 2. Org-Unit, Actor et Role

Les noms exacts dépendent du métamodèle et des solutions HOPEX activées, mais la distinction conceptuelle reste essentielle.

### Org-Unit
Une unité organisationnelle relativement stable : direction, département, équipe, entité légale.

### Actor
Un acteur participant à une activité ou interaction.

### Role
Une responsabilité ou fonction tenue par un acteur ou une unité.

Exemple MayaBank :

```text
Org-Unit : Payments Operations
Role     : Payment Incident Manager
Actor    : personne ou groupe tenant ce rôle
```

## 3. Pourquoi ne pas modéliser uniquement l'organigramme

Un organigramme décrit la structure hiérarchique.

Une architecture métier doit aussi décrire :

- ownership de capabilities ;
- ownership de processus ;
- ownership de services ;
- responsabilités de décision ;
- collaboration transverse ;
- partenaires externes ;
- accountability de la donnée.

## 4. Ownership vs execution

Un owner n'est pas forcément celui qui exécute quotidiennement.

```text
Capability Owner
≠
Process Performer
≠
Application Owner
≠
Data Owner
```

Exemple :

```text
Fraud Decisioning capability
Owner: Head of Fraud Management

Investigate Fraud Alert process
Performed by: Fraud Operations

Fraud Engine application
Owner: Fraud IT Product Team
```

Cette séparation rend les arbitrages beaucoup plus clairs.

## 5. RACI dans le repository

Une matrice RACI peut être utile lorsqu'elle reste liée aux objets canoniques.

```text
R = Responsible
A = Accountable
C = Consulted
I = Informed
```

Exemple :

| Object | Payments | Fraud | Ops | Platform |
|---|---|---|---|---|
| Payment Orchestration Capability | A/R | C | C | C |
| Fraud Decisioning Capability | C | A/R | C | C |
| Event Streaming Platform | C | C | C | A/R |
| Payment Incident Process | C | C | A/R | C |

Éviter les RACI indépendantes dans Excel qui ne partagent aucune identité avec le repository.

## 6. Organisation fonctionnelle vs produit

### Fonctionnelle

```text
Development
Infrastructure
Operations
Security
```

### Produit/domaine

```text
Payments Product Team
Fraud Product Team
Customer Identity Team
```

Une transformation moderne peut passer d'un modèle à l'autre ou adopter une structure matricielle.

HOPEX peut servir à analyser ce changement si les capabilities, processes, applications et owners sont reliés.

## 7. External actors

Ne pas oublier :

- régulateurs ;
- payment schemes ;
- fournisseurs ;
- fintech partners ;
- cloud providers ;
- outsourcing partners ;
- clients entreprises ;
- merchants.

Exemple :

```text
Payment Scheme
→ imposes operational rules
→ exchanges payment messages
→ constrains service availability
```

## 8. Team Topologies et architecture

Sans transformer HOPEX en outil RH, on peut documenter les responsabilités architecturales de structures telles que :

- stream-aligned team ;
- platform team ;
- enabling team ;
- complicated-subsystem team.

Exemple MayaBank :

```text
Payments Product Team
→ owns Payment Orchestrator
→ contributes to Payment Orchestration capability

Platform Engineering
→ owns OpenShift Platform
→ owns Event Streaming Platform
```

## 9. Ownership lifecycle

Un owner doit rester à jour.

Contrôles possibles :

```text
Object without owner
Owner belongs to retired Org-Unit
Owner not reviewed > 12 months
Critical capability without accountable unit
Application owner ≠ known governance source
```

## 10. Organization changes

Lors d'une réorganisation :

1. identifier les Org-Units touchées ;
2. identifier leurs owned capabilities ;
3. identifier processus et services ;
4. identifier applications/données sous responsabilité ;
5. définir le target ownership ;
6. planifier la transition ;
7. conserver l'historique utile ;
8. supprimer les références obsolètes seulement après migration.

## 11. MayaBank — exemple de modèle

```text
Retail Banking
 └─ Digital Channels

Payments
 ├─ Payment Product Management
 ├─ Payment Engineering
 └─ Payment Operations

Risk
 └─ Fraud Management

Technology
 └─ Platform Engineering
```

Relations principales :

```text
Payment Product Management
→ owns Instant Payment Service

Payment Engineering
→ owns Payment Orchestrator

Payment Operations
→ performs Handle Payment Exception

Fraud Management
→ owns Fraud Decisioning capability

Platform Engineering
→ owns Event Streaming Platform
```

## 12. Anti-patterns

- une Org-Unit par projet temporaire ;
- réutiliser le nom d'un individu comme objet permanent ;
- utiliser l'organigramme pour représenter les capabilities ;
- owner vide sur les objets critiques ;
- 4 owners « principaux » pour la même décision ;
- ne jamais retirer les anciennes responsabilités ;
- confondre application owner et business owner.

## 13. Entretien

**Pourquoi relier organisation et capability ?**  
Pour identifier qui est accountable du développement et de la maturité d'une aptitude métier.

**Pourquoi séparer business owner et application owner ?**  
Parce qu'ils portent des responsabilités différentes : valeur/capability d'un côté, actif IT de l'autre.

**Quelle donnée organisationnelle faut-il éviter dans un EAM ?**  
Les détails RH volatils sans utilité architecturale ; le repository doit conserver le niveau nécessaire à la décision.