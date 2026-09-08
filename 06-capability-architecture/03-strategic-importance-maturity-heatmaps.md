# 03 — Strategic Importance, Maturity, Performance et Heatmaps

## 1. Deux axes à ne jamais confondre

Une capability peut être **stratégiquement importante** mais faible en maturité, ou peu stratégique mais déjà très mature.

```text
Strategic Importance = combien cette capability compte pour la stratégie
Maturity / Performance = à quel niveau elle fonctionne aujourd'hui
```

Le croisement des deux axes guide les investissements.

## 2. Échelle d'importance proposée MayaBank

```text
1 = Commodity / support
2 = Necessary
3 = Important
4 = Strategic
5 = Differentiating / critical to strategy
```

Cette échelle est pédagogique ; elle doit être remplacée par le modèle de scoring du client si celui-ci existe.

## 3. Échelle de maturité proposée

```text
1 = Ad hoc
2 = Repeatable
3 = Defined
4 = Managed
5 = Optimized
```

Le score ne vaut rien sans critères observables.

Exemple pour `Instant Payment Execution` :

- disponibilité ;
- automatisation ;
- performance ;
- résilience ;
- qualité opérationnelle ;
- conformité ;
- couverture fonctionnelle.

## 4. Current vs Target

Chaque capability évaluée peut porter :

```text
Current maturity
Target maturity
Gap = Target - Current
Assessment date
Evidence/source
Assessor/owner
```

## 5. Heatmap

Une heatmap traduit une évaluation en vue décisionnelle. Elle ne remplace jamais les scores sources.

Exemples de dimensions :

- maturity gap ;
- strategic importance ;
- risk exposure ;
- investment need ;
- application health ;
- technology obsolescence.

## 6. Priorisation simple

```text
Priority ≈ Strategic Importance × Maturity Gap
```

Cette formule n'est qu'un exemple. On peut ajouter risque, coût, dépendances, bénéfices et urgence réglementaire.

## 7. Exemple MayaBank

| Capability | Importance | Current | Target | Gap | Lecture |
|---|---:|---:|---:|---:|---|
| Instant Payment Execution | 5 | 3 | 5 | 2 | investissement prioritaire |
| Fraud Decisioning | 5 | 2 | 5 | 3 | priorité critique |
| Customer Notification | 3 | 3 | 4 | 1 | amélioration ciblée |
| Batch Reporting | 2 | 4 | 4 | 0 | maintenir |
| Legacy File Transfer | 1 | 2 | 1 | -1 | candidat retrait |

## 8. Evidence-based assessment

Mauvais : `Maturity = 2 parce que l'architecte pense que c'est faible`.

Meilleur : score justifié par indicateurs, audits, SLA/SLO, incidents, couverture fonctionnelle, dette, satisfaction métier et résultats de contrôle.

## 9. Gouvernance

Pour chaque campagne d'évaluation :

1. définir les critères ;
2. fixer l'échelle ;
3. identifier les évaluateurs ;
4. recueillir les preuves ;
5. modérer les scores ;
6. valider avec owner ;
7. publier la heatmap ;
8. relier les gaps aux initiatives.

## 10. Anti-patterns

- changer les couleurs sans changer les données ;
- comparer des scores issus de méthodes différentes ;
- noter toutes les capabilities à 5 en importance ;
- produire une heatmap sans date d'évaluation ;
- utiliser la maturité comme jugement sur une équipe ;
- confondre santé applicative et maturité métier.