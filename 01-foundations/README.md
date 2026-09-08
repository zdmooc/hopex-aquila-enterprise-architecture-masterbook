# Partie I — HOPEX Aquila Foundations & Ecosystem

## Objectif

Cette première partie donne le socle nécessaire avant de manipuler le repository ou de construire des cartographies. Elle répond à cinq questions :

1. Qu'est réellement HOPEX Aquila ?
2. Quels composants composent la plateforme actuelle ?
3. Quelles familles de solutions s'appuient sur le repository commun ?
4. Comment distinguer langage de modélisation, référentiel EAM, solution métier et intégration ?
5. Comment allons-nous utiliser MayaBank comme fil rouge ?

## Résultat attendu

À la fin de cette partie, le lecteur doit pouvoir expliquer HOPEX sans le réduire à « un outil de dessin » et sans le confondre avec ArchiMate ou TOGAF.

Il doit être capable de présenter la chaîne suivante :

```text
HOPEX Platform
→ Core Back-End
→ Repository
→ Web Front-End / Workspaces
→ Solutions métier et architecture
→ GraphQL / REST / intégrations
→ analyses, rapports, cartographies et gouvernance
```

## Baseline produit vérifiée — 8 septembre 2026

| Composant | Baseline observée | Rôle principal |
|---|---|---|
| HOPEX Core Back-End Aquila 6.2 | 62.18.0+774 — 03/09/2026 | logique métier + accès repository |
| HOPEX Aquila Web Front-End | 62.18.0+143 — 02/09/2026 | portail web utilisateurs |
| HOPEX GraphQL | 62.18.0+69 — 02/09/2026 | API GraphQL, queries/mutations |
| HOPEX REST API | 62.18.0+69 — 02/09/2026 | read/write repository, documents, export diagrams |
| HOPEX MCP Server | 62.18.0+8 — 24/08/2026 | exposition HOPEX à des clients MCP/IA |
| GraphQL IDE | branche 62.x, versions 2026 | aide à la construction de requêtes |
| ServiceNow Integration | Aquila 6.2, version 62.13.x publiée en 2026 | synchronisation HOPEX ↔ ServiceNow |

Ces versions sont des **constats datés**, pas des versions à apprendre par cœur. La règle professionnelle est de toujours vérifier la compatibilité des modules avec le HOPEX Core installé.

## Le mental model à retenir

```text
Entreprise réelle
      ↓
Objets d'architecture et de gouvernance
      ↓
HOPEX Repository
      ↓
Relations + propriétés + cycles de vie + ownership
      ↓
Diagrams / matrices / reports / dashboards
      ↓
Décisions d'architecture et de transformation
```

## Ce que HOPEX n'est pas

HOPEX n'est pas :

- un simple éditeur de diagrammes ;
- un clone d'Archi ;
- un langage de modélisation ;
- TOGAF ;
- uniquement un CMDB ;
- uniquement un inventaire d'applications ;
- uniquement un outil BPM ;
- uniquement un outil GRC.

HOPEX est une plateforme de gestion et d'analyse d'un **référentiel d'entreprise connecté**, sur lequel plusieurs solutions et perspectives peuvent s'appuyer.

## Fait produit vs pratique pédagogique

Dans ce masterbook :

- **Fait produit vérifié** : capacité explicitement documentée par MEGA/HOPEX.
- **Pratique recommandée** : convention proposée pour un référentiel d'entreprise exploitable.
- **Cas MayaBank** : exemple fictif construit pour apprendre.
- **Hypothèse de lab** : simulation utilisée quand l'accès au produit n'est pas disponible.

Nous éviterons de transformer une convention pédagogique en « fonctionnalité officielle HOPEX ».

## Navigation

1. [Baseline produit et versions](01-current-product-baseline.md)
2. [HOPEX comme plateforme EAM](02-what-hopex-is.md)
3. [Architecture de plateforme et composants](03-platform-components.md)
4. [Portfolio de solutions et cas d'usage](04-solution-portfolio.md)
5. [Repository et single source of truth](05-repository-paradigm.md)
6. [Personas, workspaces et responsabilités](06-personas-and-workspaces.md)
7. [HOPEX, ArchiMate et TOGAF](07-standards-archimate-togaf.md)
8. [Accès, licences, training et environnement](08-access-licensing-training.md)
9. [MayaBank — cas fil rouge](09-mayabank-running-case.md)
10. [Anti-patterns, exercices et validation](10-antipatterns-labs-review.md)
11. [Sources officielles Partie I](11-official-sources.md)

## Critère de sortie Partie I

La Partie I est acquise lorsque le lecteur sait expliquer, sans écran HOPEX :

```text
Pourquoi un repository partagé ?
Quels composants portent le front, le back et les APIs ?
Quelles solutions consomment ce repository ?
Quelle différence entre HOPEX et ArchiMate ?
Quelle différence entre HOPEX et une CMDB ?
Comment MayaBank sera structurée dans le référentiel ?
```
