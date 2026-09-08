# 08 — Business Information, Objects & Policies

## 1. Pourquoi l'information appartient à la Business Architecture

Une capability ou un processus ne fonctionne pas sans information. La Business Architecture doit donc identifier les concepts métier essentiels avant de descendre vers les modèles de données techniques.

Exemple MayaBank :

```text
Customer
Account
Payment Order
Beneficiary
Fraud Decision
Payment Status
Settlement Position
```

Ce sont des concepts métier ; ils ne sont pas encore des tables, topics Kafka ou JSON schemas.

## 2. Business Object vs Data Object technique

```text
Business concept : Payment Order
Logical data    : Payment Transaction Record
Physical data   : table PAYMENT_TX / event payment.executed.v1
```

La Partie IX détaillera l'Information & Data Architecture.

## 3. Information ownership

Pour chaque information importante, documenter :

- business owner ;
- steward ;
- authoritative source ;
- classification ;
- lifecycle ;
- retention ;
- privacy/regulatory constraints ;
- consumers majeurs.

## 4. Information × Capability

Exemple :

```text
Fraud Decisioning
uses Customer Risk Profile
uses Payment Order
produces Fraud Decision
```

Cette cartographie permet d'identifier les capabilities dépendantes d'informations critiques.

## 5. Information × Process

```text
Execute Payment
reads Payment Order
updates Payment Status
produces Payment Confirmation
```

## 6. Information × Business Service

```text
Payment Status Service
exposes Payment Status
```

La donnée devient ainsi reliée à la valeur délivrée.

## 7. Information × Application

Ne pas commencer directement par les tables.

Préférer :

```text
Business Information
→ logical information responsibility
→ Application support
→ physical implementation
```

## 8. Business glossary

Un glossary gouverné réduit les ambiguïtés.

Exemple :

```text
Payment Order
Instruction submitted by a payer to transfer funds to a beneficiary.
```

À distinguer de :

```text
Payment Transaction
Technical/operational record of execution state.
```

## 9. Policy & Business Rule

Une policy exprime une règle structurante ou principe de gouvernance.

Exemples MayaBank :

```text
Every instant payment must receive a final status.
Sensitive payment data must be retained according to regulatory policy.
High-risk payments require enhanced fraud decisioning.
```

Le niveau technique d'implémentation n'est pas la policy elle-même.

## 10. Rule traceability

Bonne chaîne :

```text
Regulatory Driver
→ Business Policy
→ Business Rule
→ Process Control
→ Application Requirement
→ Technical Control
```

Cette traçabilité est particulièrement utile en banque.

## 11. Data classification business view

Catégories possibles :

```text
Public
Internal
Confidential
Restricted
```

ou une taxonomie d'entreprise plus détaillée.

Le repository doit utiliser une classification contrôlée et non des libellés libres.

## 12. Retention & lifecycle

L'information peut avoir :

- active period ;
- legal retention ;
- archival ;
- deletion ;
- anonymization.

Ne pas confondre lifecycle de l'information et lifecycle de l'application qui la stocke.

## 13. MayaBank example

```text
Payment Order
Owner: Payments Business
Classification: Confidential
Used by: Payment Orchestration
Processed by: Execute Instant Payment
Supported by: Payment Orchestrator
Constraints: retention + auditability + integrity
```

## 14. Anti-patterns

- un business object par table ;
- un concept métier par champ JSON ;
- aucune définition ;
- owner inconnu ;
- source autoritative non documentée ;
- policy stockée uniquement dans une note libre ;
- mêmes concepts avec plusieurs noms ;
- données sensibles sans classification.

## 15. Entretien

**Pourquoi modéliser l'information au niveau business ?**  
Pour rendre explicites les concepts utilisés par les métiers et relier leur ownership aux capabilities, processus et services avant les choix techniques.

**Pourquoi est-ce important en transformation ?**  
Parce qu'on peut remplacer une application sans perdre l'identité ni les règles de gouvernance de l'information qu'elle supporte.