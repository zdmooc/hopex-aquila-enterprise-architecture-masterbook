# Annexe — Sources officielles, faits vérifiés et frontière pédagogique

## 1. Principe

Cette Partie VII distingue explicitement :

```text
Fait produit vérifié
≠
Bonne pratique d'architecture/process governance
≠
Hypothèse pédagogique MayaBank
```

HOPEX étant un produit propriétaire, ce repository n'essaie pas de reconstituer une documentation interne et ne copie pas de formation propriétaire.

## 2. Baseline HOPEX vérifiée — septembre 2026

### HOPEX Core Back-End Aquila 6.2

Source officielle MEGA Store :

https://store.mega.com/modules/details/hopex.core

Version observée au 8 septembre 2026 :

```text
62.18.0+774
publication : 03/09/2026
```

Le Store présente le Core comme le back-end de la plateforme donnant accès à la logique métier et au repository, et met en avant la connexion des perspectives business, IT, data et risk.

### HOPEX Aquila Web Front-End

Source officielle :

https://store.mega.com/modules/details/hopex.dtpx

Version observée :

```text
62.18.0+143
publication : 02/09/2026
```

Le Store décrit le Web Front-End comme le portail pour enterprise architects, process modelers, risk managers, auditors et autres stakeholders EA/GRC.

### HOPEX REST API

Source officielle :

https://store.mega.com/modules/details/hopex.rest.api

Version observée :

```text
62.18.0+69
publication : 02/09/2026
```

Le Store indique que l'API permet notamment l'accès read/write au repository, l'upload/download de documents et l'export de diagrammes.

## 3. HOPEX REST API V5 / GraphQL BPA

Workspace Postman officiel MEGA :

https://www.postman.com/mega-international/mega-international-s-public-workspace/documentation/27vy1fl/hopex-rest-api-v5

Faits vérifiés :

- catalogue REST API V5 public ;
- authentification et accès aux environnements/repositories ;
- appels GraphQL aux solutions HOPEX ;
- endpoint BPA synchrone documenté ;
- exemple public de lecture de `businessprocess` avec `id` et `name` ;
- schéma SDL BPA exposé dans le workspace.

Exemple conceptuel conforme à l'exemple public :

```graphql
query {
  businessprocess {
    id
    name
  }
}
```

Ne pas extrapoler les relations ou attributs sans lire le SDL/schema de la version réellement utilisée.

## 4. HOPEX Simulation Engine

Source officielle MEGA Store :

https://store.mega.com/modules/details/simulation.engine

Faits vérifiés :

- module officiel ;
- tag Business Process Analysis ;
- dépendance HOPEX Business Process Analysis ;
- licence HOPEX Process Simulation requise ;
- scénarios `what-if` ;
- production de reports ;
- import de process description/performance metrics depuis des outils de Process Mining ;
- initialisation de données de simulation à partir d'inputs de Process Mining ;
- versions 62.x publiées en 2026 ;
- version 62.11.0+7247 visible, publiée le 13/05/2026 ;
- release note mentionnant le packaging compatible Aquila Java 17 JRE.

Le masterbook n'en déduit pas que toute installation HOPEX dispose de la simulation : licence/module/configuration doivent être vérifiés.

## 5. APQC Process Classification Framework — module HOPEX

Source officielle MEGA Store :

https://store.mega.com/modules/details/framework.apqc.cross.industry

Faits vérifiés :

- module Cross Industry ;
- Process Map root ;
- Process Categories hierarchy niveaux 1 et 2 ;
- Value Streams/stages niveaux 3 et 4 ;
- related Performance Indicators ;
- option value stream à activer pour certains niveaux ;
- tag Business Process Analysis.

Le contenu APQC est soumis à ses propres conditions/licences. Ce repository ne le reproduit pas.

## 6. Training database publique

Source officielle MEGA Store :

https://store.mega.com/modules/details/backup.training

Faits utiles :

- backup de training Aquila 6.2 CU5 publié en 2026 ;
- données prévues pour Consultant-Led Training ou E-learning ;
- HOPEX Business Process Analysis fait partie des cursus listés ;
- d'autres solutions HOPEX sont également présentes.

Aucun backup, contenu de cours, secret ou donnée propriétaire n'est copié dans ce repository.

## 7. AI-Driven Process Modeling — module Store

Source officielle :

https://store.mega.com/modules/details/chatgpt.bpmnimport

Faits publics :

