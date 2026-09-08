# 04 — Technology Architecture & Standards

## 1. Pourquoi cartographier les technologies

Une application peut être métierment critique tout en reposant sur une technologie en fin de support. Sans relation application ↔ technologie, ce risque reste invisible.

Questions typiques :

- quelles applications utilisent Java 11 ?
- quels systèmes dépendent d'un middleware en fin de vie ?
- quelles technologies sont approuvées, tolérées ou interdites ?
- où existe-t-il plusieurs produits remplissant le même rôle ?
- quelles applications doivent migrer avant une date de fin de support ?

## 2. Produit, technologie, plateforme et standard

Ne pas confondre :

```text
Concept technologique : Container Platform
Produit             : Red Hat OpenShift
Version              : 4.x
Standard interne     : Strategic / approved
Instance runtime     : OCP-PROD-A
```

Ces niveaux peuvent être séparés selon le besoin de gouvernance.

## 3. Technology catalog

Un catalogue minimal peut contenir :

| Champ | Exemple |
|---|---|
| Name | Red Hat OpenShift |
| Category | Container Platform |
| Vendor | Red Hat |
| Lifecycle | Strategic |
| Support end | date gouvernée |
| Standard status | Preferred |
| Owner | Platform Architecture |
| Source | technology governance |

Les champs réels sont ceux du métamodèle HOPEX activé.

## 4. Technology standard

Un standard sert à orienter les choix futurs.

Exemple de statuts pédagogiques :

```text
Emerging
Preferred
Permitted
Tolerated
Deprecated
Forbidden
```

Une taxonomie doit être courte, comprise et associée à des règles.

## 5. Lifecycle fournisseur vs lifecycle interne

Deux temporalités :

```text
Vendor lifecycle
- GA
- maintenance
- end of support

Enterprise lifecycle
- evaluate
- strategic
- contain
- retire
```

Une version encore supportée par l'éditeur peut être `Retire` chez MayaBank parce qu'elle n'est plus stratégique.

## 6. Technology debt

La dette technologique devient analysable si :

```text
Technology
→ has lifecycle
→ has support dates
→ is used by Applications
→ Applications support Capabilities
```

Alors :

```text
obsolete technology
→ impacted applications
→ impacted processes/capabilities
→ business exposure
```

## 7. Technology duplication

Exemple MayaBank :

```text
Container platforms:
- OpenShift
- Kubernetes managed service
- legacy Docker Swarm
- proprietary PaaS
```

Question : faut-il quatre plateformes ou existe-t-il une convergence cible ?

Le repository doit fournir les facts avant la décision.

## 8. OpenShift

Modèle recommandé :

```text
Technology/Product : Red Hat OpenShift
Role               : Container Platform
Standard status    : Preferred
Owner              : Cloud Platform Architecture
Supports           : payment applications
```

Les clusters opérationnels peuvent être gérés dans la CMDB et reliés sélectivement si nécessaire.

## 9. Kafka

```text
Technology/Product : Apache Kafka / Confluent selon contexte
Role               : Event Streaming Technology
Platform service   : MayaBank Event Streaming Platform
Consumers          : Payment Orchestrator, Fraud, Analytics
```

Ne pas confondre le produit avec le service d'architecture fourni à l'entreprise.

## 10. Bases de données

Une application peut dépendre de :

```text
Database Technology: Oracle
Platform: Exadata Service
Logical Data Store: Payment Operational Data
```

Le niveau exact à conserver dépend de l'analyse attendue.

## 11. Standards de sécurité

Exemples de standards liés :

- TLS minimum ;
- OAuth/OIDC ;
- secrets management ;
- approved cryptography ;
- container security ;
- database encryption.

Les standards doivent être liés aux technologies ou patterns concernés, pas uniquement publiés dans un PDF.

## 12. Standards et architecture target

```text
Current technology = Deprecated
Target standard     = Preferred
Migration initiative
→ applications impacted
```

C'est la base d'une roadmap technologique exploitable.

## 13. Matrice technologie × application

| Application | Technology | Status | Action |
|---|---|---|---|
| Payment Orchestrator | OpenShift | Preferred | keep |
| Legacy Hub | WAS | Deprecated | migrate |
| Fraud Engine | Java 17 | Preferred | keep |
| Batch Adapter | old MQ | Retire | replace |

## 14. Anti-patterns

- 1 objet par patch ;
- `OpenShift Prod` modélisé comme technologie alors qu'il s'agit d'une instance ;
- lifecycle sans source ;
- standard sans owner ;
- statut `Preferred` sans date de revue ;
- technologie non reliée aux applications ;
- catalogue importé mais jamais utilisé dans les décisions.

## 15. Questions d'entretien

**Comment détecter le risque technologique ?**  
En reliant lifecycle/support des technologies aux applications puis aux capacités et processus supportés.

**Produit et plateforme sont-ils identiques ?**  
Non. Un produit peut implémenter une plateforme ou un service d'architecture.

**Pourquoi un standard dans HOPEX ?**  
Pour rendre le choix technologique traçable et analyser la conformité du portefeuille.
