# 05 — Repository et Single Source of Truth

## 1. Le repository est le produit principal

Un programme HOPEX échoue souvent quand l'organisation se concentre sur la mise en forme des diagrammes et sous-estime la gouvernance des objets.

Le repository doit être pensé comme un produit de données d'architecture :

```text
Object type
+ stable identity
+ naming
+ properties
+ relationships
+ ownership
+ lifecycle
+ source
+ validation status
+ update process
```

## 2. Objet canonique

Un objet canonique est l'objet de référence réutilisé par plusieurs vues, rapports et intégrations.

Exemple MayaBank :

```text
Application = Payment Orchestrator
Canonical ID = MB-APP-002
Business owner = Head of Payments
IT owner = Payments Platform Team
Lifecycle = Strategic
Criticality = Critical
Source = Architecture repository
```

Le même Payment Orchestrator peut apparaître dans :

- une cartographie applicative ;
- une matrice application/process ;
- une vue de dépendances ;
- un roadmap ;
- un rapport de criticité ;
- une synchronisation ServiceNow.

## 3. Doublons

Exemples de doublons fréquents :

```text
Payment Orchestrator
Payment-Orchestrator
PAY_ORCH
Orchestrateur Paiement
Payment Orchestrator PROD
```

Avant de fusionner, vérifier si la différence représente :

- un alias ;
- une instance ;
- un environnement ;
- un produit ;
- une application logique ;
- un composant ;
- un simple doublon.

La déduplication est d'abord un problème sémantique.

## 4. Source of truth

Le terme ne signifie pas « HOPEX doit être maître de tout ».

Une architecture mature peut définir :

| Information | Source maître possible |
|---|---|
| Application logique | HOPEX / portfolio |
| Business owner | HOPEX ou référentiel organisationnel |
| CI serveur | ServiceNow CMDB |
| Version runtime détectée | Discovery/CMDB |
| Financial actuals | ERP/FinOps |
| Data classification | Data Governance |
| Risk finding | GRC/IRM |

Le repository HOPEX peut consommer, enrichir et relier ces données sans remplacer les systèmes spécialisés.

## 5. Stable identifiers

Les noms changent. Les identifiants doivent rester stables.

Règle MayaBank proposée :

```text
MB-CAP-xxx  Capability
MB-PROC-xxx Process
MB-APP-xxx  Application
MB-DATA-xxx Data concept
MB-TEC-xxx  Technology
MB-ORG-xxx  Organization
MB-TRF-xxx  Transformation item
```

C'est une convention pédagogique, pas un format imposé par HOPEX.

## 6. Ownership

Pour chaque classe d'objet importante, définir :

```text
Business owner
IT owner
Repository steward
Source system
Validation authority
Refresh frequency
```

Sans owner, l'objet devient progressivement orphelin.

## 7. Lifecycle

Le lifecycle sert à la décision, pas à décorer une fiche.

Exemple :

```text
Emerging
→ Strategic
→ Tolerated
→ Sunset
→ Retired
```

Ces valeurs sont un exemple de gouvernance. Ne pas les présenter comme une enum HOPEX universelle.

Une politique doit définir :

- signification de chaque état ;
- qui le modifie ;
- conséquences sur les projets ;
- date d'effet ;
- exceptions.

## 8. Quality dimensions

Qualité d'un objet :

- completeness ;
- accuracy ;
- consistency ;
- uniqueness ;
- timeliness ;
- ownership ;
- traceability.

Un taux de complétude de 100 % ne prouve pas l'exactitude.

## 9. Relations gouvernées

Éviter les relations « parce que visuellement ça semble lié ».

Exemple :

```text
Capability → supported by → Application
Application → exchanges with → Application
Application → uses → Technology
Application → owned by → Organization
Application → impacted by → Project
```

Les noms réels des relations dépendent du métamodèle HOPEX. La Partie II vérifiera le vocabulaire disponible avant d'industrialiser ces exemples.

## 10. Repository minimal viable

Pour démarrer MayaBank :

```text
Capabilities
Business Processes
Applications
Application Services/APIs
Information concepts
Technology products/platforms
Organizations/owners
Transformation initiatives
```

Puis seulement les propriétés qui soutiennent un cas d'usage :

```text
criticality
lifecycle
owner
strategic fit
source
last review
```

## 11. Anti-patterns

### Repository encyclopédique
Tout modéliser avant d'avoir un usage.

### Property cemetery
Créer 80 propriétés, en remplir 15.

### Diagram-owned data
La vérité vit dans un diagramme au lieu de l'objet.

### Environment explosion
Créer une nouvelle Application pour DEV/UAT/PROD alors que le concern vise l'application logique.

### Uncontrolled customization
Ajouter un type custom dès qu'un terme n'est pas compris.

## 12. Revue de qualité MayaBank

Pour `Payment Orchestrator`, vérifier :

- existe-t-il une seule application logique ?
- owner défini ?
- lifecycle défini ?
- business process relié ?
- API/service relié ?
- technologies reliées ?
- source connue ?
- date de dernière revue ?
- doublons détectés ?
- dépendances critiques connues ?

## 13. Principe clé

```text
A good HOPEX repository is not the biggest model.
It is the smallest governed model that answers important decisions reliably.
```
