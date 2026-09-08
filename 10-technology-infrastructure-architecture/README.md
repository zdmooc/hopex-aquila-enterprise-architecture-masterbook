# Partie X — Technology & Infrastructure Architecture

Cette partie approfondit la **Technology & Infrastructure Architecture** dans Bizzdesign Hopex / HOPEX Aquila : technologies, produits, versions, standards, plateformes, compute, OpenShift, cloud, réseau, stockage, HA/DR, sécurité, observabilité, lifecycle et architectures current/transition/target.

Elle complète les parties précédentes sans les répéter :

```text
Partie IV
HOPEX IT Architecture transverse

Partie VIII
Application Architecture détaillée

Partie IX
Information & Data Architecture détaillée

Partie X
Technology & Infrastructure Architecture détaillée

Parties XIII–XIV
Portfolio, coûts, rationalisation et transformation roadmaps
```

Le fil rouge reste **MayaBank**.

---

# Objectifs

À la fin de cette partie, vous devez savoir :

- construire un Technology Catalog canonique ;
- distinguer technology family, product, version, platform et instance ;
- gouverner Preferred / Allowed / Deprecated et les exceptions ;
- relier technologies ↔ plateformes ↔ applications ↔ métier ;
- analyser le lifecycle et l’obsolescence ;
- comprendre le rôle d’IT-Pedia dans HOPEX ;
- construire une Platform Service Card ;
- modéliser OpenShift sans transformer HOPEX en console Kubernetes ;
- distinguer control plane, worker, namespace et workload ;
- raisonner requests/limits/capacity ;
- analyser les failure domains ;
- modéliser réseau, zones, load balancing, DNS et connectivité hybride ;
- distinguer block/file/object storage ;
- distinguer backup, snapshot et réplication ;
- construire un modèle HA/DR ;
- définir RTO/RPO ;
- analyser active/active vs active/passive ;
- modéliser identity, secrets, PKI et trust boundaries ;
- construire metrics/logs/traces et SLI/SLO ;
- gérer capacity et operational readiness ;
- construire current / transition / target ;
- intégrer GreenOps/FinOps sans sacrifier la résilience ;
- défendre une architecture infrastructure en Architecture Board.

---

# Chapitres

## 01 — Rôle, périmètre et méthode

[Ouvrir](01-technology-infrastructure-role-scope-method.md)

Couvre :

- rôle de la Technology Architecture ;
- frontières avec Application/Data/Portfolio ;
- Technology vs Application ;
- Technology vs Platform vs Instance ;
- niveaux L0/L1/L2/L3 ;
- méthode en 12 étapes ;
- baseline MayaBank.

## 02 — Technology Catalog, produits, versions et standards

[Ouvrir](02-technology-catalog-products-versions-standards.md)

Couvre :

- family/product/version/platform ;
- Technology ID Card ;
- standard status ;
- lifecycle evidence ;
- Application × Technology ;
- Platform × Product ;
- exceptions ;
- obsolescence ;
- debt.

## 03 — Platform Services & Runtime Foundations

[Ouvrir](03-platform-services-runtime-foundations.md)

Couvre :

- platform as a service ;
- Platform Service Card ;
- shared platform risk ;
- runtime foundation ;
- environments ;
- tenancy ;
- control plane/workload plane ;
- dependencies ;
- onboarding ;
- retirement.

## 04 — Compute, containers, OpenShift et cloud

[Ouvrir](04-compute-container-openshift-cloud.md)

Couvre :

- bare metal/VM/container ;
- OpenShift architecture conceptuelle ;
- namespaces ;
- worker pools ;
- requests/limits ;
- scaling ;
- stateful workloads ;
- failure domains ;
- cloud/hybrid ;
- landing zones.

## 05 — Network, connectivity, zones & load balancing

[Ouvrir](05-network-connectivity-zones-load-balancing.md)

Couvre :

- zones de confiance ;
- north-south/east-west ;
- load balancing ;
- DNS ;
- firewall boundaries ;
- API gateway ;
- service mesh ;
- hybrid connectivity ;
- partner connectivity ;
- latency budget ;
- multi-site routing.

## 06 — Storage, backup, replication & data services

[Ouvrir](06-storage-backup-replication-data-services.md)

Couvre :

- block/file/object ;
- persistent volumes ;
- storage classes ;
- backup ≠ replication ;
- snapshot ≠ backup ;
- RPO ;
- restore testing ;
- database HA ;
- storage failure domains ;
- encryption ;
- capacity.

## 07 — High Availability, Disaster Recovery & Resilience

[Ouvrir](07-high-availability-disaster-recovery-resilience.md)

Couvre :

- HA vs resilience vs DR ;
- RTO/RPO ;
- failure scenario catalog ;
- active/active ;
- active/passive ;
- application/infrastructure resilience ;
- dependency-aware DR ;
- failover/failback ;
- recovery testing ;
- evidence.

## 08 — Security Architecture, Identity, Secrets & Trust Boundaries

[Ouvrir](08-security-identity-secrets-trust-boundaries.md)

Couvre :

- human/service/machine identity ;
- authentication vs authorization ;
- federation ;
- service identity ;
- secrets ;
- certificates ;
- trust boundaries ;
- network/platform security ;
- supply-chain security ;
- encryption ;
- privileged access.

## 09 — Observability, Operations, SRE & Capacity

[Ouvrir](09-observability-operations-sre-capacity.md)

