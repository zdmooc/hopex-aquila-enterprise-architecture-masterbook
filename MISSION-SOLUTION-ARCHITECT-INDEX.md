# Mission Index — Architecte Solution / Logiciel

Ce fichier permet de retrouver rapidement les parties du masterbook qui démontrent les compétences attendues dans une mission d'**Architecte Solution / Logiciel** sans détourner HOPEX de son rôle de plateforme EAM.

## 1. Cartographie SI et dépendances

- [IT Architecture — rôle et méthode](04-it-architecture/01-it-architecture-role-and-method.md)
- [Interfaces, interactions et flows](04-it-architecture/03-interfaces-interactions-flows.md)
- [Dependency & Impact Analysis](04-it-architecture/08-dependency-impact-analysis.md)
- [Application Dependency Mapping](08-application-architecture/06-dependency-mapping-impact-analysis.md)
- [Enterprise Cartography & Dependency Analysis](12-enterprise-cartography-dependency-analysis/README.md)

Compétences démontrées :
- catalogue applicatif ;
- relations provider/consumer ;
- flux synchrones/asynchrones ;
- dépendances directes/transitives ;
- critical paths ;
- blast radius ;
- SPOF candidates ;
- impact d'un changement ou d'une panne.

## 2. AS-IS / Transition / TO-BE

- [Current, Transition & Target — IT](04-it-architecture/07-current-transition-target.md)
- [Current, Transition & Target — Application](08-application-architecture/11-current-transition-target-application-architecture.md)
- [Migration / Decommission Impact Scenarios](12-enterprise-cartography-dependency-analysis/08-change-migration-decommission-impact-scenarios.md)

Compétences démontrées :
- current architecture ;
- gap analysis ;
- transition architectures ;
- coexistence legacy/cible ;
- exit criteria ;
- decommissioning ;
- dependency-aware target.

## 3. Roadmaps de transformation

- [IT Transformation Roadmaps](04-it-architecture/09-it-transformation-roadmaps.md)
- [Business Assessments, Gaps & Roadmaps](05-business-architecture/10-assessments-gaps-and-roadmaps.md)
- [Capability Scenarios, Investments & Roadmaps](06-capability-architecture/05-scenarios-investments-roadmaps.md)

Le masterbook relie les gaps aux initiatives plutôt que de produire une cible isolée.

## 4. Architecture applicative et intégration

- [Application Architecture](08-application-architecture/README.md)
- [Interfaces, Flows & Contracts](08-application-architecture/04-interactions-interfaces-flows-contracts.md)
- [Integration Architecture Patterns](08-application-architecture/05-integration-architecture-patterns.md)
- [NFR — Resilience, Security, Observability](08-application-architecture/08-non-functional-architecture-resilience-security-observability.md)

Patterns couverts :
- API ;
- event-driven ;
- MQ/queue ;
- ESB/mediation ;
- batch/file ;
- orchestration/choreography ;
- adapters ;
- eventual consistency ;
- resilience and observability.

## 5. API Management dans le référentiel d'architecture

Le masterbook maintient la frontière suivante :

```text
HOPEX
  logical service/interface
  provider/consumer
  owner
  lifecycle
  dependency
  business/process traceability

API Management platform
  OpenAPI
  gateway policies
  quotas/keys
  runtime analytics
  developer portal
```

Voir [Interfaces, Interactions & Application Flows](04-it-architecture/03-interfaces-interactions-flows.md).

La profondeur API Management exécutable/référence est maintenue dans le dépôt séparé `zdmooc/mayabank-api-management-architecture`.

## 6. IAM / Security / Cloud / OpenShift

- [Technology & Infrastructure Architecture](10-technology-infrastructure-architecture/README.md)
- [Security, Identity, Secrets & Trust Boundaries](10-technology-infrastructure-architecture/08-security-identity-secrets-trust-boundaries.md)
- [Compute, Containers, OpenShift & Cloud](10-technology-infrastructure-architecture/04-compute-container-openshift-cloud.md)

Les dépôts spécialistes restent :
- `zdmooc/iam-etat-de-lart-2026` — architecture IAM transverse ;
- `zdmooc/keycloak-enterprise-roadmap-v7` — profondeur Keycloak et preuves runtime ;
- `zdmooc/mayabank-api-management-architecture` — API Management, HLD/LLD/UML/OWASP.

## 7. Diagrammes, matrices et Architecture Board

- [Relationships, Diagrams, Matrices & Views](11-relationships-diagrams-matrices-views/README.md)
- [Viewpoints & Stakeholder Concerns](11-relationships-diagrams-matrices-views/04-diagrams-viewpoints-stakeholders-concerns.md)
- [Impact / Blast Radius Views](11-relationships-diagrams-matrices-views/09-impact-dependency-blast-radius-views.md)
- [MayaBank Enterprise Cartography Reference Model](12-enterprise-cartography-dependency-analysis/12-mayabank-enterprise-cartography-reference-model.md)

## 8. UML / HLD / LLD — frontière volontaire

Ce masterbook **ne prétend pas être un cours UML ni un dépôt LLD logiciel**.

HOPEX porte :
- cartographie ;
- référentiel ;
- dépendances ;
- transformation ;
- gouvernance ;
- vues décisionnelles.

Les preuves HLD/LLD/UML applicatives sont maintenues dans `mayabank-api-management-architecture`. Cette séparation évite de confondre EAM et conception détaillée d'un composant logiciel.

## 9. Parcours démonstration 10 minutes

Pour un entretien :

1. montrer `04-it-architecture/03-interfaces-interactions-flows.md`;
2. montrer `04-it-architecture/07-current-transition-target.md`;
3. montrer `08-application-architecture/05-integration-architecture-patterns.md`;
4. montrer `12-enterprise-cartography-dependency-analysis/README.md`;
5. terminer par le modèle MayaBank et une analyse de blast radius.

Le message à faire passer : **la cartographie n'est pas un dessin ; c'est un graphe gouverné utilisé pour l'impact analysis et la trajectoire de transformation**.
