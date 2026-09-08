# 99 — Sources officielles, faits vérifiés et frontière d’interprétation

## 1. Baseline de vérification

Sources publiques consultées en septembre 2026.

Objectif : distinguer clairement :

```text
Verified Hopex product fact
vs
Architecture / graph-analysis best practice
vs
MayaBank teaching hypothesis
```

---

# A. Sources Bizzdesign Hopex

## 2. Bizzdesign Hopex — page produit

Source :

`https://bizzdesign.com/transformation-suite/hopex`

Version ressources :

`https://resources.bizzdesign.com/transformation-suite/hopex`

Faits publics utilisés :

- Hopex connecte business, IT, risk et data dans une source de vérité ;
- cartographie des data flows et dependencies ;
- détection de risques et impacts cachés ;
- lifecycle application/technology ;
- analyses multidimensionnelles ;
- support de la transformation.

La page publique française exprime également la capacité à cartographier les flux de données et dépendances afin d’identifier risques et impacts cachés.

---

## 3. Bizzdesign Hopex — page française

Source :

`https://bizzdesign.com/fr/suite-logicielle-de-transformation/bizzdesign-hopex`

Fait public retenu :

```text
Cartographier les flux de données et les dépendances
pour détecter les risques et les impacts cachés.
```

Cette formulation soutient directement le positionnement de la Partie XII.

---

## 4. Global Bank case study

Source :

`https://bizzdesign.com/customers/customer-stories/banking-platforms`

Faits publics utilisés :

- repository enterprise partagé ;
- identification d’applications inutilisées et decommissioning ;
- workflows d’attestation ;
- data quality ;
- impact analysis ;
- what-if analysis pour transformation planning.

Ce cas soutient l’usage de dependency/impact analysis pour décision et transformation.

---

## 5. Nordea — Application Management & Rationalization

Source :

`https://bizzdesign.com/customers/customer-stories/how-nordea-uses-application-management-achieve-rationalization`

Faits publics utilisés :

- repository centralisé d’applications ;
- information réutilisable et maintenable ;
- dependency mapping ;
- impact analysis pour planification de changement ;
- incident management analysis ;
- publication interne de l’information.

---

## 6. Mid-Market Company — connected repository

Source :

`https://bizzdesign.com/customers/customer-stories/mid-market-company`

Faits publics utilisés :

- repository connecté ;
- cartographie personnes/processus/technologies ;
- difficulté des spaghetti diagrams trop complexes ;
- approche par couches ;
- usage Hopex 360 pour diffusion ;
- Architecture Council.

Cette source soutient la règle du masterbook : ne pas construire une carte géante illisible.

---

## 7. Global Insurance Company — connected repository

Source :

`https://bizzdesign.com/customers/customer-stories/global-insurance-company`

Faits publics utilisés :

- vues architecturales centralisées ;
- connexion business, IT, risk et data ;
- capability maps ;
- liens risks ↔ processes ;
- shared source of truth.

---

## 8. Large Global Insurer

Source :

`https://bizzdesign.com/customers/customer-stories/large-global-insurer`

Faits publics utilisés :

- enterprise-wide IT repository ;
- lifecycle/obsolescence ;
- transformation analysis ;
- impact of change ;
- alignment IT/business ;
- risk/threat/control context.

---

# B. Sources Bizzdesign — méthodes / repository

## 9. Enterprise Architecture Repository article

Source :

`https://resources.bizzdesign.com/blog/enterprise-architecture-repository-example-structure-and-benefits`

Faits publics utilisés :

- repository connecté ;
- drill-down ;
- impact analysis ;
- migration planning ;
- integrations avec CMDB et autres sources ;
- API/connectors pour discovery.

Le masterbook conserve explicitement la frontière :

```text
EA Repository ≠ CMDB
```

---

## 10. Application Rationalization article

Source :

`https://resources.bizzdesign.com/blog/application-rationalization`

Faits publics utilisés :

- dependency mapping ;
- visualisation/analyse des dépendances ;
- impact of removing/changing applications ;
- rationalization decision support.

---

# C. Sources HOPEX Store — baseline technique

## 11. HOPEX Core Back-End Aquila 6.2

Source :

`https://store.mega.com/modules/details/hopex.core`

Baseline vérifiée septembre 2026 :

```text
Product: HOPEX Core Back-End Aquila 6.2
Latest visible version: 62.18.0+774
Published: 2026-09-03
```

Description publique utilisée :

- business logic ;
- repository access ;
- digital representation of enterprise ;
- connections business, IT, data, risk ;
- single source of truth ;
- actionable insights.

---

## 12. HOPEX REST API

Source :

`https://store.mega.com/modules/details/hopex.rest.api`

Baseline vérifiée :

```text
Latest visible version: 62.18.0+69
Published: 2026-09-02
```

Faits publics :

