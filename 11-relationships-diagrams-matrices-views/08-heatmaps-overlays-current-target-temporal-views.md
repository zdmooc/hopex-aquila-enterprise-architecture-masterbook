# 08 — Heatmaps, Overlays, Current/Target & Temporal Views

## 1. Pourquoi utiliser une heatmap

Une heatmap permet de faire ressortir une dimension de décision sans redessiner toute l’architecture.

Exemples :

```text
Capability maturity
Application health
Technology obsolescence
Risk level
Strategic importance
Transformation progress
```

## 2. Heatmap = data + visual rule

Une heatmap fiable repose sur :

```text
canonical objects
+ property/metric
+ explicit scale
+ legend
+ date
```

La couleur seule ne crée pas une analyse.

## 3. Scales

Exemple pédagogique :

```text
1 = Critical
2 = Weak
3 = Acceptable
4 = Good
5 = Strategic strength
```

La définition de chaque niveau doit être documentée.

## 4. Capability heatmap

Question : quelles capabilities doivent être priorisées ?

Dimensions possibles :

- strategic importance ;
- maturity ;
- performance ;
- transformation urgency.

Ne pas superposer quatre couleurs différentes dans la même vue.

## 5. Application health overlay

Exemple de score composite :

```text
Business fit
Technical fit
Risk
Lifecycle
Cost
```

La construction détaillée des scores portefeuille sera traitée en Partie XIII.

Ici, on se concentre sur leur **représentation**.

## 6. Technology lifecycle overlay

```text
Preferred
Allowed
Deprecated
Unsupported
```

Très utile sur une vue Application → Technology.

## 7. Risk overlay

Une vue peut mettre en évidence :

- critical applications ;
- high-risk technologies ;
- uncontrolled processes ;
- restricted data.

Toujours expliciter la source du niveau de risque.

## 8. Label overlay

Quand la couleur ne suffit pas :

```text
[Critical]
[Target 2028]
[Owner: Payments IT]
[Confidence: Medium]
```

## 9. Tooltip / additional context

Une vue visuelle peut rester légère tout en donnant accès à plus d’information au survol ou à l’ouverture de l’objet, selon les capacités de la plateforme.

## 10. Current / Target comparison

Trois patterns principaux.

### Pattern A — side-by-side

```text
CURRENT | TARGET
```

Bon pour comparaison directe.

### Pattern B — separate views

Deux vues indépendantes mais mêmes conventions.

Bon pour architecture complexe.

### Pattern C — overlay

Même topologie avec statuts :

```text
Keep
Change
Add
Retire
```

Bon pour un scope limité.

## 11. Transition view

Le target seul ne montre pas la trajectoire.

Ajouter :

```text
Current
→ Transition 1
→ Transition 2
→ Target
```

avec dépendances et contraintes.

## 12. Delta view

La vue delta répond à :

```text
What changes?
What stays?
What disappears?
What is introduced?
```

## 13. Temporal validity

Afficher :

- snapshot date ;
- horizon ;
- validity assumptions ;
- migration wave.

## 14. Before / after

Exemple MayaBank :

### Before

```text
Channel
→ Legacy Gateway
→ Core
→ synchronous Notification
```

### After

```text
Channel
→ API Management
→ Payment Orchestrator
→ Core / Fraud / Clearing
→ events
→ Notification
```

## 15. Heatmap + matrix

Combinaison utile :

```text
Capability × Application matrix
+ color by application lifecycle risk
```

Mais attention : l’outil exact et la capacité de combinaison dépendent de la configuration HOPEX.

## 16. Heatmap + dependency view

Exemple : colorer les technologies selon obsolescence dans un graphe de dépendances.

Cela permet de visualiser immédiatement où le risque se propage.

## 17. Data-quality heatmap

Exemple :

```text
Green  = verified
Amber  = stale
Red    = missing owner/source
```

Très utile pour piloter l’amélioration du repository.

## 18. Avoid false precision

Ne pas utiliser une échelle 0–100 si les données proviennent d’une appréciation qualitative imprécise.

Préférer une taxonomie limitée et documentée.

## 19. MayaBank — overlays recommandés

1. Capability maturity.
2. Application lifecycle.
3. Technology standard status.
4. Relationship confidence.
5. Transformation wave.
6. Risk severity.
7. Data classification.

## 20. Review checklist

- metric defined ?
- source known ?
- scale documented ?
- legend visible ?
- date visible ?
- accessible without color ?
- not mixing unrelated dimensions ?

## 21. Anti-patterns

- heatmap sans métrique ;
- rouge/vert sans définition ;
- score composite opaque ;
- target non daté ;
- overlay illisible ;
- current et target mélangés sans légende ;
- fausse précision numérique.

## 22. Questions d’entretien

**Quelle différence entre heatmap et dashboard ?**  
La heatmap enrichit une structure ou une cartographie ; le dashboard agrège des indicateurs et sera traité plus loin.

**Pourquoi dater une heatmap ?**  
Parce que maturity, health, lifecycle et risk évoluent.

**Quand utiliser un delta view ?**  
Lorsque la décision porte explicitement sur ce qui change entre current et target.