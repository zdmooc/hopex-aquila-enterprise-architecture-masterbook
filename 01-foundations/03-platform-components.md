# 03 — Architecture de plateforme et composants

## 1. Vue logique simplifiée

Le masterbook utilisera la vue logique suivante pour raisonner sur HOPEX Aquila :

```text
Users / Architects / Analysts / Admins
                ↓
        HOPEX Web Front-End
                ↓
         HOPEX Core Back-End
                ↓
           HOPEX Repository
                ↑
     ┌──────────┼───────────┐
     │          │           │
 GraphQL     REST API     Add-ons
     │          │           │
 GraphiQL   Documents     ServiceNow
     │       Diagrams       MCP
     └──────────┴───────────┘
                ↓
      External ecosystem / AI
```

C'est une vue pédagogique. Le détail d'installation dépend de l'architecture réelle du client et de la documentation de la release.

## 2. HOPEX Core Back-End

Le Core est le cœur fonctionnel de la plateforme :

- logique métier ;
- accès aux données du repository ;
- services nécessaires aux solutions ;
- base commune pour les modules/add-ons compatibles.

D'un point de vue architecte, le Core est la référence de compatibilité à contrôler lors d'un upgrade.

## 3. Web Front-End

Le front web fournit l'accès aux utilisateurs selon leurs profils et leurs solutions.

Ne pas confondre :

```text
Web Front-End = interface utilisateur
Repository = connaissance persistée
Core = logique et accès repository
```

Un problème d'affichage n'est donc pas automatiquement un problème de repository.

## 4. GraphQL

Le module GraphQL expose des schémas permettant de demander précisément les champs et relations nécessaires.

Mental model :

```text
Client
→ GraphQL endpoint
→ schema
→ query / mutation
→ repository
→ réponse JSON
```

Intérêts :

- requêtes ciblées ;
- introspection du schéma ;
- lecture des relations ;
- mutations lorsqu'elles sont autorisées ;
- intégration avec applications et dashboards.

## 5. REST API HOPEX

Le module REST fournit des capacités d'intégration autour du repository. Le Store officiel mentionne notamment :

- read/write ;
- documents ;
- export de diagrammes.

Point important : l'API REST HOPEX actuelle s'appuie sur des mécanismes liés au framework GraphQL. Il faut donc étudier la documentation de la release avant de projeter une architecture générique « REST classique ».

## 6. GraphQL IDE

GraphQL IDE fournit un environnement GraphiQL destiné aux développeurs.

Usage dans notre futur lab :

```text
1. explorer le schema
2. identifier le type Application
3. sélectionner id/name/lifecycle
4. ajouter relations utiles
5. filtrer/paginer
6. valider la réponse
7. transformer la requête en intégration automatisée
```

Nous ne fabriquerons pas de schémas HOPEX inexistants : les exemples concrets devront être vérifiés contre un environnement ou une documentation officielle accessible.

## 7. MCP Server

HOPEX MCP Server est un add-on officiel apparu dans la branche Aquila actuelle.

Conceptuellement :

```text
AI client / agent
→ MCP
→ HOPEX MCP Server
→ GraphQL / repository
→ connaissance d'architecture contrôlée
```

Cas d'usage potentiels :

- rechercher une application ;
- résumer ses dépendances ;
- identifier un owner ;
- préparer une analyse d'impact ;
- enrichir un assistant d'architecture.

Mais le design doit traiter :

- authentification ;
- autorisation ;
- portée des données ;
- informations sensibles ;
- audit ;
- hallucination côté client IA ;
- distinction lecture / mutation.

## 8. ServiceNow Integration

Le connecteur officiel est particulièrement intéressant pour les entreprises possédant :

```text
HOPEX = architecture logique / portfolio / transformation
ServiceNow = CMDB / configuration opérationnelle / ITSM
```

Questions d'architecture :

- quel système est source maître de l'Application ?
- quel identifiant permet le rapprochement ?
- quels objets sont synchronisés ?
- dans quel sens ?
- quelle fréquence ?
- que faire d'une suppression ?
- comment gérer les conflits ?
- comment mesurer la qualité ?

## 9. Data flow d'intégration recommandé

Ne pas commencer par « connecter tout ».

Commencer par :

```text
Use case
→ objects required
→ source of truth
→ keys
→ mapping
→ direction
→ frequency
→ validation
→ monitoring
→ rollback / reconciliation
```

## 10. Exemple MayaBank

Scénario futur :

```text
ServiceNow CMDB
  fournit instances techniques et CIs
        ↓
Integration
        ↓
HOPEX
  rapproche applications logiques
        ↓
Enterprise Architecture
  ajoute capability, business owner, lifecycle, roadmap
        ↓
MCP / GraphQL
  permet interrogation assistée du référentiel
```

Le principe est de **compléter** les sources, pas de créer deux inventaires concurrents.

## 11. Points de revue d'architecture

- compatibilité versions ;
- disponibilité des add-ons ;
- licences ;
- authentication ;
- authorization ;
- network flows ;
- secrets ;
- monitoring ;
- API quotas éventuels ;
- error handling ;
- data ownership ;
- sync semantics ;
- auditability ;
- upgrade strategy.
