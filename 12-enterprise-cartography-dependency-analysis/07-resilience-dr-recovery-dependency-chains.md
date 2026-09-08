# 07 — Resilience, DR & Recovery Dependency Chains

## 1. Pourquoi la résilience est une analyse de dépendances

Une architecture peut afficher plusieurs replicas, plusieurs sites et plusieurs bases tout en échouant si un service partagé reste indisponible.

L’analyse de résilience doit donc partir du graphe :

```text
Business Service
→ Applications
→ Platforms
→ Data
→ Network
→ Identity
→ External Services
→ Operational Dependencies
```

---

## 2. Service recovery chain

Exemple MayaBank :

```text
Instant Payment Service
→ Digital Channel
→ API Management
→ Payment Orchestrator
→ IAM
→ Core Account Service
→ Database
→ Clearing Gateway
→ External Clearing Service
```

Pour restaurer le service, il faut comprendre l’ordre de dépendance entre ces éléments.

---

## 3. Recovery order vs dependency direction

Si :

```text
Payment Orchestrator → depends on → IAM
```

alors la reprise doit généralement restaurer IAM avant Payment Orchestrator.

Le recovery order est souvent l’inverse du sens de consommation.

---

## 4. Recovery graph

Construire un sous-graphe contenant uniquement :

- services critiques ;
- hard dependencies ;
- données nécessaires ;
- plateformes indispensables ;
- external services ;
- operational dependencies.

Exclure les dépendances facultatives pour obtenir un `minimum viable service`.

---

## 5. Minimum viable service

Question :

> Quels composants doivent être disponibles pour exécuter un paiement valide, même en mode dégradé ?

Exemple pédagogique :

```text
Required
API Management
IAM
Payment Orchestrator
Fraud Decision
Core Account
Clearing Gateway

Can be delayed
Notification
Analytics
Some reporting
```

À valider métier/risk.

---

## 6. Recovery tier

Taxonomie pédagogique :

```text
R0 = foundational services
R1 = critical transaction services
R2 = critical operations/support
R3 = non-critical/reporting
```

Le client peut avoir sa propre classification.

---

## 7. RTO propagation

Le RTO d’un service métier ne se répartit pas automatiquement de façon égale.

Si :

```text
Business RTO = 30 minutes
```

et qu’il faut restaurer :

```text
IAM
DB
OpenShift
Application
Validation
```

les budgets techniques doivent être compatibles avec l’objectif global.

---

## 8. RPO propagation

Un RPO global dépend des stores impliqués :

```text
Payment state
Fraud decision
Clearing state
Reconciliation state
```

Une seule base avec RPO insuffisant peut rendre le RPO métier incohérent.

---

## 9. HA vs DR dependency graph

### HA

Traite souvent une perte locale :

```text
node / instance / AZ
```

### DR

Traite une perte plus large :

```text
site / region / platform
```

Les dépendances externes et de contrôle plane deviennent cruciales.

---

## 10. Shared control-plane dependency

Une application active sur deux sites peut dépendre d’un seul :

- IAM control plane ;
- DNS ;
- PKI ;
- GitOps ;
- secrets backend ;
- database primary ;
- network hub.

Le multi-site doit être analysé à travers ces dépendances.

---

## 11. Data recovery dependencies

Exemple :

```text
Restore DB
→ validate schema
→ restore payment state
→ verify Kafka offsets/replay
→ reconcile external clearing state
```

Le redémarrage technique ne prouve pas la cohérence métier.

---

## 12. Event recovery dependency

Après une panne Event Streaming :

- producer backlog ;
- consumer lag ;
- duplicate replay ;
- ordering ;
- schema compatibility ;
- reconciliation.

La cartographie doit identifier les consommateurs critiques.

---

## 13. External dependency during DR

Le PRA interne peut être réussi mais le service rester indisponible si :

```text
External Clearing
Telecom
Cloud service
Certificate authority
Fraud data provider
```

n’est pas accessible depuis le site de secours.

---

## 14. Network recovery chain

```text
DNS
→ routing
→ firewall
→ load balancer
→ ingress
→ service
```

Chaque niveau peut conditionner le suivant.

---

## 15. Identity recovery chain

```text
Directory / federation
→ token service
→ service identities
→ privileged admin
→ application access
```

Sans accès privilégié, l’équipe peut être incapable d’exécuter la reprise.

---

## 16. Observability dependency

L’observabilité n’est pas toujours nécessaire au fonctionnement, mais elle est souvent nécessaire pour :

