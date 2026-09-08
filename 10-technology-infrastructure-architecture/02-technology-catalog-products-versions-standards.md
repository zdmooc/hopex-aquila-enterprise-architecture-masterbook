# 02 — Technology Catalog, produits, versions et standards

## 1. Pourquoi un catalogue technologique

Un Technology Catalog fiable permet de répondre :

```text
Quelles technologies utilisons-nous ?
Dans quelles versions ?
Pour quelles plateformes et applications ?
Avec quel statut de standard ?
Avec quel cycle de support ?
Quels changements ont le plus grand blast radius ?
```

## 2. Niveaux à distinguer

```text
Technology family
Container Platform

Technology product
Red Hat OpenShift

Version / release family
4.x

Managed platform
MayaBank OpenShift Platform

Deployment instance
OCP-PROD-EU
```

Ne pas fusionner ces niveaux dans un seul objet nommé `OpenShift`.

## 3. Technology ID Card

| Champ | Exemple MayaBank |
|---|---|
| Canonical Name | Red Hat OpenShift |
| Family | Container Platform |
| Vendor | Red Hat |
| Standard Status | Preferred |
| Lifecycle | Supported |
| Owner | Platform Engineering |
| Consumers | Payments, Fraud, API |
| Criticality | High |
| Target Direction | Strategic |
| Evidence Date | 2026-09 |

## 4. Statuts de standard

Taxonomie pédagogique :

```text
Preferred
Allowed
Tolerated
Deprecated
Prohibited
Under Assessment
```

Les statuts réels doivent être alignés sur la gouvernance client.

## 5. Technology Standard vs Technology Product

Un produit décrit **ce qui est utilisé**.

Un standard décrit **ce qui est recommandé ou autorisé**.

Exemple :

```text
Product: Java 17
Standard: Preferred Java runtime for new backend services
```

## 6. Versions

Ne pas créer un objet entreprise pour chaque patch si cela n’aide aucune décision.

Granularité possible :

- major version pour portefeuille ;
- minor version si support/security significatif ;
- patch exact dans CMDB/asset tooling.

## 7. Lifecycle evidence

Pour chaque technologie critique :

```text
Support start
Mainstream support end
Extended support end
Internal deprecation date
Exception expiry
Evidence source
Evidence date
```

Ne jamais conserver un statut lifecycle sans source et sans date.

## 8. Application × Technology

| Application | Platform/Technology |
|---|---|
| Payment Orchestrator | OpenShift / Java |
| Fraud Decision Service | OpenShift / Java |
| Event Streaming | Kafka |
| Core Account Service | Oracle / Java |
| Reconciliation | PostgreSQL / Kafka |

Cette matrice permet d’identifier le blast radius d’une obsolescence.

## 9. Platform × Product

```text
MayaBank OpenShift Platform
├─ OpenShift
├─ RHCOS
├─ Ingress / Load Balancing
├─ Storage classes
├─ Observability agents
└─ Identity integration
```

Les détails exacts doivent suivre l’environnement réel.

## 10. Approved patterns

Le standard peut aussi porter sur une combinaison :

```text
Backend service
→ Java
→ container image
→ OpenShift
→ API Management
→ centralized observability
```

Un pattern n’est pas un produit.

## 11. Exception management

Une dérogation doit préciser :

- scope ;
- justification ;
- risk owner ;
- mitigation ;
- expiry date ;
- target remediation.

## 12. Obsolescence analysis

Chaîne :

```text
Technology version
→ managed platforms
→ applications
→ processes/capabilities
→ business services
```

## 13. Technology debt

Exemples :

- version hors support ;
- vendor lock-in non maîtrisé ;
- absence d’automatisation ;
- plateforme sans DR ;
- protocole ancien ;
- OS non standard ;
- dépendance unique non remplaçable.

## 14. MayaBank — catalogue de référence

```text
Container: OpenShift
Runtime: Java
Streaming: Kafka
API: API Management
Relational DB: PostgreSQL / Oracle
Identity: OIDC/SAML-capable IAM
Observability: metrics/logs/traces platform
Automation: GitOps / CI/CD
Backup: enterprise backup service
```

Les produits exacts non vérifiés restent des choix pédagogiques et non des faits HOPEX.

## 15. Quality gates

Refuser un objet technologique si :

- nom ambigu ;
- family absente ;
- owner inconnu ;
- version sans usage ;
- lifecycle sans evidence date ;
- statut standard non gouverné ;
- aucune relation avec plateforme/application.

## 16. Anti-patterns

- catalogue = liste de vendors ;
- `Java` dupliqué 50 fois ;
- environnement créé comme version ;
- lifecycle copié sans source ;
- produit = standard ;
- toutes les dépendances techniques au même niveau.

## 17. Questions d’entretien

**Pourquoi une evidence date ?**  
Parce que les cycles de support changent ; une information non datée devient rapidement trompeuse.

**Preferred et Supported sont-ils synonymes ?**  
Non. Une technologie peut encore être supportée mais ne plus être préférée pour de nouveaux développements.
