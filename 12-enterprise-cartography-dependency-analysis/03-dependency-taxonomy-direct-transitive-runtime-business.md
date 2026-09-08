# 03 — Dependency Taxonomy : Direct, Transitive, Runtime, Business & External

## 1. Pourquoi une taxonomie

Deux objets reliés ne signifient pas nécessairement qu’ils dépendent l’un de l’autre de la même manière.

Une bonne cartographie distingue plusieurs familles de dépendances afin de pouvoir répondre à des questions différentes.

---

## 2. Direct dependency

Une dépendance directe existe lorsque l’objet A nécessite explicitement l’objet B pour fournir une fonction ou un service.

Exemple :

```text
Payment Orchestrator
→ invokes
Core Account Service
```

Si le Core Account Service est indisponible, l’exécution du paiement peut être bloquée.

---

## 3. Transitive dependency

```text
Payment Orchestrator
→ Core Account Service
→ Oracle Platform
```

Payment Orchestrator dépend indirectement de la plateforme Oracle.

La criticité transitive doit être interprétée selon la chaîne réelle.

---

## 4. Functional dependency

Une application dépend fonctionnellement d’une autre lorsqu’une responsabilité métier nécessaire est externalisée.

```text
Payment Orchestrator
→ needs Fraud Decision
→ Fraud Decision Service
```

Même si l’appel technique change, la dépendance fonctionnelle reste.

---

## 5. Technical dependency

Une dépendance technique est liée au moyen d’implémentation.

```text
Payment Orchestrator
→ uses
Java Runtime

Payment Orchestrator
→ runs on
OpenShift Platform
```

Elle peut être remplacée sans modifier la responsabilité métier de l’application.

---

## 6. Runtime dependency

Une dépendance runtime est nécessaire pendant l’exécution.

Exemples :

- DNS ;
- IAM ;
- load balancer ;
- database ;
- message broker ;
- external API ;
- certificate service.

Une dépendance architecturale documentée peut être plus stable qu’une instance runtime particulière.

---

## 7. Build-time dependency

Exemples :

```text
Source repository
Artifact registry
Build platform
Dependency repository
Code-signing service
```

Une panne build-time n’arrête pas forcément le service déjà en production, mais bloque les corrections et déploiements.

---

## 8. Deployment dependency

Exemples :

```text
GitOps controller
Container registry
Secrets provisioning
Infrastructure pipeline
```

À distinguer du runtime pour les scénarios de continuité.

---

## 9. Data dependency

```text
Fraud Decision Service
→ reads
Customer Risk Profile
```

Une donnée peut être critique même si son producteur n’est pas appelé en temps réel.

---

## 10. Information dependency vs storage dependency

### Information

```text
Notification Service
→ needs
Payment Status
```

### Storage

```text
Notification Service
→ reads
Notification Store
```

Changer de base de données ne supprime pas la dépendance à l’information métier.

---

## 11. Control dependency

Certaines opérations ne sont autorisées qu’après un contrôle.

```text
Execute Payment
→ requires
Fraud Approval
```

Cette dépendance peut être réglementaire ou liée au risk appetite.

---

## 12. Organizational dependency

Exemple :

```text
Payment Platform
→ operated by
Platform Engineering
```

Un service peut être techniquement redondé mais dépendre d’une seule équipe disposant de la compétence critique.

---

## 13. Supplier dependency

Exemples :

- SaaS provider ;
- cloud provider ;
- telecom carrier ;
- payment scheme ;
- certificate authority ;
- vendor support ;
- external data provider.

La supplier dependency doit être reliée aux applications et services impactés.

---

## 14. Geographic dependency

```text
Application
→ deployed in
Region A
```

ou :

```text
Platform
→ depends on
Data Center X
```

Cela permet l’analyse de concentration géographique.

---

## 15. Network dependency

```text
Application A
→ connects through
Network Zone / Gateway
→ Application B
```

Une architecture multi-site peut dépendre d’un même backbone, firewall cluster ou DNS.

---

## 16. Identity dependency

```text
Application
→ authenticates through
IAM Platform
```

L’IAM est souvent une dépendance transverse avec fort blast radius.

---

## 17. Time dependency

Certaines dépendances ne sont critiques que dans une fenêtre donnée.

Exemples :

- batch de fin de journée ;
- settlement cutoff ;
- reporting réglementaire ;
- certificate renewal ;
- month-end processing.

Une cartographie statique doit documenter cette temporalité si elle change la criticité.

---

## 18. Synchronous dependency

```text
A waits for B
```

Caractéristiques :

- latency coupling ;
- availability coupling ;
- propagation des timeouts ;
- risque de cascading failure.

---

## 19. Asynchronous dependency

```text
A publishes event
B consumes later
```

Elle réduit certains couplages temporels mais introduit :

- broker dependency ;
- lag ;
- backlog ;
- ordering ;
- replay ;
- consistency issues.

---

