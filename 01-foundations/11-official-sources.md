# 11 — Sources officielles de la Partie I

Cette page sépare les faits produit vérifiés des conventions pédagogiques du masterbook.

## Sources MEGA / HOPEX vérifiées le 8 septembre 2026

### HOPEX Core Back-End Aquila 6.2

https://store.mega.com/modules/details/hopex.core

Faits utilisés :

- Core Back-End Aquila 6.2 ;
- logique métier et accès repository ;
- version 62.18.0+774 observée ;
- publication du build 03/09/2026.

### HOPEX Aquila Web Front-End

https://store.mega.com/modules/details/hopex.dtpx

Faits utilisés :

- portail web ;
- profils EA, process modeling, risk, audit et stakeholders ;
- version 62.18.0+143 observée ;
- publication 02/09/2026.

### HOPEX GraphQL

https://store.mega.com/modules/details/hopex.graphql

Faits utilisés :

- API layer GraphQL ;
- endpoint/schema driven ;
- queries et mutations ;
- introspection ;
- version 62.18.0+69 observée ;
- publication 02/09/2026.

### HOPEX REST API

https://store.mega.com/modules/details/hopex.rest.api

Faits utilisés :

- lecture/écriture du repository ;
- documents upload/download ;
- export de diagrammes ;
- accès dépendant des solutions/licences ;
- version 62.18.0+69 observée ;
- publication 02/09/2026.

### HOPEX MCP Server

https://store.mega.com/modules/details/hopex.mcp.server

Faits utilisés :

- add-on MCP officiel ;
- dépendance GraphQL ;
- tag AI ;
- version 62.18.0+8 observée ;
- build publié le 24/08/2026.

### HOPEX GraphQL IDE

https://store.mega.com/modules/details/graphql.ide

Faits utilisés :

- IDE GraphQL / GraphiQL ;
- dépendances GraphQL et REST API selon version.

### ServiceNow Integration

https://store.mega.com/modules/details/servicenow.integrations.hopex

Faits utilisés :

- intégration officielle ;
- scheduler ;
- connexion sécurisée ;
- Aquila 6.2 ;
- licence HOPEX ServiceNow requise ;
- accès ServiceNow séparé.

### Training Database

https://store.mega.com/modules/details/backup.training

Faits utilisés :

- HOPEX 6.2 CU5 Training ;
- SQL Server 2022 ;
- données de cours pour ITBM, ITPM, BPA, IT Architecture, Information Architecture, Data Governance et IRM.

### Demo Database

https://store.mega.com/modules/details/backup.demo

Faits utilisés :

- backup de démonstration Aquila 6.2 ;
- données, rapports et utilisateurs de démo ;
- SQL Server 2022 ;
- version à aligner avec Core.

## Documentation HOPEX

Le Store référence aussi la documentation Aquila :

https://doc.mega.com/hopex-aquila-en

Certaines pages ou fonctionnalités peuvent nécessiter une authentification ou une licence.

## Frontière normative du masterbook

Les éléments suivants sont **pédagogiques** et ne sont pas présentés comme normes HOPEX :

- IDs `MB-APP-xxx`, `MB-CAP-xxx`, etc. ;
- exemples de lifecycle `Strategic/Tolerated/Sunset` ;
- RACI ;
- source-of-truth matrix MayaBank ;
- noms de relations conceptuels lorsque le métamodèle natif n'a pas encore été vérifié ;
- architecture MayaBank ;
- datasets CSV futurs ;
- processus de revue proposé.

## Règle pour la suite

Avant d'introduire une fonctionnalité spécifique HOPEX dans une nouvelle partie :

1. chercher une source officielle actuelle ;
2. vérifier la version ;
3. distinguer Core / solution / add-on ;
4. vérifier licences et dépendances ;
5. ne pas recopier de documentation propriétaire longue ;
6. paraphraser et citer la source ;
7. signaler explicitement les simulations pédagogiques.
