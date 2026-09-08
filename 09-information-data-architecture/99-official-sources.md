# 99 — Sources officielles et frontière de vérification

## 1. Règle de cette partie

HOPEX est un produit propriétaire. Ce masterbook distingue :

```text
Fait produit vérifié
≠ pratique d’architecture recommandée
≠ exemple pédagogique MayaBank
```

Les informations produit ci-dessous sont basées sur des pages publiques MEGA/Bizzdesign consultables en septembre 2026.

---

## 2. HOPEX Core Back-End Aquila 6.2

Source :

https://store.mega.com/modules/details/hopex.core

Faits utilisés :

- HOPEX Core Back-End Aquila 6.2 ;
- branche publique 62.18.x ;
- latest observé : `62.18.0+774` ;
- publication : 03/09/2026 ;
- positionnement : repository connecté business, IT, data et risk.

Cette baseline est cohérente avec la Partie I.

---

## 3. HOPEX Web Front-End

Source :

https://store.mega.com/modules/details/hopex.dtpx

Faits utilisés :

- le Web Front-End expose notamment les solutions HOPEX Data Governance et HOPEX Information Architecture ;
- version Aquila observée : `62.18.0+143` ;
- publication : 02/09/2026.

Ne pas déduire de cette page les écrans exacts disponibles dans une licence client.

---

## 4. HOPEX Data Governance — offre publique

Source :

https://siteprod.mega.com/data-governance-tool

La page publique présente notamment :

- business glossary ;
- data dictionary ;
- data catalog ;
- functional data lineage ;
- data modeling ;
- analysis ;
- collaboration ;
- technical data lineage ;
- data compliance ;
- privacy management.

Elle positionne aussi la solution comme connectée à l’Enterprise Architecture, BPM et Risk/Compliance.

---

## 5. HOPEX Data Governance — features

Source :

https://siteprod.mega.com/features/hopex-data-governance

Faits utilisés dans le masterbook :

### Functional data lineage

- connexion des données aux business processes, applications et risks ;
- visualisation des transformations ;
- impact assessment ;
- data-flow dependency analysis.

### Modeling tool

- physical models ;
- database reverse engineering ;
- création de logical et conceptual layers connectés ;
- navigation entre physical/logical/conceptual pour impact analysis.

Le masterbook ne prétend pas que chaque option est disponible avec toutes les licences/configurations.

---

## 6. Information Architecture vs Data Governance

Source :

https://siteprod.mega.com/product-hopex-data-governance-pricing

Cette page publique compare les périmètres Data Governance et Information Architecture et mentionne notamment :

- business glossary ;
- database reverse engineering ;
- physical/logical/conceptual modeling ;
- centralized repository ;
- workflows/portal ;
- metadata discovery ;
- automatic data catalog ;
- automatic data lineage en option selon offre ;
- data quality assessment/remediation ;
- internal data policies ;
- regulation import.

La structure commerciale et les options peuvent évoluer ; toujours vérifier l’offre client réelle.

---

## 7. HOPEX Data Discovery

Source :

https://store.mega.com/modules/details/data.discovery

Faits publics observés :

- module HOPEX Data Discovery ;
- dépend de HOPEX Data Governance ;
- licence spécifique DDISC mentionnée ;
- compatibility annoncée à partir d’HOPEX Data Governance Aquila V6.2.4 sur la page actuelle ;
- version publique observée : `62.15.0+3` ;
- version 62.11.0+7247 publiée le 13/05/2026 et 62.15.0+3 visible au 08/07/2026.

Le catalogue de connecteurs et les conditions techniques doivent être vérifiés dans la documentation client.

---

## 8. HOPEX Data Source Extractor

Source :

https://store.mega.com/modules/details/tool.data.source.extractor

Faits utilisés :

- tags Information Architecture et Data Governance ;
- extraction via data sources ODBC ;
- requirements HOPEX Data Governance ou HOPEX Data Architecture indiqués publiquement ;
- version publique observée `15.9.0+6859`, publiée le 19/06/2025.

Cette ressource confirme l’existence d’outillage d’extraction de metadata, pas une couverture universelle de toutes les plateformes.