## 20. Hard dependency

Une dépendance hard bloque la fonction principale.

Exemple :

```text
Payment Orchestrator
→ Core Account Service
```

si aucun débit ne peut être exécuté sans Core.

---

## 21. Soft dependency

Une dépendance soft dégrade le service sans bloquer le résultat principal.

Exemple :

```text
Payment completed
but Notification Service unavailable
```

Le paiement peut rester valide, avec notification différée.

---

## 22. Optional dependency

Une fonctionnalité secondaire peut être désactivée sans impact sur la chaîne critique.

Elle doit être explicitement distinguée pour ne pas gonfler artificiellement le blast radius.

---

## 23. Fallback dependency

Exemple :

```text
Primary Fraud Service
→ fallback to
Rule Engine B
```

Une dépendance de fallback devient critique uniquement en cas de perte du primaire.

---

## 24. Dependency state

Taxonomie pédagogique :

```text
Current
Planned
Target
Temporary
Deprecated
Retired
```

Une dépendance temporaire de migration ne doit pas devenir permanente par défaut.

---

## 25. Dependency criticality

Une relation peut porter ou être associée à :

```text
Critical
High
Medium
Low
```

Mais la criticité doit découler d’un scénario documenté.

---

## 26. Dependency rationale

Pour les liens critiques, conserver une justification :

```text
Why needed?
What happens if unavailable?
Is fallback available?
Is dependency synchronous?
What is maximum tolerated outage?
Who owns remediation?
```

---

## 27. MayaBank — dependency register

| Consumer | Dependency | Type | Criticality | Failure effect |
|---|---|---|---|---|
| Payment Orchestrator | Core Account Service | Functional/runtime | Critical | payment cannot execute |
| Payment Orchestrator | Fraud Decision Service | Control/runtime | Critical | decision unavailable |
| Payment Orchestrator | Event Streaming | Async/runtime | High | downstream events delayed |
| Notification | Event Streaming | Async/runtime | Medium | notification delayed |
| Payment Orchestrator | IAM | Security/runtime | Critical | authorization/authentication failure |
| Reconciliation | Payment Status Data | Data | High | reconciliation incomplete |

Valeurs pédagogiques à adapter au contexte réel.

---

## 28. Dependency layering

Même service, plusieurs dépendances :

```text
Payment Orchestrator
├─ functional → Fraud Decision
├─ data → Payment State
├─ runtime → OpenShift
├─ security → IAM
├─ integration → API Management
├─ asynchronous → Kafka
└─ operational → Observability
```

Cette vue est plus utile qu’un simple `depends on` généralisé.

---

## 29. Dependency ambiguity

Mauvais :

```text
A depends on B
```

sans savoir :

- pourquoi ;
- quand ;
- dans quel sens ;
- avec quel fallback ;
- pour quelle fonction.

---

## 30. Dependency vs association

Toute association n’est pas une dépendance.

```text
Application owned by Org Unit
```

est une relation de responsabilité.

Elle peut devenir importante dans une analyse organisationnelle, mais n’est pas nécessairement une dépendance runtime.

---

## 31. Dependency vs co-location

Deux applications déployées sur le même cluster :

```text
A and B on OpenShift cluster
```

ne signifie pas que A dépend fonctionnellement de B.

Elles partagent toutefois un failure domain.

---

## 32. Shared dependency

```text
A → IAM
B → IAM
C → IAM
```

La plateforme IAM devient une dépendance commune.

Cette concentration doit être analysée indépendamment des liens applicatifs directs.

---

## 33. Hidden dependency

Dépendance absente du repository mais révélée par :

- incident ;
- logs ;
- CMDB ;
- network flow ;
- workshop ;
- deployment manifest ;
- code/configuration ;
- architecture review.

Elle doit passer par un processus de validation avant d’être considérée comme vérité canonique.

---

## 34. Anti-patterns

- une seule relation `depends on` pour tout ;
- confondre hard et soft dependency ;
- ignorer build/deployment dependencies ;
- oublier les external providers ;
- considérer asynchronous comme « sans dépendance » ;
- confondre shared failure domain et direct functional dependency ;
- absence de rationale pour les dépendances critiques.

---

## 35. Questions d’entretien

**Quelle différence entre dépendance fonctionnelle et technique ?**  
La première concerne une responsabilité nécessaire au métier ; la seconde concerne un moyen d’implémentation ou d’exécution.

**Asynchronous signifie-t-il découplé de toute dépendance ?**  
Non. Le couplage temporel baisse, mais le broker, les contrats, les backlogs et la cohérence deviennent de nouvelles dépendances.

**Qu’est-ce qu’une soft dependency ?**  
Une dépendance dont la perte dégrade une fonction sans bloquer le service métier principal.

**Pourquoi cartographier les dépendances build-time ?**  
Parce qu’elles influencent la capacité à corriger, reconstruire et redéployer pendant un incident ou une transformation.
