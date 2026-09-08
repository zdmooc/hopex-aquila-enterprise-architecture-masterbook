# 01 — Baseline produit HOPEX Aquila

## 1. Pourquoi figer une baseline

HOPEX évolue par releases et modules. Dans un projet réel, il faut donc distinguer :

- la version du **Core Back-End** ;
- la version du **Web Front-End** ;
- les versions des **add-ons** ;
- les dépendances entre modules ;
- les licences fonctionnelles disponibles ;
- la version de la base de données de démonstration ou de formation.

Une documentation d'architecture qui dit seulement « HOPEX 6.2 » peut être insuffisante pour diagnostiquer une incompatibilité ou reproduire un lab.

## 2. Baseline observée au 8 septembre 2026

### Core Back-End

Le Store MEGA publie **HOPEX Core Back-End Aquila 6.2**. La version observée la plus récente est :

```text
62.18.0+774
publication : 03/09/2026
module : hopex.core
kind : Hopex
publisher : MEGA International
```

Le Core porte notamment la logique métier et l'accès au repository.

### Web Front-End

Le module `hopex.dtpx` fournit le portail web HOPEX Aquila. La version observée :

```text
62.18.0+143
publication : 02/09/2026
module : hopex.dtpx
publisher : MEGA International
```

Il est destiné à plusieurs profils, dont architectes d'entreprise, process modelers, risk managers, auditors et autres stakeholders EA/GRC.

### HOPEX GraphQL

Baseline observée :

```text
62.18.0+69
publication : 02/09/2026
module : hopex.graphql
```

Le module expose le repository au travers d'un schéma GraphQL. Il permet des **queries** et des **mutations** et offre un modèle self-describing exploitable par introspection.

### HOPEX REST API

Baseline observée :

```text
62.18.0+69
publication : 02/09/2026
module : hopex.rest.api
```

Le Store décrit notamment :

- lecture/écriture du repository ;
- upload/download de documents ;
- export de diagrammes ;
- accès à des objets comme applications, business processes et capabilities selon les schémas/licences disponibles.

### HOPEX MCP Server

Baseline observée :

```text
62.18.0+8
publication : 24/08/2026
module : hopex.mcp.server
```

Le module dépend de `hopex.graphql` et permet d'exposer des capacités HOPEX via MCP. Cela ouvre des scénarios d'assistance IA, d'interrogation contrôlée du référentiel et d'intégration avec des clients supportant le protocole.

### GraphQL IDE

HOPEX dispose également d'un module **GraphQL IDE** basé sur GraphiQL pour aider les développeurs à explorer les schémas et construire les requêtes.

### ServiceNow Integration

Un add-on officiel `servicenow.integrations.hopex` existe pour Aquila 6.2. Le Store mentionne notamment :

- synchronisation HOPEX / ServiceNow ;
- planification via scheduler ;
- connexion sécurisée aux deux plateformes ;
- besoin d'une licence HOPEX ServiceNow ;
- accès ServiceNow séparé.

Ce module sera traité en détail en Partie XX.

## 3. Base de formation officielle

Le Store fournit une sauvegarde de base destinée à la formation :

```text
HOPEX Databases backup — HOPEX 6.2 CU5 — Training
SQL Server 2022
```

Elle contient des données utilisées dans plusieurs cursus :

- HOPEX IT Business Management ;
- HOPEX IT Portfolio Management ;
- HOPEX Business Process Analysis ;
- HOPEX IT Architecture ;
- HOPEX Information Architecture ;
- HOPEX Data Governance ;
- HOPEX Integrated Risk Management.

Cela confirme que l'écosystème HOPEX est multi-domaines et que le repository peut être exploité par plusieurs solutions complémentaires.

## 4. Base Demo

Une base de démonstration Aquila 6.2 est également publiée pour tests/démonstrations, avec données, rapports et utilisateurs de presales. Elle requiert SQL Server 2022 et doit correspondre à la version du Core concerné.

## 5. Règle de compatibilité

Ne jamais raisonner :

```text
module 62.x + Core 62.x = forcément compatible
```

Toujours vérifier :

```text
Core exact
+ version module
+ dépendances déclarées
+ licence fonctionnelle
+ prérequis runtime / DB
+ documentation release
```

## 6. Baseline MayaBank proposée

Pour les labs documentaires du masterbook :

```text
Produit de référence : HOPEX Aquila 6.2
Branche documentaire : 62.18.x
Base logique : repository MayaBank fictif
Intégrations étudiées : REST / GraphQL / ServiceNow / MCP
DB de lab réelle : seulement si accès officiel disponible
```

Nous n'intégrerons jamais dans GitHub un backup propriétaire HOPEX ni des contenus de formation non redistribuables.

## 7. Checklist architecte

Avant toute mission HOPEX, demander :

1. version exacte du Core ;
2. mode de déploiement ;
3. environnement(s) disponibles ;
4. modules installés ;
5. licences fonctionnelles ;
6. métamodèle standard ou customisé ;
7. sources maîtres des données ;
8. intégrations existantes ;
9. règles de gouvernance ;
10. propriétaires des objets ;
11. processus de publication/validation ;
12. stratégie de montée de version.

## 8. Erreurs fréquentes

- apprendre une capture d'écran d'une ancienne release comme vérité produit ;
- confondre version marketing Aquila 6.2 et build technique ;
- supposer qu'un add-on est installé parce qu'il existe dans le Store ;
- supposer que la REST API donne accès à toutes les données sans licence fonctionnelle ;
- concevoir une intégration sans connaître les droits et schémas réellement exposés ;
- prendre une base Demo pour une architecture de production.
