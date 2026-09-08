# 04 — Mapping processus ↔ applications, données et architecture

## 1. Pourquoi le mapping est central

Un processus isolé décrit ce que l'entreprise fait. Le mapping cross-layer permet de comprendre **comment le SI rend cette exécution possible**.

Chaîne d'analyse :

```text
Business Process
   ↓
Activity
   ↓
Application / Service
   ↓
Information / Data
   ↓
Technology / Platform
```

## 2. Process ↔ Application

Pour chaque processus majeur, identifier les applications qui supportent son exécution.

Exemple :

| Process/Activity | Application |
|---|---|
| Initiate Payment | Mobile Banking |
| Validate Payment | Payment Orchestrator |
| Fraud Decision | Fraud Decision Service |
| Execute Clearing | Payment Orchestrator / Clearing Adapter |
| Notify Customer | Notification Service |

## 3. Activity ↔ Application

Le niveau process peut être trop grossier.

```text
Execute Instant Payment
```

supporté par dix applications ne dit pas quelle application intervient où.

Le mapping au niveau activité permet :

- impact analysis ;
- rationalisation ;
- identification des handoffs ;
- design target ;
- migration progressive.

## 4. Process ↔ Data

Un processus consomme et produit de l'information.

Exemple :

| Activity | Reads | Writes |
|---|---|---|
| Validate Request | Payment Instruction | Validation Result |
| Fraud Check | Payment + Customer Context | Fraud Decision |
| Clear Payment | Payment Instruction | Clearing Result |
| Notify Customer | Payment Status | Notification Record |

## 5. CRUD n'est pas toujours nécessaire

Une matrice CRUD complète peut être utile, mais elle peut aussi devenir très lourde.

Utiliser le niveau de précision approprié :

```text
Process → Data Domain
```

pour stratégie,

ou :

```text
Activity → Data Object → Read/Create/Update
```

pour design détaillé.

## 6. Process ↔ Capability

Une capability décrit ce que l'entreprise sait faire ; le processus décrit comment elle le fait.

```text
Capability: Payment Execution
        ↓ enabled by
Process: Execute Instant Payment
```

Cette relation permet de relier transformation métier et optimisation opérationnelle.

## 7. Process ↔ Organization

Identifier :

- Process Owner ;
- activity responsibility ;
- participant ;
- escalation owner ;
- operational team.

Ne pas confondre organisation hiérarchique et responsabilité de processus.

## 8. Process ↔ Technology

Éviter de mapper directement chaque activité à des serveurs physiques.

Préférer :

```text
Process
→ Application
→ Platform
→ Technology
```

Puis descendre plus bas uniquement pour un besoin d'impact ou de résilience.

## 9. Process ↔ Risk / Control

Exemple :

```text
Process: Execute Instant Payment
Activity: Fraud Check
Risk: fraudulent transaction accepted
Control: real-time fraud decision
```

Cette chaîne est plus exploitable qu'une liste de risques indépendante.

## 10. Process ↔ KPI

Relier un KPI au bon niveau.

```text
End-to-end process KPI
→ Processing Time

Activity KPI
→ Fraud Decision Latency
```

## 11. Impact analysis

Question :

> Que se passe-t-il si `Payment Orchestrator` est remplacé ?

Navigation :

```text
Payment Orchestrator
→ supported activities
→ processes
→ capabilities
→ business services
→ stakeholders
```

Autre question :

> Quelles étapes dépendent d'une technologie obsolète ?

```text
Technology
→ applications
→ activities
→ processes
```

## 12. Redundancy analysis

Si trois applications supportent la même activité :

```text
Validate Payment
├─ Legacy Validator A
├─ Legacy Validator B
└─ Payment Orchestrator
```

Questions :

- réelle redondance ?
- périmètres différents ?
- transition en cours ?
- application shadow ?
- opportunité de rationalisation ?

## 13. Handoff analysis

Les problèmes apparaissent souvent aux transitions :

```text
Team A → Team B
Application A → Application B
Synchronous → Asynchronous
Automated → Manual
```

Ces handoffs doivent être visibles dans le repository et le diagramme.

## 14. Exemple MayaBank de bout en bout

```text
Capability
Payment Execution
   ↓
Process
Execute Instant Payment
   ↓
Activity
Fraud Check
   ↓
Application
Fraud Decision Service
   ↓
Data
Payment / Customer Context
   ↓
Platform
OpenShift + Event Streaming
```

## 15. Matrices utiles

### Process × Application
Détecte couverture et redondance.

### Activity × Application
Permet impact détaillé.

### Process × Data
Comprend dépendances informationnelles.

### Process × Risk/Control
Soutient compliance.

### Process × Organization
Clarifie ownership/RACI.

## 16. Règles de gouvernance

- réutiliser les objets canoniques ;
- ne pas recréer une application dans le modèle BPMN ;
- relier une activité à la bonne application de référence ;
- éviter le mapping massif sans objectif ;
- documenter la source des relations automatisées ;
- revoir les mappings lors d'une transformation applicative.