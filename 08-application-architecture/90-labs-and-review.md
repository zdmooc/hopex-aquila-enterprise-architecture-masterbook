# 90 — Labs pratiques et questions de contrôle

## 1. Objectif

Ces exercices transforment la Partie VIII en pratique d’architecte solution / architecte d’entreprise.

Ils peuvent être réalisés :

- dans HOPEX Aquila si un environnement/licence est disponible ;
- sur Markdown/Draw.io/ArchiMate pour apprendre le raisonnement ;
- dans un repository de lab MayaBank ;
- en atelier d’entretien.

Les noms exacts de menus, diagram types et propriétés doivent être adaptés à la configuration HOPEX utilisée.

---

# Labs

## Lab 01 — Canonical Application Catalog

Créer le catalogue MayaBank avec au minimum :

- Digital Channel ;
- API Management ;
- IAM ;
- Payment Orchestrator ;
- Fraud Decision Service ;
- Core Account Service ;
- Clearing Gateway ;
- Event Streaming ;
- Notification Service ;
- Reconciliation Service ;
- Observability Platform ;
- Legacy Payment Hub.

**Livrable :** table avec ID, purpose, domain, owner, lifecycle, criticality.

**Contrôle :** aucun environnement ne doit être créé comme application séparée.

## Lab 02 — Duplicate Detection

Ajouter volontairement :

```text
PAY ORCH
Payment Orchestration
Payment Orchestrator PROD
```

Identifier les doublons et définir alias/canonical name.

**Livrable :** règle Search Before Create.

## Lab 03 — Application Granularity

Classer les éléments suivants :

```text
Payment Orchestrator
payments-prod namespace
Fraud Decision API
Java 21
Payment Validation microservice
PostgreSQL cluster
Instant Payment capability
```

**Livrable :** Application / Service / Component / Technology / Deployment / Capability.

## Lab 04 — Capability × Application Matrix

Construire la matrice de couverture du domaine Payments.

**Contrôle :** expliquer chaque relation importante.

## Lab 05 — Process Activity × Application

Mapper `Execute Instant Payment` activité par activité.

**Livrable :** matrice Activity → Primary Application → Supporting Application.

## Lab 06 — Responsibility Map

Pour chaque responsabilité :

```text
Authentication
Payment orchestration
Fraud decision
Funds check
Clearing
Notification
Reconciliation
```

identifier l’application principale.

**Contrôle :** aucune responsabilité critique ne doit avoir deux owners primaires sans justification.

## Lab 07 — Application Interaction Diagram

Dessiner :

```text
Channel → API Mgmt → Payment Orchestrator
Payment Orchestrator → Fraud/Core/Clearing
Payment Orchestrator → Event Streaming
Event Streaming → Notification/Reconciliation
```

Nommer toutes les interactions.

## Lab 08 — Interface Catalogue

Créer six interfaces :

- Payment Initiation API ;
- Payment Status API ;
- Fraud Decision API ;
- Funds Check API ;
- Clearing Submission Interface ;
- PaymentStatusChanged Event.

Pour chacune : provider, consumers, data, style, version, owner.

## Lab 09 — Hidden Dependency Hunt

Ajouter trois dépendances héritées :

- direct SQL ;
- nightly file ;
- shared MQ queue.

Analyser pourquoi elles sont souvent absentes des diagrammes.

## Lab 10 — Integration Pattern Review

Pour dix interactions, choisir :

```text
sync API
async event
messaging command
batch/file
adapter
```

Justifier chaque choix.

## Lab 11 — Synchronous Chain Analysis

Chaîne :

```text
Channel → API → Orchestrator → Fraud → Core → Clearing
```

Identifier :

- latency budget ;
- timeout ;
- retry ;
- propagation de panne ;
- critical path.

## Lab 12 — Event-Driven Decoupling

Transformer notification synchrone en :

```text
PaymentStatusChanged
→ Event Streaming
→ Notification Service
```

Documenter conséquences : eventual consistency, replay, idempotency, monitoring.

## Lab 13 — Dependency Blast Radius

Scénario : Event Streaming indisponible.

Lister :

- impacted applications ;
- impacted processes ;
- degraded functions ;
- functions that can continue.

## Lab 14 — Interface Deprecation

`Fraud Decision API v1` doit être retirée.

Créer :

- consumer list ;
- target v2 ;
- migration status ;
- deprecation date ;
- owner ;
- exit criteria.

## Lab 15 — Deployment View

Modéliser :

```text
Payment Orchestrator
→ OpenShift PROD
→ payments namespace
```

plus site/DR de haut niveau.

**Contrôle :** ne pas transformer tous les pods en applications.

## Lab 16 — Shared Failure Domain

Supposer que Payments, Fraud et Notification tournent sur le même cluster.

