# 04 — Criticality, Critical Dependency Paths & Business Impact

## 1. Pourquoi la criticité ne se résume pas à une couleur

Une dépendance critique doit être justifiable par une chaîne d’impact :

```text
Failure
→ technical effect
→ application effect
→ process effect
→ business service effect
→ customer/regulatory/financial effect
```

Une pastille rouge sans cette chaîne ne suffit pas.

---

## 2. Object criticality vs dependency criticality

### Object criticality

Exemple :

```text
Payment Orchestrator = Critical application
```

### Dependency criticality

```text
Payment Orchestrator → Core Account Service = Critical dependency
Payment Orchestrator → Notification = Medium dependency
```

Une application critique peut avoir des dépendances non critiques.

---

## 3. Business criticality

Sources possibles :

- business service tier ;
- customer impact ;
- financial impact ;
- regulatory obligation ;
- operational impact ;
- maximum tolerated outage ;
- business continuity assessment.

Ne pas inventer les niveaux : les reprendre du cadre client.

---

## 4. Critical dependency path

Dans ce masterbook, un `critical dependency path` est une chaîne de dépendances dont la rupture empêche ou dégrade fortement un résultat métier critique.

Exemple :

```text
Instant Payment Service
→ Payment Orchestrator
→ Core Account Service
→ Database Platform
→ Storage
```

Autre branche :

```text
Instant Payment Service
→ Payment Orchestrator
→ Clearing Gateway
→ External Clearing Service
```

---

## 5. Attention au terme critical path

Le `critical path` de gestion de projet correspond à une notion de planification différente.

Ici, on parle de **chaîne critique de dépendances architecturales**.

Toujours préciser le contexte pour éviter l’ambiguïté.

---

## 6. Hard-stop path

Une chaîne hard-stop bloque totalement le service.

```text
Payment Orchestrator
→ Core Account Service
→ Core Database
```

Si aucune alternative n’existe, la perte du DB bloque le paiement.

---

## 7. Degraded path

```text
Payment Orchestrator
→ Event Streaming
→ Notification Service
```

Une panne peut autoriser le paiement mais retarder la notification.

La cartographie doit donc distinguer :

```text
STOP
DEGRADED
DELAYED
MANUAL FALLBACK
NO MATERIAL IMPACT
```

Taxonomie pédagogique à adapter.

---

## 8. Business impact chain

Exemple :

```text
IAM outage
↓
Payment Orchestrator cannot authenticate/authorize
↓
Payment initiation fails
↓
Execute Instant Payment unavailable
↓
Real-Time Payments capability degraded
↓
Customer payments rejected or delayed
```

Cette chaîne permet de défendre la criticité en Architecture Board.

---

## 9. Criticality inheritance — usage prudent

Il est tentant de dire :

```text
Critical business service
→ everything below is Critical
```

C’est souvent faux.

Certaines dépendances sont :

- facultatives ;
- dégradables ;
- protégées par fallback ;
- hors chemin principal.

La criticité doit être propagée avec règles explicites.

---

## 10. Dependency impact dimensions

Score pédagogique possible :

```text
Business impact
Availability coupling
Data criticality
Regulatory impact
Fallback quality
Recovery complexity
Shared concentration
Evidence confidence
```

Ne pas présenter ce score comme un algorithme Hopex natif sans vérification.

---

## 11. Example scoring model

Échelle 1–5 pédagogique :

```text
Business Impact       5
Availability Coupling 5
Fallback              1  (faible fallback = risque fort)
Shared Concentration  4
Recovery Complexity   3
```

Le score peut aider à prioriser une revue, mais ne remplace pas l’analyse qualitative.

---

## 12. Service tiers

Exemple pédagogique MayaBank :

```text
Tier 0 = foundational shared services
Tier 1 = critical customer/business services
Tier 2 = important operational services
Tier 3 = non-critical/supporting services
```

Ne pas imposer cette taxonomie au client.

---

## 13. Foundational dependencies

Services souvent transverses :

- DNS ;
- IAM ;
- PKI ;
- network ;
- API gateway ;
- container platform ;
- database ;
- event platform ;
- observability ;
- secrets service.

Le fait d’être partagé ne suffit pas à être critique : il faut mesurer les consommateurs et alternatives.

---

## 14. Path completeness

Une chaîne critique doit inclure les dépendances qui peuvent réellement arrêter le service.

Exemple incomplet :

```text
Payment App → Core
```

Exemple enrichi :

