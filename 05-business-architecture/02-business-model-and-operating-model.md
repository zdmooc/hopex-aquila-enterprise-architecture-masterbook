# 02 — Business Model & Operating Model

## 1. Deux niveaux différents

Le **business model** explique comment l'entreprise crée, délivre et capture de la valeur.

L'**operating model** explique comment elle s'organise pour exécuter cette promesse de manière répétable.

```text
Business Model
Why / For whom / What value
        ↓
Operating Model
Capabilities / Organization / Processes / Information / Technology
```

HOPEX n'impose pas à lui seul une méthode unique de business model. Le repository doit surtout permettre de relier les décisions business aux objets d'architecture qui les matérialisent.

## 2. Business model : questions à capturer

Pour un domaine MayaBank, documenter au minimum :

- segment/stakeholder servi ;
- proposition de valeur ;
- produits/services ;
- canaux ;
- partenaires clés ;
- contraintes réglementaires ;
- economics majeurs ;
- risques structurants ;
- outcomes recherchés.

Le but n'est pas de recopier un Business Model Canvas dans HOPEX sans relations. Le but est d'exploiter les décisions.

## 3. Exemple MayaBank — Instant Payments

```text
Stakeholders
Retail customers
Merchants
Operations
Compliance

Value proposition
Instant, secure, 24x7 payment execution

Business services
Instant Payment Service
Payment Status Service
Exception Handling Service

Channels
Mobile Banking
Web Banking
Partner API

Key partners
Payment schemes
Identity provider
Fraud services
Clearing infrastructure
```

Puis relier ces informations aux capabilities et aux applications.

## 4. Operating model

Un operating model utile répond à :

```text
Who
What capability
Which process
Which information
Which location/channel
Which application support
Which governance
```

Exemple :

```text
Payments Operations
  owns → Payment Operations capability
  operates → Handle Payment Exception process
  consumes → Payment Investigation Information
  uses → Operations Portal
  monitored by → Payment Operations KPIs
```

## 5. Les cinq dimensions du modèle opératoire

### Capabilities
Ce que l'organisation doit savoir faire.

### Organization
Qui porte la responsabilité et les compétences.

### Processes
Comment le travail circule.

### Information
Quelles informations sont nécessaires pour agir et décider.

### Technology enablement
Quels systèmes permettent l'exécution.

Un sixième axe est souvent indispensable : **governance**.

## 6. Centralisé, fédéré, distribué

Une transformation peut choisir plusieurs modèles.

### Centralisé

```text
One fraud capability
One fraud platform
Central team
```

Avantages : standardisation, contrôle.

Risques : bottleneck, distance avec les métiers.

### Fédéré

```text
Central standards
Domain execution
Shared platform
```

Avantages : autonomie encadrée.

Risques : cohérence plus difficile.

### Distribué

```text
Each domain owns capability + process + technology
```

Avantages : vitesse locale.

Risques : duplication et fragmentation.

HOPEX permet surtout d'expliciter où se trouvent les capabilities, ownerships et systèmes afin de comparer ces modèles.

## 7. Operating model et transformation

Ne pas dessiner seulement :

```text
Current organization → Target organization
```

Analyser les écarts sur :

- capability ;
- skills ;
- process ;
- responsibility ;
- data ;
- technology ;
- governance ;
- metrics.

## 8. Exemple MayaBank — passage à l'event-driven

Current :

```text
Payments teams organized per legacy application
Manual incident correlation
Point-to-point integrations
```

Target :

```text
Payments domain ownership
Shared Event Streaming Platform
Product-aligned teams
End-to-end observability
Common API/event standards
```

Le changement n'est pas uniquement technique : l'operating model change aussi.

## 9. Principes de modélisation

### Principe 1
Un operating model doit être relié aux decisions de transformation.

### Principe 2
Une organisation n'est pas une capability.

### Principe 3
Une application ne doit pas définir à elle seule le périmètre d'une équipe cible.

### Principe 4
Les rôles temporaires de projet ne doivent pas polluer le modèle opératoire permanent.

### Principe 5
Chaque responsabilité importante doit avoir un owner identifiable.

## 10. Matrices utiles

### Capability × Org-Unit

| Capability | Payments | Fraud | Operations | Platform |
|---|---:|---:|---:|---:|
| Payment Orchestration | A/R | C | C | C |
| Fraud Decisioning | C | A/R | C | C |
| Payment Operations | C | C | A/R | C |
| Event Streaming | C | C | C | A/R |

### Capability × Application

Montre la couverture IT.

### Process × Org-Unit

Montre les responsabilités d'exécution.

### Service × Channel

Montre l'exposition client/partenaire.

## 11. Anti-patterns

- organiser le modèle autour de noms d'applications historiques ;
- confondre équipe et capability ;
- représenter uniquement la structure hiérarchique ;
- ignorer les partenaires externes ;
- oublier l'information et la gouvernance ;
- décrire la cible sans les gaps de compétences ;
- copier un canvas sans relations au repository.

## 12. Entretien

**Quelle différence entre business model et operating model ?**  
Le business model exprime la logique de valeur ; l'operating model décrit la manière structurée de délivrer cette valeur.

**Pourquoi l'EA s'intéresse-t-elle à l'operating model ?**  
Parce que les choix d'organisation, de capability, de process et de technologie doivent être cohérents pour rendre une transformation exécutable.