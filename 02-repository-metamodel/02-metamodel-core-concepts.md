# 02 — Metamodel Core Concepts

## 1. Pourquoi le métamodèle est central

Le métamodèle définit **les types d'objets possibles, leurs propriétés et leurs relations autorisées**.

Sans métamodèle :

```text
Application
Capability
Process
Technology
```

ne seraient que des libellés.

Avec métamodèle :

```text
MetaClass Application
  → possède des attributs
  → peut être reliée à certaines classes
  → peut participer à des vues/rapports
  → peut être exposée via schémas/API
```

## 2. Faits techniques vérifiés

Le workspace public MEGA expose un endpoint :

```text
POST /HOPEXGraphQL/api/MetaModel
```

avec une requête d'exemple :

```graphql
query {
  metaClass(filter: {name_starts_with:"Meta"}) {
    name
  }
}
```

L'exemple de réponse contient notamment :

```text
MetaAttribute
MetaClass
MetaAssociation
MetaAssociationEnd
MetaModel
MetaAssociationType
MetaAttributeValue
MetaClassifier
MetaTrigger
MetaList
MetaViewport
MetaTool
MetaTreeNode
...
```

Cela confirme que le métamodèle n'est pas seulement une notion pédagogique : il est représenté comme donnée interrogeable.

## 3. MetaModel

Un **MetaModel** décrit un ensemble cohérent de concepts de modélisation.

Mental model :

```text
MetaModel
  ├─ MetaClasses
  ├─ MetaAttributes
  ├─ MetaAssociations
  ├─ Association Ends
  ├─ classifiers/lists
  └─ rules/supporting metadata
```

Le détail exact dépend du métamodèle installé et des solutions HOPEX activées.

## 4. MetaClass

Une MetaClass définit une catégorie d'objets.

Exemples rencontrés dans les ressources HOPEX :

```text
Application
Business Capability
Business Process
Org-Unit
Software Technology
Content
```

Le template ITPM officiel mentionne explicitement plusieurs de ces concepts et parle de **metaclass**.

## 5. MetaAttribute

Un MetaAttribute définit une propriété portée par des instances de MetaClass.

Exemple conceptuel :

```text
MetaClass: Application
MetaAttributes:
- Name
- Lifecycle
- Criticality
- Vendor
- Status
```

Tous les noms ci-dessus ne doivent pas être supposés présents à l'identique dans toutes les configurations. Le principe est plus important que l'écran.

## 6. MetaAssociation

Une MetaAssociation définit un lien sémantique entre objets.

Exemple conceptuel :

```text
Application
  ↔ Business Capability

Application
  ↔ Software Technology

Application
  ↔ Org-Unit
```

La relation ne doit jamais être choisie uniquement parce qu'on veut « relier deux boîtes ».

## 7. MetaAssociationEnd

Une association possède des extrémités qui donnent du sens à la navigation dans chaque direction.

Exemple conceptuel :

```text
Application -- supported capability --> Capability
Capability  -- supporting application --> Application
```

Les libellés et règles exacts dépendent du métamodèle HOPEX concerné.

## 8. MetaClassifier et listes

Le métamodèle peut aussi encadrer des valeurs contrôlées et classifications.

Pourquoi ?

Sans contrôle :

```text
Criticality = High
Criticality = Critical
Criticality = C1
Criticality = Important
```

Avec vocabulaire gouverné :

```text
Criticality ∈ {Low, Medium, High, Critical}
```

Cela rend les rapports fiables.

## 9. Metamodel vs repository data

```text
Metamodel
= règles du langage du repository

Repository data
= objets réels de l'entreprise
```

Exemple :

```text
MetaClass Application
≠
MayaBank Payment Orchestrator
```

Le premier définit un type. Le second est une instance.

## 10. Métamodèle standard vs vocabulaire métier

Ne pas créer une MetaClass simplement parce qu'un métier utilise un mot particulier.

Exemple :

```text
"Payment Hub"
```

peut être :

- une Application ;
- une plateforme ;
- une solution logique ;
- un produit ;
- un regroupement.

La première question est sémantique : **qu'est-ce que cet objet dans l'architecture ?**

## 11. Règle de décision

Avant extension :

```text
1. le concept existe-t-il déjà ?
2. une propriété suffit-elle ?
3. une classification suffit-elle ?
4. une relation existante suffit-elle ?
5. le nouveau concept apporte-t-il une analyse durable ?
6. peut-on le gouverner ?
7. quelles APIs/rapports seront impactés ?
```

## 12. Exemple MayaBank

Besoin : représenter « OpenShift ».

Mauvaise approche :

```text
Créer MetaClass OpenShift
```

Approche plus robuste :

```text
Identifier la MetaClass standard pertinente
→ Software Technology / plateforme selon contexte
→ instance = Red Hat OpenShift
→ relations = applications supportées / standards / deployment context
```

## 13. Anti-patterns

- une MetaClass par produit ;
- un MetaAttribute pour chaque besoin ponctuel de reporting ;
- Association générique partout ;
- création d'une classe custom sans owner ;
- duplication d'une classe standard avec un autre nom ;
- modification du métamodèle directement en production sans cycle de test ;
- schéma GraphQL custom généré sans gouvernance de version.

## 14. Entretien

**Qu'est-ce qu'un métamodèle ?**  
Le modèle qui définit les types d'objets, propriétés, associations et règles structurantes du repository.

**Pourquoi est-il important pour une API ?**  
Parce que l'API expose des objets selon des schémas dérivés ou mappés à cette structure ; une extension du métamodèle peut donc avoir un impact d'intégration.