```text
Payment App
→ IAM
→ API Management
→ Core
→ Database
→ Storage
→ Network/DNS
```

Seulement si ces relations sont réelles et pertinentes.

---

## 15. Shared critical dependency

```text
Payment Orchestrator ─┐
Fraud Service ────────┼→ IAM Platform
API Management ───────┘
```

L’IAM peut être un point de concentration de criticité.

---

## 16. Upstream business exposure

Pour un composant technique :

```text
OpenShift Platform
→ hosted applications
→ supported processes
→ capabilities
→ business services
```

Le résultat est une vue d’exposition métier.

---

## 17. Downstream technical exposure

Pour un service métier :

```text
Instant Payment Service
→ processes
→ applications
→ platforms
→ technologies
→ external dependencies
```

Le résultat est une vue de dépendance technique.

---

## 18. Criticality and environment

Une dépendance peut être :

```text
Critical in PROD
Low in DEV
Medium in UAT
```

Ne pas fusionner les environnements si cela fausse l’analyse.

---

## 19. Criticality and time window

Exemple :

```text
Settlement batch
Critical between 22:00–23:00
Less critical outside window
```

La temporalité peut être représentée comme attribut ou documentation selon le modèle.

---

## 20. Criticality and manual fallback

Un fallback manuel peut réduire l’impact immédiat, mais introduit :

- capacité limitée ;
- risque d’erreur ;
- dépendance aux équipes ;
- temps de traitement ;
- auditabilité.

Il ne transforme pas automatiquement une dépendance critique en dépendance faible.

---

## 21. Criticality and data consistency

Une chaîne peut rester disponible mais produire des données incohérentes.

Exemple :

```text
Payment accepted
Event not published
Reconciliation delayed
```

La criticité doit donc considérer disponibilité **et intégrité**.

---

## 22. Criticality and compliance

Une fonction peut être techniquement contournable mais réglementairement obligatoire.

Exemple : contrôle AML/fraud selon cas.

Le business continuity design doit respecter les contrôles obligatoires réels du client.

---

## 23. Critical Dependency Register

| Dependency | Consumer | Effect | Fallback | Owner | Evidence | Review |
|---|---|---|---|---|---|---|
| IAM | Payment Orchestrator | payment auth blocked | none | IAM Team | verified | quarterly |
| Kafka | Notification | delayed notification | queue/replay | Platform | verified | quarterly |
| Clearing Service | Clearing Gateway | external settlement blocked | scheme-specific | Payments | verified | monthly |

Exemple pédagogique.

---

## 24. Review questions

Pour chaque chemin critique :

1. Quel est le résultat métier ?
2. Quelle dépendance peut l’arrêter ?
3. Quel fallback existe ?
4. Quel failure domain est partagé ?
5. Quelle donnée peut être perdue ?
6. Quel contrôle peut être contourné ou bloqué ?
7. Quel RTO/RPO s’applique ?
8. Quelle preuve confirme la relation ?

---

## 25. MayaBank — chemin critique instant payment

```text
Customer
→ Digital Channel
→ API Management
→ Payment Orchestrator
├→ IAM
├→ Fraud Decision Service
├→ Core Account Service
└→ Clearing Gateway
   → External Clearing Service
```

Branches non nécessairement hard-stop :

```text
Event Streaming
→ Notification
→ Analytics
```

Le statut exact dépend des exigences métier.

---

## 26. MayaBank — business exposure view

Si `Core Account Service` tombe :

```text
Applications affected
→ Payment Orchestrator

Processes affected
→ Execute Instant Payment
→ Account Balance Management

Capabilities affected
→ Payment Execution
→ Account Servicing
```

À confirmer selon repository réel.

---

## 27. Anti-patterns

- tout marquer Critical ;
- propager automatiquement la criticité sans logique ;
- ignorer le fallback ;
- score unique non explicable ;
- critical path limité aux applications sans infra ;
- RTO/RPO utilisés comme simples décorations ;
- confondre impact client et impact technique.

---

## 28. Questions d’entretien

**Qu’est-ce qu’une dépendance critique ?**  
Une dépendance dont la perte provoque un impact métier, opérationnel, réglementaire ou data majeur selon un scénario documenté.

**Pourquoi ne pas propager automatiquement la criticité ?**  
Parce que certaines branches sont dégradables, asynchrones, facultatives ou disposent de fallback.

**Qu’est-ce qu’une chaîne critique architecturale ?**  
Une séquence de dépendances nécessaires au maintien d’un résultat métier critique.