Analyser :

- blast radius ;
- critical service impact ;
- mitigation ;
- besoin réel ou non de séparation.

## Lab 17 — NFR Catalogue

Pour Payment Orchestrator, définir :

- availability ;
- performance ;
- scalability ;
- RTO/RPO ;
- security ;
- audit ;
- observability.

Distinguer objective, architecture response et operational evidence.

## Lab 18 — Performance Budget

Construire un budget P95 pédagogique pour 2 secondes end-to-end.

Répartir :

- API ingress ;
- fraud ;
- funds ;
- clearing ;
- persistence ;
- orchestration overhead.

Vérifier que la somme et les marges sont cohérentes.

## Lab 19 — Data Responsibility Map

Mapper :

- Payment Instruction ;
- Fraud Decision ;
- Account/Funds ;
- Clearing Result ;
- Payment Status ;
- Notification Record.

Identifier source of truth et consumers.

## Lab 20 — Shared Database Refactoring

Current : Legacy Payment Hub et Notification Legacy accèdent au même schema.

Target : Payment Status API + event.

Produire :

- current coupling ;
- target boundary ;
- transition ;
- data migration/reconciliation.

## Lab 21 — Obsolescence Impact

Choisir une technologie fictive EOL utilisée par Legacy Payment Hub.

Construire :

```text
Technology
→ Application
→ Process
→ Business Service
→ Initiative
```

## Lab 22 — Current / Transition / Target

Produire trois vues cohérentes :

1. Current Legacy Payment Hub.
2. Transition avec adapter et nouveau orchestrator.
3. Target avec events et legacy retiré.

## Lab 23 — Decommission Readiness

Construire une checklist de retrait du Legacy Payment Hub :

- consumers = 0 ;
- data migrated/archived ;
- jobs stopped ;
- interfaces retired ;
- contracts/licences ;
- monitoring ;
- owner sign-off.

## Lab 24 — Architecture Board

Préparer un dossier d’une page pour :

> Remplacer Legacy Payment Hub par Payment Orchestrator sur OpenShift.

Inclure :

- driver ;
- current ;
- options ;
- target ;
- dependencies ;
- data ;
- NFR ;
- security ;
- migration ;
- risks ;
- decisions.

---

# Questions corrigées

## Q01

Quelle différence entre Application Architecture et Application Portfolio Management ?

**Réponse :** l’Application Architecture décrit responsabilités, services, interactions, dépendances, données, déploiements et cible ; l’APM gouverne le portefeuille, la valeur, les coûts, risques et décisions de rationalisation/investissement.

## Q02

Une application est-elle un serveur ?

**Réponse :** non. L’application est un actif logique ; le serveur ou cluster fait partie de son déploiement/technologie.

## Q03

Une application est-elle une capability ?

**Réponse :** non. La capability exprime ce que l’entreprise sait faire ; l’application la supporte.

## Q04

Pourquoi éviter une application par environnement ?

**Réponse :** DEV/UAT/PROD sont des déploiements d’un même actif logique, sauf si des différences fonctionnelles/ownership justifient réellement des actifs distincts.

## Q05

Quel est le minimum d’une Application ID Card ?

**Réponse :** nom canonique, purpose, domaine, owner, lifecycle, criticality et liens business/dépendances clés.

## Q06

Pourquoi Search Before Create ?

**Réponse :** pour éviter doublons, alias non maîtrisés et fragmentation du repository.

## Q07

Quand modéliser un microservice comme objet ?

**Réponse :** lorsque ce niveau sert une décision d’architecture ; pas systématiquement dans les vues d’entreprise.

## Q08

Quelle différence entre interaction et interface ?

**Réponse :** l’interaction décrit une relation d’échange ; l’interface est le contrat exposé par un provider et consommé par un ou plusieurs consumers.

## Q09

Pourquoi un simple trait entre applications est-il insuffisant ?

**Réponse :** il ne précise ni direction, ni purpose, ni data, ni contrat, ni criticité.

## Q10

Qui possède une interface ?

**Réponse :** conceptuellement le provider en porte la responsabilité de contrat, avec gouvernance des consumers et changements.

## Q11

REST est-il une sémantique métier ?

**Réponse :** non. REST est un style/transport ; `Fraud Decision` ou `Payment Status` décrit la sémantique.

## Q12

Kafka topic = event métier ?

**Réponse :** non automatiquement. Le topic est un canal technique ; l’événement est un fait sémantique qui doit être gouverné.

## Q13

Quand préférer asynchrone ?

**Réponse :** lorsque le producer ne doit pas attendre les consumers, que plusieurs consumers réagissent, ou que le découplage temporel/replay est utile.

## Q14

Quel est le risque d’une longue chaîne synchrone ?

