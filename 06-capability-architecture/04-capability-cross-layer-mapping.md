# 04 — Capability Mapping vers Applications, Data et Technologies

## 1. Pourquoi mapper les capacités

Une capability map seule répond à « ce que l'entreprise doit savoir faire ». Le mapping permet de répondre à « avec quels moyens » et « avec quels risques ».

## 2. Capability ↔ Application

Le mapping doit identifier les applications qui supportent une capability et, quand le métamodèle le permet, la nature du support.

Questions :

- combien d'applications supportent cette capability ?
- existe-t-il des doublons ?
- existe-t-il une dépendance unique ?
- quelles applications sont en fin de vie ?
- quelles applications sont stratégiques ?

Exemple MayaBank :

```text
Capability: Instant Payment Execution
  ├─ Payment Orchestrator
  ├─ Fraud Decision Service
  ├─ Customer Notification
  └─ Payment Ledger
```

## 3. Smart mapping ≠ mapping automatique aveugle

Une suggestion de mapping issue d'un import ou d'un mécanisme automatisé doit être validée. Un nom similaire ne prouve pas une relation sémantique.

## 4. Capability ↔ Data

Une capability peut dépendre de domaines de données ou information concepts.

```text
Fraud Decisioning
→ Customer Identity
→ Account
→ Transaction
→ Device / Session context
```

Cette vue aide à identifier :

- données critiques ;
- domaines sans owner ;
- qualité insuffisante ;
- duplication ;
- contraintes de protection et de résidence.

## 5. Capability ↔ Technology

Le mapping technologique permet de répondre :

```text
Capability stratégique
→ applications support
→ technologies utilisées
→ lifecycle/obsolescence
```

Une capability très stratégique qui dépend d'une technologie obsolète devient un risque d'architecture.

## 6. Capability ↔ Value Stream / Process

```text
Capability = aptitude
Value Stream = étapes de création de valeur
Process = exécution détaillée
```

Le mapping donne un contexte d'usage. Une capability peut contribuer à plusieurs value streams et processus.

## 7. Capability ↔ Organization

On peut distinguer :

- accountable owner ;
- contributing units ;
- operational owner ;
- architecture steward.

Éviter de confondre ownership et hiérarchie de capability.

## 8. Capability ↔ Initiative / Project

Le mapping projet sert à vérifier la stratégie d'investissement :

```text
Project / Initiative
→ improves Capability
→ closes Assessment Gap
→ changes Applications/Technology
```

## 9. Analyse de couverture

Pour chaque capability, construire une fiche :

```text
Importance
Current/Target maturity
Applications count
Critical applications
Technology risk
Data dependencies
Owner
Initiatives
```

## 10. Exemple de détection de redondance

```text
Payment Case Management
→ App A
→ App B
→ App C
```

Si les trois réalisent le même besoin avec forte duplication fonctionnelle, la capability devient un point d'entrée pour rationalisation.

## 11. Exemple de sous-couverture

```text
Real-Time Fraud Decisioning
Importance = 5
Maturity = 2
Supporting applications = 1 legacy component
Technology lifecycle = end-of-support soon
```

Le problème n'est pas seulement applicatif : il devient un gap de capability stratégique.

## 12. Règle de qualité

Ne jamais créer un mapping pour remplir une matrice. Chaque relation doit avoir un sens explicite et, si possible, une source ou un owner responsable.