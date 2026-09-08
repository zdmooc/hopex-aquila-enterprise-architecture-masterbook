# 10 — MayaBank Navigation Playbook

## 1. Objectif

Ce playbook décrit comment un architecte navigue dans un repository MayaBank sans transformer HOPEX en simple catalogue d’écrans.

Le principe est toujours :

```text
question d’architecture
→ trouver l’objet canonique
→ inspecter ses propriétés
→ suivre ses relations
→ ouvrir les vues pertinentes
→ filtrer le périmètre
→ analyser les impacts
→ décider / corriger
```

## 2. Point de départ : Payment Orchestrator

Objet de référence :

```text
MayaBank Payment Orchestrator
Class       : Application
Domain      : Payments
Owner       : Payments Domain
Lifecycle   : Strategic
Criticality : Critical
```

L’architecte doit ensuite pouvoir répondre à :

- quelles capabilities cette application supporte-t-elle ?
- quels processus métier en dépendent ?
- quelles interfaces expose-t-elle ?
- quelles données manipule-t-elle ?
- quelles technologies utilise-t-elle ?
- quelles applications consomment ses services ?
- sur quelle plateforme s’exécute-t-elle ?
- quels projets la transforment ?
- existe-t-il un remplacement cible ?

## 3. Parcours Application → Business

```text
Payment Orchestrator
→ supported Business Capability
→ Instant Payment Processing
→ related Business Process
→ Execute Instant Payment
→ business owner / domain
```

Questions :

- l’application est-elle réellement critique pour la capability ?
- existe-t-il plusieurs applications sur la même capability ?
- la redondance est-elle voulue ou historique ?

## 4. Parcours Application → Technology

```text
Payment Orchestrator
→ software technologies
→ Java / PostgreSQL client / Kafka client
→ hosting platform
→ OpenShift
```

Ne pas descendre automatiquement jusqu’aux pods et containers. Le bon niveau dépend de la décision EA.

## 5. Parcours Application → Interfaces

```text
Payment Orchestrator
→ Payment Initiation API
→ consumers
→ Mobile Banking
→ Corporate Gateway
```

Puis :

```text
Payment Orchestrator
→ publishes Payment Event
→ Event Streaming Platform
→ Fraud / Notification / Reporting consumers
```

Ce parcours permet une première impact analysis.

## 6. Parcours Application → Data

Questions :

- quelles informations sont produites ?
- quelles informations sont consommées ?
- quel système est maître ?
- quelles données sont sensibles ?
- quelles dépendances sont synchrones/asynchrones ?

Exemple :

```text
Payment Transaction
→ produced/updated by Payment Orchestrator
→ consumed by Fraud Engine
→ retained in Payment Data Store
```

## 7. Parcours Application → Lifecycle

```text
Current status
→ Strategic
Target status
→ Retain / Modernize
Transformation initiative
→ Payment Cloud-Native Modernization
Target platform
→ OpenShift
```

L’architecte doit distinguer :

- état actuel ;
- choix stratégique ;
- date cible ;
- projet qui produit le changement.

## 8. Parcours Capability → Applications

Partir d’une capability est souvent plus utile que partir du SI.

```text
Real-Time Payment Processing
→ supporting applications
→ Payment Orchestrator
→ Fraud Engine
→ Notification Service
→ Settlement Adapter
```

Questions :

- quelles applications sont critiques ?
- lesquelles sont redondantes ?
- lesquelles sont en fin de vie ?
- quelles technologies deviennent bloquantes ?

## 9. Parcours Technology → Applications

Exemple :

```text
Technology = WebSphere
→ used by applications
→ legacy Payment Gateway
→ Settlement Adapter
→ Admin Console
```

Cette vue est essentielle pour une stratégie de sortie technologique.

## 10. Parcours Owner → Portfolio

```text
Owner = Payments Domain
→ Applications
→ Capabilities
→ Processes
→ Projects
```

Cela permet de détecter :

- objets sans ownership ;
- ownership trop concentré ;
- applications orphelines ;
- incohérences entre organisation et portefeuille.

## 11. Parcours Incident d’architecture

Question : « Kafka doit être remplacé. Qu’est-ce qui est impacté ? »

```text
Event Streaming Platform
→ applications using it
→ interfaces / event flows
→ business processes
→ critical capabilities
→ owners
→ projects already touching these objects
```

C’est ce type de navigation qui justifie le repository commun.

## 12. Parcours Green IT

Question : « Quelles applications candidates à rationalisation consomment une plateforme coûteuse ? »

```text
Technology Platform
→ hosted applications
→ lifecycle
→ business criticality
→ redundancy
→ transformation roadmap
```

La mesure carbone détaillée peut venir d’un outil externe ; HOPEX peut porter la vue de décision et les objets structurants.

## 13. Routine quotidienne architecte

### Matin
- consulter les objets modifiés ;
- vérifier les demandes de validation ;
- contrôler les objets critiques sans owner/lifecycle ;
- revoir les changements de portefeuille.

### Pendant une étude
- rechercher avant de créer ;
- réutiliser les objets existants ;
- enrichir propriétés et relations ;
- créer une vue dédiée au concern ;
- documenter les hypothèses.

### Avant Architecture Board
- produire la vue de décision ;
- vérifier impacts ;
- vérifier current/target ;
- identifier exceptions ;
- rattacher les décisions aux objets.

## 14. Checklist MayaBank

Pour chaque application majeure :

- [ ] objet canonique ;
- [ ] owner ;
- [ ] lifecycle ;
- [ ] criticality ;
- [ ] business support ;
- [ ] technologies majeures ;
- [ ] interfaces majeures ;
- [ ] data dependencies ;
- [ ] projets de transformation ;
- [ ] target state ;
- [ ] dernière revue ;
- [ ] source de l’information.

## 15. Anti-patterns

- navigation uniquement par diagramme ;
- création d’un objet dès qu’on ne le voit pas immédiatement ;
- confusion entre absence dans une vue et absence dans le repository ;
- utilisation de noms libres comme clés ;
- recherche limitée au libellé exact ;
- impact analysis sans parcourir les relations indirectes ;
- current et target mélangés.
