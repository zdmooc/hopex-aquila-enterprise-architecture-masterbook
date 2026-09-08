# 08 — Labs pratiques et questions de contrôle

## 1. Objectif

Cette série transforme la théorie BPA en exercices directement exploitables dans un environnement HOPEX ou, sans licence, sur papier/Markdown avec le même raisonnement repository.

## 2. Labs

### Lab 01 — Process landscape
Construire le paysage L0/L1 de MayaBank autour de Customer, Payments, Risk, Finance et Technology.

**Livrable :** hiérarchie de processus avec owners.

### Lab 02 — Process scoping
Définir précisément les start/end boundaries de `Execute Instant Payment`.

**Contrôle :** éviter de mélanger initiation, settlement détaillé et notification technique.

### Lab 03 — Happy path BPMN
Modéliser le happy path du paiement instantané.

### Lab 04 — XOR gateways
Ajouter les décisions : valid/invalid, fraud approve/reject, funds available/unavailable.

### Lab 05 — Event-based timeout
Modéliser l'attente du résultat clearing avec réponse ou timeout.

### Lab 06 — Pools and lanes
Séparer Customer, MayaBank et Clearing Network, puis structurer les lanes MayaBank.

### Lab 07 — Subprocess decomposition
Extraire `Run Fraud Decision` en subprocess.

### Lab 08 — Exception catalogue
Construire au moins 8 exceptions avec trigger, action et owner.

### Lab 09 — RACI
Construire une matrice RACI pour Payments, Fraud, Operations et Platform.

### Lab 10 — Risk/control mapping
Relier au moins 5 risques à des contrôles et aux activités concernées.

### Lab 11 — KPI catalogue
Définir STP, P95 Processing Time, Timeout Rate, Repair Rate et Notification Failure Rate avec formule/source/target.

### Lab 12 — Process × Application Matrix
Mapper les activités aux applications.

### Lab 13 — Process × Data Matrix
Mapper Payment Instruction, Fraud Decision, Clearing Result et Payment Status.

### Lab 14 — Impact analysis
Analyser l'impact du remplacement de Payment Orchestrator.

### Lab 15 — Bottleneck analysis
Identifier trois bottlenecks potentiels et les données nécessaires pour les confirmer.

### Lab 16 — Process mining dataset
Créer un mini event log de 20 cas avec Case ID, Activity et Timestamp, incluant deux variantes et un loop.

### Lab 17 — Conformance analysis
Comparer l'event log du Lab 16 au modèle cible.

### Lab 18 — Simulation scenario
Comparer Current vs Target avec réduction du manual review rate.

### Lab 19 — Automation candidate assessment
Noter 10 activités selon volume, règles, données, risque et bénéfice.

### Lab 20 — Target process
Produire le target process MayaBank avec idempotency, event-driven status et exception routing.

### Lab 21 — Compliance by design
Ajouter une réglementation fictive, deux exigences et quatre contrôles aux étapes concernées.

### Lab 22 — Review workflow
Définir Draft → Review → Approved → Published → Retired et les rôles associés.

### Lab 23 — Process variant decision
Décider si Domestic Instant Payment et Cross-Border Payment doivent être variantes, processus séparés ou même processus paramétré.

### Lab 24 — Architecture Board
Préparer une synthèse d'une page : current, pain points, target, risks, applications impactées, KPIs, roadmap.

## 3. Questions de contrôle corrigées

### Q01
Quelle différence fondamentale entre Process Architecture et BPMN ?

**Réponse :** Process Architecture structure le paysage, les niveaux, ownerships et relations ; BPMN décrit la logique d'exécution détaillée.

### Q02
Une capability décrit-elle la même chose qu'un process ?

**Réponse :** Non. La capability décrit ce que l'entreprise sait faire ; le process décrit comment le travail est exécuté.

### Q03
Pourquoi ne faut-il pas commencer par toutes les exceptions ?

**Réponse :** Le happy path fournit la structure lisible ; les exceptions sont ensuite ajoutées ou décomposées pour éviter le spaghetti.

### Q04
Quand utiliser XOR ?

**Réponse :** Quand une seule branche parmi plusieurs est choisie selon une condition.

### Q05
Quand utiliser AND ?

**Réponse :** Quand plusieurs branches doivent s'exécuter en parallèle ou être synchronisées.

### Q06
Quel est l'intérêt d'une event-based gateway ?

**Réponse :** Choisir le chemin en fonction du premier événement reçu, par exemple réponse clearing ou timeout.

### Q07
Pool et lane sont-ils équivalents ?

**Réponse :** Non. Le pool représente un participant majeur ; les lanes structurent les responsabilités internes d'un participant.

### Q08
Un message flow peut-il relier deux activités d'une même lane ?

**Réponse :** Normalement non ; le sequence flow exprime l'ordre interne. Le message flow est destiné aux échanges entre participants/pools.

### Q09
Pourquoi utiliser un subprocess ?

**Réponse :** Pour décomposer le détail, favoriser la réutilisation et maintenir la lisibilité.

### Q10
BPMN Message Event = Kafka event ?

**Réponse :** Non. Les niveaux sémantiques sont différents ; le mapping doit être explicite.

