# 06 — Business Services, Products & Offerings

## 1. Pourquoi distinguer service et produit

Un **business service** représente une valeur ou capacité exposée à un consommateur interne ou externe. Un **product/offer** assemble généralement plusieurs services, règles, conditions et engagements dans une proposition identifiable.

Exemple MayaBank :

```text
Product
Instant Payment Offering

Business Services
Instant Payment Service
Payment Status Service
Payment Exception Service
```

## 2. Service vs Capability

```text
Capability = aptitude interne
Service    = valeur exposée
```

Exemple :

```text
Capability: Payment Orchestration
Service   : Instant Payment Service
```

Une même capability peut soutenir plusieurs services.

## 3. Service vs Process

Le process réalise ou contribue au service.

```text
Business Service
Instant Payment Service
       ↑
Business Process
Execute Instant Payment
```

Le service reste stable même si le process est amélioré.

## 4. Service consumer

Toujours expliciter le consommateur :

- customer ;
- merchant ;
- partner ;
- internal operations ;
- another business unit ;
- regulator.

Sans consommateur, le service devient un simple libellé abstrait.

## 5. Service catalog

Un catalogue utile porte :

- name ;
- description ;
- owner ;
- consumers ;
- channels ;
- capabilities ;
- supporting processes ;
- supporting applications ;
- SLA/SLO métier ;
- lifecycle ;
- regulatory constraints.

## 6. Products / offerings

Exemple MayaBank :

```text
Instant Payment Offering
├─ Instant Payment Service
├─ Beneficiary Verification Service
├─ Payment Status Service
└─ Notification Service
```

Le produit peut aussi contenir des conditions : pricing, eligibility, geographies, channels.

## 7. Product × Capability

Permet d'identifier les capabilities nécessaires à l'offre.

```text
Instant Payment Offering
→ Payment Initiation
→ Payment Orchestration
→ Fraud Decisioning
→ Customer Notification
→ Payment Operations
```

## 8. Product × Application

Ne pas lier directement sans contexte si la chaîne métier est disponible.

Préférer :

```text
Product
→ Business Service
→ Process/Capability
→ Application
```

Cette trace est plus explicable lors d'un impact analysis.

## 9. SLA / SLO métier

Exemples :

```text
Availability 24x7
P95 confirmation < 5 sec
Customer notification < 10 sec
Exception acknowledgement < 2 min
```

La cible technique se déduit ensuite de ces attentes.

## 10. Business service lifecycle

Un service possède potentiellement :

```text
Idea → Planned → Active → Restricted → Retired
```

Le lifecycle exact dépend des conventions du client.

Lors d'un retrait de service, analyser :

- products using it ;
- processes realizing it ;
- customer journeys ;
- applications ;
- contracts ;
- regulatory obligations.

## 11. Internal business services

Tous les services ne sont pas externes.

Exemples :

```text
Fraud Decision Service
Payment Investigation Service
Customer Identity Verification Service
```

Ils peuvent être consommés par d'autres domaines métiers.

## 12. Service ownership

Séparer :

```text
Business Service Owner
Application Owner
Process Owner
Capability Owner
```

L'absence de cette distinction crée des responsabilités ambiguës.

## 13. MayaBank example

```text
Retail Customer
   consumes
Instant Payment Service
   supported by
Payment Orchestration capability
   realized through
Execute Instant Payment process
   supported by
Payment Orchestrator
```

## 14. Anti-patterns

- un business service par API ;
- un product par application ;
- services sans consumers ;
- services sans owner ;
- service catalog jamais relié aux capabilities ;
- SLA techniques utilisés comme seule définition métier ;
- product et business service utilisés comme synonymes.

## 15. Entretien

**Pourquoi modéliser les business services ?**  
Pour relier ce que l'entreprise délivre réellement aux capabilities, processus et systèmes nécessaires.

**Quel bénéfice pour l'impact analysis ?**  
On peut partir d'une application affectée et remonter jusqu'aux services et produits clients touchés.