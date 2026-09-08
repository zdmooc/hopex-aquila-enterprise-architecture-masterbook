# 08 — Process governance operating model, lifecycle, versioning et publication

## 1. Pourquoi une gouvernance dédiée

Un repository BPA devient rapidement obsolète si la gouvernance repose uniquement sur la bonne volonté des modelers.

La gouvernance doit préciser :

- qui peut proposer un processus ;
- qui le modélise ;
- qui valide le contenu métier ;
- qui valide les liens IT/data/risk ;
- qui approuve ;
- qui publie ;
- qui maintient ;
- qui décide du retrait.

Le détail des statuts et workflows dépend de la configuration HOPEX du client. Le modèle ci-dessous est une **pratique recommandée**, pas une promesse d'écran ou de workflow standard identique dans toutes les installations.

## 2. Rôles fondamentaux

### Process Owner

Accountable du résultat end-to-end.

Responsabilités :

- arbitrer le scope ;
- valider les outcomes ;
- accepter les risques résiduels métier ;
- approuver la cible ;
- prioriser les améliorations.

### Process Steward

Garant opérationnel du contenu du repository.

Responsabilités :

- préparer les revues ;
- maintenir descriptions et relations ;
- suivre les demandes de modification ;
- contrôler la qualité ;
- coordonner les SMEs.

### Process Analyst / Architect

Structure le modèle, les niveaux, les vues et l'analyse.

### Subject Matter Expert

Valide la réalité opérationnelle d'une partie du processus.

### Application / Solution Architect

Valide les relations avec applications, services, interfaces et technologies lorsque nécessaires.

### Risk / Compliance

Valide risks, controls, obligations et audit points.

### Data Steward

Valide les objets informationnels/data critiques.

### Repository Administrator

Administre configuration, droits et mécanismes de publication selon le modèle de gouvernance global.

## 3. RACI de gouvernance

Exemple MayaBank :

| Activité | Owner | Steward | Analyst | SME | Risk | Architect |
|---|---|---|---|---|---|---|
| définir scope/outcome | A | R | R | C | C | C |
| modéliser BPMN | C | R | R | C | I | C |
| valider opérations | A | R | C | R | C | I |
| valider controls | C | C | I | C | A/R | I |
| valider app/data links | I | C | R | C | I | A/R |
| approuver publication | A | R | C | C | C | C |
| revue périodique | A | R | C | C | C | C |

RACI ne doit pas être confondu avec les permissions techniques du produit.

## 4. Lifecycle recommandé

```text
Proposed
→ Draft
→ In Review
→ Approved
→ Published
→ Under Change
→ Published (new approved baseline)
→ Retired
```

Statuts optionnels selon contexte :

```text
Rejected
Suspended
Deprecated
Archived
```

Le nombre de statuts doit rester minimal.

## 5. Proposed

Utiliser un état de proposition lorsque l'organisation veut filtrer les demandes avant de créer un modèle complet.

Informations minimales :

- business need ;
- proposed owner ;
- expected outcome ;
- parent/domain ;
- raison de création ;
- recherche de doublons effectuée.

## 6. Draft

Le modeler construit :

- scope ;
- hierarchy ;
- happy path ;
- exceptions principales ;
- participants ;
- relations essentielles ;
- owner ;
- premières métriques.

Un Draft n'est pas une vérité officielle.

## 7. In Review

La revue doit être multi-perspective.

### Revue métier

- logique correcte ;
- responsabilités correctes ;
- exceptions réalistes ;
- terminology correcte.

### Revue architecture

- application mappings ;
- données ;
- interfaces critiques ;
- current/target cohérents.

### Revue risk/compliance

- risques ;
- contrôles ;
- SoD ;
- checkpoints réglementaires.

### Revue qualité repository

- doublons ;
- naming ;
- relations orphelines ;
- objets canoniques ;
- dates de revue.

## 8. Approved vs Published

`Approved` signifie que les autorités définies ont validé le contenu.

`Published` signifie que cette baseline est exposée comme référence officielle aux consommateurs autorisés.

Selon le client, ces notions peuvent être fusionnées ou séparées.

## 9. Publication

La publication doit préciser :

- audience ;
- date d'effet ;
- version/baseline ;
- owner ;
- review date ;
- changements significatifs ;
- liens vers procédures opérationnelles si elles existent.

## 10. Under Change

Le modèle officiel ne doit pas disparaître pendant qu'une nouvelle version est préparée.

Principe :

```text
Published baseline N
+ work-in-progress N+1
```

La stratégie exacte dépend des mécanismes de version disponibles dans l'environnement client.

## 11. Versioning sémantique de gouvernance

La numérotation ci-dessous est pédagogique :

### Major change

- outcome modifié ;
- scope modifié ;
- changement majeur d'orchestration ;
- nouvelle obligation structurante ;
- fusion/split de processus.

### Minor change

- activité ajustée ;
- clarification ;
- nouveau mapping ;
- contrôle supplémentaire sans changement d'outcome.

### Editorial change

- wording ;
- layout ;
- description ;
- correction non sémantique.

Ne pas supposer qu'HOPEX applique automatiquement cette convention.

## 12. Baseline current / transition / target

Pour une transformation importante, séparer :

```text
Current process
Transition process
Target process
```

