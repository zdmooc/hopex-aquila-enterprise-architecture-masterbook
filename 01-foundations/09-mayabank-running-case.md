# 09 — MayaBank, cas fil rouge

## 1. Pourquoi MayaBank

MayaBank permet d'apprendre HOPEX avec un domaine réaliste mais fictif : banque, paiements, API, événements, OpenShift, data, résilience et transformation.

Le but est d'éviter des exemples abstraits du type `Application A → Server B`.

## 2. Contexte entreprise

MayaBank possède :

- canaux mobile/web ;
- paiements instantanés ;
- paiements traditionnels ;
- moteur de fraude ;
- gestion des limites ;
- ledger/core banking ;
- clearing adapters ;
- event streaming ;
- plateformes OpenShift ;
- bases relationnelles ;
- IAM ;
- observabilité ;
- deux sites principaux ;
- applications legacy à retirer.

## 3. Drivers

- demande client temps réel ;
- résilience 24x7 ;
- réduction du time-to-market ;
- réduction du couplage legacy ;
- traçabilité end-to-end ;
- sécurité et conformité ;
- rationalisation applicative ;
- réduction de l'empreinte infrastructure.

## 4. Capabilities initiales

```text
Real-Time Payment Processing
Fraud Detection
Payment Authorization
Settlement & Reconciliation
Customer Notification
Payment Observability
Identity & Access Management
Platform Engineering
```

Ces noms sont pédagogiques. Leur implémentation dans HOPEX dépendra du métamodèle réel étudié en Partie II.

## 5. Business processes

```text
Initiate Payment
Validate Payment
Perform Fraud Check
Check Limits
Execute Payment
Settle Payment
Notify Customer
Reconcile Status
Handle Exception
```

## 6. Applications

```text
MB-APP-001 Payment API Gateway
MB-APP-002 Payment Orchestrator
MB-APP-003 Fraud Engine
MB-APP-004 Limit Management
MB-APP-005 Ledger Adapter
MB-APP-006 Clearing Adapter
MB-APP-007 Notification Service
MB-APP-008 Payment Status Service
MB-APP-009 Legacy Payment Hub
```

## 7. Technology

```text
OpenShift Platform
Kafka Event Streaming
Relational Database Platform
IAM/OIDC Platform
Secrets Platform
Observability Platform
GitOps Platform
API Management Platform
```

## 8. Information

```text
Payment Order
Payment Transaction
Payment Status
Fraud Score
Customer Account
Clearing Instruction
Settlement Result
Notification
```

## 9. Organizations

```text
Payments Business
Payments IT
Platform Engineering
Cybersecurity
Fraud Operations
Enterprise Architecture
Data Office
Operations / SRE
```

## 10. Transformation

Baseline :

```text
Legacy Payment Hub
+ point-to-point integration
+ manual deployment
+ fragmented monitoring
```

Transition :

```text
API Gateway
+ Payment Orchestrator
+ Kafka
+ hybrid coexistence
```

Target :

```text
modular payment architecture
+ governed APIs/events
+ OpenShift runtime
+ observability
+ controlled decommissioning
```

## 11. Questions auxquelles HOPEX devra répondre

### Portfolio
- quelles applications sont stratégiques ?
- lesquelles sont en sunset ?
- lesquelles sont redondantes ?

### Impact
- que se passe-t-il si Kafka est indisponible ?
- quels processus dépendent du Fraud Engine ?
- quelles applications utilisent une technologie obsolète ?

### Transformation
- quels projets retirent le Legacy Payment Hub ?
- quels gaps restent ouverts ?
- quels états de transition existent ?

### Governance
- quel owner est responsable de chaque application ?
- quelles fiches n'ont pas été revues ?
- quelles relations proviennent de ServiceNow ?

## 12. Identité canonique

Convention pédagogique :

```text
MB-CAP-xxx capabilities
MB-PROC-xxx processes
MB-APP-xxx applications
MB-INF-xxx information
MB-TEC-xxx technologies
MB-ORG-xxx organizations
MB-TRF-xxx transformation
```

Les IDs facilitent les labs Git/CSV mais ne prétendent pas remplacer les identifiants natifs HOPEX.

## 13. Source mapping

| Donnée | Source proposée |
|---|---|
| capability | EA / business architecture |
| business owner | organisation / EA |
| application logical record | HOPEX |
| CI runtime | ServiceNow |
| technology standard | architecture/platform governance |
| lifecycle decision | portfolio authority |
| risk/control | IRM/GRC |
| review date | HOPEX governance |

## 14. Views futures

Nous construirons progressivement :

1. Capability map ;
2. Business Process/Application map ;
3. Application cooperation/dependencies ;
4. API & Event map ;
5. Technology standards map ;
6. OpenShift deployment landscape ;
7. Application portfolio heatmap ;
8. Obsolescence view ;
9. Risk impact view ;
10. Transformation roadmap ;
11. ServiceNow reconciliation view ;
12. Executive transformation dashboard.

## 15. Règle du fil rouge

Chaque nouvelle partie devra enrichir **les mêmes objets MayaBank**, au lieu de recréer un exemple indépendant. À terme, la Partie XXI consolidera le modèle d'entreprise complet.
