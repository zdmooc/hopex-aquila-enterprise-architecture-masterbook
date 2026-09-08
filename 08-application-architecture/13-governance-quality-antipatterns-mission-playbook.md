# 13 — Gouvernance, qualité, anti-patterns et playbook de mission

## 1. Une architecture applicative n’est utile que si elle reste vraie

Le principal risque n’est pas l’absence de diagramme.

C’est un repository rempli de modèles devenus faux.

La gouvernance doit répondre :

```text
Who owns the application?
Who validates dependencies?
Who approves interface changes?
When was the model reviewed?
Which source is authoritative?
Which target state is approved?
```

## 2. Rôles

### Application Owner
Responsable de l’actif applicatif et de sa maintenance fonctionnelle/technique selon modèle client.

### Solution Architect
Conçoit les changements, dépendances et target architecture.

### Enterprise Architect
Maintient cohérence transverse, standards et trajectoires.

### Integration Architect
Gouverne patterns et contrats d’intégration.

### Data Architect / Data Owner
Valide responsabilités et impacts data.

### Platform Architect
Valide déploiement et contraintes plateforme.

### Security Architect
Valide trust boundaries, identity, protection et risques.

### Operations/SRE
Valide observability, resilience, recovery et exploitabilité.

## 3. Lifecycle de revue d’un modèle

Exemple pédagogique :

```text
Draft
→ Architecture Review
→ Approved
→ Published
→ Under Change
→ Revalidated
→ Retired
```

Le workflow réel dépend de la configuration HOPEX et de la gouvernance entreprise.

## 4. Triggers de revue

Revue obligatoire lors de :

- nouveau projet ;
- changement d’interface ;
- migration cloud/OpenShift ;
- changement de provider ;
- incident majeur ;
- technology EOL ;
- changement réglementaire ;
- decommission ;
- fusion d’applications ;
- changement de data ownership.

## 5. Architecture Definition of Done

Une modification applicative structurante ne devrait pas être considérée terminée si :

- application objects non mis à jour ;
- interfaces non documentées ;
- dependencies non revues ;
- target/current incohérents ;
- data ownership absent ;
- NFR non testés ;
- operational readiness absente ;
- decommission impact non traité.

## 6. Naming quality

Applications : noms fonctionnels stables.

Interfaces : nom qui exprime le service/contrat.

Events : nom de fait passé.

Exemples :

```text
Payment Orchestrator
Fraud Decision API
PaymentStatusChanged
```

Éviter :

```text
APP123
New Service
Interface 01
Topic-prod-v2-final
```

## 7. Relationship quality

Une relation doit être :

- nécessaire ;
- sémantiquement comprise ;
- orientée correctement ;
- reliée à des objets canoniques ;
- maintenable ;
- idéalement sourcée pour les dépendances critiques.

## 8. Diagram quality

Un diagramme doit répondre à une question.

Exemples :

```text
What supports Instant Payment?
What depends on Payment Orchestrator?
How will Notification be decoupled?
Where are the shared failure domains?
```

Éviter les diagrammes encyclopédiques.

## 9. Data quality indicators

- owner completeness ;
- purpose completeness ;
- lifecycle completeness ;
- business mapping completeness ;
- interface ownership completeness ;
- dependency review freshness ;
- duplicate rate ;
- orphan applications ;
- orphan interfaces ;
- stale target states.

## 10. Anti-pattern — application wallpaper

Symptôme : 200 boîtes et flèches sur une page.

Correction : vues par domaine/question + repository navigable.

## 11. Anti-pattern — infrastructure disguised as application architecture

Symptôme :

```text
VM001 → VM002 → DB003
```

sans responsabilités applicatives.

Correction : partir des applications/services, descendre au déploiement seulement si nécessaire.

## 12. Anti-pattern — project copy

Chaque projet recrée :

```text
Payment Orchestrator Project A
Payment Orchestrator Project B
```

Correction : réutiliser l’objet canonique et créer des vues/initiatives.

## 13. Anti-pattern — all microservices in enterprise view

Un diagramme devient inutilisable.

Correction : application/service macro + vues solution détaillées.

## 14. Anti-pattern — interface without owner

Une API existe techniquement mais personne ne maîtrise sa compatibilité.

Correction : provider owner + lifecycle/version policy.

## 15. Anti-pattern — hidden consumer

Un fichier, batch ou requête SQL est absent du modèle.

Correction : campagne de dependency discovery + validation owner.

## 16. Anti-pattern — target only

Architecture magnifique mais current inconnu.

Correction : baseline current + gaps + transition states.

## 17. Anti-pattern — current only

Cartographie sans décision.

Correction : utiliser le modèle pour impact, target et roadmap.

## 18. Anti-pattern — cloud washing

Legacy déplacé sur containers sans changement de coupling/state.

Correction : distinguer rehost/replatform/refactor/rearchitect.

## 19. Anti-pattern — event washing

Tous les échanges deviennent Kafka sans réflexion.

Correction : sélectionner interaction style selon besoin de coupling, latency et consistency.

## 20. Anti-pattern — CMDB copy

Copier des milliers de CIs dans HOPEX sans use case.

Correction : intégrer seulement les objets/relations nécessaires au raisonnement d’architecture.

## 21. Anti-pattern — architecture as documentation after project

Le modèle est rempli après go-live.

Correction : utiliser le repository pour concevoir, revoir et décider avant implémentation, puis réconcilier avec le réel.

