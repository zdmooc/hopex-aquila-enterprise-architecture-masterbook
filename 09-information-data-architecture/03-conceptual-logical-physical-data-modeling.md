# 03 — Conceptual, Logical & Physical Data Modeling

## 1. Trois niveaux à ne pas confondre

```text
Conceptual
= concepts métier et relations essentielles

Logical
= structure détaillée indépendante d’un DBMS

Physical
= implémentation dans une technologie précise
```

## 2. Conceptual Data Model

Le conceptual model répond à :

- quels concepts structurent le domaine ?
- comment sont-ils reliés ?
- quelles distinctions métier sont importantes ?

Exemple MayaBank :

```text
Customer
1 ─── owns ─── * Account

Customer
1 ─ initiates ─ * Payment

Payment
1 ─ has ─ 1..* Payment Status Event

Payment
1 ─ assessed by ─ 0..* Fraud Decision
```

Pas de nom de table, index, partition ou type Oracle ici.

## 3. Logical Data Model

Le logical model précise :

- entities ;
- attributes ;
- identifiers ;
- relationships ;
- cardinalities ;
- optionality ;
- normalization decisions ;
- business rules structurantes.

Exemple :

```text
Payment
- PaymentId
- EndToEndId
- DebtorAccountId
- CreditorAccountReference
- Amount
- Currency
- RequestedExecutionTimestamp
- CurrentStatus
```

## 4. Physical Data Model

Le physical model décrit une implémentation :

```text
Schema PAYMENT
Table PAYMENT_TX
Column PAYMENT_ID UUID
Column AMOUNT DECIMAL(18,2)
Index IX_PAYMENT_E2E
Partition by execution_date
```

Le niveau physique dépend du DBMS et de la plateforme.

## 5. Traçabilité entre niveaux

La valeur vient de la chaîne :

```text
Business Term
→ Conceptual Entity
→ Logical Entity/Attribute
→ Physical Table/Column
```

Cela permet d’analyser l’impact d’un changement de définition métier sur l’implémentation.

## 6. Reverse engineering

Les pages publiques HOPEX Data Governance indiquent la capacité de démarrer les modèles physiques par database reverse engineering puis de générer des couches logiques et conceptuelles connectées.

Règle : reverse engineering crée une **matière technique**, pas automatiquement un modèle métier propre.

Après import, il faut :

1. nettoyer le scope ;
2. identifier les objets utiles ;
3. relier aux concepts ;
4. documenter ownership et usage ;
5. éliminer ou masquer le bruit technique.

## 7. Keys

### Business Key

Identifiant métier stable lorsque possible.

### Surrogate Key

Identifiant technique utilisé pour performance ou implémentation.

Ne pas confondre :

```text
CustomerNumber
≠ CUSTOMER_SK
```

## 8. Cardinalités

Les cardinalités expriment des règles structurelles.

Exemple :

```text
Account 1 → * Payment
Payment 1 → 0..* Fraud Decision
Payment 1 → * Status History
```

Une cardinalité doit être validée avec le métier et l’implémentation cible.

## 9. Normalisation

La normalisation peut réduire anomalies et duplication dans les modèles transactionnels.

Mais l’architecture enterprise doit reconnaître d’autres modèles :

- dimensional ;
- document ;
- key-value ;
- graph ;
- event payload ;
- denormalized read model.

Ne pas juger automatiquement un modèle dénormalisé comme mauvais sans contexte.

## 10. Transactional vs Analytical

### Transactional

Optimisé pour opérations métier cohérentes et fréquentes.

### Analytical

Optimisé pour exploration, agrégation, reporting ou ML.

Exemple MayaBank :

```text
Payment Operational Store
→ transaction processing

Payment Analytics Store
→ trends / KPIs / fraud analytics
```

## 11. Canonical Data Model

Un canonical model peut réduire les mappings N×N lorsqu’il est réellement partagé.

Mais il devient dangereux si :

- trop générique ;
- gouverné par personne ;
- tous les systèmes doivent s’y conformer intégralement ;
- il mélange domaines indépendants.

Préférer un périmètre clair et des contrats versionnés.

## 12. Bounded Context et Data Model

Dans une architecture DDD :

```text
Customer in CRM context
≠ Customer in Fraud context automatically
```

Les contextes peuvent avoir des modèles différents d’un même concept.

Le repository doit documenter la correspondance plutôt que forcer un faux modèle universel.

## 13. Event schemas

Un event schema est un contrat de données temporel.

Exemple :

```text
PaymentStatusChanged
- eventId
- paymentId
- previousStatus
- newStatus
- changedAt
- reasonCode
- correlationId
```

Questions :

- qui possède le schema ?
- quelle version ?
- compatibilité backward/forward ?
- PII présente ?
- durée de rétention ?

## 14. API payloads

Un API payload n’est pas automatiquement le modèle logique enterprise.

Il peut être :

- projection ;
- command ;
- response ;
- agrégat ;
- version contractuelle.

Le mapping vers les informations canoniques doit être explicite quand nécessaire.

## 15. Schema evolution

Avant modification :

```text
Schema change
→ producers
→ consumers
→ mappings
→ stores
→ lineage
→ reports
→ controls
```

La compatibilité doit être évaluée avant déploiement.

## 16. Exemple MayaBank — conceptual

```text
Customer
  ↓ owns
Account
  ↓ funds
Payment
  ↓ evaluated by
Fraud Decision
  ↓ routed through
Clearing
  ↓ produces
Settlement Result
```

## 17. Exemple MayaBank — logical

Entités principales :

- Customer ;
- Account ;
- Payment ;
- Payment Party ;
- Payment Status History ;
- Fraud Decision ;
- Clearing Submission ;
- Clearing Result ;
- Reconciliation Item.

## 18. Exemple MayaBank — physical

Implémentation pédagogique possible :

```text
PAYMENT_DB
  PAYMENT
  PAYMENT_STATUS_HISTORY
  CLEARING_SUBMISSION
  CLEARING_RESULT
```

Les détails exacts restent hors du scope enterprise si non nécessaires.

## 19. Modeling quality gates

Avant publication :

- chaque modèle a un scope ;
- niveau conceptual/logical/physical explicite ;
- entities nommées avec langage métier ;
- relations documentées ;
- cardinalités plausibles ;
- ownership connu ;
- liens inter-level disponibles ;
- aucune duplication non expliquée ;
- modèle current ou target identifié.

## 20. Anti-patterns

- conceptual model contenant des tables ;
- physical model présenté comme vérité métier ;
- reverse engineering publié sans nettoyage ;
- modèle de 500 entités sur une seule vue ;
- API DTO = enterprise information model ;
- absence de version ou de status ;
- modèle logique sans business terms ;
- schéma Kafka sans owner.
