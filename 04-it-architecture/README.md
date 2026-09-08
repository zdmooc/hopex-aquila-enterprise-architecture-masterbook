# Partie IV — HOPEX IT Architecture

Cette partie transforme le repository HOPEX en outil de décision IT : **applications, interfaces, flows, technologies, deployment, lifecycle, obsolescence, current/target, impact analysis et roadmaps**.

Elle ne se limite pas à expliquer des écrans. Le but est de savoir construire et gouverner une architecture exploitable dans HOPEX, puis l'utiliser pour répondre à des questions de transformation.

## Chapitres

1. [Rôle et méthode HOPEX IT Architecture](01-it-architecture-role-and-method.md)
2. [Application Architecture](02-application-architecture.md)
3. [Interfaces, Interactions & Application Flows](03-interfaces-interactions-flows.md)
4. [Technology Architecture & Standards](04-technology-architecture-standards.md)
5. [Deployment Architecture & Environments](05-deployment-architecture-environments.md)
6. [Lifecycle, Obsolescence & Technical Debt](06-lifecycle-obsolescence-technical-debt.md)
7. [Current, Transition & Target Architecture](07-current-transition-target.md)
8. [Dependency & Impact Analysis](08-dependency-impact-analysis.md)
9. [IT Transformation Roadmaps](09-it-transformation-roadmaps.md)
10. [MayaBank IT Architecture Reference Model](10-mayabank-it-architecture-reference.md)
11. [IT Architecture Governance & Anti-patterns](11-governance-antipatterns.md)
12. [20 Labs + 30 Questions](12-labs-and-review.md)
13. [Sources officielles et publiques](13-official-sources.md)

## Compétences visées

À la fin de la Partie IV, l'architecte doit pouvoir :

- construire un inventaire applicatif canonique ;
- choisir une granularité utile ;
- mapper applications ↔ capabilities/processes ;
- représenter interfaces et flows sans confondre logique et implémentation ;
- cartographier technologies et standards ;
- relier application ↔ technology ↔ deployment ;
- distinguer vendor lifecycle et enterprise lifecycle ;
- détecter l'obsolescence et la dette ;
- analyser un blast radius ;
- distinguer HA et DR ;
- construire current / transition / target ;
- relier les gaps à une roadmap ;
- préparer une architecture review ;
- maintenir la frontière HOPEX ↔ CMDB ↔ API Management ↔ platform tooling.

## Mental model

```text
BUSINESS
Capability / Process
      ↓
APPLICATION
Application / Service / Interface / Flow
      ↓
TECHNOLOGY
Platform / Product / Standard
      ↓
DEPLOYMENT
Environment / Shared Services / Resilience
      ↓
GOVERNANCE
Lifecycle / Obsolescence / Risk
      ↓
TRANSFORMATION
Current → Transition → Target → Decommission
```

## MayaBank

Le cas fil rouge de cette partie est la modernisation des paiements :

```text
CURRENT
Legacy Payment Hub
+ WebSphere
+ Legacy MQ
+ point-to-point

TRANSITION
API Gateway
+ Payment Orchestrator
+ legacy clearing coexistence
+ Event Platform

TARGET
Payment Orchestrator
+ Fraud Decision Service
+ Event Streaming
+ OpenShift
+ Standard Observability
+ governed HA/DR
```

Toutes les architectures MayaBank sont pédagogiques et doivent être mappées au métamodèle réel du client.

## Ce que les sources publiques actuelles confirment

Le positionnement actuel HOPEX/Bizzdesign met en avant :

- applications, processes et business capabilities ;
- data flows et application interdependencies ;
- technology investments ;
- automatic discovery / mapping ;
- technology lifecycle ;
- business impact analysis ;
- application rationalization ;
- cloud migration.

Les ressources historiques HOPEX IT Architecture confirment aussi les concepts de scenario/application environment/deployment, mais ne sont pas utilisées comme preuve d'un écran Aquila 6.2 identique.

## Labs

20 labs couvrent :

- inventaire canonique ;
- capability mapping ;
- flows ;
- application environment ;
- technology catalog ;
- standards ;
- EOL ;
- deployment ;
- HA/DR ;
- SPOF ;
- current/target ;
- transition ;
- blast radius ;
- rationalisation ;
- roadmap ;
- decommission ;
- architecture board ;
- repository quality ;
- frontière HOPEX/CMDB.

## Règle professionnelle

```text
Une bonne IT Architecture HOPEX
≠ beaucoup de diagrammes

Une bonne IT Architecture HOPEX
= objets canoniques
+ relations fiables
+ lifecycles
+ standards
+ impacts
+ target
+ roadmap
+ gouvernance
```
