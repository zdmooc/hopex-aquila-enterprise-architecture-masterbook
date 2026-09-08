# 13 — Governance, Data Quality, Anti-Patterns & Mission Playbook

## 1. Une cartographie sans gouvernance se dégrade vite

Les dépendances changent en permanence :

- application releases ;
- API versions ;
- platform upgrades ;
- migrations ;
- decommissioning ;
- team ownership ;
- external providers ;
- data flows.

Une cartographie fiable nécessite une operating model.

---

## 2. Roles

### Enterprise Architect

- définit les principes ;
- arbitre les standards de cartographie ;
- assure cohérence cross-domain.

### Domain Architect

- maintient les dépendances structurantes du domaine ;
- valide cross-domain dependencies.

### Solution Architect

- documente les dépendances de solution ;
- met à jour current/target/transitions.

### Application Owner

- atteste consumers/providers ;
- valide lifecycle et criticality.

### Platform Owner

- maintient services partagés et consumers principaux.

### Data Owner / Steward

- valide data dependencies et source of truth.

### Risk / Security

- valide controls, classification et critical exposure.

### Repository Administrator

- gouverne métamodèle, imports, permissions et quality rules.

---

## 3. RACI pédagogique

| Activity | EA | Domain Arch | App Owner | Platform Owner | Data | Risk |
|---|---|---|---|---|---|---|
| Define relation rules | A | R | C | C | C | C |
| Validate app dependencies | C | R | A/R | C | C | C |
| Validate platform consumers | C | C | C | A/R |  |  |
| Validate data lineage | C | C | C |  | A/R | C |
| Critical path review | A | R | R | R | C | C |
| Decommission approval | C | R | A | C | C | C |

À adapter à l’organisation.

---

## 4. Dependency lifecycle

Taxonomie recommandée :

```text
Proposed
Discovered
In Review
Verified
Deprecated
Retired
```

Le métamodèle/workflow réel peut être différent.

---

## 5. Source hierarchy

Sources possibles :

```text
Owner attestation
Architecture documentation
Runtime observation
CMDB / ServiceNow
API gateway inventory
Network flow
Deployment manifests
Code/configuration
Workshop
Inference
```

La priorité dépend de la relation.

---

## 6. Evidence record

Pour dépendance critique :

```text
Source
Evidence date
Validator
Confidence
Last review
Next review
Notes
```

---

## 7. Attestation workflow

Exemple pédagogique :

1. dependency discovered/imported ;
2. owner receives review ;
3. owner confirms/rejects ;
4. architect resolves conflict ;
5. relation becomes Verified ;
6. periodic re-attestation.

---

## 8. Review cadence

Cadence proportionnée :

```text
Critical shared dependencies → frequent
Normal application dependencies → periodic
Stable strategic maps → quarterly/biannual
Retired objects → archive/close
```

Ne pas imposer une fréquence universelle.

---

## 9. Trigger-based review

Revue déclenchée par :

- major release ;
- incident ;
- migration ;
- acquisition ;
- vendor change ;
- new critical API ;
- platform upgrade ;
- audit finding ;
- security event.

---

## 10. Quality dimensions

### Completeness

Les relations nécessaires existent-elles ?

### Accuracy

Sont-elles vraies ?

### Consistency

Respectent-elles la même sémantique ?

### Freshness

Sont-elles récentes ?

### Ownership

Quelqu’un est-il responsable ?

### Traceability

Peut-on retrouver la source ?

---

## 11. Quality rules

Exemples :

```text
Critical Application must have Owner
Critical Application must support ≥1 Process/Capability
Critical Application must have Platform/Deployment context
Critical Interface must have Provider and Consumer
Critical Dependency must have Evidence and Owner
Target object must not depend on Retired technology without exception
```

Les règles exactes doivent être adaptées au métamodèle.

---

## 12. Quality dashboard inputs

Mesures possibles :

