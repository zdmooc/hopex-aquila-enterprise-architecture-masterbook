# 99 — Sources officielles, faits produit et frontière de vérification

## 1. Principe

HOPEX/Bizzdesign Hopex est un produit propriétaire.

Cette Partie VIII sépare strictement :

```text
Fait produit vérifié
≠
Bonne pratique d’architecture
≠
Hypothèse pédagogique MayaBank
```

Aucune documentation propriétaire, support de formation ou contenu sous licence n’est reproduit substantiellement.

## 2. Baseline HOPEX Aquila

### HOPEX Core Back-End Aquila 6.2

Source publique :

https://store.mega.com/modules/details/hopex.core

Vérification du 8 septembre 2026 :

```text
Latest branch observed: 62.18.x
HOPEX Core Back-End: 62.18.0+774
Publish date listed for this build: 03/09/2026
```

Éléments utilisés :

- repository central ;
- connexions business / IT / data / risk ;
- plateforme unique de connaissance.

Le numéro exact doit toujours être revérifié lorsqu’une version récente est importante.

## 3. HOPEX Enterprise Architecture offer / pricing matrix

Source publique :

https://www.mega.com/product-hopex-enterprise-architecture-pricing

ou page Bizzdesign/HOPEX équivalente après migration de marque.

Éléments publics utilisés dans cette Partie VIII :

- Application Portfolio Management ;
- Application Catalog & Lifecycle ;
- Solution Architecture ;
- Application Architecture Modeling ;
- Deployment Architecture & infrastructure modeling ;
- Business Architecture ;
- Business Process Architecture ;
- Data Architecture.

Cette page confirme le positionnement fonctionnel mais ne constitue pas une spécification exhaustive du métamodèle.

## 4. HOPEX Platform features

Source publique :

https://www.mega.com/features/hopex-platform

Éléments utilisés :

- configurable metamodel ;
- profiles and permissions ;
- assessment engine ;
- surveys/campaigns ;
- reports/dashboards ;
- enterprise portal ;
- collaboration/workflows ;
- open APIs ;
- REST and GraphQL integration capabilities.

Ces fonctions peuvent dépendre de la licence, du rôle, de la configuration et des modules activés.

## 5. Application Portfolio Management public page

Source Bizzdesign :

https://bizzdesign.com/application-portfolio-management-apm-software

Source guide :

https://bizzdesign.com/blog/what-is-application-portfolio-management-amp

Éléments utilisés comme contexte :

- application inventory ;
- lifecycle ;
- ownership ;
- assessments ;
- dashboards ;
- rationalization ;
- transformation decisions.

La Partie VIII n’approfondit pas le scoring de portefeuille afin de réserver ce sujet aux Parties XIII–XIV.

## 6. Application Rationalization playbook

Ressource publique de la communauté Bizzdesign/MEGA :

https://community.mega.com/mega/attachments/mega/cx-mxforum-board/43/1/Playbook%20PDF%20-%20Application%20Rationalization%20%28EN%29.pdf

Éléments méthodologiques publics utilisés :

- inventory applications ;
- lifecycles ;
- exchanges ;
- technologies ;
- capabilities ;
- application portfolios ;
- ownership ;
- workflow pour contrôler additions/removals ;
- publication de l’inventaire.

Le masterbook ne reproduit ni diagrammes ni texte substantiel de ce document.

## 7. Cas client Nordea

Source Bizzdesign :

https://bizzdesign.com/customers/customer-stories/how-nordea-uses-application-management-achieve-rationalization

Éléments de contexte public :

- consolidation de l’information applicative ;
- application management ;
- dependency mapping ;
- decommissioning ;
- rationalization ;
- réutilisation du repository pour compliance et transformation.

Cette source illustre un usage réel ; elle ne définit pas les règles MayaBank.

## 8. Training database officielle

Source Store :

https://store.mega.com/modules/details/backup.training

Version observée en septembre 2026 :

```text
HOPEX Databases backup — HOPEX 6.2 CU5 — Training
published 05/06/2026
```

Le Store indique des données de formation pour plusieurs cursus, notamment :

- HOPEX IT Business Management ;
- HOPEX IT Portfolio Management ;
- HOPEX Business Process Analysis ;
- HOPEX IT Architecture ;
- HOPEX Information Architecture ;
- HOPEX Data Governance ;
- HOPEX Integrated Risk Management.

Aucun backup, mot de passe ou contenu de cours n’est repris dans le repository.

## 9. ITPM Excel Import Template

Source :

https://store.mega.com/modules/details/itpm.importexceltemplate

Version observée :

```text
62.7.0+7206
Aquila prerequisite
release in 2026
```

La page publique montre que le template manipule notamment des informations liées à :

- applications ;
- application flows/content ;
- technologies ;
- org-units ;
- business capability map selon release notes.

Le template n’est pas utilisé comme définition normative du métamodèle.

## 10. IT-Pedia integration

Source :