- read/write repository ;
- upload/download documents ;
- export diagrams ;
- relationship data accessible according to solution schemas/licensing.

Cette API peut être utilisée pour analyses complémentaires, sous réserve de droits et schémas disponibles.

---

## 13. HOPEX GraphQL

Source :

`https://store.mega.com/modules/details/hopex.graphql`

Baseline vérifiée :

```text
Latest visible version: 62.18.0+69
Published: 2026-09-02
```

Faits publics :

- GraphQL API layer ;
- query/update repository ;
- schema-driven ;
- possibilité de demander attributs et relationships ;
- intégration avec applications/dashboards/custom tools.

Le Store public donne notamment un exemple de query sur les applications.

---

# D. Ce qui est un fait produit vérifié

## 14. Facts utilisés dans la Partie XII

Sont traités comme faits publics vérifiés :

1. Hopex repose sur un repository connecté business/IT/data/risk.
2. Hopex met publiquement en avant la cartographie des data flows et dependencies.
3. Hopex met publiquement en avant impact analysis et hidden impacts.
4. Des cas clients publics décrivent dependency mapping et impact analysis pour changement/rationalisation.
5. Hopex peut exposer repository/relationships par GraphQL/REST selon configuration/licensing.
6. Hopex 360 est mentionné dans des cas publics pour partager les modèles/diagrammes.
7. La baseline Core publique visible est 62.18.0+774 au 3 septembre 2026.

---

# E. Ce qui n’est PAS présenté comme fonction Hopex native

## 15. Graph theory methods

Les concepts suivants sont utilisés comme pratiques analytiques générales :

```text
BFS
DFS
k-hop traversal
shortest path
degree
in-degree
out-degree
centrality
betweenness
connected components
strongly connected components
bridge
articulation point
community detection
```

Le masterbook **n’affirme pas** qu’Hopex expose chacun de ces algorithmes comme bouton, rapport ou fonction standard.

Ils peuvent être implémentés :

- avec les fonctions disponibles dans le contexte client ;
- via API/export ;
- via outil analytique complémentaire.

---

## 16. Blast-radius scoring

Les formules, scores, weights et seuils décrits dans la Partie XII sont pédagogiques.

Ils ne sont pas présentés comme score Hopex standard.

---

## 17. Dependency confidence

Les classifications :

```text
Verified
Observed
Imported
Inferred
Unverified
Stale
```

sont des recommandations de gouvernance du masterbook.

Ne pas prétendre qu’il s’agit des statuts exacts du métamodèle client.

---

## 18. Criticality taxonomy

Les niveaux :

```text
Critical / High / Medium / Low
Tier 0 / Tier 1 / Tier 2 / Tier 3
STOP / DEGRADED / DELAYED
```

sont pédagogiques, sauf s’ils existent explicitement chez le client.

---

## 19. DR recovery order

Les séquences de reprise MayaBank sont des hypothèses d’enseignement.

Elles doivent être dérivées de l’architecture réelle, des BIA, RTO/RPO, runbooks et tests PRA du client.

---

# F. MayaBank : hypothèses pédagogiques

## 20. Architecture fictive

MayaBank est une banque fictive.

Les éléments suivants sont créés pour apprentissage :

- Payment Orchestrator ;
- Fraud Decision Service ;
- Core Account Service ;
- Clearing Gateway ;
- Event Streaming ;
- Notification Service ;
- Reconciliation Service ;
- OpenShift Platform ;
- shared IAM ;
- API Management ;
- External Clearing Service.

Ils ne décrivent pas une architecture Bizzdesign/MEGA officielle.

---

## 21. Critical dependencies MayaBank

Les classifications hard/soft, criticality, fallback et recovery tiers sont pédagogiques.

Elles servent à apprendre la méthode et doivent être validées dans toute mission réelle.

---

# G. Règles de citation et d’usage

## 22. Sources publiques

Le masterbook paraphrase les capacités publiques utiles et conserve les liens.

Il ne reproduit pas de documentation propriétaire ou de training sous licence.

---

## 23. Documentation client

Dans une mission réelle, compléter avec :

- métamodèle installé ;
- documentation de version ;
- configuration des solutions/licences ;
- workflows ;
- API schemas ;
- CMDB ;
- architecture dossiers ;
- BIA/PRA ;
- incidents ;
- vendor support information.

---

## 24. Règle de prudence

Ne jamais écrire :

```text
HOPEX automatically computes betweenness centrality
```

sans preuve produit/version/client.

Préférer :

```text
Betweenness centrality is a useful graph-analysis method.
It can be calculated using available HOPEX capabilities or via API/export depending on the client environment.
```

---

## 25. Baseline finale Partie XII

```text
Date: September 2026
HOPEX Core Back-End: 62.18.0+774
HOPEX REST API: 62.18.0+69
HOPEX GraphQL: 62.18.0+69
```

Le masterbook prévoit une revérification globale en Partie XXIV.
