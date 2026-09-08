# 13 — Labs & Review — Business Architecture

## Objectif

Ces exercices sont conçus pour être réalisables sur papier, Markdown ou dans HOPEX lorsqu'un environnement/licence est disponible. Ils préparent aussi les entretiens d'architecte.

---

# Labs

## LAB 01 — Scope the Business Architecture

**Situation** : MayaBank veut réduire les incidents sur les paiements instantanés.

Produire :

1. 5 stakeholders ;
2. leurs concerns ;
3. 4 drivers ;
4. 4 outcomes mesurables ;
5. le périmètre métier ;
6. les exclusions.

**Critère** : aucune application ne doit être utilisée comme point de départ du scope.

## LAB 02 — Capability discovery

À partir des besoins suivants : initiation, validation, fraude, routage, clearing, notification et investigation, construire une capability map L1/L2/L3.

**Piège** : ne pas créer `Kafka`, `Payment API` ou `Ops Team` comme capabilities.

## LAB 03 — Capability naming review

Corriger :

```text
Run Fraud Engine
Payments Department
Kafka Events
New Instant Payment Project
Validate Payment Screen
```

Proposer des capabilities stables.

## LAB 04 — Organization × Capability

Construire une matrice RACI entre :

```text
Payments Business
Fraud Management
Payment Operations
Platform Engineering
```

et :

```text
Payment Orchestration
Fraud Decisioning
Payment Operations
Event Distribution
```

Identifier les capabilities sans accountable owner.

## LAB 05 — Value Stream

Construire le value stream :

```text
Initiate → Validate → Decide → Execute → Confirm
```

Pour chaque stage :

- value gained ;
- capability required ;
- metric ;
- failure mode.

## LAB 06 — Customer Journey

Construire le parcours Mobile Instant Payment avec :

- touchpoints ;
- customer emotions/expectations ;
- pain points ;
- underlying value stages ;
- business services.

## LAB 07 — Service Catalog

Créer 8 business services MayaBank.

Pour chacun :

- consumer ;
- owner ;
- capability ;
- process ;
- SLA/SLO métier ;
- lifecycle.

## LAB 08 — Product decomposition

Décomposer :

```text
Retail Instant Payment Offering
```

en services, channels, policies et capabilities.

## LAB 09 — Process Architecture

Créer une architecture L1/L2/L3 pour `Manage Payments`.

Ne pas utiliser BPMN détaillé.

## LAB 10 — Process × Application

Construire une matrice pour :

```text
Validate Payment
Execute Payment
Handle Exception
Investigate Payment
```

vs :

```text
Payment Orchestrator
Fraud Engine
Ops Portal
Notification Service
```

Identifier les dépendances critiques.

## LAB 11 — Business Information Map

Créer les objets métier :

```text
Payment Order
Customer
Beneficiary
Fraud Decision
Payment Status
Investigation Case
```

Définir owner, steward, classification et process usage.

## LAB 12 — Policy Traceability

Partir de :

> Every instant payment must reach an explicit final status.

Construire :

```text
Policy
→ Business Rule
→ Process Control
→ Application Requirement
→ Technical Control
```

## LAB 13 — Strategic Traceability

Partir de l'outcome :

```text
24x7 resilient payment execution
```

Relier au minimum :

- 4 capabilities ;
- 3 value stages ;
- 2 services ;
- 3 applications ;
- 3 technologies ;
- 3 initiatives.

## LAB 14 — Capability Assessment

Noter de 1 à 5 : importance, maturity, performance, risk pour 8 capabilities.

Créer deux heatmaps distinctes :

1. maturity gap ;
2. business risk.

Expliquer pourquoi il ne faut pas fusionner automatiquement les scores.

## LAB 15 — Gap analysis

Current :

```text
manual exception handling
point-to-point status interfaces
weak transaction visibility
```

Target :

```text
automated exception classification
shared event status model
end-to-end observability
```

Produire des gaps formulés comme différences current/target.

## LAB 16 — Options analysis

Comparer :

1. moderniser le hub legacy ;
2. strangler progressif ;
3. nouvelle plateforme cible.

Critères : value, risk, cost, time-to-value, migration complexity, reversibility.

## LAB 17 — Transition states

Créer quatre états :

```text
Current
Transition 1
Transition 2
Target
```

Pour chacun : capabilities, services, applications et operating model.

## LAB 18 — Business Roadmap

Construire 4 waves avec :

- objective ;
- gaps closed ;
- capabilities improved ;
- initiatives ;
- dependency ;
- KPI.

## LAB 19 — Repository quality audit

Auditer un repository fictif contenant :

- 10% capabilities sans owner ;
- doublons de services ;
- processus orphelins ;
- heatmaps sans date ;
- Org-Units obsolètes.

Définir un plan de correction priorisé.

## LAB 20 — Architecture Board

Préparer une soutenance de 15 minutes :

```text
Why change
→ stakeholder/outcomes
→ capability gaps
→ value-stream pain points
→ target operating model
→ IT impacts
→ roadmap
→ KPIs
```

Répondre ensuite aux objections : coût, complexité, ownership, risque de migration, valeur client.

---

# Questions de contrôle

## Q01
Une capability décrit principalement :

A. une équipe  
B. une aptitude durable  
C. une application  
D. une séquence BPMN

**Réponse : B.**

## Q02
Un value stream décrit principalement :

