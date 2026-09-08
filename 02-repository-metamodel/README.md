# Partie II — Repository, Metamodel & Object Model

Cette partie explique le cœur conceptuel de HOPEX : **le repository et le métamodèle qui donnent un sens aux objets, propriétés et relations**.

Le but n'est pas d'apprendre des écrans par cœur. Il faut comprendre pourquoi HOPEX sait distinguer une Application, une Business Capability, une Org-Unit, un Business Process ou une Software Technology, puis comment ces objets sont reliés et gouvernés.

## Contenu

1. [Repository as System of Record](01-repository-as-system-of-record.md)
2. [Metamodel Core Concepts](02-metamodel-core-concepts.md)
3. [MetaClass, Object & Instance](03-metaclass-object-instance.md)
4. [MetaAttribute, Properties & Values](04-metaattribute-properties-values.md)
5. [MetaAssociation, Ends & Cardinality](05-metaassociation-ends-cardinality.md)
6. [Identity, Naming, Keys & Deduplication](06-identity-naming-keys-deduplication.md)
7. [Hierarchy, Classification & Inheritance](07-hierarchy-classification-inheritance.md)
8. [Standard vs Custom Metamodel](08-standard-vs-custom-metamodel.md)
9. [GraphQL Metamodel Introspection](09-graphql-metamodel-introspection.md)
10. [MayaBank Canonical Object Model](10-mayabank-canonical-object-model.md)
11. [Governance & Anti-patterns](11-governance-antipatterns.md)
12. [Labs & Review Questions](12-labs-and-review.md)
13. [Official & Public Technical Sources](13-official-sources.md)

## Faits produit vérifiés utilisés dans cette partie

Le workspace public MEGA/Postman expose un endpoint GraphQL de métamodèle :

```text
/HOPEXGraphQL/api/MetaModel
```

La réponse d'exemple publiée contient notamment les métaclasses suivantes :

```text
MetaAttribute
MetaClass
MetaAssociation
MetaAssociationEnd
MetaModel
MetaAssociationType
MetaAttributeValue
MetaClassifier
MetaList
MetaViewport
...
```

Le Store officiel documente également un **GraphQL Mapping Json Generator** qui demande de créer un métamodèle dans **MetaStudio**, d'y placer la partie du métamodèle souhaitée, puis d'utiliser son identifiant pour générer le mapping JSON servant au schéma GraphQL.

Ces éléments donnent une base suffisamment solide pour comprendre que HOPEX dispose bien d'un **métamodèle explicite et interrogeable**, et que les schémas d'intégration dérivent de ce modèle.

## Chaîne mentale

```text
MetaModel
  ↓
MetaClass
  ↓
Object / Instance
  ↓
MetaAttribute → Value
  ↓
MetaAssociation → Related Object
  ↓
Repository graph
  ↓
Views / reports / analysis / APIs
```

## Principe MayaBank

Le repository cible doit éviter les objets créés pour un seul diagramme.

```text
Application canonique
+ identifiant
+ nom normalisé
+ owner
+ lifecycle
+ propriétés
+ relations
+ source de vérité
= objet réutilisable partout
```

## Résultat attendu

À la fin de cette partie, le lecteur doit pouvoir :

- expliquer la différence entre métamodèle et données du repository ;
- distinguer MetaClass, instance, MetaAttribute et MetaAssociation ;
- concevoir des relations sans transformer le repository en graphe arbitraire ;
- définir une stratégie d'identité et de déduplication ;
- expliquer quand étendre le métamodèle et quand ne pas le faire ;
- inspecter conceptuellement le métamodèle via GraphQL ;
- définir un modèle canonique MayaBank cohérent avant tout import massif ;
- identifier les anti-patterns de repository les plus dangereux.

## Règle d'or

```text
Un bon diagramme peut masquer un mauvais repository.
Un bon repository permet de produire plusieurs bons diagrammes.
```