Couvre :

- metrics/logs/traces ;
- monitoring vs observability ;
- correlation ;
- golden signals ;
- SLI/SLO/SLA ;
- error budget ;
- alerting ;
- incident flow ;
- capacity ;
- headroom ;
- performance testing ;
- operational readiness.

## 10 — Technology Lifecycle, Obsolescence, Standards & Debt

[Ouvrir](10-technology-lifecycle-obsolescence-standards-debt.md)

Couvre :

- vendor vs internal lifecycle ;
- evidence ;
- IT-Pedia ;
- health dimensions ;
- debt item ;
- obsolescence propagation ;
- standards ;
- exception management ;
- Technology Radar ;
- skills/license risks.

## 11 — Current, Transition & Target Infrastructure

[Ouvrir](11-current-transition-target-infrastructure.md)

Couvre :

- current baseline ;
- target drivers ;
- rehost/replatform/refactor/replace/retire ;
- coexistence ;
- dependency sequencing ;
- data gravity ;
- dual-run ;
- cutover ;
- decommission ;
- MayaBank migration waves.

## 12 — MayaBank Technology & Infrastructure Reference Model

[Ouvrir](12-mayabank-technology-infrastructure-reference-model.md)

Contient :

- 9 technology domains ;
- 8 platform services ;
- Application × Platform ;
- Platform × Technology ;
- logical deployment ;
- network zones ;
- OpenShift model ;
- failure domains ;
- critical path ;
- NFR ;
- storage ;
- HA/DR ;
- security ;
- observability ;
- lifecycle ;
- current/target ;
- transition waves ;
- 12 matrices ;
- 12 vues.

## 13 — Gouvernance, GreenOps, anti-patterns & mission playbook

[Ouvrir](13-governance-greenops-antipatterns-mission-playbook.md)

Couvre :

- architecture roles ;
- governance lifecycle ;
- quality gates ;
- Architecture Board ;
- GreenOps ;
- capacity efficiency ;
- carbon awareness ;
- cost awareness ;
- anti-patterns ;
- mission 4 semaines ;
- interview cases ;
- maturity model.

---

# Pratique

## 90 — 24 labs + 40 questions corrigées

[Ouvrir](90-labs-and-review.md)

Labs :

1. Technology Catalog.
2. Product vs Platform.
3. Application × Platform.
4. Platform × Technology.
5. Technology Standards.
6. IT-Pedia Impact Scenario.
7. OpenShift Logical Architecture.
8. Namespace Governance.
9. Capacity Model.
10. Network Zones.
11. Load Balancer SPOF.
12. Hybrid Connectivity.
13. Storage Architecture.
14. Backup vs Replication.
15. RTO/RPO Matrix.
16. Failure Domain Analysis.
17. DR Dependency Order.
18. Security Trust Boundaries.
19. Certificate Expiry Scenario.
20. Observability Architecture.
21. Capacity Under Failure.
22. Technology Obsolescence.
23. Current/Transition/Target.
24. Architecture Board.

Puis **40 questions corrigées**.

---

# Sources

## 99 — Sources officielles et frontière de vérification

[Ouvrir](99-official-sources.md)

Sources principales :

- Bizzdesign Hopex ;
- HOPEX Core Back-End Aquila 6.2 / 62.18.x ;
- IT-Pedia integration ;
- ITPM Excel Import Template ;
- Bizzdesign Support ;
- Bizzdesign Hopex SLA ;
- Red Hat OpenShift official architecture docs ;
- Kubernetes official architecture docs.

Les faits produit sont séparés des pratiques d’architecture et du cas MayaBank.

---

# Cas MayaBank — Current

```text
VM-heavy infrastructure
Legacy middleware
Point-to-point network flows
Shared storage dependencies
Fragmented monitoring
Manual provisioning
Partial DR
Technology obsolescence
```

# Target

```text
Governed platform services
OpenShift for suitable workloads
API Management
Kafka/Event Streaming
Resilient data services
Segmented network zones
Central IAM / secrets / PKI
Metrics + logs + traces
IaC / GitOps
Tested DR
Technology lifecycle governance
GreenOps / capacity efficiency
```

---

# Règles à retenir

```text
Technology ≠ Application
Product ≠ Platform
Version ≠ Environment
Namespace ≠ Application
Replica count ≠ HA proof
Replication ≠ Backup
Snapshot ≠ Backup automatically
Multi-site ≠ DR proof
RTO/RPO ≠ technical guess
Supported ≠ Preferred
CMDB ≠ Enterprise Architecture Repository
Monitoring ≠ Observability
Target ≠ Migration Plan
```

---

# Chiffres de la Partie X

- 13 chapitres complets ;
- 1 README de synthèse ;
- 1 modèle Technology & Infrastructure MayaBank ;
- 9 technology domains ;
- 8 platform services de référence ;
- 12 matrices ;
- 12 vues ;
- 24 labs ;
- 40 questions corrigées ;
- sources actuelles séparées des recommandations ;
- frontière explicite avec CMDB/runtime tooling.

---

# Partie suivante

**Partie XI — Relationships, Diagrams, Matrices & Views**

Elle approfondira :

- relations du repository ;
- direction et sémantique ;
- relation quality ;
- diagrams ;
- matrices ;
- filters ;
- viewpoints ;
- current/target overlays ;
- impact views ;
- heatmaps ;
- visual conventions ;
- enterprise communication patterns.