A. la progression de valeur  
B. l'organigramme  
C. les composants techniques  
D. les tickets projet

**Réponse : A.**

## Q03
Un customer journey est surtout :

A. outside-in  
B. un inventaire d'applications  
C. un modèle de DB  
D. une CMDB

**Réponse : A.**

## Q04
Capability et process sont :

A. synonymes  
B. aptitude vs manière d'exécuter  
C. application vs serveur  
D. produit vs service

**Réponse : B.**

## Q05
Le meilleur point de départ d'une architecture métier est :

A. la liste des serveurs  
B. stakeholder/decision/outcome  
C. le catalogue Kafka  
D. l'organigramme uniquement

**Réponse : B.**

## Q06
Une Org-Unit répond principalement à :

A. qui  
B. pourquoi  
C. quel protocole  
D. quelle table

**Réponse : A.**

## Q07
Le business service représente :

A. une valeur exposée  
B. une VM  
C. un projet  
D. une capability technique

**Réponse : A.**

## Q08
Un process owner est forcément l'application owner :

A. vrai  
B. faux

**Réponse : B.**

## Q09
Une capability map utile doit idéalement être reliée :

A. uniquement aux équipes  
B. à stratégie, applications et initiatives  
C. uniquement aux couleurs  
D. uniquement aux processus

**Réponse : B.**

## Q10
Une heatmap sans méthode de scoring est :

A. fiable  
B. décorative/ambiguë  
C. une API  
D. un workflow

**Réponse : B.**

## Q11
Le value stream doit être composé de :

A. applications  
B. grandes stages de valeur  
C. tickets  
D. serveurs

**Réponse : B.**

## Q12
Customer Journey et Value Stream :

A. sont identiques  
B. se complètent  
C. ne doivent jamais être reliés  
D. sont techniques

**Réponse : B.**

## Q13
Une business information est :

A. forcément une table  
B. un concept métier avant implémentation physique  
C. un pod  
D. un projet

**Réponse : B.**

## Q14
La source autoritative et l'owner sont :

A. toujours la même chose  
B. des concepts distincts  
C. inutiles  
D. des technologies

**Réponse : B.**

## Q15
Un gap correctement formulé compare :

A. current et target  
B. deux couleurs  
C. deux personnes  
D. deux versions Git

**Réponse : A.**

## Q16
Une initiative est :

A. un objectif stratégique  
B. une action de transformation  
C. une capability  
D. un business object

**Réponse : B.**

## Q17
Pourquoi les transition states sont-ils importants ?

A. pour ajouter des diagrammes  
B. pour assurer une trajectoire opérable  
C. pour supprimer les owners  
D. pour remplacer les KPIs

**Réponse : B.**

## Q18
Une application peut soutenir :

A. une seule capability uniquement  
B. plusieurs capabilities  
C. aucune relation métier  
D. seulement un serveur

**Réponse : B.**

## Q19
Une capability peut être soutenue par :

A. plusieurs applications  
B. une seule application par définition  
C. uniquement une équipe  
D. seulement un process

**Réponse : A.**

## Q20
`Kafka` doit être modélisé comme business capability :

A. oui  
B. non

**Réponse : B.**

## Q21
Le rôle d'une Capability × Application Matrix est notamment :

A. détecter les couvertures/dépendances  
B. calculer la RAM  
C. modifier Git  
D. créer des utilisateurs

**Réponse : A.**

## Q22
Un product/offering peut assembler :

A. plusieurs business services  
B. uniquement un serveur  
C. uniquement une Org-Unit  
D. seulement un process

**Réponse : A.**

## Q23
La meilleure manière de justifier une plateforme technique est :

A. tendance technologique  
B. trace vers outcomes/capability gaps  
C. préférence personnelle  
D. nom du fournisseur

**Réponse : B.**

## Q24
Un repository business mature doit surveiller :

A. objects without owners  
B. duplicates  
C. stale data  
D. toutes les réponses

**Réponse : D.**

## Q25
L'organigramme suffit pour décrire le business :

A. vrai  
B. faux

**Réponse : B.**

## Q26
Business Architecture et BPA :

A. mêmes granularités  
B. complémentaires avec niveaux différents  
C. incompatibles  
D. uniquement techniques

**Réponse : B.**

## Q27
Une policy est :

A. une implémentation technique exacte  
B. une règle/principe gouvernant le métier  
C. une application  
D. une capability

**Réponse : B.**

## Q28
Un outcome doit idéalement être :

A. mesurable  
B. uniquement visuel  
C. un nom de projet  
D. un nom d'application

**Réponse : A.**

## Q29
Pourquoi relier Business Architecture et IT Architecture ?

A. pour comprendre comment le SI soutient la valeur et les capabilities  
B. pour tout transformer en CMDB  
C. pour supprimer les processes  
D. pour éviter les stakeholders

**Réponse : A.**

## Q30
Le principe principal d'un repository HOPEX est :

A. dupliquer les objets par diagramme  
B. réutiliser des objets canoniques  
C. créer une MetaClass par projet  
D. remplacer les owners par des notes

**Réponse : B.**

---

# Seuil de maîtrise interne

- **27–30** : très bon niveau Partie V ;
- **23–26** : bon, revoir les confusions ;
- **18–22** : revoir capabilities/value streams/traceability ;
- **<18** : reprendre les chapitres 01 à 10 avant de continuer.

Ce seuil est pédagogique et n'est pas un score de certification HOPEX officiel.