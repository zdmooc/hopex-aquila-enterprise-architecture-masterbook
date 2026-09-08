# 07 — Quality gates, anti-patterns et dette de modélisation BPA

## 1. Positionnement du chapitre

Ce chapitre traite la **qualité du repository et des modèles**. Le cycle de vie détaillé, les workflows d'approbation et le versioning sont traités au chapitre 08. La mesure de performance et la maturité sont traitées au chapitre 09.

L'objectif n'est pas d'accumuler des diagrammes mais de maintenir un patrimoine de processus fiable, lisible et exploitable pour l'analyse.

## 2. Définition d'un modèle publiable

Un modèle est publiable si un reviewer peut répondre rapidement à :

- quel est son scope ?
- quel outcome métier produit-il ?
- qui est accountable end-to-end ?
- où commence-t-il et où finit-il ?
- quelles exceptions majeures sont couvertes ?
- quelles applications et données sont critiques ?
- quels risques et contrôles structurants s'appliquent ?
- quels KPIs permettent de juger sa performance ?
- quelle version fait autorité ?

Un diagramme est une vue ; la qualité doit porter sur les objets et relations du repository autant que sur le dessin.

## 3. Quality gate — identité et scope

Minimum :

```text
Name
Outcome
Scope
Start boundary
End boundary
Process Owner
Parent process
Lifecycle status
Review date
```

Naming recommandé : `Verb + Business Object`.

Exemples :

```text
Execute Instant Payment
Handle Payment Exception
Investigate Fraud Alert
Reconcile Payment
```

À éviter :

```text
Payment Process
Process 12
Processing
New Payment FINAL
```

## 4. Quality gate — BPMN

Avant publication :

1. start/end explicites ;
2. activités nommées par une action ;
3. gateways nommées par une question ou une décision compréhensible ;
4. conditions de sortie cohérentes ;
5. pools/lanes utilisés avec une sémantique stable ;
6. message flows réservés aux échanges entre participants ;
7. timeouts significatifs représentés ;
8. exceptions critiques représentées ou déléguées à un subprocess ;
9. niveau de granularité homogène ;
10. aucune dépendance technique inutile dans une vue métier.

## 5. Quality gate — repository

Le reviewer vérifie que les objets référencés sont canoniques :

- application existante et non recréée dans le process ;
- organisation existante ;
- data/information object gouverné si réutilisé ;
- risk/control existant si partagé ;
- capability existante ;
- initiative de transformation existante.

Principe :

```text
Link existing object
>
Create duplicate object
```

## 6. Search Before Create

Avant de créer un process :

- rechercher par nom et synonymes ;
- comparer parent process ;
- comparer owner ;
- comparer outcome ;
- comparer start/end boundaries ;
- comparer populations/canaux/pays réellement couverts.

Deux noms différents peuvent représenter le même processus. Deux noms identiques peuvent représenter des scopes différents.

## 7. Anti-pattern — BPMN wallpaper

Symptôme : le diagramme est beau mais n'est relié à aucun objet utile.

Conséquences :

- aucune impact analysis ;
- aucune traçabilité risk/control ;
- aucune ownership claire ;
- maintenance manuelle ;
- faible valeur en transformation.

Correction : utiliser le diagramme comme une **vue du repository connecté**.

## 8. Anti-pattern — procédure utilisateur déguisée en process

Exemple :

```text
Open App A
Click Submit
Open App B
Copy reference
Click Validate
```

Cela peut être une procédure utile, mais ce n'est pas nécessairement le niveau stable d'un business process.

Correction :

```text
Business activity
→ operating procedure
→ application interaction
```

séparés lorsqu'ils répondent à des besoins différents.

## 9. Anti-pattern — pool par microservice

Un diagramme métier avec un pool pour chaque composant devient une architecture technique déguisée.

Correction : garder les participants métier/externes nécessaires dans le BPMN, puis mapper les activités vers les applications/services canoniques dans le repository.

## 10. Anti-pattern — toutes les exceptions sur un seul diagramme

Symptôme : 80 branches, 30 gateways et une lecture impossible.

Correction :

```text
Main process
+ exception subprocesses
+ exception catalogue
+ operational playbook
```

Le diagramme principal doit conserver la logique end-to-end.

## 11. Anti-pattern — absence d'owner end-to-end

Chaque équipe possède son activité mais personne n'est accountable du résultat global.

Conséquence : optimisation locale, SLA contradictoires, handoffs non traités.