**Réponse :** latence, propagation de panne, budgets timeout complexes et retry storms.

## Q15

Orchestration et choreography sont-elles exclusives ?

**Réponse :** non. Une architecture peut orchestrer le cœur d’un process et publier des événements pour découpler les fonctions downstream.

## Q16

Pourquoi l’idempotency est-elle importante pour les paiements ?

**Réponse :** pour éviter qu’un retry ou doublon ne déclenche plusieurs exécutions financières.

## Q17

Un shared database est-il toujours interdit ?

**Réponse :** non, mais il crée souvent ownership et coupling forts ; il doit être explicite et justifié.

## Q18

Que signifie blast radius ?

**Réponse :** l’étendue des applications, services métier et capacités impactés par la panne ou le changement d’un élément.

## Q19

Plusieurs pods éliminent-ils un SPOF ?

**Réponse :** non. Il peut subsister un SPOF logique, data, réseau, platform, external provider ou configuration.

## Q20

HOPEX remplace-t-il une CMDB ?

**Réponse :** non. HOPEX porte l’intention et les relations d’architecture ; la CMDB gère les CIs opérationnels et leur état de run.

## Q21

Pourquoi séparer application et deployment ?

**Réponse :** l’identité logique de l’application doit survivre à un changement de plateforme, région, cluster ou environnement.

## Q22

Application sur OpenShift = cloud-native ?

**Réponse :** pas nécessairement. Une application containerisée peut conserver sessions, filesystem coupling, shared DB ou architecture monolithique.

## Q23

RTO et RPO sont-ils la même chose ?

**Réponse :** non. RTO vise le temps de rétablissement ; RPO la perte de données maximale acceptable exprimée en temps.

## Q24

Pourquoi un SLA individuel ne garantit-il pas le SLA end-to-end ?

**Réponse :** parce qu’un service dépend d’une chaîne de composants dont les indisponibilités se combinent.

## Q25

Monitoring technique suffit-il ?

**Réponse :** non. Il faut aussi mesurer outcomes métier, erreurs fonctionnelles, timeouts, repairs et parcours end-to-end.

## Q26

Pourquoi un correlation ID ?

**Réponse :** pour relier logs/traces/événements d’une même transaction à travers plusieurs applications.

## Q27

Database = Data Domain ?

**Réponse :** non. Une database est un support technique ; un data domain représente un périmètre informationnel/métier.

## Q28

Une copie analytics est-elle source of truth ?

**Réponse :** pas automatiquement ; la source authoritative doit être explicitement définie.

## Q29

Kafka = event sourcing ?

**Réponse :** non. Event sourcing implique que la séquence d’événements gouvernée constitue la source de vérité de l’état.

## Q30

Pourquoi une migration applicative doit-elle inclure les données ?

**Réponse :** parce que responsabilités, history, source of truth, coexistence et cutover dépendent de la migration/reconciliation data.

## Q31

Application lifecycle et technology lifecycle sont-ils identiques ?

**Réponse :** non. Une application peut rester stratégique tout en utilisant une technologie arrivant en fin de support.

## Q32

Que doit contenir une dérogation à un standard ?

**Réponse :** owner, scope, raison, risque, mitigation, expiration et plan de remédiation.

## Q33

Rehost = modernisation complète ?

**Réponse :** non. Rehost change principalement l’hébergement et peut conserver la dette applicative.

## Q34

Pourquoi modéliser un transition state ?

**Réponse :** parce que la coexistence legacy/target est un véritable état d’architecture avec ses propres risques, données et dépendances.

## Q35

Quel danger avec dual write ?

**Réponse :** divergence de données, erreurs partielles, ownership ambigu et reconciliation complexe.

## Q36

Quand retirer l’objet application du repository ?

**Réponse :** après retrait réel et conservation de l’historique nécessaire ; pas au début du projet de décommission.

## Q37

Quel indicateur montre qu’un dependency graph est peu fiable ?

**Réponse :** relations sans owner/source/date de validation, ou taux important de consumers inconnus.

## Q38

Pourquoi ne pas intégrer toutes les ressources Kubernetes dans HOPEX ?

**Réponse :** cela transforme l’EA repository en inventaire runtime difficile à maintenir ; seules les relations structurantes nécessaires aux décisions doivent remonter.

## Q39

Quelle articulation TOGAF / ArchiMate / HOPEX ?

**Réponse :** TOGAF fournit méthode/gouvernance, ArchiMate un langage de modélisation, HOPEX un repository et des capacités d’analyse/gouvernance ; les objets ne sont pas automatiquement équivalents.

## Q40

Quelle question finale doit-on poser devant un diagramme applicatif ?

**Réponse :** quelle décision, quel impact ou quel risque ce modèle permet-il de comprendre mieux qu’avant ?
