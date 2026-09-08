# 06 — Lists, Filters, Sorting & Review Queues

## 1. Une liste est une requête métier

Une liste utile répond à une question explicite.

Mauvais :

```text
All Applications
```

sans but.

Meilleur :

```text
Critical payment applications
with no owner
or lifecycle review overdue
```

## 2. Colonnes utiles

Pour une revue applicative MayaBank :

```text
Name
External ID
Domain
Owner
Lifecycle
Criticality
Last Review
Source
```

Ajouter une colonne seulement si elle sert le tri, la comparaison ou la décision.

## 3. Filtrage

Exemples :

```text
Domain = Payments
Criticality = Critical
Lifecycle ∈ {Tolerate, Migrate, Retire}
Owner is empty
Last Review older than 12 months
```

Les valeurs et catégories exactes doivent être alignées sur le métamodèle/solution client.

## 4. Tri

Le tri sert à créer une file de travail :

```text
1. Criticality DESC
2. Review Age DESC
3. Lifecycle risk
```

## 5. Saved views / reusable filters

Quand l'environnement permet d'enregistrer ou réutiliser des vues/listes, gouverner celles qui deviennent collectives.

Éviter :

```text
Application List Final
Application List Final2
My List
New List
```

Préférer des noms basés sur le concern :

```text
PAY — Applications requiring lifecycle review
EA — Critical applications without owner
TECH — Technologies nearing end of support
```

## 6. Bulk review

Une revue de masse ne signifie pas modification aveugle de masse.

Processus :

```text
Filter
→ detect candidates
→ inspect exceptions
→ validate owner/source
→ controlled update
→ quality check
```

## 7. Export

Un export Excel/CSV peut être utile pour analyse ponctuelle, mais ne doit pas devenir une seconde source de vérité.

Règle :

```text
Export = projection
HOPEX = canonical repository
```

## 8. Liste de qualité MayaBank

Créer au minimum ces files de revue :

1. Applications sans owner ;
2. Applications sans lifecycle ;
3. Applications critiques non revues ;
4. Technologies non reliées ;
5. Capabilities sans support applicatif ;
6. Doublons suspects ;
7. Objets dont la source est inconnue.

## 9. Listes et gouvernance

Chaque liste collective doit avoir :

```text
Purpose
Population rule
Columns
Filters
Owner
Review cadence
Action expected
```

## 10. Anti-patterns

- liste de 80 colonnes ;
- filtre caché non documenté ;
- export modifié puis jamais réimporté ;
- KPI calculé sur une population inconnue ;
- liste personnelle utilisée comme reporting officiel ;
- modification en masse sans exception handling.

## 11. Exercice

Définir cinq listes opérationnelles pour MayaBank. Pour chacune, écrire :

```text
Concern
Population
Filters
Columns
Sort
Expected action
Owner
Frequency
```

Si aucune action n'est attendue, transformer la liste en rapport ou la supprimer.