- % critical apps with complete dependency map ;
- % verified relations ;
- stale relation count ;
- orphan critical objects ;
- unknown consumers ;
- unowned interfaces ;
- untested DR dependencies ;
- temporary dependencies past expiry.

Reporting détaillé en Partie XV.

---

## 13. Dependency review board

Pour les shared platforms :

```text
Top consumers
Critical paths
Current incidents
Capacity
Lifecycle
DR evidence
Known debt
Upcoming changes
```

---

## 14. Architecture Board entry criteria

Une décision de changement devrait fournir :

- current dependency view ;
- target dependency view ;
- blast radius ;
- unknowns ;
- criticality ;
- migration sequence ;
- recovery/fallback ;
- owners ;
- data quality/confidence.

---

## 15. Architecture Board exit criteria

```text
Decision recorded
Risks accepted/mitigated
Dependencies assigned
Unknowns converted to actions
Target relations approved
Temporary relations have expiry
```

---

## 16. Change governance

Lorsqu’une application change :

1. compare current vs target ;
2. identify relation deltas ;
3. assess blast radius ;
4. notify owners ;
5. test critical paths ;
6. update repository after deployment ;
7. retire obsolete dependencies.

---

## 17. Incident feedback loop

Après incident :

```text
Observed dependency
vs
Repository dependency
```

Écarts :

- missing edge ;
- wrong criticality ;
- hidden shared service ;
- stale fallback ;
- incorrect recovery order.

Transformer l’incident en amélioration de la cartographie.

---

## 18. Discovery governance

Les imports automatiques ne doivent pas être publiés comme vérité sans règles.

Pipeline recommandé :

```text
Discover
→ Normalize
→ Match canonical object
→ Classify relation
→ Validate
→ Publish
```

---

## 19. Conflict resolution

Exemple :

```text
CMDB says A → B
Owner says relation removed
Network flow still observes A → B
```

Process :

1. conserver evidence ;
2. dater les sources ;
3. investiguer ;
4. résoudre ;
5. documenter décision.

---

## 20. Manual vs automatic source

Automatic n’est pas toujours plus correct.

Exemple : réseau observe un appel technique mais ne comprend pas sa sémantique métier.

Manual n’est pas toujours plus fiable : owner peut oublier un consumer.

Combiner sources.

---

## 21. Anti-pattern — spaghetti map

Symptômes :

- centaines d’objets ;
- lignes croisées ;
- aucune question ;
- tous les niveaux mélangés.

Remédiation :

```text
Scope
Layers
Filters
Domain maps
Subgraphs
Matrices
```

---

## 22. Anti-pattern — fake precision

```text
Blast Radius = 87.42
```

avec relations non validées.

Remédiation : confidence + known unknowns.

---

## 23. Anti-pattern — dependency inflation

Créer `depends on` pour toute relation augmente artificiellement le graphe.

Remédiation : relation taxonomy stricte.

---

## 24. Anti-pattern — forgotten external dependency

Cartographie interne parfaite mais absence de :

- clearing ;
- SaaS ;
- cloud ;
- network carrier ;
- certificate authority.

---

## 25. Anti-pattern — target fantasy

Target map sans :

- transition ;
- coexistence ;
- migration dependency ;
- owners ;
- dates ;
- decommission plan.

---

## 26. Anti-pattern — stale graph

Une cartographie de 18 mois utilisée pour changement critique sans revalidation.

Toujours afficher freshness/confidence.

---

## 27. Mission Playbook — semaine 1

### Scope & baseline

Livrables :

- stakeholder map ;
- critical business services ;
- top applications/platforms ;
- data sources ;
- known incidents ;
- current cartography maturity.

Workshops :

```text
Business criticality
Application dependencies
Platform dependencies
Data/control dependencies
```

---

## 28. Mission Playbook — semaine 2

### Build dependency graph

Actions :

- normalize objects ;
- map direct dependencies ;
- map external dependencies ;
- map shared platforms ;
- validate critical paths ;
- record evidence/confidence.

---

## 29. Mission Playbook — semaine 3

### Analyze

