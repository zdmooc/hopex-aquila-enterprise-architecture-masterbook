# 07 — Filters, Queries, Scoping & Derived Views

## 1. Pourquoi filtrer

Le repository contient plus d’informations qu’une vue ne doit en montrer.

Filtrer permet de passer de :

```text
Enterprise repository
→ relevant subset
→ decision-ready view
```

## 2. Filter vs deletion

Masquer un objet dans une vue ne signifie pas supprimer l’objet du repository.

De même :

```text
not shown
≠ does not exist
```

Cette distinction doit être claire pour le lecteur.

## 3. Filter dimensions

Exemples :

- business domain ;
- organization ;
- geography ;
- criticality ;
- lifecycle ;
- environment ;
- owner ;
- strategic importance ;
- transformation wave ;
- technology status ;
- data classification ;
- risk level.

## 4. Scope by relationship

Exemple : afficher uniquement les applications qui supportent `Payment Execution`.

```text
Capability
→ supported by
Applications
```

Puis étendre un niveau :

```text
Applications
→ technologies
```

## 5. Depth

Pour une exploration d’impact :

```text
Depth 0 = selected object
Depth 1 = direct dependencies
Depth 2 = dependencies of dependencies
Depth 3+ = use carefully
```

Au-delà, le bruit augmente rapidement.

## 6. Upstream vs downstream

Deux filtres différents :

```text
Who do I depend on?
Who depends on me?
```

Ils répondent à des questions différentes.

## 7. Current-only filter

Exemple :

```text
Lifecycle = Active
Environment = PROD
Validity = current
```

Utile pour une vue opérationnelle.

## 8. Target-only filter

```text
Target state = Planned/Strategic
Horizon = 2028
```

Utile pour une architecture cible.

## 9. Criticality filter

```text
Criticality in {Critical, High}
```

Permet de réduire un landscape avant une revue de résilience.

## 10. Quality filter

Exemple :

```text
show relations where confidence != Verified
```

ou :

```text
show objects without owner
```

Les filtres servent donc aussi à la qualité du repository.

## 11. Derived view

Une vue dérivée est calculée à partir du repository selon un ensemble de règles.

Exemple conceptuel :

```text
All active applications
where domain = Payments
and criticality >= High
and target_direction != Retire
```

## 12. Saved scope

Pour une gouvernance reproductible, un scope récurrent doit avoir :

- un nom ;
- un owner ;
- une définition ;
- des critères ;
- une date de revue.

## 13. Query-driven analysis

Une requête peut être plus adaptée qu’un diagramme lorsque l’on cherche :

```text
applications using deprecated technology
applications without owner
processes with no supporting application
critical apps without DR platform
initiatives impacting the same capability
```

## 14. Filter chain

Exemple MayaBank :

```text
Domain = Payments
→ Lifecycle = Active
→ Environment = PROD
→ Criticality = Critical
→ Relation depth = 2
```

Résultat : un graphe de dépendances exploitable.

## 15. Visible filter state

Un lecteur doit savoir qu’une vue est filtrée.

Afficher dans titre, sous-titre ou légende :

```text
Scope: Payments / PROD / Critical only / Current
```

## 16. Hidden filters

Anti-pattern dangereux : publier une vue qui semble complète alors qu’elle masque 80 % des éléments sans l’indiquer.

## 17. Combining filters

Plusieurs dimensions peuvent produire une vue très utile :

```text
Technology status = Deprecated
AND Application criticality = Critical
AND Lifecycle = Active
```

Question : quelles applications critiques dépendent encore d’une technologie à retirer ?

## 18. Filter vs viewpoint

Le viewpoint définit la structure du besoin.

Le filter réduit les données de l’instance de vue.

```text
Viewpoint = Application Technology Risk
Filter = Payments domain, PROD, 2026-Q3
```

## 19. MayaBank — saved scopes

Recommandations pédagogiques :

```text
PAYMENTS-CRITICAL-PROD
PAYMENTS-TARGET-2028
LEGACY-RETIREMENT-CANDIDATES
OCP-CRITICAL-CONSUMERS
PAYMENT-DATA-RESTRICTED
```

## 20. Query quality

Une requête doit documenter :

- object types ;
- relation types ;
- depth ;
- filters ;
- exclusions ;
- expected semantics.

## 21. Performance consideration

Les très grands scopes et les explorations profondes peuvent devenir coûteux et peu lisibles. Préférer une démarche progressive :

```text
start narrow
→ validate
→ expand only if needed
```

## 22. Anti-patterns

- filtre caché ;
- scope non daté ;
- requête sans définition ;
- profondeur 5 sur tout le repository ;
- sauvegarder 50 variantes quasi identiques ;
- utiliser un filtre pour masquer une mauvaise qualité de données.

## 23. Questions d’entretien

**Quelle différence entre filtre et suppression ?**  
Le filtre réduit une représentation ; la suppression modifie le repository.

**Pourquoi afficher le scope ?**  
Pour éviter qu’une vue partielle soit interprétée comme une vue exhaustive.

**Quand utiliser une query plutôt qu’un diagramme ?**  
Quand la question porte d’abord sur la sélection, la conformité ou la détection d’anomalies.