# 10 — Anti-patterns, labs et revue de Partie I

## 1. Anti-patterns à éliminer

### 1.1 HOPEX = Visio amélioré
Erreur : ne voir que les diagrammes.

Correction : raisonner objets, relations, propriétés, owners, lifecycle, sources et analyses.

### 1.2 Tout mettre dans HOPEX
Erreur : vouloir remplacer CMDB, ERP, Data Catalog et GRC par un seul repository.

Correction : définir les sources maîtres et synchronisations nécessaires.

### 1.3 Copier chaque environnement
Erreur : créer une application logique DEV, UAT et PROD alors que le concern est portfolio.

Correction : distinguer application logique, déploiement et CI.

### 1.4 Personnaliser avant de comprendre
Erreur : créer immédiatement de nouveaux types et relations.

Correction : comprendre le métamodèle standard, puis justifier chaque extension par un use case durable.

### 1.5 Tout importer de ServiceNow
Erreur : reproduire toute la CMDB.

Correction : importer ou rapprocher seulement les objets/relations utiles à la décision EA.

### 1.6 Absence d'owner
Erreur : le repository steward devient responsable de la vérité de tous les objets.

Correction : owner métier/IT + steward + source system + cycle de revue.

### 1.7 Lifecycle sans conséquence
Erreur : marquer une technologie « obsolete » sans workflow ou décision.

Correction : relier lifecycle à standards, projets, exceptions et roadmaps.

### 1.8 API = accès total
Erreur : croire que REST/GraphQL permet tout.

Correction : vérifier licence, schéma, authentication, authorization et mutations disponibles.

### 1.9 Diagramme = vérité
Erreur : ajouter une boîte visuelle sans objet canonique gouverné.

Correction : le diagramme doit représenter la connaissance du repository.

### 1.10 Standard = produit
Erreur : confondre TOGAF/ArchiMate avec HOPEX.

Correction : garder méthode, langage et plateforme distincts.

---

# LAB 01 — Expliquer HOPEX en 5 minutes

Sans notes, expliquer :

```text
1. problème résolu
2. repository
3. Core / Web
4. solutions
5. API/intégrations
6. gouvernance
```

Critère : ne jamais dire seulement « outil de cartographie ».

---

# LAB 02 — Sources of truth MayaBank

Pour chaque donnée, choisir la source maître :

- application logique ;
- serveur PROD ;
- business owner ;
- technology version détectée ;
- lifecycle target ;
- coût réel ;
- risque ;
- architecture principle.

Puis justifier les synchronisations.

Exemple :

```text
Server PROD → ServiceNow CMDB
Application logical record → HOPEX
Business owner → HOPEX/HR/Org source selon gouvernance
```

Il n'existe pas une réponse universelle : l'objectif est de rendre le contrat de données explicite.

---

# LAB 03 — Détecter les doublons

Inventaire brut :

```text
Payment Orchestrator
PAYMENT ORCHESTRATOR
Payment Orch PROD
Payment-Orch
Legacy Payment Hub
Legacy Payment Hub PROD
Kafka Payment
Kafka Cluster PROD
Event Streaming Platform
```

Pour chaque ligne, décider :

- duplicate ;
- alias ;
- instance ;
- environment ;
- application ;
- technology platform.

Puis construire le modèle canonique minimal.

---

# LAB 04 — Persona / Concern / View

Associer :

| Persona | Concern |
|---|---|
| CIO | rationalisation |
| Solution Architect | dependencies |
| CISO | blast radius / risk |
| Platform Architect | technology standards |
| Business Architect | capabilities/processes |
| Portfolio Manager | lifecycle |

Pour chacun, définir les objets minimum à montrer. Ne pas proposer une seule vue universelle.

---

# LAB 05 — Architecture d'intégration

Dessiner en texte :

```text
ServiceNow
→ Integration
→ HOPEX
→ GraphQL / REST
→ Architecture Assistant
```

Ajouter :

