# 99 — Sources officielles & frontière de vérification

## 1. Principe

Cette partie distingue trois niveaux :

```text
[PRODUIT VÉRIFIÉ]
Information soutenue par une source publique Bizzdesign/Hopex ou par les endpoints produit déjà vérifiés dans le masterbook.

[PRATIQUE RECOMMANDÉE]
Pattern de modélisation, gouvernance ou visualisation proposé dans ce masterbook.

[CAS PÉDAGOGIQUE]
Architecture fictive MayaBank.
```

Cette séparation évite de transformer une bonne pratique en prétendue fonctionnalité native.

---

## 2. Bizzdesign Hopex — page produit actuelle

**Source :** Bizzdesign Hopex — Software Transformation Suite.

La page publique consultée en septembre 2026 met notamment en avant :

- unified repository ;
- rapports, dashboards et enterprise portal ;
- self-service views pour les stakeholders ;
- automatisation de la collecte ;
- workflows ;
- architecture d’entreprise, application portfolio, technology portfolio, business process, data et GRC dans une plateforme connectée.

Référence publique :

`https://resources.bizzdesign.com/transformation-suite/hopex`

Page française :

`https://bizzdesign.com/fr/suite-logicielle-de-transformation/bizzdesign-hopex`

**Usage dans cette partie :** justifier le principe de repository connecté, publication et vues adaptées aux parties prenantes.

---

## 3. Bizzdesign Hopex Service Level Agreement — 2026

**Source :** `Bizzdesign Hopex Service Level Agreement v20260123`.

La documentation contractuelle publique mentionne notamment une catégorie de service :

```text
WebSite / Portal (Hopex 360)
```

et des services liés au repository et à l’exploitation de la plateforme.

Référence :

`https://bizzdesign.com/sites/default/files/2026-01/Bizzdesign%20Hopex%20Service%20Level%20Agreement%20v20260123%20EN.pdf`

**Usage :** confirmer l’existence actuelle du Hopex 360 Viewer/portal dans l’offre.

Ne pas en déduire des droits, capacités ou workflows précis sans contrat client.

---

## 4. Connected Repository customer story

**Source :** Bizzdesign customer story — mid-market company.

La source publique décrit :

- passage d’artefacts dispersés à un repository connecté ;
- démarche par couches plutôt qu’un « spaghetti diagram » ;
- utilisation de Hopex 360 pour rendre modèles et diagrammes accessibles ;
- Architecture Council pour gouverner les travaux.

Référence :

`https://bizzdesign.com/customers/customer-stories/mid-market-company`

**Usage :** soutenir les pratiques `layered views`, publication et gouvernance.

---

## 5. Global Auto Manufacturer customer story

**Source :** Bizzdesign customer story — leading global auto manufacturer.

La publication décrit notamment :

- application diagrams ;
- visualizations ;
- dashboards ;
- compréhension des écosystèmes, données et interdépendances ;
- usage de Bizzdesign Hopex pour architecture business, information et technology en plus de l’APM.

Référence :

`https://bizzdesign.com/customers/customer-stories/leading-global-auto-manufacturer`

**Usage :** confirmer la place des diagrammes/visualisations comme moyens d’exploitation du repository.

---

## 6. Technical Capabilities article

**Source :** Bizzdesign — Technical Capabilities for Business Success.

La publication indique que Bizzdesign Hopex peut visualiser l’architecture technique sous forme notamment de :

```text
diagrams
matrices
dashboards
```

et mentionne l’impact analysis.

Référence :

`https://resources.bizzdesign.com/blog/technical-capabilities`

**Usage :** soutenir l’utilisation de diagrammes, matrices et impact analysis dans cette partie.

Cette source est une publication de contenu Bizzdesign et non une spécification exhaustive d’écran ou de métaclasse.

---

## 7. Financial Services customer story

**Source :** Bizzdesign — financial services company.

La publication décrit :

- visualisations et dashboards ;
- visibilité holistique sur ecosystems, data et interdependencies ;
- personas et accès structurés ;
- architecture actionnable pour la planification.