## 22. Playbook mission — semaine 1

### Jour 1

- comprendre scope ;
- identifier stakeholders ;
- récupérer standards et current diagrams ;
- identifier source of truth.

### Jour 2

- extraire application catalog ;
- dédupliquer ;
- définir canonical IDs ;
- identifier owners.

### Jour 3

- mapper capabilities/processes ;
- identifier business services critiques.

### Jour 4

- construire dependency graph ;
- identifier interfaces critiques ;
- découvrir hidden integrations.

### Jour 5

- revue collective ;
- produire gaps ;
- prioriser analyses semaine 2.

## 23. Playbook mission — semaine 2

- NFR ;
- data responsibilities ;
- deployment/failure domains ;
- security boundaries ;
- lifecycle/technology risk ;
- current architecture baseline.

## 24. Playbook mission — semaine 3

- target principles ;
- target application map ;
- integration decisions ;
- migration options ;
- transition states ;
- impact analysis.

## 25. Playbook mission — semaine 4

- architecture board ;
- decision log ;
- roadmap ;
- repository quality gates ;
- handover owners ;
- operationalization.

## 26. Atelier application architecture

Agenda 2h :

```text
00:00 scope/outcome
00:15 application responsibilities
00:40 dependencies/interfaces
01:05 data and NFR
01:25 current pain points
01:40 target principles
01:55 decisions/actions
```

## 27. Questions à poser à un Application Owner

1. Quelle responsabilité unique porte l’application ?
2. Qui sont ses utilisateurs ?
3. Quels services expose-t-elle ?
4. Quels systèmes consomme-t-elle ?
5. Qui la consomme ?
6. Quelles données maîtrise-t-elle ?
7. Quel est son lifecycle ?
8. Quels NFR sont contractuels ?
9. Où est-elle déployée ?
10. Quel est son plus gros risque ?
11. Quelle est sa cible à 2–3 ans ?
12. Quels changements majeurs sont prévus ?

## 28. Architecture Board pack

Une synthèse efficace :

1. contexte/business driver ;
2. current architecture ;
3. problème mesuré ;
4. principles ;
5. options ;
6. target architecture ;
7. data/security/NFR ;
8. impacts ;
9. transition ;
10. risks/decisions.

## 29. Option analysis

Exemple : Fraud Service.

### Option A — internal service

Avantages : contrôle et intégration.

Risques : coût/run/model operations.

### Option B — SaaS

Avantages : time-to-market et service spécialisé.

Risques : data residency, vendor dependency, latency, contract.

### Option C — hybrid

Avantages : flexibilité.

Risques : complexité.

L’architecture repository doit capturer décision et impacts, pas seulement le gagnant.

## 30. Interview case 1

**Question :** Une application a 40 consumers et doit être remplacée. Que faites-vous ?

**Réponse structurée :**

1. inventory consumers/interfaces ;
2. classify criticality ;
3. define target contract ;
4. compatibility/adapter strategy ;
5. migrate waves ;
6. observability ;
7. deprecation governance ;
8. remove old interface only after evidence.

## 31. Interview case 2

**Question :** Le métier veut 99.99% de disponibilité mais le service dépend d’un SaaS à 99.9%.

**Réponse :** analyser l’objectif end-to-end, le contrat fournisseur, alternatives/degraded mode, buffering, failover possible et aligner expectation métier ; l’application locale ne peut compenser magiquement une dépendance moins disponible.

## 32. Interview case 3

**Question :** Faut-il mettre tous les microservices dans HOPEX ?

**Réponse :** non par principe. Le niveau de granularité doit servir une décision. Les microservices peuvent rester dans des outils de solution/observabilité, tandis que HOPEX conserve applications, services et dépendances structurantes.

## 33. Interview case 4

**Question :** Comment détecter un SPOF ?

**Réponse :** analyser non seulement infrastructure mais dépendances logiques, shared platforms, external providers, data stores, identity, DNS/network et opérations. Plusieurs pods ne suppriment pas un SPOF de design.

## 34. Interview case 5

**Question :** Application Architecture et ArchiMate ?

**Réponse :** ArchiMate fournit un langage standard de modélisation ; HOPEX est le repository/plateforme. Un objet HOPEX n’est pas automatiquement un élément ArchiMate, même si certaines vues peuvent utiliser le framework ArchiMate.

## 35. TOGAF articulation

```text
TOGAF
method/governance

ArchiMate
modeling language

HOPEX
repository + analysis + governance

Application Architecture
one architecture domain/use case modeled and governed in that ecosystem
```

## 36. Signes de maturité

### Level 1 — Inventory
Applications listées.

### Level 2 — Ownership
Catalog propre + owners/lifecycle.

### Level 3 — Connected
Business, interfaces, data, technology reliés.

### Level 4 — Decision Support
Impact analysis, NFR, target/transition utilisés.

### Level 5 — Continuous Governance
Automated discovery selectively reconciled, workflows, quality metrics, roadmaps et architecture boards s’appuient sur le repository.

## 37. Checklist finale

Une Partie VIII appliquée en mission doit permettre :

- catalogue canonique ;
- responsibility maps ;
- business alignment ;
- interfaces gouvernées ;
- integration patterns ;
- dependency impact ;
- data responsibility ;
- deployment view ;
- NFR/resilience ;
- lifecycle/debt ;
- current/transition/target ;
- quality governance.
