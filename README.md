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

### Partie II — Repository, Metamodel & Object Model
### Partie III — UI, Navigation, Objects, Properties & Workspaces
### Partie IV — HOPEX IT Architecture
### Partie V — Business Architecture
### Partie VI — Capability Architecture
### Partie VII — Business Process Analysis
### Partie VIII — Application Architecture
### Partie IX — Information & Data Architecture
### Partie X — Technology & Infrastructure Architecture
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
