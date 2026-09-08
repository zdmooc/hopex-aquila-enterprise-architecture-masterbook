# 09 — Enterprise Landscapes, Domains, Segmentation & Federated Cartography

## 1. Pourquoi la cartographie entreprise doit être segmentée

Une entreprise bancaire contient des milliers d’objets. Une cartographie utile doit organiser le repository par **domaines, niveaux et responsabilités**, sans casser l’unicité des objets canoniques.

Objectif :

```text
One repository
+ many governed scopes
+ many audience-specific maps
= scalable enterprise cartography
```

---

## 2. Enterprise Landscape

Vue L0 pédagogique :

```text
Business Domains
├─ Customer
├─ Payments
├─ Accounts
├─ Fraud & Financial Crime
├─ Operations
├─ Compliance
├─ Data
└─ Shared Platforms
```

Elle ne montre pas tous les objets ; elle montre les zones structurantes.

---

## 3. Domain cartography

Chaque domaine peut posséder une vue plus détaillée :

```text
Payments
├─ Capabilities
├─ Processes
├─ Applications
├─ Data
├─ Platforms
├─ Risks
└─ Initiatives
```

Les objets restent les mêmes objets canoniques du repository.

---

## 4. Domain boundary

Une frontière de domaine doit être définie par une responsabilité durable, pas par un diagramme ou un projet.

Questions :

- quelle business responsibility ?
- quel owner ?
- quelles capabilities ?
- quelles informations maîtrisées ?
- quels services exposés ?
- quelles dépendances externes ?

---

## 5. Shared services domain

Certains objets sont transverses :

```text
IAM
API Management
Event Streaming
Observability
Backup/Recovery
Network Services
Cloud/OpenShift Platform
```

Ne pas les dupliquer dans chaque domaine.

---

## 6. Cross-domain dependency

Exemple :

```text
Payments
→ consumes
Fraud Decision

Payments
→ uses
Customer Identity

Payments
→ depends on
Shared IAM
```

Les dépendances cross-domain sont souvent plus importantes que les liens internes au domaine.

---

## 7. Domain interaction map

Vue compacte :

```text
Customer ─→ Payments ─→ Account
               │
               ├→ Fraud
               ├→ Compliance
               └→ Operations
```

Chaque flèche doit être décomposable vers des relations réelles.

---

## 8. Application landscape by domain

Exemple :

```text
Payments
- Payment Orchestrator
- Clearing Gateway
- Reconciliation

Fraud
- Fraud Decision Service

Shared
- API Management
- IAM
- Event Streaming
```

---

## 9. Business capability landscape

Une capability map peut servir de point d’entrée pour naviguer vers :

```text
Capability
→ processes
→ applications
→ data
→ technology
```

La carte ne doit pas devenir un second catalogue indépendant.

---

## 10. Process landscape

Hiérarchie :

```text
L0 Value Chain
→ L1 End-to-End Process
→ L2 Process
→ L3 Subprocess/Activity
```

Le niveau exact suit la gouvernance client.

---

## 11. Information landscape

Exemple :

```text
Customer
Account
Payment
Fraud
Clearing
Reference Data
Operations
```

Puis naviguer vers producers/consumers et systems of record.

---

## 12. Technology landscape

Exemple :

```text
Compute / Container
Integration
Data
Network
Security
Observability
Automation
Backup / DR
```

Relier aux platforms et applications pour éviter un catalogue technologique isolé.

---

## 13. Geographic cartography

Dimensions possibles :

- country ;
- legal entity ;
- region ;
- datacenter ;
- cloud region ;
- business unit.

Ne pas ajouter geography si elle n’aide aucune décision.

---

## 14. Legal entity scope

Utile lorsque :

- ownership juridique diffère ;
- contraintes réglementaires diffèrent ;
- données doivent être séparées ;
- application deployment diffère.

---

## 15. Product / customer segment scope

Une application peut supporter plusieurs segments :

```text
Retail
Corporate
SME
Internal Operations
```

Le scope doit être une relation ou classification gouvernée.

---

## 16. Current vs target enterprise map

Ne pas créer deux repositories.

Préférer :

```text
Canonical objects
+ temporal/lifecycle attributes
+ current views
+ target views
```

selon les capacités/metamodel réels.

---

## 17. Federated ownership

Un repository central peut être alimenté par plusieurs domaines :

```text
Central EA
→ standards / metamodel / governance

Domain architects
→ domain objects / relations

Application owners
→ application attestations

Data owners
→ information ownership
```

---

## 18. Federation ≠ duplication

Mauvais :