- add-on taggé Business Process Analysis ;
- génération de process diagrams depuis une description textuelle ;
- statut beta indiqué dans la release note publique ;
- version 62.10.0+7238 visible en 2026.

Ce module n'est pas requis pour la Partie VII et ne doit pas être présenté comme une capacité standard activée partout.

## 8. BPMN — source normative publique

Object Management Group :

https://www.omg.org/spec/BPMN/2.0.2/

Fait vérifié : BPMN 2.0.2 est une spécification formelle OMG.

Le chapitre BPMN de ce masterbook explique uniquement les concepts nécessaires avec des exemples originaux MayaBank ; il ne reproduit pas la norme.

## 9. Camunda 8 — source runtime publique

Documentation officielle :

https://docs.camunda.io/docs/components/concepts/processes/

Points utilisés dans le chapitre 11 :

- processus modélisé en BPMN ;
- déploiement comme process definition ;
- exécution comme process instance ;
- Zeebe présenté comme workflow engine ;
- orchestration de tasks/endpoints.

Source de modélisation BPMN :

https://docs.camunda.io/docs/components/modeler/bpmn/automating-a-process-using-bpmn/

Camunda est utilisé uniquement pour expliquer la frontière repository vs runtime.

## 10. Pega — sources runtime/workflow publiques

Workflow Automation :

https://www.pega.com/products/platform/workflow-automation

Business Process Orchestration :

https://www.pega.com/business-process-orchestration

Points utilisés :

- workflow automation ;
- Case Management & BPM ;
- orchestration de systèmes/services ;
- human work ;
- RPA/process mining/decision capabilities présentées publiquement selon les offres.

Pega est utilisé comme exemple de plateforme d'automatisation/case management, pas comme comparatif commercial exhaustif.

## 11. Faits produit que la Partie VII peut affirmer

À partir des sources publiques vérifiées :

- HOPEX Aquila dispose d'un portail pour process modelers ;
- HOPEX propose une solution/empreinte Business Process Analysis ;
- un endpoint GraphQL BPA public est documenté ;
- les business processes peuvent être adressés via l'API selon le schéma publié ;
- un Simulation Engine officiel BPA existe ;
- ce moteur sait exécuter des scénarios what-if ;
- il sait exploiter des inputs provenant du process mining ;
- un module APQC Process Classification Framework existe ;
- une training database contient des données BPA ;
- des add-ons BPA existent dans le Store.

## 12. Ce que la Partie VII ne doit pas affirmer sans vérification client

Ne pas promettre :

- le nom exact d'un workspace client ;
- le nom exact des MetaClasses/associations custom ;
- un workflow d'approbation particulier ;
- un mécanisme de versioning identique partout ;
- une synchronisation Camunda/Pega ↔ HOPEX ;
- un process mining engine natif complet ;
- la Simulation Engine installée/licenciée ;
- une auto-publication ;
- un dashboard précis ;
- un type de diagramme disponible dans tous les profils ;
- une permission particulière ;
- un round-trip BPMN automatique.

## 13. Recommandations pédagogiques MayaBank

Ne sont pas des fonctionnalités produit imposées :

- lifecycle Proposed/Draft/Review/Approved/Published/Retired ;
- score de qualité sur 100 ;
- taxonomie d'exceptions ;
- KPI thresholds ;
- maturity model 1–5 ;
- naming conventions ;
- RACI ;
- target process ;
- backlog d'initiatives ;
- classification des fallbacks ;
- architecture event-driven ;
- séparation des sources de vérité proposée.

## 14. Cas MayaBank

Tout ce qui concerne :

```text
MayaBank
Payment Orchestrator
Fraud Decision Service
Clearing Gateway
Notification Service
OpenShift Platform
Kafka/Event Streaming
```

est fictif/pédagogique sauf lorsqu'un concept technologique générique est explicitement expliqué.

## 15. Règle de citation dans les futures parties

Pour chaque fait dépendant d'une version :

1. vérifier le Store/éditeur ;
2. noter la date ;
3. noter la version ;
4. distinguer module standard/add-on/licence ;
5. ne pas extrapoler ;
6. ne pas copier de documentation propriétaire substantiellement.

## 16. Baseline de travail de la Partie VII

```text
HOPEX Aquila 6.2
Core Back-End 62.18.0+774
Web Front-End 62.18.0+143
REST API 62.18.0+69
GraphQL/REST public workspace verified
Simulation Engine official add-on verified
```

La baseline devra être revérifiée si une partie ultérieure dépend d'une version plus récente.