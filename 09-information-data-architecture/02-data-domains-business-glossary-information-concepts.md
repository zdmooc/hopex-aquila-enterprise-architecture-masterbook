# 02 — Data Domains, Business Glossary et Information Concepts

## 1. Data Domain

Un Data Domain regroupe un ensemble cohérent d’informations sous une responsabilité de gouvernance commune.

Exemples MayaBank :

```text
Customer
Account
Payment
Fraud & Financial Crime
Product
Reference Data
Finance
Risk
Operations
```

Un domaine ne doit pas être créé parce qu’une application existe. Il représente une cohérence métier durable.

## 2. Domain vs Application

```text
Payment Domain
≠ Payment Orchestrator

Customer Domain
≠ CRM

Fraud Domain
≠ Fraud Decision Service
```

Une application peut consommer plusieurs domaines. Un domaine peut être distribué sur plusieurs applications.

## 3. Business Glossary

Le glossary crée un vocabulaire partagé.

Un terme de qualité doit au minimum contenir :

```text
Preferred term
Definition
Business owner
Data steward
Domain
Aliases
Status
Examples
Related concepts
Rules / constraints
Source
```

## 4. Exemple — Payment Instruction

```text
Preferred term : Payment Instruction
Domain         : Payment
Definition     : demande structurée autorisant l’exécution d’un transfert selon un scheme donné
Owner          : Head of Payments Data
Steward        : Payments Data Steward
Aliases        : Payment Order, Instruction de paiement
Status         : Approved
```

La définition doit expliquer le concept et non copier une structure JSON.

## 5. Business Term vs Data Element

```text
Business Term
Payment Status

Logical attribute
Payment.status

Physical column
PAYMENT.STATUS_CD
```

Les trois niveaux doivent être reliés mais ne sont pas interchangeables.

## 6. Synonymes et homonymes

### Synonymes

```text
Customer ID
Client Identifier
Party ID
```

Il faut désigner un terme préféré et documenter les aliases.

### Homonymes

Le mot `Account` peut désigner :

- compte bancaire ;
- compte utilisateur IAM ;
- compte comptable.

Le glossary doit lever l’ambiguïté par domaine et définition.

## 7. Concept maps

Une Information Concept Map montre les concepts et leurs relations sans descendre au modèle physique.

Exemple :

```text
Customer
  ├─ owns → Account
  └─ initiates → Payment

Payment
  ├─ debits → Account
  ├─ produces → Payment Status
  ├─ evaluated by → Fraud Decision
  └─ settled through → Clearing Result
```

## 8. Taxonomie des données MayaBank

### Party & Customer

- Customer ;
- Party ;
- Legal Entity ;
- Contact Point ;
- Identity ;
- Consent.

### Account

- Account ;
- Balance ;
- Reservation ;
- Account Status.

### Payment

- Payment Instruction ;
- Payment ;
- Payment Status ;
- Payment Scheme ;
- Settlement Instruction ;
- Reconciliation Item.

### Fraud

- Fraud Context ;
- Fraud Score ;
- Fraud Decision ;
- Alert.

## 9. Ownership model

### Data Owner

Accountable pour le domaine ou l’information.

### Data Steward

Responsable de la qualité documentaire et de la coordination de gouvernance.

### Data Custodian

Rôle plus technique autour de la plateforme ou du stockage, selon l’organisation.

### Producer

Système ou processus qui crée la donnée.

### Consumer

Système ou processus qui l’utilise.

Ces rôles doivent être explicités plutôt que déduits du nom d’une application.

## 10. Domain boundaries

Une frontière est utile lorsqu’elle permet de répondre à :

- qui décide de la définition ?
- qui porte les règles de qualité ?
- qui accepte les changements ?
- où est le système de référence ?
- quelles équipes doivent être consultées ?

## 11. Cross-domain relationships

Exemple :

```text
Customer Domain
Customer
  ↓ initiates
Payment Domain
Payment
  ↓ evaluated by
Fraud Domain
Fraud Decision
```

Les relations cross-domain sont souvent les plus importantes pour l’architecture.

## 12. Reference Data vs Master Data

### Reference Data

Jeux de valeurs relativement stables utilisés pour classification ou validation.

Exemples :

- country codes ;
- currencies ;
- payment schemes ;
- status codes.

### Master Data

Entités métier partagées et gouvernées sur la durée.

Exemples :

- Customer ;
- Product ;
- Legal Entity.

Les définitions exactes doivent suivre le cadre de gouvernance du client.

## 13. Golden Record

Un golden record est une représentation maîtrisée d’une entité, souvent issue d’un processus de rapprochement ou MDM.

Ne pas déclarer `golden source` sans mécanisme réel de gouvernance.

## 14. Data Products

Dans une organisation data product-oriented, un Data Product peut regrouper :

```text
Data set
+ contract
+ owner
+ quality objectives
+ access policy
+ documentation
+ lifecycle
```

Le Data Product n’est pas automatiquement équivalent au Data Domain.

## 15. Quality rules du glossary

Refuser un terme si :

- définition circulaire ;
- absence de domaine ;
- owner inconnu ;
- doublon non résolu ;
- terme défini par une implémentation technique ;
- statut non gouverné ;
- acronymes non explicités.

## 16. Matrice Domain × Information

| Domain | Key information |
|---|---|
| Customer | Customer, Identity, Consent |
| Account | Account, Balance, Reservation |
| Payment | Payment Instruction, Payment Status |
| Fraud | Fraud Context, Fraud Decision |
| Reference Data | Currency, Country, Scheme |

## 17. Matrice Information × Owner

| Information | Owner | Steward |
|---|---|---|
| Customer | Customer Data Owner | Customer Steward |
| Account | Core Banking Data Owner | Account Steward |
| Payment | Payments Data Owner | Payment Steward |
| Fraud Decision | Fraud Data Owner | Fraud Steward |

## 18. Anti-patterns

- domaine = application ;
- glossary rempli de noms de colonnes ;
- owner = équipe IT par défaut ;
- 500 termes sans workflow de validation ;
- créer un terme pour chaque champ JSON ;
- plusieurs définitions concurrentes non arbitrées ;
- aucune relation entre glossary et architecture.

## 19. MayaBank target

```text
Domain
→ governed glossary
→ canonical concepts
→ owners/stewards
→ application responsibilities
→ lineage
→ quality rules
```

Le glossary devient ainsi une porte d’entrée vers l’architecture, pas un dictionnaire isolé.