---

## 9. Database Design Oracle 19c

Source :

https://store.mega.com/modules/details/database.design.oracle19c

Faits utilisés :

- module de types de données Oracle 19c pour la conception de bases dans HOPEX ;
- tags Information Architecture / Data Governance ;
- dépendance HOPEX Core ;
- version publique `17.0.3+6762` publiée le 18/06/2024.

Le masterbook utilise cette source uniquement pour confirmer la capacité de modélisation physique DBMS-specific, sans recopier la documentation propriétaire.

---

## 10. SQL ANSI Database Design

Source :

https://store.mega.com/modules/details/database.design.sql.ansi.9075.1992

Faits utilisés :

- types SQL nécessaires à la conception relationnelle ;
- usage logique/physique ;
- requirements HOPEX Data Governance / Information Architecture.

---

## 11. BCBS 239 sample

Source :

https://store.mega.com/modules/details/sample.bcbs239

Faits utilisés :

- contenu de référence BCBS 239 proposé sur le Store ;
- usage possible dans Information Architecture pour relier Data Assets et principes de conformité ;
- requirement HOPEX Data Governance indiqué.

Important : le contenu réglementaire réel doit être lu depuis les sources réglementaires officielles et le cadre conformité du client. Le repository GitHub ne recopie pas ce contenu sous licence.

---

## 12. Training Database Aquila 6.2 CU5

Source :

https://store.mega.com/modules/details/backup.training

Faits utilisés :

- backup de training Aquila 6.2 CU5 publié le 05/06/2026 ;
- données de training pour :
  - HOPEX Information Architecture ;
  - HOPEX Data Governance ;
  - HOPEX IT Architecture ;
  - Business Process Analysis ;
  - IT Business/Portfolio Management ;
  - Integrated Risk Management.

Aucun backup, mot de passe, contenu propriétaire de formation ou données de training ne sont copiés dans ce repository.

---

## 13. Ce qui est un fait produit vérifié

Les pages publiques permettent de soutenir :

- existence de HOPEX Data Governance ;
- existence de HOPEX Information Architecture ;
- business glossary / data catalog ;
- functional data lineage ;
- technical lineage positionné dans l’offre ;
- data modeling conceptual/logical/physical ;
- database reverse engineering ;
- impact analysis entre couches ;
- metadata/data discovery ;
- data quality/compliance use cases ;
- connexion data ↔ applications/processes/risks ;
- modules DBMS-specific ;
- training content officiel pour Information Architecture et Data Governance.

---

## 14. Ce qui est une pratique recommandée du masterbook

Ne pas présenter comme règle HOPEX :

- la taxonomie MayaBank des data domains ;
- Public/Internal/Confidential/Restricted ;
- le maturity model en 5 niveaux ;
- la structure des Data Contracts ;
- les quality gates ;
- les transition waves ;
- les 12 matrices MayaBank ;
- les 12 vues MayaBank ;
- les règles de source-of-truth ;
- la mission 4 semaines.

Ce sont des constructions pédagogiques/orientées mission.

---

## 15. Ce qui doit être vérifié en environnement client

Avant toute mission réelle :

1. version exacte HOPEX ;
2. licence Data Governance / Information Architecture ;
3. modules Data Discovery disponibles ;
4. connecteurs metadata ;
5. metamodel custom ;
6. workflows owner/steward ;
7. diagram types ;
8. lineage configuration ;
9. quality assessment capabilities ;
10. privacy/compliance modules ;
11. reports/dashboards ;
12. import/export rules ;
13. rights/security ;
14. DBMS design modules installés ;
15. intégrations data catalog/lineage tierces ;
16. naming conventions client.

---

## 16. Règle de propriété intellectuelle

Ne jamais :

- copier une formation MEGA ;
- reproduire massivement la documentation propriétaire ;
- publier des backups officiels ;
- publier des clés/licences ;
- présenter un contenu Store sous licence comme contenu libre.

Toujours :

```text
source publique
→ compréhension
→ reformulation originale
→ exemple MayaBank
```