- diagnostiquer ;
- valider la reprise ;
- suivre le backlog ;
- confirmer les SLO ;
- prouver la stabilité.

Elle doit apparaître dans le recovery plan.

---

## 17. Backup service dependency

Le backup est une dépendance de recovery et non nécessairement runtime.

```text
Service running
≠ Backup service available
```

Mais lors d’un incident destructif, le backup devient critique.

---

## 18. Recovery evidence

Pour chaque dépendance critique :

```text
Last tested
Test scope
Observed recovery time
Observed data loss
Known limitation
Owner
Evidence link
```

Une architecture PRA sans test est une hypothèse.

---

## 19. Dependency-aware DR test

Scénario : perte du site A.

Étapes :

1. vérifier services foundation au site B ;
2. restaurer/activer data services ;
3. vérifier IAM/PKI/secrets ;
4. activer plateformes ;
5. activer applications critiques ;
6. tester interfaces externes ;
7. valider processus métier ;
8. vérifier replay/reconciliation ;
9. mesurer RTO/RPO réels.

---

## 20. Recovery dependency matrix

| Service | Depends on | Recovery tier | RTO | Evidence |
|---|---|---|---|---|
| Payment Orchestrator | IAM, OCP, DB, Core | R1 | client-defined | test |
| Clearing Gateway | Network, PKI, Partner | R1 | client-defined | test |
| Notification | Kafka, provider | R2 | client-defined | test |

---

## 21. Failure scenario catalog

Exemples :

```text
Single pod failure
Worker failure
Cluster failure
Database failure
Kafka failure
IAM failure
DNS failure
Site failure
External clearing failure
Certificate expiry
Corrupted payment data
```

Chaque scénario traverse un sous-graphe différent.

---

## 22. Dependency-specific fallback

Exemple :

```text
Primary clearing link unavailable
→ secondary network route?
→ alternate endpoint?
→ queued transaction?
→ reject safely?
```

Le fallback doit être modélisé comme mécanisme réel, pas comme note vague.

---

## 23. Safe degradation

Une dégradation acceptable doit préserver :

- intégrité ;
- contrôles obligatoires ;
- audit trail ;
- cohérence de statut ;
- absence de double traitement.

---

## 24. Cascading failure

Exemple :

```text
Core slows down
→ Payment Orchestrator threads accumulate
→ API timeouts
→ retries increase
→ load rises
→ outage spreads
```

La cartographie des dépendances doit être enrichie par les caractéristiques runtime pour analyser ce type de cascade.

---

## 25. Failure containment

Questions :

- circuit breaker ?
- timeout budget ?
- queue isolation ?
- bulkhead ?
- rate limiting ?
- degraded mode ?

Ces mécanismes appartiennent au design de solution ; la cartographie peut documenter leur existence au niveau utile.

---

## 26. MayaBank — recovery sequence pédagogique

```text
1. Network / DNS / IAM / PKI
2. Data platforms
3. OpenShift / runtime platforms
4. Core Account Service
5. Fraud Decision Service
6. Payment Orchestrator
7. Clearing Gateway
8. Event Streaming consumers
9. Notification / Reconciliation
10. Reporting / Analytics
```

Cet ordre est pédagogique, à adapter à l’architecture réelle.

---

## 27. MayaBank — DR gap example

Supposons :

```text
Payment Orchestrator = dual-site
Core DB = dual-site
Clearing Gateway = dual-site
IAM = only site A
```

Le service reste dépendant du site A via IAM.

La cartographie révèle un faux sentiment de résilience.

---

## 28. Architecture Board deliverable

Pour un service critique :

- recovery dependency view ;
- RTO/RPO matrix ;
- top shared dependencies ;
- untested dependencies ;
- external dependencies ;
- fallback status ;
- DR gaps ;
- remediation roadmap.

---

## 29. Anti-patterns

- multi-site = DR automatique ;
- recovery plan sans graphe de dépendances ;
- RTO métier copié sur chaque composant ;
- ignorer IAM/DNS/PKI ;
- oublier external services ;
- backup = replication ;
- démarrage technique = service restauré ;
- PRA non testé.

---

## 30. Questions d’entretien

**Pourquoi inverser parfois la dépendance pour la reprise ?**  
Parce qu’un consommateur ne peut être restauré utilement avant ses prérequis.

**Qu’est-ce qu’un minimum viable service ?**  
Le sous-ensemble minimal de dépendances permettant de rendre le service métier essentiel de façon sûre.

**Pourquoi l’observabilité fait-elle partie du recovery graph ?**  
Parce qu’elle permet de diagnostiquer et valider que la reprise est réellement saine.
