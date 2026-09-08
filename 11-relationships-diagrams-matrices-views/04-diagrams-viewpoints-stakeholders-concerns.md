# 04 — Diagrams, Viewpoints, Stakeholders & Concerns

## 1. Un diagramme répond à un concern

Le point de départ n’est pas la palette graphique.

Le point de départ est :

```text
Who needs to know what, to decide what?
```

Exemple MayaBank :

```text
Stakeholder : Head of Payments
Concern     : modernization risk
Question    : can Legacy Payment Gateway be retired safely?
```

## 2. Diagram vs model

Un modèle est un ensemble structuré d’objets et de relations.

Un diagramme est une représentation visuelle d’un sous-ensemble de ce modèle.

Le même objet peut apparaître dans plusieurs diagrammes sans duplication sémantique.

## 3. Viewpoint

Dans ce masterbook, un viewpoint est défini comme un **contrat de représentation** :

```text
Stakeholder
Concern
Allowed content
Scope rules
Visual rules
Decision intent
```

Ne pas supposer qu’un nom de viewpoint conceptuel correspond automatiquement à un objet ou écran HOPEX précis.

## 4. Executive viewpoint

Contenu typique :

```text
Strategic objectives
Capabilities
Major applications/platforms
Risks
Transformation initiatives
```

Exclure : endpoints, tables, pods, règles techniques détaillées.

## 5. Business viewpoint

```text
Capability
→ Value Stream
→ Process
→ Business Service
→ Information
```

Question : comment l’entreprise délivre-t-elle une valeur ?

## 6. Application cooperation viewpoint

```text
Applications
→ services/interfaces
→ major information flows
```

Question : quels systèmes collaborent et où sont les couplages ?

## 7. Technology viewpoint

```text
Applications
→ platforms
→ technology products
→ deployment/failure domains
```

Question : quelles dépendances technologiques conditionnent le fonctionnement ?

## 8. Data viewpoint

```text
Information/Data Domain
→ producer
→ store/source of truth
→ transformations
→ consumers
```

Question : où naît et circule l’information critique ?

## 9. Risk viewpoint

```text
Asset / Process
→ Risk
→ Control
→ Implementation
```

Question : quels risques sont couverts, par quels contrôles et où ?

## 10. Transformation viewpoint

```text
Current
→ gaps
→ initiatives
→ transition state
→ target
```

Question : comment passer de l’état actuel à la cible ?

## 11. Scope

Chaque vue doit expliciter :

```text
Domain
Geography
Business unit
Environment
Lifecycle state
Time horizon
```

## 12. Time horizon

Exemples :

```text
Current — Q3 2026
Transition — 2027
Target — 2028
```

Ne jamais utiliser uniquement la couleur pour distinguer ces horizons.

## 13. Inclusion rules

Exemple :

```text
Include only:
- critical applications
- production interfaces
- technologies with high blast radius
- active transformation initiatives
```

## 14. Exclusion rules

Exemple :

```text
Exclude:
- DEV-only dependencies
- low-level library dependencies
- temporary migration scripts
- pod-level runtime instances
```

## 15. Drill-down

Une bonne architecture visuelle est hiérarchique.

```text
L0 Executive
↓
L1 Domain Landscape
↓
L2 Cooperation / Dependencies
↓
L3 Solution Detail
```

Chaque niveau doit pouvoir être compris indépendamment.

## 16. Multiple concerns = multiple views

Ne pas tenter de faire tenir :

- stratégie ;
- process ;
- applications ;
- data ;
- network ;
- risks ;
- roadmap ;

sur un seul diagramme.

## 17. Storytelling

Une vue de décision peut suivre :

```text
Context
→ Problem
→ Current dependencies
→ Risk
→ Target change
→ Expected outcome
```

## 18. Hopex / repository principle

Les références publiques Bizzdesign mettent en avant le repository connecté, les visualisations, diagrammes et vues adaptées aux parties prenantes. Le détail des modèles disponibles dépend de la configuration et des solutions activées.

## 19. MayaBank — quatre vues minimales

### Executive Payment Modernization
Capability → current pain → target initiative.

### Application Cooperation
Channel → API Management → Payment Orchestrator → Fraud/Core/Clearing.

### Data Flow
Payment Instruction → Payment State → Clearing Result → Payment Status.

### Technology Dependency
Applications → OpenShift/Kafka/DB/IAM/Observability.

## 20. Validation avec stakeholder

Questions :

1. La vue répond-elle à votre question ?
2. Un objet important manque-t-il ?
3. Une relation paraît-elle fausse ?
4. La temporalité est-elle claire ?
5. Quelle décision prenez-vous à partir de cette vue ?

## 21. Anti-patterns

- viewpoint défini uniquement par la notation ;
- diagramme sans stakeholder ;
- scope implicite ;
- diagramme qui prétend répondre à dix questions ;
- drill-down absent ;
- architecture « cible » sans date ni hypothèse ;
- détail technique dans une vue exécutive.

## 22. Questions d’entretien

**Quelle différence entre view et viewpoint ?**  
Le viewpoint définit le besoin et les règles de représentation ; la view est une instance concrète appliquée à un scope.

**Pourquoi plusieurs vues sur les mêmes objets ?**  
Parce que les mêmes objets doivent répondre à des concerns différents sans être dupliqués dans le repository.

**Pourquoi expliciter les exclusions ?**  
Pour éviter qu’un lecteur interprète l’absence d’un élément comme une absence réelle dans l’architecture.