Référence :

`https://bizzdesign.com/customers/customer-stories/financial-services-company`

**Usage :** soutenir l’approche audience/persona et decision-ready visualization.

---

## 8. Large Global Insurer customer story

La publication décrit notamment :

- single source of truth sur les technologies ;
- visibilité sur les impacts ;
- metrics et dashboards sur la technology health ;
- élimination de silos de développement.

Référence :

`https://content.bizzdesign.com/customers/customer-stories/large-global-insurer`

**Usage :** soutenir les principes de shared architecture view et impact visibility.

---

## 9. AWE customer story

La publication explique que diagrams et modeling ont été utilisés pour comprendre comment logiciels, applications et technologies s’assemblent et pour obtenir de la visibilité business sur un estate complexe.

Référence :

`https://bizzdesign.com/customers/customer-stories/atomic-weapons-establishment`

**Usage :** soutenir le rôle de la modélisation structurée pour rendre un paysage complexe compréhensible.

---

## 10. MetaAssociation — vérification interne du masterbook

La Partie II a déjà documenté, à partir de l’endpoint public de métamodèle HOPEX Aquila utilisé lors de la baseline, les concepts :

```text
MetaAssociation
MetaAssociationEnd
MetaAssociationType
```

Voir :

`../02-repository-metamodel/05-metaassociation-ends-cardinality.md`

**Usage :** soutenir l’affirmation qu’une relation fait partie du métamodèle explicite et possède des extrémités navigables.

Les cardinalités et noms exacts doivent toujours être vérifiés dans le métamodèle réellement installé chez le client.

---

## 11. Partie III — UI baseline

La Partie III avait déjà établi les principes :

```text
Diagram = structure / relations / flow
Matrix  = coverage / many-to-many comparison
List    = properties / review queue
Report  = aggregation / decision indicator
```

Voir :

`../03-ui-navigation-workspaces/07-diagrams-matrices-views.md`

La Partie XI approfondit la gouvernance de ces représentations sans prétendre que tous les patterns pédagogiques correspondent à des objets natifs du produit.

---

## 12. Frontière avec la documentation Horizzon

La base d’aide Bizzdesign actuelle contient aussi des pages détaillées sur :

- viewpoints ;
- view filters ;
- color/label/tooltip/chart/table views ;
- relation cross-reference tables.

Ces pages sont aujourd’hui classées dans l’aide **Horizzon**.

Elles peuvent être utiles pour comprendre l’écosystème Bizzdesign, mais la Partie XI **ne les utilise pas comme preuve qu’une fonction identique est présente dans Hopex**.

Principe :

```text
Horizzon feature
≠ automatically Hopex feature
```

---

## 13. Points explicitement recommandés — non revendiqués comme natifs

Les éléments suivants sont des patterns du masterbook :

- taxonomie `Verified / High / Medium / Low / Inferred` ;
- saved scopes `PAYMENTS-*` ;
- visual grammar MayaBank ;
- conventions `Keep / Change / Add / Retire` ;
- bibliothèque de 12 vues MayaBank ;
- quality gates ;
- mission playbook quatre semaines ;
- maturity model à cinq niveaux ;
- fréquence de revue proposée ;
- conventions de lignes/labels.

Ils doivent être adaptés au métamodèle, à l’UI et à la gouvernance du client.

---

## 14. Points à vérifier lors d’une vraie mission Hopex

Avant de configurer ou d’annoncer une capacité :

1. version exacte de Hopex ;
2. solutions activées ;
3. métamodèle installé ;
4. profils/personas ;
5. droits de création/édition ;
6. types de diagrammes disponibles ;
7. matrices disponibles ;
8. possibilités de filtres ;
9. capacités du portail Hopex 360 ;
10. workflow de publication ;
11. possibilités d’import/export ;
12. APIs et intégrations disponibles.

---

## 15. Date de vérification

Baseline documentaire de cette Partie XI : **septembre 2026**.

Les sources web et offres produit peuvent évoluer. La Partie XXIV réalisera la revérification finale de l’ensemble du masterbook.