```text
Payments creates IAM copy
Fraud creates IAM copy
Customer creates IAM copy
```

Bon :

```text
One IAM object
→ reused across domain views
```

---

## 19. Domain stewardship

Pour chaque domaine :

```text
Domain Owner
Domain Architect
Data Steward
Application Owners
Review cadence
Quality KPIs
```

---

## 20. Cross-domain architecture council

Sujets :

- shared dependencies ;
- conflicts de ownership ;
- duplicate capabilities ;
- shared technology ;
- enterprise standards ;
- transformation collisions.

---

## 21. Enterprise Map Catalog

Catalogue recommandé :

| Map | Scope | Audience | Owner | Review |
|---|---|---|---|---|
| Capability Landscape | Enterprise | Exec/EA | Business Arch | quarterly |
| Application Landscape | Enterprise | EA/IT | App Arch | monthly |
| Data Domain Map | Enterprise | Data/EA | Data Arch | quarterly |
| Technology Landscape | Enterprise | Tech/EA | Tech Arch | monthly |
| Payment Dependency Map | Payments | Solution/Ops | Payment Arch | monthly |

Cadences pédagogiques.

---

## 22. Map hierarchy

```text
Enterprise Map
↓
Domain Map
↓
Capability/Process Map
↓
Application Cooperation Map
↓
Dependency Subgraph
↓
Solution Detail
```

L’utilisateur doit pouvoir descendre progressivement.

---

## 23. Navigation contract

Une map devrait répondre :

- où suis-je ?
- quel scope ?
- quel niveau ?
- où aller ensuite ?
- quel owner ?
- quelle date ?

---

## 24. Large-scale graph partitioning — concept

Pour analyser un grand graphe, on peut partitionner par :

- domain ;
- object type ;
- geography ;
- criticality ;
- platform ;
- lifecycle.

C’est une pratique analytique, pas une fonctionnalité Hopex affirmée ici.

---

## 25. Community detection — usage prudent

Des méthodes de graph analysis peuvent détecter des clusters fortement connectés.

Utilité :

- révéler des domaines techniques naturels ;
- identifier coupling clusters ;
- proposer migration units.

Le résultat doit être confronté au sens métier.

---

## 26. Enterprise hubs

Une cartographie entreprise doit afficher les dépendances transverses structurantes :

```text
IAM
API Management
Event Streaming
Core Banking
Network
Cloud/OpenShift
```

sans surcharger toutes les vues.

---

## 27. Boundary map

Pour un domaine, afficher :

```text
Inside
→ domain applications/data/processes

Boundary
→ exposed services/interfaces

Outside
→ consumers/providers/shared platforms
```

Très utile pour architecture review.

---

## 28. Context map

Une context map répond :

> Comment ce domaine s’insère dans l’entreprise ?

Elle montre seulement les dépendances externes majeures.

---

## 29. Landscape completeness

Questions de qualité :

- chaque capability a-t-elle un owner ?
- chaque application a-t-elle un domain ?
- chaque critical application a-t-elle un process/business service ?
- chaque platform partagée a-t-elle des consumers ?
- chaque domain a-t-il des interfaces avec l’extérieur ?

---

## 30. MayaBank — enterprise domain map

```text
Customer
   ↓ Identity / Channels
Payments
   ↔ Fraud
   ↔ Account/Core
   ↔ Compliance
   ↔ Operations
   ↓ Clearing
External Payment Ecosystem

Shared Platforms
API / IAM / Kafka / OpenShift / Observability / Data
```

---

## 31. MayaBank — Payment domain boundary

Inside :

```text
Payment Orchestrator
Clearing Gateway
Reconciliation
Payment Data
```

Outside dependencies :

```text
Digital Channel
Fraud Decision
Core Account
IAM
Event Streaming
External Clearing
```

---

## 32. Anti-patterns

- une map enterprise avec tous les détails ;
- domaine = équipe projet ;
- objets partagés copiés par domaine ;
- current et target dans des repositories indépendants sans traçabilité ;
- maps sans owner ;
- domain map sans cross-domain dependencies ;
- federation sans règles de qualité communes.

---

## 33. Questions d’entretien

**Comment scaler une cartographie d’entreprise ?**  
Avec des objets canoniques, des scopes hiérarchiques, une gouvernance fédérée et des vues par niveau/audience.

**Pourquoi les cross-domain dependencies sont-elles importantes ?**  
Parce qu’elles concentrent souvent les risques de coordination, de transformation et de continuité.

**Federated repository signifie-t-il plusieurs copies ?**  
Non. La responsabilité de maintenance peut être distribuée tout en conservant une identité canonique partagée.
