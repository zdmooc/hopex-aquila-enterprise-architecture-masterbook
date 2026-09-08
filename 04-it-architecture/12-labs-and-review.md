# 12 — Labs, Exercises & Review

Cette série est conçue pour être réalisable **sans accès HOPEX** sous forme de modélisation papier/Markdown, puis à rejouer dans une instance HOPEX si un environnement de formation est disponible.

---

# LAB 01 — Canonical Application Inventory

## Objectif
Construire l'inventaire applicatif du domaine Payments sans doublons.

## Données brutes

```text
Payment Hub
Payment Hub Prod
Legacy Payments
Payments Application
Fraud Engine
Fraud Service
Notification Hub
```

## Travail

1. identifier les doublons probables ;
2. définir les objets canoniques ;
3. attribuer owner, criticality et lifecycle ;
4. documenter les décisions de fusion.

## Correction attendue

Ne pas conclure uniquement sur les noms. Vérifier la sémantique. `Payment Hub`, `Payment Hub Prod`, `Legacy Payments` peuvent être trois libellés du même système, mais il faut une preuve/source.

---

# LAB 02 — Capability Mapping

## Données

Applications :

- Payment Orchestrator ;
- Fraud Engine ;
- Notification Hub ;
- Identity Platform.

Capabilities :

- Real-Time Payment Processing ;
- Fraud Detection ;
- Customer Authentication ;
- Customer Communication.

## Travail
Créer la matrice application × capability.

## Correction possible

| Application | Capability |
|---|---|
| Payment Orchestrator | Real-Time Payment Processing |
| Fraud Engine | Fraud Detection |
| Identity Platform | Customer Authentication |
| Notification Hub | Customer Communication |

Une application peut en supporter plusieurs ; la matrice doit refléter le contexte réel.

---

# LAB 03 — Flow Mapping

## Scenario

```text
Mobile App
→ Payment API
→ Payment Orchestrator
→ Fraud API
→ Fraud Engine
```

Après acceptation :

```text
Payment Orchestrator
→ PaymentStatusChanged
→ Kafka
→ Notification Hub
```

## Travail
Séparer :

- applications ;
- interfaces ;
- flows ;
- technologies/platforms.

## Correction

`Kafka` n'est pas automatiquement une application. Le Payment Status Event est distinct de la plateforme qui le transporte.

---

# LAB 04 — Application Environment

## Travail
Dessiner l'environnement du Payment Orchestrator avec :

- upstream ;
- downstream ;
- interfaces ;
- shared services.

## Minimum attendu

```text
Channels
↓
API Platform
↓
Payment Orchestrator
├─ Fraud Engine
├─ Identity
├─ DB Service
├─ Event Platform
└─ Clearing
```

---

# LAB 05 — Technology Catalog

## Technologies

```text
WebSphere
OpenShift
Java 8
Java 21
Kafka
Legacy MQ
Oracle
PostgreSQL
```

## Travail
Pour chacune :

- category ;
- enterprise lifecycle ;
- source ;
- owner ;
- applications using it.

## Point de vigilance
Les statuts ne doivent pas être inventés comme facts réels. Pour le lab, les valeurs sont pédagogiques.

---

# LAB 06 — Standards Decision

## Contexte
MayaBank veut standardiser les runtimes applicatifs.

Options :

- WAS + Java 8 ;
- OpenShift + Java LTS ;
- unmanaged Kubernetes ;
- VM + custom runtime.

## Travail
Construire une décision avec :

- criteria ;
- standard status ;
- exceptions ;
- impacted apps.

## Correction attendue
Le résultat n'est pas universel. La qualité est dans la traçabilité de la décision et des impacts.

---

# LAB 07 — Obsolescence Impact

## Contexte
`Legacy MQ` doit être retiré.

Relations :

```text
Legacy MQ
→ Legacy Payment Hub
→ Batch Adapter
```

## Travail
Remonter jusqu'aux processus/capabilities impactés et proposer une action.

## Correction

```text
Legacy MQ
→ apps
→ payment processes
→ business capabilities
→ migration initiative
```

---

# LAB 08 — Deployment Architecture

## Travail
Construire le déploiement cible :