Correction : un Process Owner accountable, complété par des Activity Owners/Stewards.

## 12. Anti-pattern — duplicate process variants

Exemples de dette :

```text
Execute Payment v1
Execute Payment v2
Execute Payment FINAL
Execute Payment FINAL2
Execute Payment France
Execute Payment Paris
```

Une variante doit correspondre à une différence durable, gouvernée et utile à l'analyse.

## 13. Anti-pattern — application-centric ownership

Un business process n'est pas automatiquement possédé par l'équipe qui maintient l'application principale.

L'Accountable doit être défini selon le résultat métier, pas selon le composant technique le plus visible.

## 14. Anti-pattern — KPI vanity

Métriques faibles :

- nombre de diagrammes créés ;
- nombre d'activités dessinées ;
- nombre d'utilisateurs connectés sans contexte d'usage.

Métriques utiles :

- cycle time ;
- STP ;
- error/rework ;
- SLA breach ;
- control effectiveness ;
- customer/business outcome.

## 15. Anti-pattern — mapping massif sans question d'analyse

Relier chaque activité à chaque serveur, table et document rend le repository coûteux à maintenir.

Avant un mapping, écrire la question :

```text
What decision will this relationship support?
```

Puis choisir la granularité minimale suffisante.

## 16. Anti-pattern — process mining = vérité normative

Les logs montrent l'exécution observée.

Ils ne prouvent pas :

- ce qui aurait dû être exécuté ;
- la conformité réglementaire ;
- le bon niveau de contrôle ;
- le target process.

Comparer toujours `observed` à `governed/current` et `target`.

## 17. Anti-pattern — simulation sans hypothèses

Un résultat de simulation n'est pas une prédiction garantie.

Exiger :

- source des volumes ;
- distributions/temps de service ;
- probabilités de branches ;
- capacité des ressources ;
- période observée ;
- limites du scénario.

## 18. Anti-pattern — automatiser toute tâche manuelle

Une tâche manuelle peut être :

- un contrôle intentionnel ;
- une décision experte ;
- une exception rare ;
- une étape à supprimer plutôt qu'à automatiser.

Séquence recommandée :

```text
Understand
→ Simplify
→ Standardize
→ Control
→ Automate
→ Measure
```

## 19. Anti-pattern — modèle sans date de revue

Un processus critique non revu depuis plusieurs années doit être considéré comme **non fiable** jusqu'à validation.

La date de création ne remplace pas la date de revue.

## 20. Process model debt

La dette de modélisation peut être évaluée par :

- owner manquant ;
- relations orphelines ;
- applications obsolètes ;
- modèles non revus ;
- doublons ;
- KPI sans source ;
- contrôles sans preuve ;
- variantes non justifiées ;
- diagrammes trop complexes.

## 21. Score qualité proposé

Exemple pédagogique sur 100 :

| Dimension | Points |
|---|---:|
| identity/scope | 15 |
| ownership | 10 |
| BPMN readability | 20 |
| exceptions | 10 |
| application/data links | 15 |
| risks/controls | 10 |
| KPIs | 10 |
| lifecycle/review | 10 |

Ce score n'est pas une fonctionnalité imposée par HOPEX ; c'est une méthode de gouvernance MayaBank.

## 22. MayaBank — revue de `Execute Instant Payment`

Bloquer la publication si l'un des éléments suivants manque :

- Payment Process Owner ;
- clearing timeout ;
- duplicate handling ;
- Fraud Decision Service mapping ;
- Payment Orchestrator mapping ;
- reconciliation control ;
- P95 processing time source ;
- review date ;
- target version si transformation en cours.

## 23. Checklist de revue en Architecture/Process Board

1. Le process répond-il à une question métier claire ?
2. Le niveau de détail est-il cohérent ?
3. Les objets liés sont-ils canoniques ?
4. Les exceptions majeures sont-elles visibles ?
5. Les risques critiques possèdent-ils des contrôles ?
6. Les KPIs sont-ils réellement mesurables ?
7. Les liens IT/data sont-ils maintenables ?
8. Les variantes sont-elles justifiées ?
9. Le modèle actuel et le modèle cible sont-ils distingués ?
10. Une responsabilité de maintenance existe-t-elle après publication ?

## 24. Règle de sortie

Un modèle qui ne peut pas être maintenu ne doit pas être détaillé davantage.

La meilleure qualité n'est pas le maximum d'information ; c'est le **minimum fiable suffisant pour décider, gouverner et analyser**.