### Q11
Quel est le rôle d'un Process Owner ?

**Réponse :** Porter la responsabilité end-to-end du résultat du processus.

### Q12
RACI pilote-t-il automatiquement les permissions HOPEX ?

**Réponse :** Non par principe ; RACI documente les responsabilités. Les mécanismes d'autorisation sont distincts.

### Q13
Quelle différence entre risk et incident ?

**Réponse :** Le risque est une possibilité avec impact potentiel ; l'incident est un événement réellement survenu.

### Q14
Pourquoi relier un contrôle à une activité ?

**Réponse :** Pour savoir où et comment le risque est traité et permettre l'auditabilité.

### Q15
Donner un exemple de contrôle préventif.

**Réponse :** Validation d'entrée, authorization, duplicate prevention.

### Q16
Donner un exemple de contrôle détectif.

**Réponse :** Reconciliation, monitoring ou anomaly detection.

### Q17
Quelle différence KPI/SLA/SLO ?

**Réponse :** KPI mesure une performance ; SLA formalise un engagement ; SLO définit un objectif de niveau de service.

### Q18
Pourquoi mapper process et applications ?

**Réponse :** Pour l'impact analysis, la rationalisation, le design target et la compréhension de la couverture IT.

### Q19
Pourquoi le mapping Activity × Application est-il parfois préférable ?

**Réponse :** Il montre précisément où chaque application intervient dans un processus complexe.

### Q20
Pourquoi mapper process et data ?

**Réponse :** Pour comprendre les informations nécessaires, leurs usages et les impacts de transformation/data governance.

### Q21
Le process mining remplace-t-il le process model ?

**Réponse :** Non. Il révèle l'exécution observée ; le modèle gouverné décrit aussi le standard, l'intention et la cible.

### Q22
Quel minimum faut-il dans un event log ?

**Réponse :** Case ID, Activity et Timestamp ; d'autres attributs enrichissent l'analyse.

### Q23
Simulation = prédiction certaine ?

**Réponse :** Non. Elle compare des scénarios selon des hypothèses et paramètres explicites.

### Q24
Quelle séquence avant automatisation ?

**Réponse :** Understand → Simplify → Standardize → Control → Automate → Measure.

### Q25
Pourquoi RPA peut-il être une dette ?

**Réponse :** Il peut figer une interaction UI fragile et masquer une cible d'intégration plus robuste.

### Q26
Quel problème avec une procédure « click by click » dans un modèle de process architecture ?

**Réponse :** Elle confond logique métier stable et mode opératoire dépendant d'une application.

### Q27
Comment gouverner les variantes de processus ?

**Réponse :** Les créer seulement lorsqu'une différence durable et utile justifie une variante, avec règles de scope et ownership.

### Q28
Pourquoi définir une baseline KPI avant transformation ?

**Réponse :** Pour mesurer objectivement le gain et éviter une amélioration seulement déclarative.

### Q29
Quel intérêt de connecter processus, risques et contrôles ?

**Réponse :** Rendre la conformité et l'auditabilité traçables dans le contexte opérationnel réel.

### Q30
Quels objets sont impactés si Payment Orchestrator change ?

**Réponse :** Activities/processes, applications, données, contrôles, KPIs, technologies et initiatives liées selon le repository.

### Q31
Pourquoi la notification client ne doit-elle pas forcément annuler le paiement si elle échoue ?

**Réponse :** Le résultat financier et le mécanisme de notification sont deux responsabilités différentes ; la compensation doit être sémantiquement correcte.

### Q32
Pourquoi l'idempotency est-elle importante ?

**Réponse :** Pour empêcher qu'un retry ou doublon ne produise une exécution financière multiple.

### Q33
Pourquoi modéliser explicitement les timeouts ?

**Réponse :** Parce que dans un système distribué, l'absence de réponse est un scénario métier/technique réel nécessitant traitement.

### Q34
Qu'est-ce qu'un process handoff ?

**Réponse :** Une transition entre équipes, applications ou modes d'exécution qui peut créer délai, erreur ou perte de responsabilité.

### Q35
Qu'est-ce qu'un vanity KPI ?

**Réponse :** Un indicateur facile à afficher mais peu lié au résultat, par exemple le nombre de diagrammes produits.

### Q36
Quel signe indique un repository BPA mature ?

**Réponse :** Les processus sont gouvernés, reliés aux applications/data/risks, mesurés et utilisés pour conduire des transformations.

### Q37
Que doit contenir un contrôle de qualité avant publication ?

**Réponse :** owner, scope, start/end, conventions BPMN, exceptions critiques, mappings, date de revue et qualité des données.

### Q38
Pourquoi ne pas mapper toutes les technologies directement aux activités ?

**Réponse :** Cela crée trop de granularité et duplique la CMDB ; passer d'abord par les applications/platforms pertinentes.

### Q39
Quelle différence entre current process et target process ?

**Réponse :** Current décrit l'exécution existante ; target décrit le fonctionnement voulu après transformation.

### Q40
Quelle question finale doit toujours être posée ?

**Réponse :** Quelle décision ou amélioration ce modèle permet-il réellement de prendre ?