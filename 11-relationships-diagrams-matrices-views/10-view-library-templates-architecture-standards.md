# 10 — Reusable View Library, Templates & Architecture Standards

## 1. Pourquoi une bibliothèque de vues

Une organisation mature ne redéfinit pas à chaque projet :

- les mêmes diagrammes ;
- les mêmes matrices ;
- les mêmes couleurs ;
- les mêmes règles de scope ;
- les mêmes conventions de nommage.

Elle maintient une **View Library** réutilisable.

## 2. View template

Un template décrit :

```text
Name
Purpose
Stakeholder
Concern
Allowed object types
Allowed relation types
Required properties
Layout convention
Legend
Scope rules
Review frequency
Owner
```

## 3. Naming convention

Exemple :

```text
<Domain> — <View Type> — <State> — <Scope> — <Date/Horizon>
```

Exemple :

```text
Payments — Application Cooperation — Current — PROD — 2026-Q3
```

## 4. Mandatory enterprise views

Bibliothèque MayaBank recommandée :

1. Enterprise Capability Map.
2. Business Process Landscape.
3. Application Landscape.
4. Application Cooperation.
5. Information Concept Map.
6. Technology Landscape.
7. Application → Technology Dependency.
8. Current/Target Transformation.
9. Risk/Control View.
10. Executive Transformation View.

## 5. Mandatory matrices

1. Capability × Application.
2. Process × Application.
3. Application × Technology.
4. Application × Data.
5. Application × Owner.
6. Risk × Control.
7. Initiative × Capability.
8. Initiative × Application.

## 6. Domain-specific views

Chaque domaine peut ajouter des vues spécialisées sans casser le standard entreprise.

Exemple Payments :

```text
Instant Payment Critical Path
Clearing Integration View
Fraud Decision Dependencies
Payment Data Lineage
```

## 7. Template vs copy

Le template fournit des règles.

Il ne doit pas encourager à copier des objets du repository dans un nouveau silo.

## 8. Visual grammar standard

Définir à l’échelle entreprise :

- sens de lecture ;
- conventions current/target ;
- lifecycle colors ;
- criticality indicators ;
- annotation rules ;
- title format ;
- legend format.

## 9. Scope standard

Pour chaque vue publiée :

```text
Domain
Environment
Lifecycle
Time horizon
Filter
Snapshot date
```

## 10. Template quality gate

Avant publication d’un nouveau type de vue :

1. Quel concern ?
2. Une vue existante suffit-elle ?
3. Quels objets sont requis ?
4. Quelles relations sont autorisées ?
5. Quelles décisions seront prises ?
6. Qui maintient le template ?

## 11. View catalog

Le catalogue peut contenir :

| View Type | Owner | Audience | Mandatory | Review |
|---|---|---|---|---|
| Application Landscape | EA | Architects/IT | Yes | Quarterly |
| Executive Transformation | EA Office | Executives | Yes | Quarterly |
| Technology Risk | Tech Architecture | Architecture Board | Yes | Monthly/Quarterly |
| Solution Detail | Project Architect | Delivery | No | Project lifecycle |

Les fréquences sont pédagogiques.

## 12. Versioning

Une convention visuelle elle-même évolue.

Exemple :

```text
View Standard v1
→ retired
View Standard v2
→ current
```

Documenter les changements importants.

## 13. Migration of legacy diagrams

Processus :

```text
Inventory
→ classify
→ identify canonical objects
→ rebuild relationships
→ apply standard template
→ validate owner
→ retire duplicate diagram
```

Ne pas simplement importer une image et déclarer le travail terminé.

## 14. PowerPoint / Visio coexistence

Des supports externes resteront utiles pour communication ponctuelle.

Règle :

```text
HOPEX repository = source architecture
PPT/Visio = communication artifact when needed
```

Éviter de maintenir la vérité dans les deux.

## 15. Diagram retirement

Une vue doit pouvoir être retirée si :

- plus de stakeholder ;
- scope obsolète ;
- remplacée ;
- impossible à maintenir ;
- doublon.

## 16. View owner

Le propriétaire garantit :

- pertinence ;
- scope ;
- cycle de revue ;
- alignment aux standards ;
- résolution des anomalies.

## 17. MayaBank — structure de bibliothèque

```text
00-Executive
01-Business
02-Process
03-Application
04-Data
05-Technology
06-Risk
07-Transformation
08-Solution-Views
09-Archived
```

Il s’agit d’une recommandation documentaire, pas d’une structure HOPEX imposée.

## 18. Architecture Board pack

Pack minimal :

```text
Executive context
Current architecture
Target architecture
Impact/dependency view
Key matrix
Risks/controls
Decision requested
```

## 19. Anti-patterns

- nouveau template par projet ;
- conventions incompatibles entre domaines ;
- bibliothèque sans owner ;
- 80 templates quasi identiques ;
- diagrammes anciens jamais retirés ;
- PowerPoint devenant la source de vérité.

## 20. Questions d’entretien

**Pourquoi standardiser les vues ?**  
Pour rendre l’architecture comparable, lisible et maintenable à l’échelle de l’entreprise.

**Quelle différence entre template et diagramme ?**  
Le template définit les règles ; le diagramme applique ces règles à un scope concret.

**Faut-il interdire PowerPoint ?**  
Non. Il reste utile pour la communication, mais la vérité architecturale doit rester dans le repository gouverné.