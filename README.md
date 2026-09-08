# HOPEX Aquila — Enterprise Architecture Masterbook

> Construire, gouverner, analyser et industrialiser une architecture d’entreprise dans HOPEX Aquila, avec le cas fil rouge MayaBank.

Ce dépôt est un masterbook pratique consacré à **HOPEX Aquila** et à son usage par un architecte d’entreprise / architecte solution. Il combine compréhension de la plateforme, référentiel d’architecture, cartographie, gouvernance, portfolio, transformation, intégrations et pratique professionnelle.

Le cas fil rouge **MayaBank** représente une banque fictive qui modernise ses paiements, ses applications, ses données, son infrastructure et sa gouvernance d’architecture.

## Baseline produit vérifiée — septembre 2026

- HOPEX Core Back-End Aquila 6.2 — branche 62.18.x.
- HOPEX Aquila Web Front-End — branche 62.18.x.
- HOPEX REST API — branche 62.18.x.
- HOPEX GraphQL — branche 62.18.x.
- HOPEX MCP Server — add-on officiel.
- ServiceNow Integration — add-on officiel Aquila 6.2.
- Training database officielle disponible pour plusieurs solutions HOPEX, sous conditions d’accès/licence.

Les versions exactes sont documentées dans la Partie I et seront revérifiées dans la Partie XXIV.

## Programme — 24 parties

### Partie I — HOPEX Aquila Foundations & Ecosystem ✅
- [Ouvrir la Partie I](01-foundations/README.md)
- baseline produit 62.18.x, Core/Web/API/GraphQL/MCP/ServiceNow
- repository, personas, solutions, licences et training
- HOPEX ↔ ArchiMate ↔ TOGAF
- MayaBank, 7 labs, 20 questions de contrôle et sources officielles

### Partie II — Repository, Metamodel & Object Model ✅
- [Ouvrir la Partie II](02-repository-metamodel/README.md)
- MetaModel, MetaClass, MetaAttribute, MetaAssociation, MetaAssociationEnd
- identité, clés, déduplication, hiérarchies et classifications
- standard vs custom metamodel + MetaStudio + introspection GraphQL
- modèle canonique MayaBank, 12 labs et 30 questions de contrôle

### Partie III — UI, Navigation, Objects, Properties & Workspaces ✅
- [Ouvrir la Partie III](03-ui-navigation-workspaces/README.md)
- Web Front-End, workspaces, search, object pages, properties et relationships
- listes, filtres, diagrammes, matrices, favoris, collaboration et workflows
- MayaBank Navigation Playbook, 15 labs et 30 questions de contrôle

### Partie IV — HOPEX IT Architecture ✅
- [Ouvrir la Partie IV](04-it-architecture/README.md)
- applications, interfaces, flows, technologies, standards et deployment
- lifecycle, obsolescence, dette, HA/DR, current/transition/target et impact analysis
- roadmap IT + modèle MayaBank de référence + 20 labs et 30 questions de contrôle

### Partie V — Business Architecture ✅
- [Ouvrir la Partie V](05-business-architecture/README.md)
- business/operating model, organisation, capabilities, value streams et customer journeys
- services, produits, process architecture, information, stakeholders et strategic alignment
- assessments, gaps, roadmap + modèle MayaBank + 20 labs et 30 questions corrigées

### Partie VI — Capability Architecture ✅
- [Ouvrir la Partie VI](06-capability-architecture/README.md)
- taxonomy L0/L1/L2/L3, decomposition, ownership, maturity et strategic importance
- heatmaps + mappings capability↔applications/data/technologies/initiatives
- scénarios, priorisation, capability roadmaps, BIAN/MayaBank + 20 labs et 30 questions corrigées