- source master ;
- IDs ;
- authentication ;
- read/write direction ;
- frequency ;
- error handling ;
- audit.

---

# LAB 06 — Classifier les concepts

Classer dans l'une des catégories :

```text
STANDARD / METHOD
HOPEX PRODUCT
HOPEX ADD-ON
BUSINESS/EA CONCEPT
EXTERNAL SYSTEM
```

Éléments :

- ArchiMate ;
- TOGAF ;
- HOPEX Core ;
- GraphQL ;
- MCP Server ;
- Capability ;
- ServiceNow CMDB ;
- Payment Orchestrator ;
- Business Process ;
- REST API HOPEX.

---

# LAB 07 — Questions d'entretien

Répondre en moins de 90 secondes à chacune :

1. Qu'est-ce que HOPEX ?
2. Pourquoi un repository EAM ?
3. HOPEX vs CMDB ?
4. HOPEX vs ArchiMate ?
5. HOPEX vs TOGAF ?
6. Pourquoi GraphQL ?
7. Comment intégrer ServiceNow ?
8. Comment éviter les doublons ?
9. Qui est responsable de la qualité ?
10. Comment commencer un programme HOPEX ?

---

# 20 questions de contrôle

1. Quel composant porte la logique métier et l'accès repository ?
2. Quel composant fournit le portail web ?
3. Quel module permet queries/mutations GraphQL ?
4. Quel module permet notamment read/write et export de diagrammes ?
5. Quel add-on 2026 expose HOPEX via MCP ?
6. Pourquoi la version exacte du Core est-elle importante ?
7. Pourquoi un repository n'est-il pas une collection de fichiers ?
8. Qu'est-ce qu'un objet canonique ?
9. Pourquoi un owner est-il nécessaire ?
10. Pourquoi HOPEX ne doit-il pas recopier toute la CMDB ?
11. Quelle différence entre application logique et CI ?
12. Pourquoi un lifecycle doit-il avoir une gouvernance ?
13. HOPEX est-il un langage ?
14. ArchiMate est-il une plateforme EAM ?
15. TOGAF est-il un repository ?
16. Pourquoi utiliser un stable ID ?
17. Quel rôle joue le steward ?
18. Pourquoi limiter la personnalisation ?
19. Quelle est la valeur d'une training database ?
20. Quelle information est interdite dans un GitHub public ?

## Réponses courtes

1. HOPEX Core Back-End.
2. HOPEX Aquila Web Front-End.
3. HOPEX GraphQL.
4. HOPEX REST API.
5. HOPEX MCP Server.
6. Pour compatibilité des modules/add-ons et reproduire l'environnement.
7. Les mêmes objets sont partagés entre vues, rapports et analyses.
8. L'objet de référence réutilisé partout.
9. Pour garantir sens, validation et maintien de la donnée.
10. Les responsabilités et granularités sont différentes.
11. L'application est logique ; le CI représente une configuration/instance opérationnelle.
12. Un statut sans règle ni conséquence ne permet pas de décision.
13. Non.
14. Non.
15. Non.
16. Les noms changent ; l'identité doit rester stable.
17. Qualité, cohérence et facilitation du processus de gouvernance.
18. Pour éviter un métamodèle local incompréhensible et coûteux à maintenir.
19. Pratiquer avec un jeu de données prévu pour la formation.
20. Secrets, tokens, backups propriétaires et données client réelles.

## Checklist de sortie Partie I

- [ ] Je sais expliquer HOPEX sans écran.
- [ ] Je distingue Core, Front, Repository et APIs.
- [ ] Je connais les principales familles de solutions.
- [ ] Je distingue HOPEX, ArchiMate et TOGAF.
- [ ] Je sais définir une source de vérité.
- [ ] Je sais expliquer HOPEX vs CMDB.
- [ ] Je peux présenter le cas MayaBank.
- [ ] Je sais citer les limites d'accès/licence.
- [ ] Je sais expliquer pourquoi la gouvernance du repository est centrale.
- [ ] Je suis prêt pour le métamodèle de la Partie II.