https://store.mega.com/modules/details/itpm.itpedia

Version observée :

```text
62.7.0+7206
published 17/03/2026
```

Éléments vérifiés :

- integration with Eracent IT-Pedia ;
- technology import ;
- alignment avec technologies existantes ;
- updates ;
- suivi d’obsolescence ;
- rapport de comparaison/impact selon description publique.

Prérequis/licence IT-Pedia et HOPEX doivent être vérifiés en mission.

## 11. ArchiMate add-on

Source :

https://store.mega.com/modules/details/framework.archimate

Version Aquila observée :

```text
ArchiMate 3.1
62.12.0+7259
published 01/06/2026
HOPEX Aquila V6.2 required according to Store page
```

Une release note publique mentionne la synchronisation de `ArchiMate Application Component Flow` vers des flows ITPM dans une version antérieure/branche correspondante.

Ce point confirme l’intégration de concepts entre framework et repository, mais :

```text
HOPEX Application object
≠ automatically ArchiMate Application Component
```

## 12. Application Environment diagram — community evidence

Source communautaire Bizzdesign Hopex :

https://community.mega.com/t5/Hopex-How-To-Videos/How-to-automatically-create-an-Application-Environment-diagram/td-p/31353

La ressource publique montre historiquement un scénario de génération automatique d’un `Application Environment diagram` à partir de flows.

Cette ressource date d’une version antérieure ; elle est utilisée uniquement comme indice de capacité historique et ne prouve pas que le même écran/scénario existe à l’identique dans Aquila 6.2.

## 13. Ce qui est un fait produit suffisamment vérifié pour cette partie

- HOPEX/Bizzdesign Hopex couvre un use case d’Application Architecture ;
- l’offre publique inclut Application Architecture Modeling ;
- l’offre publique inclut Deployment Architecture / infrastructure modeling ;
- le repository peut relier perspectives business, IT, data et risk ;
- le produit expose des capacités de workflows/collaboration, assessments et APIs selon configuration ;
- HOPEX IT Portfolio Management / training content existe pour Aquila ;
- un module d’intégration IT-Pedia existe pour Aquila ;
- un add-on ArchiMate 3.1 existe pour Aquila.

## 14. Ce qui relève des bonnes pratiques d’architecture

Les éléments suivants ne sont pas présentés comme des fonctions HOPEX imposées :

- niveaux L0/L1/L2/L3 de vues ;
- canonical application naming ;
- règles de granularity ;
- interface ownership model ;
- synchronous latency budget ;
- retry/backoff/circuit breaker ;
- event-driven design ;
- saga ;
- source-of-truth rules ;
- NFR catalogue ;
- application architecture Definition of Done ;
- mission playbook 4 semaines.

## 15. Ce qui relève de MayaBank

Sont fictifs :

- noms des applications MayaBank ;
- organisation des domaines ;
- responsabilités détaillées ;
- criticalities ;
- technologies cibles ;
- patterns de migration ;
- current/target architectures ;
- NFR chiffrés ;
- matrices ;
- risk map ;
- roadmap.

## 16. Ce qu’il faut vérifier dans un environnement client

Avant d’affirmer qu’une fonction est disponible :

1. version exacte de HOPEX ;
2. bundle/licence ;
3. profils ;
4. métamodèle standard/custom ;
5. diagram types activés ;
6. propriétés d’Application ;
7. types de Flow/Interface disponibles ;
8. workflow de création/validation ;
9. Application Lifecycle configuré ;
10. reports/dashboards disponibles ;
11. imports/connectors ;
12. API GraphQL/REST access ;
13. ArchiMate add-on ;
14. IT-Pedia subscription/module ;
15. conventions de modélisation internes.

## 17. Sources standards externes recommandées

### The Open Group — ArchiMate

https://www.opengroup.org/archimate-forum

Utiliser la spécification/licence autorisée pour la sémantique ArchiMate.

### The Open Group — TOGAF

https://www.opengroup.org/togaf

Utiliser pour méthode et gouvernance d’architecture.

### OpenAPI Initiative

https://www.openapis.org/

Référence pour les contrats OpenAPI, sans faire de HOPEX le catalogue technique de tous les endpoints.

### CNCF / Kubernetes

https://kubernetes.io/docs/

Référence pour les concepts Kubernetes.

### Red Hat OpenShift

https://docs.redhat.com/en/documentation/openshift_container_platform/

Référence pour les concepts et opérations OpenShift.

## 18. Règle de citation du masterbook

Lorsque le texte indique :

```text
HOPEX supports X
```

une source publique doit exister ou l’affirmation doit être reformulée comme :

```text
Architecture recommendation
Client-specific configuration
MayaBank hypothesis
```

## 19. Date de vérification

Sources publiques vérifiées ou recoupées le :

```text
08/09/2026
```

Les pages Bizzdesign/MEGA pouvant évoluer après l’intégration des marques et les releases Aquila, la Partie XXIV effectuera un audit final complet des liens, versions et formations.