- blast radius ;
- hubs ;
- cycles ;
- SPOF candidates ;
- recovery chains ;
- change scenarios ;
- current/target delta.

---

## 30. Mission Playbook — semaine 4

### Govern & handover

- Architecture Board ;
- risk register ;
- dependency debt backlog ;
- ownership ;
- review cadence ;
- query library ;
- view library ;
- next 90-day roadmap.

---

## 31. Deliverable pack

1. Enterprise Context Map.
2. Domain Dependency Map.
3. Critical Dependency Register.
4. Shared Service Hub Map.
5. Blast Radius scenarios.
6. Recovery Dependency View.
7. Current/Target Delta.
8. Migration Dependency Map.
9. Quality Dashboard inputs.
10. Governance RACI.

---

## 32. 30/60/90 day plan

### 30 days

- critical scope ;
- canonical objects ;
- direct dependencies ;
- top risks.

### 60 days

- transitive analysis ;
- external dependencies ;
- recovery graph ;
- change scenarios.

### 90 days

- automation/import ;
- periodic attestations ;
- advanced analytics ;
- portfolio integration.

---

## 33. Interview case — outage shared IAM

Réponse structurée :

1. identify consumers ;
2. separate hard/soft dependency ;
3. map business exposure ;
4. verify fallback ;
5. analyze DR ;
6. validate recovery order ;
7. capture missing dependencies from incident.

---

## 34. Interview case — retire legacy application

1. direct consumers ;
2. indirect processes ;
3. data ;
4. batch ;
5. controls ;
6. external parties ;
7. target replacement ;
8. migration evidence ;
9. owner approval.

---

## 35. Interview case — 500-app spaghetti map

Réponse :

- do not redraw manually ;
- define canonical inventory ;
- segment by domain ;
- type relations ;
- build layered views ;
- use matrices/queries ;
- start with critical business outcomes.

---

## 36. Interview case — HOPEX vs CMDB

HOPEX :

```text
architecture context
business traceability
portfolio
relationships
impact analysis
transformation
```

CMDB :

```text
operational configuration items
runtime/service management context
```

Ils peuvent être intégrés ; ils ne sont pas identiques.

---

## 37. Interview case — graph analytics

Si on vous demande `centrality` :

> C’est une méthode pour repérer des nœuds structurellement importants. Je l’utiliserais comme signal, pas comme mesure directe de criticité métier. Si Hopex ne calcule pas la métrique nativement dans le contexte client, j’utiliserais API/export sans créer une seconde source de vérité.

---

## 38. Maturity model pédagogique

### Level 1 — Artifacts

Diagrammes isolés.

### Level 2 — Connected repository

Objets canoniques et relations de base.

### Level 3 — Governed dependency maps

Sources, owners, current/target, critical paths.

### Level 4 — Decision-grade impact analysis

Blast radius, recovery, change scenarios.

### Level 5 — Continuous intelligence

Discovery, attestations, analytics, portfolio integration, incident feedback.

---

## 39. Definition of Done de la Partie XII

```text
13 substantive chapters
Enterprise graph method
Dependency taxonomy
Critical paths
Blast radius
Cycles/hubs/SPOF
DR recovery order
Change/migration/decommission
Data/control dependencies
Enterprise federation
Graph analytics boundary
MayaBank full model
Governance playbook
Labs/questions/sources
```

---

## 40. Questions d’entretien

**Comment maintenir une dependency map ?**  
Avec ownership, evidence, sources automatiques/manuelles, attestations et triggers de revue.

**Comment éviter le spaghetti ?**  
En segmentant par scope, layer et question, tout en réutilisant les mêmes objets canoniques.

**Quelle est la meilleure source de dépendances ?**  
Il n’y en a pas une universelle : il faut combiner observation, inventory, architecture et validation métier/technique selon la relation.

**Que faire d’une dépendance inconnue détectée pendant un incident ?**  
La capturer comme découverte, la valider, puis mettre à jour le repository et les scénarios de reprise.
