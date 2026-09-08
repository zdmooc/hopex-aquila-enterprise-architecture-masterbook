# 07 — HOPEX, ArchiMate et TOGAF

## 1. Trois choses différentes

Le trio doit être expliqué sans ambiguïté :

```text
TOGAF    = méthode, gouvernance, architecture development
ArchiMate = langage de modélisation
HOPEX     = plateforme EAM / repository / analyses / solutions
```

Ils peuvent être utilisés ensemble mais ne se remplacent pas.

## 2. TOGAF dans un contexte HOPEX

Une organisation peut utiliser TOGAF pour structurer :

- architecture governance ;
- stakeholders ;
- requirements ;
- baseline / target ;
- gaps ;
- transition architectures ;
- implementation governance.

HOPEX peut servir de repository pour une partie des objets et livrables nécessaires, selon le métamodèle et les pratiques de l'organisation.

Exemple :

```text
TOGAF Phase A
→ vision / stakeholders / drivers
→ objets et vues gérés dans HOPEX

Phases B/C/D
→ business/application/data/technology
→ repository et cartographies HOPEX

Phases E/F
→ gaps / initiatives / roadmaps
→ portfolio/transformation dans HOPEX
```

Ce mapping est une pratique d'utilisation, pas une promesse que chaque artefact TOGAF possède un bouton HOPEX dédié.

## 3. ArchiMate dans un contexte HOPEX

ArchiMate fournit une sémantique standard pour représenter notamment :

- motivation ;
- strategy ;
- business ;
- application ;
- technology ;
- physical ;
- implementation & migration ;
- relationships ;
- viewpoints.

HOPEX peut supporter des usages liés à ArchiMate selon les solutions, versions et configurations. Ce masterbook ne supposera jamais qu'un objet HOPEX portant un nom similaire est automatiquement normatif ArchiMate.

## 4. Mapping sémantique prudent

Exemple pédagogique :

| Concern | ArchiMate | Repository HOPEX |
|---|---|---|
| aptitude métier | Capability | objet capability si disponible/configuré |
| comportement métier | Business Process | objet process |
| logiciel logique | Application Component | application/component selon métamodèle |
| plateforme | System Software/Node | technology/platform/infrastructure selon modèle |
| transformation | Work Package/Plateau/Gap | initiative/project/roadmap concepts selon solution |

Le mapping doit être validé contre le métamodèle HOPEX réel.

## 5. Pourquoi ne pas copier le métamodèle ArchiMate dans HOPEX

Une EAM contient souvent des propriétés et objets de gouvernance qui ne sont pas des éléments ArchiMate :

- cost ;
- vendor ;
- contract ;
- lifecycle status ;
- technical debt ;
- risk score ;
- source system ;
- review date ;
- accountable owner ;
- portfolio recommendation.

Ces données sont essentielles à la décision mais ne doivent pas être forcées dans le langage ArchiMate.

## 6. Une vue peut mélanger plusieurs besoins

Une cartographie HOPEX peut servir un concern de portfolio plutôt qu'un viewpoint ArchiMate normatif.

Exemple :

```text
Applications
+ lifecycle
+ risk score
+ business criticality
+ target disposition
```

Cette représentation est utile même si elle n'est pas un viewpoint ArchiMate standard.

## 7. Réutiliser le masterbook ArchiMate

Le dépôt `archimate-3-2-foundation-practitioner-masterbook` devient notre référence pour :

- sémantique des éléments ArchiMate ;
- relations ;
- views/viewpoints ;
- MayaBank cross-layer ;
- patterns API/Kafka/OpenShift ;
- migration.

Le dépôt HOPEX apprendra ensuite à transformer cette connaissance en repository gouverné.

## 8. Cas MayaBank

Chaîne conceptuelle :

```text
Goal: Resilient Real-Time Payments
↓
Capability: Real-Time Payment Processing
↓
Process: Execute Instant Payment
↓
Application: Payment Orchestrator
↓
Technology: OpenShift / Kafka / Database
↓
Initiatives / roadmap
```

Dans ArchiMate, on choisit les éléments/relations normatifs.
Dans HOPEX, on gère aussi :

```text
owner
lifecycle
criticality
vendor
standard status
source
review date
portfolio decision
project impact
```

## 9. Questions d'entretien

**HOPEX remplace-t-il TOGAF ?**
Non. TOGAF est une méthode/standard de gouvernance d'architecture ; HOPEX est une plateforme qui peut soutenir la gestion de données et livrables d'architecture.

**HOPEX remplace-t-il ArchiMate ?**
Non. ArchiMate est un langage ; HOPEX est un outil/repository pouvant supporter plusieurs conventions et analyses.

**Faut-il tout modéliser en ArchiMate dans HOPEX ?**
Non. Il faut préserver la sémantique ArchiMate lorsqu'on affirme l'utiliser, mais une EAM a aussi besoin de données de portfolio, gouvernance, risques et lifecycle hors langage.

## 10. Règle du masterbook

```text
If we say “ArchiMate”, validate against ArchiMate semantics.
If we say “HOPEX”, validate against HOPEX product/metamodel.
If we say “recommended practice”, label it as practice.
```