- OpenShift ;
- API Gateway ;
- Event Platform ;
- Database Service ;
- Identity ;
- Observability.

Distinguer :

- platform logique ;
- environment ;
- runtime instance.

---

# LAB 09 — HA vs DR

## Scenario

Application répliquée sur 3 pods dans un seul site.

Question : est-elle DR-ready ?

## Correction
Non. Trois pods augmentent la disponibilité locale mais ne garantissent pas une reprise après perte du site.

---

# LAB 10 — SPOF Analysis

## Graphe

```text
Channel
→ API Gateway
→ Payment Orchestrator
→ Fraud Engine
→ Clearing
```

Shared : Identity, DB.

## Travail
Identifier les composants dont la panne bloque le flux.

## Correction
La réponse dépend des mécanismes de résilience. Il faut distinguer dépendance logique et architecture réelle HA.

---

# LAB 11 — Current / Target

## Current

```text
WAS
Legacy MQ
point-to-point
manual DR
```

## Target

```text
OpenShift
Event Streaming
API Management
automated recovery
```

## Travail
Créer la table current → target → gap → action.

---

# LAB 12 — Transition Architecture

## Contrainte
Le legacy clearing adapter doit rester 9 mois après le démarrage du Payment Orchestrator.

## Travail
Dessiner une transition réaliste.

## Correction
La transition doit explicitement montrer le nouvel orchestrateur et l'adapter legacy, avec l'exit criterion.

---

# LAB 13 — Blast Radius

## Incident
Identity Platform indisponible.

## Travail
Calculer le blast radius logique jusqu'aux channels et capabilities.

## Correction
Ne pas relier automatiquement tous les consommateurs : vérifier quelle interface exige réellement l'identité au runtime.

---

# LAB 14 — Technology EOL Query

## Question
Lister les applications critiques utilisant une technologie `Deprecated`.

## Pseudo-requête

```text
Applications
WHERE Criticality = Critical
AND uses Technology.lifecycle = Deprecated
```

## Résultat attendu
Une liste actionnable avec application, technology, owner, remediation.

---

# LAB 15 — Application Rationalization

## Portfolio

| App | Business Fit | Technical Fit |
|---|---:|---:|
| Legacy Hub | high | low |
| Payment Orchestrator | high | high |
| Old Reporting | low | low |
| Notification Hub | medium | high |

## Travail
Classer invest / modernize / tolerate / retire.

## Correction
Le classement ne doit pas être mécanique : dépendances et contraintes doivent être vérifiées.

---

# LAB 16 — Roadmap Dependencies

Initiatives :

```text
A Event Platform
B Payment Orchestrator
C Notification Migration
D Legacy MQ Retirement
```

## Travail
Ordonner les dépendances.

## Correction possible

```text
A → B
A → C
B/C → D
```

La séquence exacte dépend du design.

---

# LAB 17 — Legacy Decommission Checklist

Construire la preuve de retrait du Legacy Payment Hub.

Minimum :

- no consumers ;
- no active flows ;
- data archived ;
- licenses stopped ;
- infrastructure removed ;
- monitoring removed ;
- CMDB updated ;
- HOPEX lifecycle updated.

---

# LAB 18 — Architecture Board

Préparer une revue de 10 minutes pour le Payment target architecture.

Structure :

```text
Context
Current
Drivers
Risks
Target
Key decisions
Dependencies
Migration
Trade-offs
Ask / approval
```

---

# LAB 19 — Repository Quality

Calculer :

```text
% apps without owner
% apps without lifecycle
% deprecated tech without remediation
% target apps without deployment
% legacy apps without retirement date
```

Puis prioriser les corrections.

---

# LAB 20 — HOPEX vs CMDB Boundary

Classer chaque information :

- logical application ;
- pod name ;
- business capability ;
- VM serial ;
- technology standard ;
- current CPU usage ;
- strategic lifecycle ;
- incident ticket ;
- deployment architecture.

## Correction indicative

HOPEX/EAM : logical application, capability, standard, strategic lifecycle, deployment architecture.

CMDB/run : pod, VM serial, runtime CPU, incident — avec synchronisation sélective si nécessaire.

---

# 30 questions de contrôle

## Q01
Pourquoi ne pas utiliser un diagramme comme source unique ?