Ne pas mélanger les trois dans un seul diagramme illisible.

La relation avec la roadmap doit permettre de répondre :

- quand la cible devient-elle effective ?
- quelles initiatives permettent le passage ?
- quelles applications sont retirées ?
- quels contrôles changent ?

## 13. Review triggers

Revue obligatoire lors de :

- changement réglementaire ;
- incident majeur ;
- dépassement KPI persistant ;
- migration applicative ;
- changement d'organisation ;
- changement de contrôle ;
- modification d'un service critique ;
- changement de canal ;
- nouvelle externalisation ;
- changement significatif de volume ;
- préparation d'un audit.

## 14. Review calendar

La fréquence dépend du risque.

Exemple pédagogique :

| Criticité | Revue minimale |
|---|---|
| critique paiement/fraude | 6 mois |
| important | 12 mois |
| standard | 18-24 mois |

Une revue événementielle peut intervenir avant la date planifiée.

## 15. Governance workflow — exemple logique

```text
Change Request
      ↓
Triage by Process Steward
      ↓
Duplicate / Scope Check
      ↓
Model Update
      ↓
Business Review
      ↓
Architecture + Risk Review
      ↓
Quality Gate
      ↓
Process Owner Approval
      ↓
Publish
      ↓
Notify stakeholders
```

Ce workflow est une recommandation, pas la description d'un workflow HOPEX standard garanti.

## 16. Change request

Chaque changement devrait contenir :

- requester ;
- reason ;
- impacted process ;
- urgency ;
- regulatory/incident/project trigger ;
- desired effective date ;
- evidence/source ;
- impacted stakeholders.

## 17. Segregation of duties dans la gouvernance

Pour un processus critique, éviter que la même personne puisse :

```text
Create
+ Review
+ Approve
```

sans contrôle indépendant.

La SoD organisationnelle du processus est distincte des permissions techniques du repository, même si les deux doivent être cohérentes.

## 18. Process retirement

Un processus peut être retiré si :

- remplacé ;
- fusionné ;
- produit/service retiré ;
- réglementation supprimée ;
- activité externalisée ;
- transformation terminée.

Avant retrait :

- identifier consommateurs ;
- identifier liens entrants ;
- conserver traçabilité historique selon politique ;
- rediriger vers le successeur ;
- mettre à jour owners/roadmaps.

## 19. Process variants governance

Créer une variante seulement si une différence est :

- durable ;
- significative ;
- utile à la décision ;
- possédée ;
- mesurable ;
- maintenable.

Exemple :

```text
Execute Instant Payment
├─ Domestic
└─ Cross-Border
```

peut être légitime si obligations, participants ou flows diffèrent réellement.

## 20. Repository authority model

Décider explicitement :

```text
HOPEX = authoritative process architecture repository
```

et documenter les frontières avec :

- Confluence ;
- SharePoint ;
- BPM runtime engine ;
- process mining tool ;
- CMDB ;
- ticketing ;
- document management.

La duplication de source de vérité est une dette de gouvernance.

## 21. Publication audience

Une même connaissance peut être exposée avec des vues différentes :

### Executive

- process landscape ;
- outcomes ;
- KPIs ;
- risks ;
- roadmap.

### Operations

- detailed flow ;
- exceptions ;
- responsibilities ;
- escalation.

### Architecture

- applications ;
- data ;
- dependencies ;
- target.

### Risk/Audit

- obligations ;
- controls ;
- evidence points.

## 22. Governance KPIs

Ne pas confondre performance du processus et performance de gouvernance.

Exemples :

- % processes avec owner ;
- % processes revus à temps ;
- % critical processes avec risk/control mapping ;
- % critical processes avec application mapping ;
- nombre de doublons identifiés ;
- délai moyen d'approbation ;
- % process models bloqués par quality gate.

## 23. MayaBank — gouvernance de `Execute Instant Payment`

### Accountable

Head of Payments / Payment Process Owner fictif.

### Stewards

Payments Process Excellence.

### Reviewers

- Fraud ;
- Compliance ;
- Operations ;
- Solution Architecture ;
- Data ;
- Platform/SRE.

### Triggers spécifiques

- change scheme ;
- clearing incident ;
- fraud control change ;
- migration Payment Orchestrator ;
- new channel ;
- SLA breach trend.

## 24. Deliverables de gouvernance

- Process Governance Charter ;
- RACI ;
- Lifecycle Policy ;
- Naming Standard ;
- Review Calendar ;
- Publication Checklist ;
- Change Request Template ;
- Retirement Checklist ;
- Quality Dashboard.

## 25. Questions d'entretien

**Pourquoi séparer Approved et Published ?**  
Parce que la validation du contenu et son exposition comme référence officielle sont deux décisions de gouvernance différentes.

**Comment éviter `FINAL2` ?**  
Avec une règle d'identité, un lifecycle, une baseline autoritative et un mécanisme de changement gouverné.

**Qui doit posséder un processus transverse ?**  
Un owner accountable du résultat end-to-end, pas nécessairement l'équipe qui possède l'application dominante.

**Quand déclencher une revue hors calendrier ?**  
Lorsqu'un changement de risque, réglementation, architecture, organisation, incident ou performance remet en cause le modèle publié.