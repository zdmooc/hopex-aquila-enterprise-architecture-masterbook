# 02 — Qu'est-ce que HOPEX ?

## 1. Une plateforme EAM, pas un outil de dessin

HOPEX sert à représenter l'entreprise dans un référentiel structuré et exploitable. La valeur n'est donc pas seulement dans les diagrammes, mais dans la capacité à relier les objets entre eux et à analyser leurs dépendances.

Mental model :

```text
Objet
+ propriétés
+ relations
+ ownership
+ lifecycle
+ source / qualité
+ vues
+ rapports
= information d'architecture gouvernable
```

Un diagramme n'est qu'une représentation d'une partie de ce graphe.

## 2. Digital representation of the enterprise

Le Core HOPEX est présenté par MEGA comme une plateforme permettant de connecter les perspectives business, IT, data et risk dans une source commune de connaissance.

Pour un architecte, cela signifie qu'un même objet peut être réutilisé dans plusieurs analyses :

```text
Application Payment Orchestrator
→ supporte une capacité
→ participe à un processus
→ consomme une API
→ dépend d'une base
→ est hébergée sur une plateforme
→ possède un lifecycle
→ est portée par un owner
→ apparaît dans un roadmap
```

Le même objet ne doit pas être recréé indépendamment dans chaque diagramme.

## 3. Les grandes familles d'usage

HOPEX peut être utilisé pour :

- Enterprise Architecture ;
- IT Architecture ;
- Business Architecture ;
- Business Process Analysis ;
- Information Architecture ;
- Data Governance ;
- IT Business Management ;
- IT Portfolio Management ;
- Integrated Risk Management ;
- analyses de transformation ;
- intégration avec l'écosystème SI.

Le périmètre exact dépend des solutions et licences installées.

## 4. Référentiel vs fichier

Dans un outil de dessin classique :

```text
Diagramme A contient une boîte Application X
Diagramme B contient une autre boîte Application X
```

Les deux boîtes peuvent diverger.

Dans un repository bien gouverné :

```text
Application X = objet canonique
View A → représente Application X
View B → représente Application X
Report → interroge Application X
API → lit Application X
Roadmap → exploite le lifecycle de Application X
```

C'est cette logique qui donne sa valeur à une plateforme EAM.

## 5. Architecture knowledge graph

On peut mentalement voir HOPEX comme un graphe de connaissance gouverné :

```text
Capability
   ↓ supported/realized by
Business Process
   ↓ supported by
Application
   ↓ deployed on / depends on
Technology
   ↓ hosted in
Infrastructure

+ Owners
+ Lifecycles
+ Risks
+ Projects
+ Standards
+ Data
```

La terminologie réelle des objets et relations dépend du métamodèle HOPEX activé. La Partie II étudiera précisément cette couche.

## 6. Ce qui fait la qualité d'un repository

Un repository n'est pas bon parce qu'il contient beaucoup d'objets.

Il est bon si :

- les objets ont un sens non ambigu ;
- les doublons sont contrôlés ;
- les propriétés utiles sont renseignées ;
- les relations sont cohérentes ;
- les owners sont identifiés ;
- les données ont une source ;
- les lifecycles sont exploitables ;
- les vues répondent à des concerns ;
- les rapports permettent une décision ;
- les données obsolètes sont détectées.

## 7. Exemple MayaBank

Mauvais référentiel :

```text
"Kafka"
"Kafka Prod"
"Kafka Cluster"
"Kafka Payment"
"Event Bus"
"Kafka New"
```

sans définition, owner ni relations.

Meilleur référentiel :

```text
Technology / Platform object: MayaBank Event Streaming Platform
Product/implementation data: Kafka
Owner: Platform Engineering
Lifecycle: strategic
Supports: Payment Event Streaming
Hosted environments: Prod / Preprod
Consumers: Payment Orchestrator, Fraud, Notifications
```

La granularité exacte sera décidée selon le métamodèle et les objectifs de gouvernance.

## 8. HOPEX vs CMDB

Une CMDB vise principalement la configuration opérationnelle et les CIs nécessaires au run. Un EAM vise principalement la compréhension, la décision et la gouvernance de l'architecture.

Les deux peuvent se compléter :

```text
HOPEX
Application logique / capability / roadmap / strategy
      ↕ synchronisation contrôlée
ServiceNow CMDB
CIs / instances / infra observée / relations opérationnelles
```

Le piège est de dupliquer intégralement la CMDB dans HOPEX. Il vaut mieux définir les responsabilités de chaque source.

## 9. HOPEX vs ArchiMate

ArchiMate = langage.
HOPEX = plateforme/repository et solutions.

On peut utiliser des concepts ArchiMate dans des modèles HOPEX lorsque le support et le métamodèle le permettent, mais :

```text
Objet HOPEX ≠ automatiquement élément ArchiMate
Diagramme HOPEX ≠ automatiquement View ArchiMate normative
```

La sémantique doit être explicitée.

## 10. HOPEX vs TOGAF

TOGAF fournit une méthode et une structure de gouvernance d'architecture. HOPEX peut soutenir certaines activités de repository, vues, roadmaps, portefeuille et traçabilité, mais le produit n'est pas la méthode elle-même.

```text
TOGAF = comment conduire et gouverner l'architecture
ArchiMate = comment exprimer visuellement des concepts
HOPEX = où gérer, relier, analyser et gouverner les données d'architecture
```

## 11. Questions d'entretien

**Pourquoi utiliser HOPEX plutôt que PowerPoint ?**
Parce que PowerPoint documente une représentation ; HOPEX permet de gérer des objets partagés, leurs relations, leur lifecycle et leurs analyses.

**Pourquoi un repository commun ?**
Pour éviter des inventaires indépendants et permettre la traçabilité entre business, applications, data, technology, risques et transformation.

**Quel risque principal ?**
Transformer le repository en cimetière de données non gouvernées. Un outil EAM sans ownership et processus de qualité perd rapidement sa valeur.