**Réponse :** parce que l'objet et ses relations doivent être réutilisables dans plusieurs vues et analyses.

## Q02
Application logique et environnement Prod sont-ils deux applications ?

**Réponse :** généralement non ; l'environnement représente un contexte de déploiement.

## Q03
Kafka est-il automatiquement une application ?

**Réponse :** non, il représente généralement une technologie ou plateforme selon le modèle.

## Q04
Pourquoi mapper application ↔ capability ?

**Réponse :** pour mesurer l'impact métier et raisonner en valeur plutôt qu'en inventaire technique.

## Q05
Interface et flow sont-ils identiques ?

**Réponse :** non ; l'interface est un point d'exposition/consommation, le flow représente un échange/interactions.

## Q06
Faut-il stocker l'OpenAPI complet dans HOPEX ?

**Réponse :** pas nécessairement ; la spécification détaillée appartient généralement à l'API management/Git.

## Q07
À quoi sert le technology lifecycle ?

**Réponse :** à identifier conformité, obsolescence et priorités de migration.

## Q08
Vendor lifecycle et enterprise lifecycle sont-ils identiques ?

**Réponse :** non.

## Q09
Qu'est-ce qu'un shared service ?

**Réponse :** une capacité/platform service utilisée par plusieurs applications et créant une dépendance transversale.

## Q10
Trois pods dans un site garantissent-ils le DR ?

**Réponse :** non.

## Q11
Quelle est la première condition d'une impact analysis fiable ?

**Réponse :** des relations correctes, sémantiques et à jour.

## Q12
Qu'est-ce qu'un blast radius ?

**Réponse :** l'ensemble des éléments potentiellement affectés par une panne ou modification.

## Q13
Pourquoi filtrer une analyse multi-hop ?

**Réponse :** pour éviter une explosion de résultats sans valeur décisionnelle.

## Q14
Une target architecture est-elle une roadmap ?

**Réponse :** non ; la target est l'état souhaité, la roadmap le chemin.

## Q15
Pourquoi modéliser une transition ?

**Réponse :** pour rendre visible la coexistence temporaire et les risques de migration.

## Q16
Quand un legacy est-il réellement retired ?

**Réponse :** quand les dépendances sont migrées et le runtime effectivement décommissionné.

## Q17
Quel lien entre obsolescence et business impact ?

**Réponse :** technologie → applications → processus/capabilities.

## Q18
Discovery automatique remplace-t-il la gouvernance ?

**Réponse :** non.

## Q19
Pourquoi conserver l'owner ?

**Réponse :** pour attribuer la responsabilité de la qualité et des décisions.

## Q20
Une couleur rouge manuelle est-elle une bonne gestion d'obsolescence ?

**Réponse :** non ; mieux vaut dériver la visualisation d'une propriété gouvernée.

## Q21
Pourquoi ne pas importer tous les pods ?

**Réponse :** leur volatilité et granularité sont souvent hors besoin EAM.

## Q22
Que doit montrer une deployment architecture ?

**Réponse :** applications, plateformes, shared services, data stores et dépendances structurantes.

## Q23
Qu'est-ce qu'une technology standard status ?

**Réponse :** une décision interne sur l'usage futur d'une technologie.

## Q24
Une technologie supportée par l'éditeur peut-elle être `Retire` en interne ?

**Réponse :** oui.

## Q25
Pourquoi documenter les external dependencies ?

**Réponse :** elles font partie du risque et du blast radius.

## Q26
Quel est le rôle d'une architecture board ?

**Réponse :** challenger et valider les choix, risques, standards et trajectoires.

## Q27
Une migration vers une nouvelle plateforme produit-elle automatiquement un gain Green IT ?

**Réponse :** non, le legacy doit réellement être décommissionné.

## Q28
Que doit contenir un exit criterion ?

**Réponse :** les conditions vérifiables permettant de quitter un état de transition ou retirer le legacy.

## Q29
Pourquoi relier une dette à une initiative ?

**Réponse :** pour transformer le constat en action gouvernée.

## Q30
Quelle est la question finale d'une IT Architecture ?

**Réponse :** quelles décisions prendre, avec quels impacts et quelle trajectoire ?
