# 07 — Hierarchy, Classification & Inheritance

## 1. Trois mécanismes à ne pas confondre

Dans un repository, plusieurs mécanismes peuvent structurer les objets :

- **hiérarchie de composition** ;
- **classification** ;
- **héritage de métamodèle**.

Ils répondent à des questions différentes.

## 2. Hiérarchie métier

Exemple Capability Map :

```text
Payments
  ├─ Payment Initiation
  ├─ Fraud Control
  ├─ Clearing & Settlement
  └─ Customer Notification
```

Le template ITPM officiel mentionne explicitement la génération d'une **Business Capability Map avec composition hiérarchique correcte** des business capabilities.

Cela confirme qu'une hiérarchie n'est pas seulement visuelle : elle peut porter une structure de composition exploitable.

## 3. Hiérarchie organisationnelle

```text
MayaBank
  └─ Technology Division
      └─ Payments IT
          └─ Platform Engineering
```

Cette hiérarchie répond à la structure organisationnelle, pas à la classification métier des applications.

## 4. Classification

Une classification ajoute un axe de lecture sans créer forcément une hiérarchie d'objets.

Exemple :

```text
Application Type = {Core Banking, Payment, Risk, Channel, Support}
```

ou :

```text
Technology Status = {Strategic, Tolerate, Retire}
```

## 5. Taxonomie vs hiérarchie d'objets

Taxonomie :

```text
Technology category
→ Middleware
→ Event Streaming
```

Objet :

```text
Red Hat AMQ Streams / Kafka platform
```

La catégorie décrit ; l'objet représente une réalité gouvernée.

## 6. Héritage de métamodèle

Dans de nombreux métamodèles, des classes peuvent partager ou spécialiser des concepts. HOPEX expose notamment `MetaClassifier` dans l'API MetaModel publique.

Cependant, cette partie ne suppose pas la structure exacte d'héritage interne d'une installation HOPEX donnée. La règle est :

```text
Inspect before extending.
```

## 7. Pourquoi l'héritage est sensible

Une extension mal pensée peut :

- dupliquer un concept standard ;
- rendre les schémas API plus difficiles à maintenir ;
- casser des rapports ;
- augmenter le coût d'upgrade ;
- créer des règles de saisie incohérentes.

## 8. Composition vs catégorie

Exemple :

```text
Payments Capability
  contains
Instant Payment Capability
```

n'est pas la même chose que :

```text
Instant Payment Capability
  category = Regulatory Critical
```

Le premier décrit une structure ; le second une classification.

## 9. Structurer les technologies

Mauvais :

```text
Kafka
OpenShift
PostgreSQL
API Gateway
```

sans taxonomie.

Meilleur :

```text
Technology Domain
  ├─ Container Platform
  ├─ Event Streaming
  ├─ Database
  └─ API Management
```

puis objets technologiques reliés aux catégories.

## 10. Arbre de capacités MayaBank

```text
Payments
├─ Initiate Payment
├─ Validate Payment
├─ Fraud Decision
├─ Execute Payment
├─ Clearing & Settlement
├─ Reconciliation
└─ Customer Notification
```

Puis analyses :

```text
Capability
→ supporting processes
→ supporting applications
→ technologies
→ owner
→ maturity
→ roadmap
```

## 11. Principe de profondeur

Une hiérarchie trop profonde devient difficile à gouverner.

Règle pratique :

```text
Utiliser seulement les niveaux nécessaires aux décisions.
```

Pas :

```text
L1 → L2 → L3 → L4 → L5 → L6 → L7
```

sans usage clair.

## 12. Multi-classification

Une application peut être classée selon plusieurs axes :

- domaine ;
- criticité ;
- lifecycle ;
- cloud suitability ;
- regulatory scope.

Éviter de transformer chacun de ces axes en nouvelle MetaClass si une classification suffit.

## 13. Gouvernance

Pour chaque hiérarchie :

- définir l'owner ;
- définir la règle parent/enfant ;
- définir la profondeur cible ;
- empêcher les cycles ;
- définir les conditions de déplacement ;
- versionner les changements majeurs de taxonomie.

## 14. Anti-patterns

- utiliser une hiérarchie pour coder un statut ;
- créer un parent `Miscellaneous` permanent ;
- dupliquer un objet dans deux branches au lieu d'utiliser une classification ;
- modifier la hiérarchie sans analyse d'impact ;
- créer une MetaClass enfant pour chaque variante locale.

## 15. Questions d'entretien

**Hiérarchie ou classification ?**  
Hiérarchie pour une structure parent/enfant réelle ; classification pour ajouter un axe de catégorisation.

**Pourquoi limiter l'héritage custom ?**  
Parce qu'il touche la structure du métamodèle et peut augmenter fortement le coût de maintenance et d'upgrade.
