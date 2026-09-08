# 05 — Relationships & Contextual Navigation

## 1. Une relation est une donnée d'architecture

Dans HOPEX, les relations entre objets sont ce qui transforme un inventaire en graphe analysable.

```text
Object + Object + Relation
→ Impact analysis
→ Traceability
→ Decision support
```

## 2. La relation doit avoir un sens

Mauvais :

```text
Application A -- related to --> Application B
```

si l'on a besoin de savoir :

- qui consomme qui ;
- qui supporte quoi ;
- qui héberge quoi ;
- qui produit/consomme une donnée ;
- qui dépend de quelle technologie.

## 3. Relation vs propriété

Si la valeur doit être navigable comme objet réutilisable, une association est souvent plus robuste qu'un texte.

Mauvais :

```text
Application.Technologies = "Kafka, PostgreSQL, OpenShift"
```

Meilleur :

```text
Application
→ Technology object Kafka
→ Technology object PostgreSQL
→ Platform object OpenShift
```

La MetaAssociation exacte dépend du métamodèle client.

## 4. Sens direct et inverse

Toute relation importante doit pouvoir être expliquée dans les deux directions.

```text
Application → supports Process
Process ← supported by Application
```

Cela permet :

- navigation top-down ;
- navigation bottom-up ;
- impact analysis ;
- contrôle de cohérence.

## 5. Cardinalité utile

La cardinalité n'est pas seulement technique. Elle révèle les situations d'architecture.

Exemple :

```text
1 Process
→ 12 Applications
```

peut indiquer une orchestration complexe.

```text
1 Technology
→ 140 Applications
```

peut révéler un large blast radius.

## 6. MayaBank — graphe minimal

```text
Real-Time Payment Capability
→ Instant Payment Process
→ Payment Orchestrator
→ Fraud Engine
→ Event Streaming Platform
→ OpenShift Platform
```

Compléter par :

```text
Owners
Interfaces
Data objects/domains
Projects / roadmap
```

## 7. Navigation contextuelle

Partir de `Fraud Engine` :

```text
Fraud Engine
→ incoming application dependencies
→ processes supported
→ data consumed
→ technology platform
→ owner
→ lifecycle
```

Puis répondre :

> Si Fraud Engine est indisponible, quels flux business sont impactés ?

## 8. Relation canonique

Éviter de créer plusieurs associations équivalentes :

```text
uses
uses technology
technology used by
technical dependency
```

sans gouvernance.

La normalisation des relations est indispensable aux rapports.

## 9. Relation et source

Pour une relation critique, savoir :

- qui l'a créée ;
- quelle source la justifie ;
- qui la valide ;
- comment elle est mise à jour ;
- si elle est manuelle ou synchronisée.

## 10. Relation et temporalité

Une dépendance peut être :

- current ;
- transition ;
- target ;
- planned retirement.

Ne pas écraser toutes les temporalités dans un graphe unique sans contexte.

## 11. Anti-patterns

- Association générique partout ;
- relations uniquement dans les diagrammes, non persistées comme données ;
- relation créée dans les deux sens comme deux liens indépendants ;
- relation sans source ;
- relation à une copie d'objet ;
- 100 % des objets reliés à un objet "Enterprise" pour éviter les orphelins.

## 12. Lab

Construire un mini-graphe MayaBank de 12 objets maximum et 20 relations maximum.

Pour chaque relation :

```text
Source class
Target class
Business meaning
Reverse navigation question
Owner/source
Current/target context
```

Puis exécuter mentalement trois analyses d'impact :

1. Kafka indisponible ;
2. Payment Orchestrator retiré ;
3. OpenShift remplacé.