### Partie VII — Business Process Analysis ✅
- [Ouvrir la Partie VII](07-business-process-analysis/README.md)
- 13 chapitres : process architecture, BPMN 2.0, governance lifecycle, risks/controls et performance
- mappings process↔capability/organization/applications/data/risks/controls/initiatives + gap/impact/bottleneck analysis
- process mining, Simulation Engine, frontière HOPEX↔Camunda/Pega/runtime BPM et repository blueprint MayaBank
- modèle MayaBank Instant Payment end-to-end + 24 labs + 40 questions corrigées + mission playbook

### Partie VIII — Application Architecture ✅
- [Ouvrir la Partie VIII](08-application-architecture/README.md)
- 13 chapitres : catalogue, granularity, business alignment, interfaces, integration et dependency mapping
- deployment, OpenShift/cloud, NFR, data responsibilities, lifecycle/obsolescence et current/transition/target
- modèle MayaBank avec 12 applications de référence, 10 matrices, 10 vues, 24 labs et 40 questions corrigées
- gouvernance, anti-patterns, mission playbook et sources publiques séparées des recommandations

### Partie IX — Information & Data Architecture ✅
- [Ouvrir la Partie IX](09-information-data-architecture/README.md)
- 13 chapitres : data domains, glossary, conceptual/logical/physical models, ownership et lifecycle
- functional/technical lineage, data quality/observability, classification/privacy/retention et persistence patterns
- Master/Reference Data, source of truth, APIs/events/batch/CDC et current/transition/target
- modèle MayaBank avec 12 matrices, 12 vues, 24 labs et 40 questions corrigées

### Partie X — Technology & Infrastructure Architecture ✅
- [Ouvrir la Partie X](10-technology-infrastructure-architecture/README.md)
- 13 chapitres : catalogue technologique, platform services, compute/OpenShift/cloud, réseau et stockage
- HA/DR, security/identity/secrets, observability/SRE/capacity, lifecycle/IT-Pedia et current/transition/target
- modèle MayaBank avec 9 technology domains, 8 platform services, 12 matrices et 12 vues
- GreenOps, 24 labs, 40 questions corrigées et sources publiques séparées des recommandations

### Partie XI — Relationships, Diagrams, Matrices & Views
### Partie XII — Enterprise Cartography & Dependency Analysis
### Partie XIII — IT Business Management & Application Portfolio
### Partie XIV — IT Portfolio Management & Transformation Roadmaps
### Partie XV — Reports, Dashboards, Analysis & Decision Support
### Partie XVI — Repository Governance & Data Quality
### Partie XVII — Administration, Roles, Rights & Security
### Partie XVIII — Customization, Extensions & Metamodel Governance
### Partie XIX — Import, Export & Data Exchange
### Partie XX — REST, GraphQL, ServiceNow, MCP & AI Integrations
### Partie XXI — MayaBank Complete HOPEX Enterprise Model
### Partie XXII — Hands-on Labs, Interview Cases & Operational Playbook
### Partie XXIII — English, Glossary & Question Bank
### Partie XXIV — Official Sources, Training/Certification Mapping & Final Audit

## Articulation avec ArchiMate

Le dépôt ArchiMate explique le **langage de modélisation** ; ce dépôt explique comment exploiter une **plateforme EAM** pour gouverner un référentiel vivant.

```text
ArchiMate
Concepts → Relations → Views → Semantics

HOPEX
Repository → Metamodel → Objects → Diagrams → Analysis → Governance → Roadmaps
```

L’objectif n’est pas de forcer chaque objet HOPEX à être un élément ArchiMate. Les deux niveaux seront reliés explicitement quand la correspondance est pertinente.

## Principe de construction

Chaque partie terminée doit fournir :

- concepts et vocabulaire ;
- fonctionnement dans HOPEX ;
- cas MayaBank ;
- erreurs et anti-patterns ;
- pratiques de gouvernance ;
- exercices ou labs quand ils sont réalisables sans licence ;
- distinction explicite entre fait produit vérifié, pratique recommandée et hypothèse pédagogique.

Aucune partie ne sera considérée terminée si elle n’est qu’un squelette.
