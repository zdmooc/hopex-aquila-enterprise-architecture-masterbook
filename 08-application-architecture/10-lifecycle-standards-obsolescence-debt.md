# 10 — Lifecycle, standards, obsolescence et dette applicative

## 1. Pourquoi le lifecycle influence l’architecture

Une application en production n’est pas automatiquement pérenne.

L’architecte doit distinguer :

```text
Business usefulness
Technical health
Lifecycle state
Technology support
Target direction
```

La décision portefeuille complète sera traitée en Partie XIII ; ici on analyse l’effet du lifecycle sur le design et les dépendances.

## 2. Lifecycle pédagogique

```text
Idea
→ Planned
→ Build
→ Production
→ Restricted Change
→ Sunset
→ Retired
```

Les statuts réels dépendent du métamodèle et de la gouvernance client.

## 3. Application lifecycle vs technology lifecycle

```text
Application
Payment Orchestrator
Lifecycle = Production

Technology
Java 17
Lifecycle = supported / target depending policy
```

Une application peut être fonctionnellement stratégique tout en utilisant une technologie à risque.

## 4. Software product lifecycle

Pour les progiciels :

- vendor support date ;
- version support ;
- security patch policy ;
- upgrade path ;
- compatibility ;
- licensing.

Le risque technologique doit être propagé vers les applications qui utilisent le produit.

## 5. Technology catalog integration

Le Store HOPEX publie un module d’intégration IT-Pedia pour Aquila, destiné au suivi d’obsolescence technologique et à la mise à jour d’un catalogue de technologies.

Fait produit vérifié : l’intégration permet notamment l’import/alignment/update de technologies et l’analyse d’impact sur les indicateurs d’obsolescence.

Cela ne signifie pas que toutes les entreprises disposent de cet add-on ou d’un abonnement IT-Pedia.

## 6. Standard vs exception

Exemple de politique interne :

```text
Strategic
Tolerated
Restricted
Prohibited
```

Une technologie peut rester en production sous dérogation.

Documenter :

- exception owner ;
- reason ;
- expiry ;
- remediation plan.

## 7. Technical debt

La dette applicative peut provenir de :

- unsupported runtime ;
- point-to-point integrations ;
- shared database ;
- manual deployment ;
- missing tests ;
- weak observability ;
- vendor lock-in ;
- obsolete framework ;
- unmaintained interface ;
- excessive coupling ;
- unsupported operating system.

## 8. Architecture debt vs code debt

Code debt :

```text
local implementation quality
```

Architecture debt :

```text
systemic coupling
shared database
obsolete integration pattern
missing ownership
single failure domain
```

Le repository d’EA est particulièrement utile pour la dette transverse.

## 9. Debt item structure

Exemple :

```text
Debt
Direct database dependency from Notification Legacy to Payment DB

Impact
schema coupling + security + migration blocker

Affected applications
Notification Legacy
Payment Orchestrator

Target
Payment Status API/Event

Initiative
Notification Modernization
```

## 10. Obsolescence impact

Navigation :

```text
Technology at risk
→ applications using technology
→ processes/business services
→ criticality
→ modernization initiatives
```

## 11. Unsupported dependency

Une application moderne peut dépendre d’un composant non supporté.

Exemple :

```text
New API
→ Legacy MQ adapter
→ unsupported library
```

La modernisation de façade ne supprime pas forcément le risque.

## 12. End-of-life application

Une application `Sunset` doit avoir :

- target replacement ;
- consumers known ;
- data disposition ;
- retirement milestone ;
- freeze/change policy ;
- operational support until exit.

## 13. Restricted change

Pour réduire risque de divergence pendant migration :

```text
Legacy application
status = restricted change
```

seules corrections obligatoires sont acceptées ; les nouvelles fonctions vont dans la cible.

Cette politique est une bonne pratique, pas une fonctionnalité HOPEX imposée.

## 14. Technical standards traceability

Exemple :

```text
Standard
External APIs must use OAuth2/OIDC policy

Applies to
Payment APIs
Customer APIs

Applications
API Management
Payment Orchestrator
Digital Channel
```

## 15. Exception governance

Une dérogation sans date de fin devient un standard de fait.

Minimum :

- owner ;
- scope ;
- reason ;
- risk ;
- expiry ;
- mitigation ;
- target remediation.

## 16. Modernization drivers

Drivers possibles :

- vendor end-of-support ;
- capacity ;
- security ;
- cloud strategy ;
- business agility ;
- merger ;
- cost ;
- resilience ;
- regulatory requirement.

Ne pas moderniser uniquement pour suivre une mode technologique.

## 17. Technology risk matrix

| Technology issue | Applications | Architecture impact |
|---|---|---|
| unsupported Java | Payment Legacy | security/support risk |
| obsolete MQ client | Clearing Adapter | integration risk |
| end-of-life database | Reconciliation Legacy | data/recovery risk |
| proprietary UI framework | Back Office Legacy | maintainability risk |

Exemples pédagogiques.

## 18. Debt prioritization

Critères possibles :

```text
Business criticality
Failure probability
Security exposure
Change blocker
Cost of delay
Remediation complexity
Dependency blast radius
```

La méthode de scoring sera traitée plus en détail dans le portefeuille.

## 19. Current vs target standard

Exemple :

```text
Current
SOAP + shared DB + batch

Target
governed APIs + events + owned data
```

Le target ne doit pas supprimer les contraintes de coexistence.

## 20. Coexistence

Pendant plusieurs années, une entreprise peut avoir :

- APIs modernes ;
- ESB ;
- MQ ;
- files ;
- mainframe ;
- SaaS ;
- Kubernetes.

Une bonne architecture documente cette réalité et la trajectoire, pas seulement la cible idéale.

## 21. Decommission readiness

Avant `Retired` :

1. no active consumers ;
2. data archived/migrated ;
3. batch/jobs stopped ;
4. access removed ;
5. monitoring removed ;
6. licenses/contracts updated ;
7. documentation updated ;
8. CMDB/deployment objects reconciled ;
9. business owner sign-off ;
10. evidence retained if required.

## 22. MayaBank scenario

Legacy :

```text
Payment Legacy Hub
- SOAP interfaces
- shared Oracle schema
- batch reconciliation
- VM deployment
```

Target :

```text
Payment Orchestrator
- REST APIs
- event-driven status
- owned state store
- OpenShift deployment
```

Migration : coexistence avec adapters et strangler steps.

## 23. Anti-patterns

- application production = application stratégique ;
- technology EOL = retrait immédiat sans impact analysis ;
- dérogation permanente ;
- dette sans owner ;
- score de dette sans preuve ;
- modernisation uniquement par rehosting ;
- masquer les composants legacy derrière une API ;
- retirer l’objet du repository avant retrait réel.

## 24. Livrables

- Application Lifecycle Map ;
- Application × Technology Lifecycle Matrix ;
- Obsolescence Impact View ;
- Architecture Debt Register ;
- Standards/Exceptions Register ;
- Sunset Application Exit Checklist ;
- Current/Target Technology Alignment View.

## 25. Frontière avec la Partie XIII

Cette partie identifie lifecycle, dette et obsolescence comme **contraintes d’architecture**.

La Partie XIII approfondira :

- business value ;
- technical fitness ;
- costs ;
- portfolio segmentation ;
- rationalization ;
- investment decisions ;
- application portfolio governance.
