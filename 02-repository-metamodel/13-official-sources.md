# 13 — Official & Public Technical Sources

Cette page sépare les sources **officielles MEGA/Bizzdesign** des sources techniques publiques utilisées pour comprendre les APIs.

## 1. HOPEX Core Back-End Aquila 6.2

Store officiel :

https://store.mega.com/modules/details/hopex.core

Points utilisés :

- HOPEX Core Back-End Aquila 6.2 ;
- branche 62.18.x observée en septembre 2026 ;
- logique métier ;
- accès au repository ;
- single source of truth reliant business, IT, data et risk.

## 2. HOPEX Aquila bundle / plateforme

Store officiel :

https://store.mega.com/bundles/details/cff0da43-8c3e-46e9-8560-97567c79622a

Points utilisés :

- plateforme Connected EA ;
- connexion EA, BPM, Data et Risk ;
- automation ;
- dashboards / analysis ;
- composition modulaire.

## 3. HOPEX REST API / GraphQL public workspace

Workspace public MEGA International sur Postman :

https://www.postman.com/mega-international/mega-international-s-public-workspace/documentation/27vy1fl/hopex-rest-api-v5

Points utilisés :

- endpoint GraphQL ITPM ;
- lecture/écriture repository ;
- exemple `application { id name }` ;
- endpoint BPA ;
- endpoint Data ;
- endpoint MetaModel ;
- exemples de headers de contexte.

## 4. MetaModel GraphQL query

Postman public :

https://www.postman.com/mega-international/mega-international-s-public-workspace/request/5zrnh64/metamodel-graphql-query-synchronous

Exemple public :

```graphql
query {
  metaClass(filter: {name_starts_with:"Meta"}) {
    name
  }
}
```

La réponse exemple contient notamment :

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

Cette source supporte directement les chapitres sur les concepts de métamodèle et l'introspection GraphQL.

## 5. GraphQL Mapping Json Generator

Store officiel :

https://store.mega.com/modules/details/graphql.mappingjsongenerator

Points utilisés :

- génération des mapping JSON servant aux schémas GraphQL ;
- besoin du thick client ;
- workflow MetaStudio ;
- création d'un Metamodel ;
- ajout d'un diagramme contenant le fragment du métamodèle ;
- usage de l'identifiant du métamodèle ;
- possibilité de travailler sur un custom metamodel ou le default metamodel.

## 6. ITPM Excel Import Template

Store officiel :

https://store.mega.com/modules/details/itpm.importexceltemplate

Points utilisés :

- import ITPM ;
- création automatique de Person (System) dans certains cas ;
- génération d'une Business Capability Map avec composition hiérarchique correcte ;
- usage de la metaclass `Content` dans une évolution du template ;
- colonnes Vendor pour Software Technology ;
- attributs Org-Unit-Type et Internal/External.

Cette source confirme l'importance pratique des MetaClasses, hiérarchies et propriétés dans les imports.

## 7. Nature des preuves

### Vérifié directement par source officielle/public workspace

- existence de MetaClass/MetaAttribute/MetaAssociation/MetaAssociationEnd ;
- endpoint MetaModel ;
- exemples GraphQL ITPM/BPA ;
- workflow MetaStudio du générateur de mapping ;
- template ITPM et capability hierarchy.

### Modèle pédagogique du masterbook

- clés `APP-PAY-001`, `CAP-PAY-001`, etc. ;
- lifecycle pédagogique Draft→Published→Retired ;
- liste de propriétés MayaBank ;
- matrice source-of-truth proposée ;
- règles de gouvernance et Definition of Done ;
- granularité recommandée.

Ces éléments ne sont pas présentés comme des écrans ou métaclasses standard HOPEX garantis.

## 8. Points volontairement non affirmés comme normes produit

Le masterbook ne fixe pas sans vérification cible :

- cardinalités exactes de chaque MetaAssociation ;
- structure exacte d'héritage des MetaClasses ;
- noms de tous les attributs standards ;
- comportement exact de chaque identifiant interne/externe ;
- permissions par défaut ;
- disponibilité de chaque schéma GraphQL dans toute installation.

Ces informations dépendent de la solution, du métamodèle, de la licence, du profil et de la version.

## 9. Règle de vérification

Avant un lab réel :

```text
Product version
+ installed solution
+ license
+ metamodel
+ profile
+ exposed schema
+ API documentation
= source of truth for execution
```

## 10. Prochaine étape

La Partie III utilisera ce socle pour étudier l'expérience de travail :

```text
Web Front-End
→ navigation
→ object pages
→ properties
→ searches
→ workspaces
→ diagrams
→ collaboration
```

sans perdre la distinction essentielle entre **UI** et **repository semantics**.
