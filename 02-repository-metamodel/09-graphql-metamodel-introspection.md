# 09 — GraphQL Metamodel Introspection

## 1. Pourquoi l'introspection est utile

Un architecte d'intégration ne doit pas deviner les objets disponibles. Le schéma doit être interrogé ou inspecté.

HOPEX fournit un endpoint public documenté pour le métamodèle :

```text
POST /HOPEXGraphQL/api/MetaModel
```

Exemple publié :

```graphql
query {
  metaClass(filter: {name_starts_with:"Meta"}) {
    name
  }
}
```

## 2. Contexte HOPEX

L'exemple Postman public montre des headers de contexte tels que :

```text
x-hopex-environment-id
x-hopex-repository-id
x-hopex-profile-id
Content-Type: application/json
Authorization: Bearer ...
```

Les mécanismes exacts d'authentification/configuration doivent être vérifiés sur l'environnement cible.

## 3. Résultat conceptuel

L'API peut retourner des métaclasses comme :

```json
{
  "data": {
    "metaClass": [
      {"name":"MetaAttribute"},
      {"name":"MetaClass"},
      {"name":"MetaAssociation"},
      {"name":"MetaAssociationEnd"},
      {"name":"MetaModel"}
    ]
  }
}
```

## 4. Pourquoi c'est important

Avant de coder :

```text
inspect schema
→ identify object type
→ identify fields
→ identify relationships
→ identify mutation capabilities
→ test with read-only query
→ only then design integration
```

## 5. Schéma fonctionnel vs MetaModel API

Deux usages différents :

### MetaModel
Comprendre la structure du référentiel.

### Solution schema
Interroger les objets métier exposés par une solution, par exemple ITPM ou BPA selon les schémas configurés.

Le workspace public montre notamment :

```text
/api/ITPM
/api/BPA
/api/Data
/api/MetaModel
```

## 6. Exemple ITPM public

Une requête publique :

```graphql
query {
  application {
    id
    name
  }
}
```

Cela montre que la MetaClass/entité `Application` peut être exposée par le schéma ITPM.

## 7. Exemple BPA public

```graphql
query {
  businessprocess {
    id
    name
  }
}
```

Le nom de champ exact dépend du mapping de schéma.

## 8. Introspection GraphQL standard

Quand elle est autorisée, GraphQL permet typiquement d'explorer :

```graphql
query {
  __schema {
    queryType { name }
    mutationType { name }
  }
}
```

Ne pas supposer que l'introspection est ouverte dans tous les environnements de production ; cela relève de la configuration et de la sécurité.

## 9. GraphQL Mapping Json Generator

Le Store officiel indique qu'un générateur construit les fichiers JSON utilisés comme schémas GraphQL à partir d'un métamodèle HOPEX sélectionné.

Chaîne mentale :

```text
HOPEX Metamodel
→ selected custom/default fragment
→ mapping JSON
→ GraphQL schema
→ queries/mutations
```

## 10. Contract testing

Une intégration doit disposer de tests de contrat :

```text
expected type exists
expected field exists
required relationship exists
mutation still accepted
permissions still correct
```

À exécuter après :

- upgrade HOPEX ;
- changement métamodèle ;
- changement mapping GraphQL ;
- changement profile/rights.

## 11. MayaBank — découverte de schéma

Avant synchronisation ServiceNow → HOPEX :

```text
1. inspect Application exposure
2. inspect external key field strategy
3. inspect owner/domain relationships
4. inspect lifecycle fields
5. test query on 5 records
6. test mutation in sandbox
7. define idempotent upsert behavior
```

## 12. Ne pas hardcoder trop tôt

Mauvais :

```javascript
application.vendor.name = ...
```

sans avoir confirmé que ce chemin existe dans le schéma cible.

Meilleur :

```text
schema discovery
+ generated/controlled client mapping
+ contract tests
```

## 13. Sécurité

Ne jamais :

- stocker token dans Git ;
- utiliser un compte administrateur pour une intégration normale ;
- demander plus de droits que nécessaire ;
- exposer MetaModel en production sans décision de sécurité ;
- journaliser des secrets.

## 14. Résilience

Une intégration GraphQL doit gérer :

- timeout ;
- retry contrôlé ;
- erreurs partielles ;
- pagination ;
- rate/volume ;
- idempotence ;
- reprise après échec ;
- observabilité.

## 15. Questions d'entretien

**Pourquoi interroger `/MetaModel` ?**  
Pour comprendre les types et concepts exposés par le métamodèle au lieu de coder à partir d'hypothèses.

**Pourquoi générer un schéma GraphQL depuis un métamodèle custom ?**  
Pour exposer de manière contrôlée un sous-ensemble cohérent des objets/propriétés/relations nécessaires à l'intégration.
