# 03 — Platform Services & Runtime Foundations

## 1. Platform as a governed service

Une plateforme est un ensemble exploité qui fournit un service technique réutilisable aux applications.

Exemples MayaBank :

```text
OpenShift Platform
Event Streaming Platform
API Management Platform
Database Platform
IAM Platform
Observability Platform
Backup & Recovery Platform
```

## 2. Platform vs product

```text
Platform
MayaBank Event Streaming Platform

built with
Kafka
Schema Registry
Connect / integration components
Observability
Security controls
```

Le produit ne suffit pas à décrire le service réellement consommé.

## 3. Platform Service Card

```text
Name
Purpose
Service owner
Supported consumers
Environments
Criticality
Availability target
RTO/RPO
Technology products
Security zone
Operational model
Capacity model
Lifecycle
Cost allocation principle
```

## 4. Shared platform risks

Une plateforme mutualisée concentre des bénéfices et des risques :

- standardisation ;
- économies d’échelle ;
- automation ;
- observabilité cohérente ;
- mais blast radius plus élevé ;
- risque de saturation ;
- dépendance à une équipe centrale ;
- dépendance vendor/product.

## 5. Runtime foundation

Pour un service applicatif moderne :

```text
Source code
→ build pipeline
→ artifact/image registry
→ runtime platform
→ network ingress/egress
→ secrets/identity
→ storage
→ observability
```

L’architecture de plateforme doit expliciter ces dépendances structurantes.

## 6. Environment model

```text
DEV
INT
UAT
PREPROD
PROD
DR
```

Les environnements ne sont pas des applications différentes.

## 7. Platform tenancy

Décisions :

- cluster partagé ou dédié ;
- tenant/namespace par domaine ;
- quotas ;
- isolation réseau ;
- séparation prod/non-prod ;
- isolation réglementaire ;
- blast radius accepté.

## 8. Control plane vs workload plane

Pour une plateforme orchestrée, distinguer :

```text
Control plane
→ gouverne le runtime

Workload plane
→ exécute les applications
```

Ne pas réduire la plateforme aux seuls workers.

## 9. Platform dependencies

Exemple OpenShift :

```text
DNS
Load Balancing
Identity
Network connectivity
Storage
Registry
Time synchronization
PKI/certificates
Observability
Backup
```

Une dépendance invisible peut devenir le vrai SPOF.

## 10. Service consumption

Une application consomme une plateforme via un contrat :

- runtime support ;
- quotas/capacity ;
- ingress ;
- storage classes ;
- secrets ;
- logging/metrics ;
- backup requirements ;
- SLOs.

## 11. Platform SLOs

Exemples :

```text
availability
API/control-plane availability
workload scheduling availability
storage availability
recovery objective
incident response
```

Les valeurs sont à définir par service réel.

## 12. Platform onboarding

Checklist :

1. owner applicatif connu ;
2. classification des données ;
3. NFR ;
4. resource profile ;
5. network flows ;
6. secrets/identity ;
7. persistent state ;
8. backup ;
9. observability ;
10. support model.

## 13. Platform retirement

Une plateforme ne peut être retirée que lorsque :

```text
Consumers = 0
Critical data migrated
Interfaces removed
Support procedures retired
Security rules cleaned
Contracts closed
```

## 14. MayaBank target platforms

```text
OpenShift Platform
API Management Platform
Kafka/Event Streaming Platform
Managed DB Services
IAM
Observability
Backup/Recovery
GitOps/Automation
```

## 15. Quality gates

- platform owner défini ;
- technology products liés ;
- consumers identifiés ;
- SLOs/RTO/RPO documentés ;
- failure domains connus ;
- lifecycle gouverné ;
- dépendances critiques visibles.

## 16. Anti-patterns

- plateforme = nom du produit uniquement ;
- aucune distinction prod/non-prod ;
- onboarding sans NFR ;
- plateforme partagée sans analyse de blast radius ;
- capacité supposée infinie ;
- DR non testé mais déclaré.
