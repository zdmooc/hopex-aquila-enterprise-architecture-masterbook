# 08 — Standard vs Custom Metamodel

## 1. Personnaliser n'est pas le premier réflexe

HOPEX permet d'étendre le métamodèle. Le Store officiel documente un **GraphQL Mapping Json Generator** qui demande de créer un métamodèle dans **MetaStudio**, d'y ajouter le fragment souhaité, puis d'utiliser son identifiant pour générer le mapping JSON destiné au schéma GraphQL.

Cette capacité ne signifie pas qu'il faut customiser systématiquement.

## 2. Ordre de préférence

Avant de créer une nouvelle MetaClass :

```text
1. réutiliser une classe standard
2. utiliser une relation standard
3. utiliser une propriété existante
4. ajouter une classification/liste si suffisant
5. ajouter une propriété custom si durable et gouvernée
6. créer une association custom si nécessaire
7. créer une MetaClass custom seulement en dernier recours
```

## 3. Pourquoi limiter les extensions

Chaque extension peut impacter :

- UI ;
- formulaires ;
- permissions ;
- rapports ;
- dashboards ;
- imports ;
- exports ;
- GraphQL ;
- REST ;
- upgrades ;
- formation ;
- support.

## 4. Bon besoin de customisation

Exemple : une banque doit gérer un concept réellement absent du modèle standard, durable, avec :

- propriétés propres ;
- relations propres ;
- cycle de vie ;
- owner ;
- analyses ;
- usage dans plusieurs processus.

Alors une extension peut être justifiée.

## 5. Mauvais besoin

```text
"Nous avons un rapport PowerPoint qui contient une colonne X"
```

Ce n'est pas suffisant pour créer une nouvelle MetaClass.

## 6. Custom property

Une propriété custom est souvent moins coûteuse qu'une classe custom.

Exemple pédagogique :

```text
Application.regulatoryTier
```

peut être préférable à :

```text
MetaClass RegulatoryApplication
```

si le concept ne change pas la nature de l'objet.

## 7. Custom association

Une association custom est justifiée si la relation :

- a une sémantique spécifique ;
- est réutilisée ;
- sert des analyses ;
- ne peut pas être représentée proprement par une relation existante.

## 8. Custom MetaClass

Critères minimaux :

```text
definition stable
+ owner
+ creation workflow
+ properties
+ relationships
+ lifecycle
+ reporting use case
+ API implications
+ migration/upgrade plan
```

## 9. MetaStudio

La ressource officielle du GraphQL Mapping Json Generator indique explicitement :

```text
Open HOPEX Windows desktop client
→ MetaStudio tab
→ create a new Metamodel
→ add a diagram
→ place the part of the metamodel needed
→ keep the absolute identifier
→ generate JSON mapping
```

Le masterbook ne reproduit pas le produit propriétaire ; il utilise cette information pour comprendre le workflow technique d'extension et d'exposition.

## 10. Environnements

Une modification de métamodèle doit suivre une chaîne contrôlée :

```text
Design
→ Sandbox/Dev
→ Test
→ integration validation
→ migration package
→ Preprod
→ Production
```

Éviter les changements directs en production.

## 11. Versioning

Pour chaque extension :

```text
Extension ID
Version
Owner
Purpose
Affected MetaClasses
Affected APIs
Affected Reports
Migration instructions
Rollback approach
```

## 12. Upgrade

Avant upgrade HOPEX :

1. inventorier toutes les customisations ;
2. comparer avec le nouveau standard ;
3. détecter les collisions ;
4. tester les APIs ;
5. tester les imports ;
6. tester les rapports ;
7. tester les droits ;
8. documenter les adaptations.

## 13. MayaBank — décision

Besoin : ajouter `Green IT Score` aux Applications.

Questions :

```text
Est-ce une propriété ? oui probablement
Est-ce une nouvelle nature d'objet ? non
Doit-elle être calculée ? peut-être
Quelle source ? Green IT assessment
Quel owner ? Sustainable IT / EA
```

Donc : **ne pas créer une MetaClass GreenApplication**.

## 14. MayaBank — second cas

Besoin : modéliser un `Regulatory Obligation` réutilisable, relié à plusieurs capabilities, applications, processes et controls.

Si aucune classe standard pertinente n'existe dans les solutions installées, une extension peut être étudiée. Mais elle doit être précédée d'une analyse du métamodèle GRC/IRM disponible.

## 15. Anti-patterns

- MetaClass par département ;
- MetaClass par produit technique ;
- propriétés sans définition ;
- customisation pour reproduire un ancien Excel ;
- extension sans owner ;
- extension non documentée ;
- même concept customisé différemment par deux équipes ;
- schéma API non retesté après changement.

## 16. Questions d'entretien

**Quand customiser HOPEX ?**  
Quand le standard ne peut pas représenter proprement un concept durable nécessaire à plusieurs analyses, et qu'on accepte le coût de gouvernance et d'upgrade.

**Pourquoi MetaStudio est important ?**  
Parce qu'il permet de travailler explicitement sur le métamodèle et constitue aussi un point de départ documenté pour générer certains mappings GraphQL custom.
