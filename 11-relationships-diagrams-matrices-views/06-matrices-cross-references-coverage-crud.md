# 06 — Matrices, Cross-References, Coverage & CRUD

## 1. Pourquoi la matrice est un outil d’architecture

Un diagramme montre bien une structure ou un flux.

Une matrice montre mieux une **couverture**, une **responsabilité** ou une **relation many-to-many**.

Exemples :

```text
Capability × Application
Process × Application
Application × Technology
Application × Data
Risk × Control
Initiative × Capability
```

## 2. Anatomy d’une matrice

```text
Rows
Columns
Relation type
Cell value
Filters
Scope
Legend
```

Une matrice sans relation définie n’est qu’un tableau décoratif.

## 3. Binary matrix

Cellule :

```text
X = relation exists
blank = no relation recorded
```

Attention : `blank` peut signifier :

- relation inexistante ;
- relation inconnue ;
- relation non encore saisie.

Ne pas confondre ces états sans convention.

## 4. Ternary / qualified matrix

Exemple pédagogique :

```text
A = authoritative
S = supporting
C = consuming
```

ou :

```text
Current
Target
Both
```

Si la plateforme ne supporte pas directement ce codage, utiliser une propriété ou un objet intermédiaire approprié plutôt qu’un artifice non gouverné.

## 5. Capability × Application

Questions :

- quelles capabilities sont sous-supportées ?
- quelles capabilities ont trop d’applications ?
- quelles applications supportent trop de domaines ?
- où existe une redondance fonctionnelle ?

Exemple :

| Capability | Digital Channel | Payment Orchestrator | Fraud Service | Core Account |
|---|---:|---:|---:|---:|
| Payment Initiation | X |  |  |  |
| Payment Execution |  | X | X | X |
| Fraud Prevention |  |  | X |  |

## 6. Process × Application

Utilité :

- identifier les activités très manuelles ;
- mesurer la fragmentation applicative ;
- préparer une migration ;
- analyser les étapes critiques.

## 7. Application × Technology

Utilité :

```text
technology obsolescence
→ impacted applications
→ business blast radius
```

La matrice est particulièrement utile pour prioriser les upgrades.

## 8. Application × Information

Elle peut représenter :

```text
Create
Read
Update
Delete
Master
Reference
Consume
Publish
```

Le choix doit être documenté.

## 9. CRUD matrix

Exemple :

| Application | Payment | Customer | Account | Fraud Decision |
|---|---|---|---|---|
| Payment Orchestrator | C/U/R | R | R | R |
| Fraud Service | R | R | R | C |
| Core Account | R |  | C/U/R |  |

Une CRUD matrix détaillée peut devenir volumineuse. L’utiliser lorsque la décision justifie ce niveau.

## 10. Risk × Control

Permet de détecter :

- risque sans contrôle ;
- contrôle couvrant plusieurs risques ;
- concentration sur un contrôle unique ;
- contrôles sans owner.

## 11. Initiative × Capability

Utilité :

- vérifier l’alignement stratégique ;
- identifier capabilities non financées ;
- détecter trop de projets sur la même capability.

## 12. Owner × Object

Exemples :

```text
Org Unit × Application
Data Owner × Data Domain
Platform Team × Platform
```

Très utile pour détecter les objets orphelins.

## 13. Matrix size

Une matrice de 500 × 500 est rarement une bonne expérience de décision.

Réduire par :

- domaine ;
- criticality ;
- lifecycle ;
- environment ;
- transformation wave ;
- owner.

## 14. Sorting

Ordres utiles :

```text
business hierarchy
application domain
criticality
lifecycle
owner
alphabetical only as fallback
```

## 15. Matrix as data-quality tool

Une matrice révèle :

- lignes vides ;
- colonnes sans relation ;
- couverture excessive ;
- doublons ;
- incohérences.

## 16. Direct editing

Certaines plateformes de modélisation permettent l’édition de relations depuis une matrice. Dans HOPEX, la capacité exacte dépend de la solution et de la configuration ; ne pas supposer qu’une opération disponible dans un autre produit Bizzdesign est identique dans Hopex.

Le principe de gouvernance reste :

```text
editing a matrix cell
= changing repository semantics
```

et doit donc être contrôlé.

## 17. Matrix vs spreadsheet

Une feuille Excel :

- facile à manipuler ;
- mais souvent déconnectée du repository.

Une matrice repository-driven :

- réutilise objets et relations ;
- reste liée aux sources canoniques ;
- peut alimenter d’autres vues.

## 18. Matrix vs diagram

```text
Need topology?      → Diagram
Need coverage?      → Matrix
Need properties?    → List
Need trend/KPI?     → Report/Dashboard
```

## 19. MayaBank — matrices obligatoires

1. Capability × Application.
2. Process × Application.
3. Application × Application Dependency.
4. Application × Technology.
5. Application × Data.
6. Application × Platform.
7. Risk × Control.
8. Initiative × Application.
9. Initiative × Capability.
10. Application × Owner.

## 20. Quality checklist

- row/column scope documenté ;
- relation type explicite ;
- cellule vide interprétable ;
- filtre visible ;
- date de snapshot si nécessaire ;
- matrice raisonnablement lisible ;
- relation issue du repository et non ressaisie.

## 21. Anti-patterns

- matrice gigantesque ;
- `X` sans définition ;
- cellules colorées sans légende ;
- spreadsheet exporté puis maintenu en parallèle ;
- fusion de current et target sans distinction ;
- CRUD exhaustif sans cas d’usage ;
- cellule éditée sans gouvernance.

## 22. Questions d’entretien

**Quel est le principal avantage d’une matrice ?**  
Comparer systématiquement des relations many-to-many et détecter couverture, gaps et redondances.

**Pourquoi une cellule vide est-elle ambiguë ?**  
Parce qu’elle peut signifier absence réelle, donnée inconnue ou donnée non collectée.

**Quand éviter une CRUD matrix ?**  
Quand le niveau de détail n’apporte aucune décision et devient trop coûteux à maintenir.