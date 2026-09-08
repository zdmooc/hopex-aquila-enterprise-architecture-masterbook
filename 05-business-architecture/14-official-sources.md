# 14 — Sources officielles et frontière de vérification

## 1. Principe

Cette partie distingue :

1. **fonctionnalité produit actuellement documentée** ;
2. **contenu/reference framework disponible dans l'écosystème HOPEX** ;
3. **pratique d'architecture recommandée par ce masterbook** ;
4. **exemple pédagogique MayaBank**.

Une pratique recommandée n'est pas présentée comme une règle propriétaire HOPEX.

## 2. HOPEX Enterprise Architecture — positionnement actuel

Source publique MEGA/Bizzdesign :

https://www.mega.com/enterprise-architecture-ea-tool

La page décrit notamment :

- repository commun business/IT ;
- applications, processes et business capabilities ;
- data flows et application interdependencies ;
- technology investments reliés aux objectifs ;
- business capability mapping ;
- industry reference content ;
- transformation et rationalisation.

## 3. Enterprise Architecture Features

Source :

https://www.mega.com/features/hopex-enterprise-architecture

Fonctionnalités utiles pour cette partie :

- diagramming business/solution architecture ;
- value stream mapping ;
- customer journey mapping ;
- As-Is / To-Be ;
- business capability mapping ;
- Capability Smart Mapping vers applications, technologies et data ;
- génération/évolution de capability maps.

Les noms exacts des fonctions disponibles dépendent de l'offre, de la release et des droits.

## 4. Pricing / functional scope

Source :

https://www.mega.com/product-hopex-enterprise-architecture-pricing

La matrice publique mentionne notamment :

- Business Capabilities Modeling ;
- Customer Journey Modeling ;
- IT Strategy & Transformation Roadmap ;
- Business Process Catalog ;
- Business Process Modeling (BPMN) ;
- Application Architecture Modeling ;
- Deployment Architecture ;
- Data Architecture.

Cette matrice est utile pour confirmer les grandes familles fonctionnelles, mais ne doit pas servir à déduire des droits sur un environnement client particulier.

## 5. Business Architecture Management

Source actuelle :

https://www.mega.com/business-architecture-management-bam-software

Les axes publics incluent :

- capability-based planning ;
- value stream management ;
- customer experience innovation ;
- connexion value streams ↔ customer journeys ↔ processes ↔ capabilities ↔ strategy ;
- capability gap/maturity assessment ;
- scenario/investment prioritization ;
- roadmaps de capability improvement.

Cette source justifie l'orientation intégrée de la Partie V.

## 6. BIAN Capability Maps

Source Store :

https://store.mega.com/modules/details/itpm.biancapabilitymaps

Le module documente un toolkit permettant de convertir le contenu BIAN ArchiMate en HOPEX Capability Maps pour certains produits, sous prérequis et droits BIAN/HOPEX.

Le masterbook :

- ne redistribue aucun contenu BIAN ;
- ne reproduit aucune capability map BIAN propriétaire ;
- utilise un modèle MayaBank original.

## 7. APQC Process Classification Framework

Source Store :

https://store.mega.com/modules/details/framework.apqc.cross.industry

Le module public mentionne :

- Process Map root ;
- Process Categories hierarchy ;
- Value Streams and stages ;
- related Performance Indicators.

L'activation et les droits doivent être vérifiés dans l'environnement réel.

## 8. ITBM Excel Import Template

Source Store :

https://store.mega.com/modules/details/itbm.importexceltemplate

Le template public documente le bulk import de données ITBM incluant :

- Strategy ;
- Transformation Stages ;
- Exhibited Business Capabilities by Stage ;
- Business Architecture.

Cela confirme que business architecture et transformation peuvent être gérées comme données structurées et non uniquement comme diagrammes.

## 9. HOPEX Core actuel

Source :

https://store.mega.com/modules/details/hopex.core

La baseline utilisée par le masterbook au 8 septembre 2026 est la branche Aquila 6.2 / 62.18.x. Le Core connecte les perspectives business, IT, data et risk dans un repository commun.

La Partie I reste la référence de version détaillée.

## 10. Anciennes ressources Community

Certaines ressources historiques HOPEX décrivent des concepts encore pédagogiquement utiles : Business Architecture, capability maps, value streams, org charts, property pages, etc.

Elles ne doivent pas être utilisées pour affirmer :

- qu'un écran Aquila 6.2 est identique ;
- qu'un menu porte encore le même nom ;
- qu'une fonctionnalité historique est disponible dans toutes les licences actuelles.

Le masterbook privilégie les concepts stables et les sources produit récentes.

## 11. Normatif vs pédagogique

### Vérifié produit

Exemples :

- HOPEX supporte business capability modeling ;
- value stream/customer journey modeling est présenté publiquement ;
- business process catalog/BPMN font partie du périmètre EA affiché ;
- repository commun business/IT/data/risk ;
- capability mapping peut être connecté aux applications/technologies/data.

### Recommandation du masterbook

Exemples :

- convention L1/L2/L3 ;
- RACI MayaBank ;
- score 1–5 proposé dans les labs ;
- noms de capabilities MayaBank ;
- architecture board checklist ;
- Definition of Done.

### Pédagogique MayaBank

Tous les noms :

```text
MayaBank Payment Orchestration
Instant Payment Service
Payment Event Backbone
Payment Orchestrator
```

sont fictifs et servent uniquement d'exercice.

## 12. Règle de prudence

Avant une mission réelle, confirmer :

```text
HOPEX exact build
+ installed solutions
+ licenses
+ metamodel
+ personas/permissions
+ available reference content
+ client customization
```

Ne jamais transformer une capture d'écran ou un article ancien en vérité universelle sur Aquila.