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

1. HOPEX Aquila Foundations & Ecosystem
2. Repository, Metamodel & Object Model
3. UI, Navigation, Objects, Properties & Workspaces
4. HOPEX IT Architecture
5. Business Architecture
6. Capability Architecture
7. Business Process Analysis
8. Application Architecture
9. Information & Data Architecture
10. Technology & Infrastructure Architecture
11. Relationships, Diagrams, Matrices & Views
12. Enterprise Cartography & Dependency Analysis
13. IT Business Management & Application Portfolio
14. IT Portfolio Management & Transformation Roadmaps
15. Reports, Dashboards, Analysis & Decision Support
16. Repository Governance & Data Quality
17. Administration, Roles, Rights & Security
18. Customization, Extensions & Metamodel Governance
19. Import, Export & Data Exchange
20. REST, GraphQL, ServiceNow, MCP & AI Integrations
21. MayaBank Complete HOPEX Enterprise Model
22. Hands-on Labs, Interview Cases & Operational Playbook
23. English, Glossary & Question Bank
24. Official Sources, Training/Certification Mapping & Final Audit

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
